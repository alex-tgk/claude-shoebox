# Create Shopify App

Generate a complete, production-ready Shopify app with OAuth authentication, embedded interface, API integration, billing, and Shopify App Store assets.

## Instructions

You are tasked with creating a COMPLETE, production-ready Shopify app. This is a one-shot command that must produce a fully functional app ready for Shopify App Store submission and revenue generation.

### Step 1: Gather Requirements

First, ask the user these essential questions:
1. **App Purpose**: What does the app do? (inventory, marketing, analytics, etc.)
2. **Core Features**: What are the 3-5 main features?
3. **Data Access**: What Shopify data does it need? (products, orders, customers)
4. **Webhooks**: What events to listen for?
5. **Pricing**: Free, one-time charge, recurring, or usage-based?
6. **Tech Stack**: Node.js, Python, or Ruby?

### Step 2: Complete App Structure

```
shopify-app/
├── server/
│   ├── index.js
│   ├── routes/
│   │   ├── auth.js
│   │   ├── webhooks.js
│   │   ├── api.js
│   │   └── billing.js
│   ├── middleware/
│   │   ├── verify-request.js
│   │   ├── verify-webhook.js
│   │   └── check-billing.js
│   ├── handlers/
│   │   ├── products.js
│   │   ├── orders.js
│   │   └── customers.js
│   ├── services/
│   │   ├── shopify-api.js
│   │   ├── database.js
│   │   └── billing.js
│   └── models/
│       ├── Shop.js
│       └── Session.js
├── web/
│   ├── frontend/
│   │   ├── pages/
│   │   │   ├── Index.jsx
│   │   │   ├── Products.jsx
│   │   │   ├── Orders.jsx
│   │   │   └── Settings.jsx
│   │   ├── components/
│   │   │   ├── Layout.jsx
│   │   │   ├── ProductList.jsx
│   │   │   └── BillingBanner.jsx
│   │   └── App.jsx
│   └── index.html
├── prisma/
│   └── schema.prisma
├── shopify.app.toml
├── .env.example
├── package.json
└── README.md
```

### Step 3: Shopify App Configuration

```toml
# shopify.app.toml
name = "my-app"
client_id = "YOUR_CLIENT_ID"
application_url = "https://your-app.com"
embedded = true

[access_scopes]
scopes = "read_products,write_products,read_orders,write_orders,read_customers,write_customers"

[auth]
redirect_urls = [
  "https://your-app.com/auth/callback"
]

[webhooks]
api_version = "2024-01"

  [[webhooks.subscriptions]]
  topics = [ "products/create", "products/update", "products/delete" ]
  uri = "/webhooks/products"

  [[webhooks.subscriptions]]
  topics = [ "orders/create", "orders/updated" ]
  uri = "/webhooks/orders"

  [[webhooks.subscriptions]]
  topics = [ "customers/data_request", "customers/redact", "shop/redact" ]
  uri = "/webhooks/gdpr"
```

```javascript
// server/index.js
import "@shopify/shopify-app-express/adapters/node";
import {
  shopifyApp,
  DeliveryMethod,
  BillingInterval,
} from "@shopify/shopify-app-express";
import { PrismaSessionStorage } from "@shopify/shopify-app-session-storage-prisma";
import { restResources } from "@shopify/shopify-api/rest/admin/2024-01";
import express from "express";
import prisma from "./db.server.js";

const PORT = process.env.PORT || 3000;

const BILLING_SETTINGS = {
  required: true,
  chargeName: "Pro Plan",
  amount: 9.99,
  currencyCode: "USD",
  interval: BillingInterval.Every30Days,
  trialDays: 7,
};

// Initialize Shopify app
const shopify = shopifyApp({
  api: {
    apiVersion: "2024-01",
    restResources,
    billing: BILLING_SETTINGS,
  },
  auth: {
    path: "/auth",
    callbackPath: "/auth/callback",
  },
  webhooks: {
    path: "/webhooks",
  },
  sessionStorage: new PrismaSessionStorage(prisma),
});

const app = express();

// Webhook handlers
const WEBHOOK_HANDLERS = {
  PRODUCTS_CREATE: {
    deliveryMethod: DeliveryMethod.Http,
    callbackUrl: "/webhooks/products/create",
    callback: async (topic, shop, body, webhookId) => {
      const payload = JSON.parse(body);
      console.log("Product created:", payload);

      // Handle product creation
      await handleProductCreate(shop, payload);
    },
  },
  PRODUCTS_UPDATE: {
    deliveryMethod: DeliveryMethod.Http,
    callbackUrl: "/webhooks/products/update",
    callback: async (topic, shop, body) => {
      const payload = JSON.parse(body);
      await handleProductUpdate(shop, payload);
    },
  },
  ORDERS_CREATE: {
    deliveryMethod: DeliveryMethod.Http,
    callbackUrl: "/webhooks/orders/create",
    callback: async (topic, shop, body) => {
      const payload = JSON.parse(body);
      await handleOrderCreate(shop, payload);
    },
  },
  // GDPR webhooks (required)
  CUSTOMERS_DATA_REQUEST: {
    deliveryMethod: DeliveryMethod.Http,
    callbackUrl: "/webhooks/gdpr/customers_data_request",
    callback: async (topic, shop, body) => {
      const payload = JSON.parse(body);
      await handleCustomerDataRequest(shop, payload);
    },
  },
  CUSTOMERS_REDACT: {
    deliveryMethod: DeliveryMethod.Http,
    callbackUrl: "/webhooks/gdpr/customers_redact",
    callback: async (topic, shop, body) => {
      const payload = JSON.parse(body);
      await handleCustomerRedact(shop, payload);
    },
  },
  SHOP_REDACT: {
    deliveryMethod: DeliveryMethod.Http,
    callbackUrl: "/webhooks/gdpr/shop_redact",
    callback: async (topic, shop, body) => {
      const payload = JSON.parse(body);
      await handleShopRedact(shop, payload);
    },
  },
};

// Register webhooks
for (const [topic, handler] of Object.entries(WEBHOOK_HANDLERS)) {
  shopify.registerWebhooks({ [topic]: handler });
}

// Body parser for webhooks
app.post("/webhooks/*", express.text({ type: "*/*" }));

// Process webhooks
app.post("/webhooks/*", async (req, res) => {
  try {
    await shopify.processWebhooks(req, res);
  } catch (error) {
    console.error("Webhook processing error:", error);
    res.status(500).send("Error processing webhook");
  }
});

// Auth routes
app.get("/auth", shopify.auth.begin());
app.get("/auth/callback", shopify.auth.callback(), async (req, res) => {
  const { session } = res.locals.shopify;

  // Save shop to database
  await prisma.shop.upsert({
    where: { shop: session.shop },
    create: {
      shop: session.shop,
      accessToken: session.accessToken,
      scope: session.scope,
      installedAt: new Date(),
    },
    update: {
      accessToken: session.accessToken,
      scope: session.scope,
    },
  });

  // Redirect to app
  res.redirect("/");
});

// Verify request middleware
app.use("/api/*", shopify.validateAuthenticatedSession());

// API Routes
app.use("/api", require("./routes/api"));

// Check billing status
app.use("/api/*", async (req, res, next) => {
  const { session } = res.locals.shopify;

  const hasPayment = await shopify.billing.check({
    session,
    plans: [BILLING_SETTINGS.chargeName],
    isTest: process.env.NODE_ENV !== "production",
  });

  if (!hasPayment) {
    const confirmationUrl = await shopify.billing.request({
      session,
      plan: BILLING_SETTINGS.chargeName,
      isTest: process.env.NODE_ENV !== "production",
    });

    return res.status(402).json({
      error: "Payment required",
      confirmationUrl,
    });
  }

  next();
});

// GraphQL endpoint
app.post("/graphql", shopify.graphql());

// Serve frontend
if (process.env.NODE_ENV === "production") {
  app.use(express.static("dist"));
  app.get("*", (req, res) => {
    res.sendFile(__dirname + "/dist/index.html");
  });
}

app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});

// Webhook handler functions
async function handleProductCreate(shop, product) {
  console.log(`New product created in ${shop}:`, product.title);

  // Your custom logic here
  await prisma.product.create({
    data: {
      shopifyId: product.id.toString(),
      shop,
      title: product.title,
      price: product.variants[0].price,
      inventory: product.variants[0].inventory_quantity,
    },
  });
}

async function handleProductUpdate(shop, product) {
  await prisma.product.update({
    where: { shopifyId: product.id.toString() },
    data: {
      title: product.title,
      price: product.variants[0].price,
      inventory: product.variants[0].inventory_quantity,
      updatedAt: new Date(),
    },
  });
}

async function handleOrderCreate(shop, order) {
  console.log(`New order in ${shop}:`, order.name);

  // Process order
  await prisma.order.create({
    data: {
      shopifyId: order.id.toString(),
      shop,
      orderNumber: order.name,
      totalPrice: order.total_price,
      customerEmail: order.customer.email,
      items: order.line_items.length,
    },
  });
}

async function handleCustomerDataRequest(shop, payload) {
  // Collect all customer data for GDPR request
  const customerId = payload.customer.id;

  const customerData = await prisma.customer.findMany({
    where: { shop, shopifyCustomerId: customerId.toString() },
  });

  // Send data to shop owner
  console.log("Customer data request:", customerData);
}

async function handleCustomerRedact(shop, payload) {
  // Delete customer data for GDPR compliance
  const customerId = payload.customer.id;

  await prisma.customer.deleteMany({
    where: { shop, shopifyCustomerId: customerId.toString() },
  });

  console.log("Customer data redacted");
}

async function handleShopRedact(shop, payload) {
  // Delete all shop data after app uninstall (48 hours)
  await prisma.shop.delete({
    where: { shop },
  });

  await prisma.product.deleteMany({ where: { shop } });
  await prisma.order.deleteMany({ where: { shop } });
  await prisma.customer.deleteMany({ where: { shop } });

  console.log("Shop data redacted");
}
```

### Step 4: Frontend with Polaris

```jsx
// web/frontend/pages/Index.jsx
import { useState, useCallback, useEffect } from "react";
import {
  Card,
  Page,
  Layout,
  TextContainer,
  Heading,
  Banner,
  Button,
  Loading,
  Frame,
} from "@shopify/polaris";
import { useAppBridge } from "@shopify/app-bridge-react";
import { Redirect } from "@shopify/app-bridge/actions";

export default function HomePage() {
  const app = useAppBridge();
  const redirect = Redirect.create(app);

  const [isLoading, setIsLoading] = useState(true);
  const [stats, setStats] = useState({
    products: 0,
    orders: 0,
    revenue: 0,
  });
  const [billingStatus, setBillingStatus] = useState(null);

  useEffect(() => {
    fetchData();
  }, []);

  const fetchData = async () => {
    try {
      const response = await fetch("/api/dashboard");
      const data = await response.json();

      if (data.billingRequired) {
        setBillingStatus({
          required: true,
          confirmationUrl: data.confirmationUrl,
        });
      } else {
        setStats(data.stats);
      }
    } catch (error) {
      console.error("Error fetching data:", error);
    } finally {
      setIsLoading(false);
    }
  };

  const handleUpgrade = useCallback(() => {
    redirect.dispatch(Redirect.Action.REMOTE, billingStatus.confirmationUrl);
  }, [billingStatus]);

  if (isLoading) {
    return (
      <Frame>
        <Loading />
      </Frame>
    );
  }

  if (billingStatus?.required) {
    return (
      <Page title="Upgrade Required">
        <Layout>
          <Layout.Section>
            <Banner
              title="Subscription Required"
              status="warning"
              action={{
                content: "Start 7-Day Free Trial",
                onAction: handleUpgrade,
              }}
            >
              <p>
                Subscribe to unlock all features. Try it free for 7 days, then
                $9.99/month.
              </p>
            </Banner>
          </Layout.Section>
        </Layout>
      </Page>
    );
  }

  return (
    <Page title="Dashboard">
      <Layout>
        <Layout.Section>
          <Banner status="success">
            <p>Welcome to MyApp! Your 7-day trial is active.</p>
          </Banner>
        </Layout.Section>

        <Layout.Section oneHalf>
          <Card sectioned>
            <Heading>Products</Heading>
            <div style={{ marginTop: "1rem" }}>
              <p style={{ fontSize: "2rem", fontWeight: "bold" }}>
                {stats.products}
              </p>
              <p>Total products managed</p>
            </div>
          </Card>
        </Layout.Section>

        <Layout.Section oneHalf>
          <Card sectioned>
            <Heading>Orders</Heading>
            <div style={{ marginTop: "1rem" }}>
              <p style={{ fontSize: "2rem", fontWeight: "bold" }}>
                {stats.orders}
              </p>
              <p>Orders processed</p>
            </div>
          </Card>
        </Layout.Section>

        <Layout.Section oneHalf>
          <Card sectioned>
            <Heading>Revenue</Heading>
            <div style={{ marginTop: "1rem" }}>
              <p style={{ fontSize: "2rem", fontWeight: "bold" }}>
                ${stats.revenue}
              </p>
              <p>Total revenue tracked</p>
            </div>
          </Card>
        </Layout.Section>

        <Layout.Section>
          <Card
            title="Getting Started"
            sectioned
            actions={[
              {
                content: "View Products",
                url: "/products",
              },
            ]}
          >
            <TextContainer>
              <p>
                Get started by connecting your products and setting up
                automation rules.
              </p>
            </TextContainer>
          </Card>
        </Layout.Section>
      </Layout>
    </Page>
  );
}
```

```jsx
// web/frontend/pages/Products.jsx
import { useState, useCallback, useEffect } from "react";
import {
  Page,
  Card,
  DataTable,
  Thumbnail,
  Button,
  Modal,
  TextField,
  FormLayout,
  Toast,
  Frame,
} from "@shopify/polaris";

export default function ProductsPage() {
  const [products, setProducts] = useState([]);
  const [selectedProduct, setSelectedProduct] = useState(null);
  const [modalActive, setModalActive] = useState(false);
  const [toastActive, setToastActive] = useState(false);
  const [isLoading, setIsLoading] = useState(true);

  useEffect(() => {
    fetchProducts();
  }, []);

  const fetchProducts = async () => {
    try {
      const response = await fetch("/api/products");
      const data = await response.json();
      setProducts(data.products);
    } catch (error) {
      console.error("Error fetching products:", error);
    } finally {
      setIsLoading(false);
    }
  };

  const handleEdit = useCallback((product) => {
    setSelectedProduct(product);
    setModalActive(true);
  }, []);

  const handleSave = async () => {
    try {
      await fetch(`/api/products/${selectedProduct.id}`, {
        method: "PUT",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(selectedProduct),
      });

      setModalActive(false);
      setToastActive(true);
      fetchProducts();
    } catch (error) {
      console.error("Error saving product:", error);
    }
  };

  const rows = products.map((product) => [
    <Thumbnail
      source={product.image || ""}
      alt={product.title}
      size="small"
    />,
    product.title,
    `$${product.price}`,
    product.inventory,
    <Button onClick={() => handleEdit(product)}>Edit</Button>,
  ]);

  const toastMarkup = toastActive ? (
    <Toast
      content="Product updated successfully"
      onDismiss={() => setToastActive(false)}
    />
  ) : null;

  return (
    <Frame>
      <Page
        title="Products"
        primaryAction={{
          content: "Sync Products",
          onAction: fetchProducts,
        }}
      >
        <Card>
          <DataTable
            columnContentTypes={["text", "text", "text", "numeric", "text"]}
            headings={["Image", "Title", "Price", "Inventory", "Actions"]}
            rows={rows}
          />
        </Card>

        <Modal
          open={modalActive}
          onClose={() => setModalActive(false)}
          title="Edit Product"
          primaryAction={{
            content: "Save",
            onAction: handleSave,
          }}
        >
          <Modal.Section>
            {selectedProduct && (
              <FormLayout>
                <TextField
                  label="Title"
                  value={selectedProduct.title}
                  onChange={(value) =>
                    setSelectedProduct({ ...selectedProduct, title: value })
                  }
                />
                <TextField
                  label="Price"
                  type="number"
                  value={selectedProduct.price}
                  onChange={(value) =>
                    setSelectedProduct({ ...selectedProduct, price: value })
                  }
                  prefix="$"
                />
                <TextField
                  label="Inventory"
                  type="number"
                  value={selectedProduct.inventory}
                  onChange={(value) =>
                    setSelectedProduct({
                      ...selectedProduct,
                      inventory: value,
                    })
                  }
                />
              </FormLayout>
            )}
          </Modal.Section>
        </Modal>

        {toastMarkup}
      </Page>
    </Frame>
  );
}
```

### Step 5: Database Schema

```prisma
// prisma/schema.prisma
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

generator client {
  provider = "prisma-client-js"
}

model Shop {
  id            String   @id @default(cuid())
  shop          String   @unique
  accessToken   String
  scope         String
  installedAt   DateTime @default(now())
  uninstalledAt DateTime?
  products      Product[]
  orders        Order[]
  customers     Customer[]
  createdAt     DateTime @default(now())
  updatedAt     DateTime @updatedAt
}

model Product {
  id         String   @id @default(cuid())
  shopifyId  String   @unique
  shop       String
  shopModel  Shop     @relation(fields: [shop], references: [shop])
  title      String
  price      String
  inventory  Int
  createdAt  DateTime @default(now())
  updatedAt  DateTime @updatedAt
}

model Order {
  id            String   @id @default(cuid())
  shopifyId     String   @unique
  shop          String
  shopModel     Shop     @relation(fields: [shop], references: [shop])
  orderNumber   String
  totalPrice    String
  customerEmail String
  items         Int
  createdAt     DateTime @default(now())
}

model Customer {
  id                 String   @id @default(cuid())
  shopifyCustomerId  String
  shop               String
  shopModel          Shop     @relation(fields: [shop], references: [shop])
  email              String
  firstName          String?
  lastName           String?
  createdAt          DateTime @default(now())
  updatedAt          DateTime @updatedAt
}

model Session {
  id          String   @id
  shop        String
  state       String
  isOnline    Boolean  @default(false)
  scope       String?
  expires     DateTime?
  accessToken String
  userId      BigInt?
}
```

### Step 6: Shopify API Integration

```javascript
// server/services/shopify-api.js
import { shopifyApi } from "@shopify/shopify-api";

const shopify = shopifyApi({
  apiKey: process.env.SHOPIFY_API_KEY,
  apiSecretKey: process.env.SHOPIFY_API_SECRET,
  scopes: process.env.SHOPIFY_API_SCOPES.split(","),
  hostName: process.env.SHOPIFY_APP_URL.replace(/https:\/\//, ""),
  apiVersion: "2024-01",
  isEmbeddedApp: true,
});

// Get products
export async function getProducts(session) {
  const client = new shopify.clients.Rest({ session });

  const response = await client.get({
    path: "products",
    query: { limit: 250 },
  });

  return response.body.products;
}

// Create product
export async function createProduct(session, productData) {
  const client = new shopify.clients.Rest({ session });

  const response = await client.post({
    path: "products",
    data: { product: productData },
  });

  return response.body.product;
}

// Update product
export async function updateProduct(session, productId, productData) {
  const client = new shopify.clients.Rest({ session });

  const response = await client.put({
    path: `products/${productId}`,
    data: { product: productData },
  });

  return response.body.product;
}

// Get orders
export async function getOrders(session) {
  const client = new shopify.clients.Rest({ session });

  const response = await client.get({
    path: "orders",
    query: { status: "any", limit: 250 },
  });

  return response.body.orders;
}

// GraphQL query
export async function graphqlQuery(session, query, variables = {}) {
  const client = new shopify.clients.Graphql({ session });

  const response = await client.query({
    data: {
      query,
      variables,
    },
  });

  return response.body;
}
```

### Step 7: Billing Integration

```javascript
// server/services/billing.js
import { BillingInterval } from "@shopify/shopify-api";

export const PRICING_PLANS = {
  FREE: {
    name: "Free Plan",
    price: 0,
    features: ["Up to 10 products", "Basic analytics", "Email support"],
  },
  PRO: {
    name: "Pro Plan",
    price: 9.99,
    interval: BillingInterval.Every30Days,
    trialDays: 7,
    features: [
      "Unlimited products",
      "Advanced analytics",
      "Priority support",
      "Custom integrations",
    ],
  },
  ENTERPRISE: {
    name: "Enterprise Plan",
    price: 29.99,
    interval: BillingInterval.Every30Days,
    features: [
      "Everything in Pro",
      "Dedicated account manager",
      "Custom development",
      "SLA guarantee",
    ],
  },
};

export async function checkBilling(shopify, session, planName) {
  const hasPayment = await shopify.billing.check({
    session,
    plans: [planName],
    isTest: process.env.NODE_ENV !== "production",
  });

  return hasPayment;
}

export async function requestBilling(shopify, session, planName) {
  const plan = PRICING_PLANS[planName];

  const confirmationUrl = await shopify.billing.request({
    session,
    plan: plan.name,
    isTest: process.env.NODE_ENV !== "production",
  });

  return confirmationUrl;
}

export async function cancelBilling(shopify, session) {
  await shopify.billing.cancel({
    session,
    isTest: process.env.NODE_ENV !== "production",
  });
}
```

### Step 8: App Store Listing

```markdown
# Shopify App Store Listing

## App Name
MyApp - [Short tagline under 70 characters]

## Tagline
Brief description of what your app does (under 70 characters)

## Key Benefits
1. **Benefit #1** - Description
2. **Benefit #2** - Description
3. **Benefit #3** - Description

## Features
### Feature 1: [Feature Name]
Detailed description of feature 1 and how it helps merchants.

### Feature 2: [Feature Name]
Detailed description of feature 2 and how it helps merchants.

### Feature 3: [Feature Name]
Detailed description of feature 3 and how it helps merchants.

## Pricing
### Free Plan
- Up to 10 products
- Basic analytics
- Email support

### Pro Plan - $9.99/month
- 7-day free trial
- Unlimited products
- Advanced analytics
- Priority support
- Custom integrations

### Enterprise Plan - $29.99/month
- Everything in Pro
- Dedicated account manager
- Custom development
- SLA guarantee

## Support
- Email: support@myapp.com
- Documentation: https://myapp.com/docs
- Live chat available

## Privacy & Security
- SOC 2 compliant
- GDPR compliant
- Data encrypted in transit and at rest
- Regular security audits

## Requirements
- Shopify plan: Any
- Compatible with: Online Store 2.0

## Screenshots
1. Dashboard overview
2. Product management
3. Analytics view
4. Settings page
5. Mobile view

## Video Demo
https://youtu.be/demo-video
```

### Step 9: Documentation

```markdown
# Shopify App Documentation

## Installation

1. Visit Shopify App Store
2. Click "Add app"
3. Review permissions
4. Click "Install app"
5. Start 7-day free trial

## Setup

### Step 1: Connect Your Products
1. Go to Products tab
2. Click "Sync Products"
3. Wait for sync to complete

### Step 2: Configure Settings
1. Go to Settings
2. Set your preferences
3. Save changes

### Step 3: Start Using
Your app is ready! Check the dashboard for insights.

## Features

### Product Management
- Sync products automatically
- Bulk edit products
- Track inventory

### Analytics
- View sales data
- Track performance
- Export reports

### Automation
- Set up rules
- Automate tasks
- Save time

## Pricing

### Free Plan
Perfect for getting started

### Pro Plan - $9.99/month
For growing businesses

### Enterprise Plan - $29.99/month
For large operations

## Support
Contact us: support@myapp.com

## API Documentation
For developers: https://myapp.com/api-docs

## Changelog
### Version 1.0.0
- Initial release
```

### Success Criteria

The command is successful when you deliver:
✅ Complete Shopify app with OAuth
✅ Embedded app interface (Polaris)
✅ Shopify API integration
✅ Webhook handling
✅ Billing integration (recurring charges)
✅ GDPR compliance webhooks
✅ Database schema
✅ App Store listing assets
✅ Privacy policy
✅ Complete documentation
✅ Ready for Shopify App Store submission

This should be a COMPLETE, PRODUCTION-READY Shopify app ready for submission and revenue generation.
