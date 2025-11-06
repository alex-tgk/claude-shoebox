# High-Converting Pricing Page Creator

Create a complete, conversion-optimized pricing page with 3-tier structure, feature comparison matrix, FAQ, social proof, psychological pricing strategies, and A/B testing setup for the product or service specified by the user.

## Instructions

Generate a comprehensive pricing page including:

### 1. Pricing Strategy & Structure

#### 3-Tier Pricing Model (Optimal for Conversions):

**Why 3 Tiers:**
- Provides choice without overwhelming
- Middle tier becomes anchor (most popular)
- Decoy effect guides to desired tier
- Clear upgrade path

**Typical Structure:**
```
BASIC (Entry Level)
- Price: $X/month
- Target: Individual users, small needs
- Purpose: Low barrier to entry

PRO (Most Popular - Anchor)
- Price: $Y/month (3-5x Basic)
- Target: Growing businesses, teams
- Purpose: Best value, drives most revenue
- Highlight: Visual emphasis

ENTERPRISE (Premium)
- Price: $Z/month or Custom
- Target: Large organizations
- Purpose: Anchors pricing perception
```

#### Pricing Psychology Principles:

**1. Anchor Pricing:**
```
Show higher "regular" price crossed out:
Regular: $299/month
Today: $99/month (Save 67%)
```

**2. Decoy Effect:**
```
BASIC: $29/month (10 users)
PRO: $79/month (50 users) ← Best Value badge
ENTERPRISE: $149/month (100 users)

PRO appears as obvious choice
```

**3. Charm Pricing:**
```
$99 instead of $100
$997 instead of $1000

Psychological threshold perception
```

**4. Price Framing:**
```
Instead of: $1,200/year
Show: Just $99/month (billed annually)

OR

$3.30/day instead of $99/month
"Less than a coffee"
```

**5. Value Stacking:**
```
Main Product: $500 value
Bonus 1: $200 value
Bonus 2: $150 value
Bonus 3: $100 value
─────────────────
Total Value: $950

Your Price: $299 (Save $651)
```

### 2. Complete Pricing Page Structure

#### Hero Section:

```html
<section class="pricing-hero">
  <header>
    <h1>Simple, Transparent Pricing</h1>
    <subtitle>
      Choose the plan that's right for you.
      No hidden fees. Cancel anytime.
    </subtitle>
  </header>

  <billing-toggle>
    <option class="monthly" selected>
      Monthly
    </option>
    <toggle-switch></toggle-switch>
    <option class="annual">
      Annual
      <badge>Save 20%</badge>
    </option>
  </billing-toggle>

  <social-proof>
    <text>Trusted by 10,000+ businesses</text>
    <logo-bar>
      [Customer Logo 1] [Customer Logo 2] [Customer Logo 3] [Customer Logo 4]
    </logo-bar>
  </social-proof>
</section>
```

#### Pricing Cards:

```html
<section class="pricing-tiers">
  <!-- BASIC PLAN -->
  <pricing-card class="basic">
    <header>
      <plan-name>Basic</plan-name>
      <tagline>For individuals getting started</tagline>
    </header>

    <pricing>
      <price-display>
        <currency>$</currency>
        <amount>29</amount>
        <period>/month</period>
      </price-display>

      <annual-savings v-if="annualSelected">
        <strikethrough>$348/year</strikethrough>
        <discount>$279/year (save $69)</discount>
      </annual-savings>

      <billing-note>Billed monthly. Cancel anytime.</billing-note>
    </pricing>

    <features>
      <h4>What's included:</h4>

      <feature-list>
        <feature>
          <icon>✓</icon>
          <text>Up to 10 projects</text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text>5 GB storage</text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text>Basic reporting</text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text>Email support</text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text>Mobile app access</text>
        </feature>

        <feature class="not-included">
          <icon>—</icon>
          <text>Advanced analytics</text>
        </feature>

        <feature class="not-included">
          <icon>—</icon>
          <text>Priority support</text>
        </feature>

        <feature class="not-included">
          <icon>—</icon>
          <text>API access</text>
        </feature>
      </feature-list>
    </features>

    <cta>
      <button class="secondary">Start Free Trial</button>
      <trial-info>14-day free trial. No credit card required.</trial-info>
    </cta>
  </pricing-card>

  <!-- PRO PLAN (Most Popular) -->
  <pricing-card class="pro featured">
    <popular-badge>
      <icon>⭐</icon>
      <text>Most Popular</text>
    </popular-badge>

    <header>
      <plan-name>Pro</plan-name>
      <tagline>For growing teams and businesses</tagline>
    </header>

    <pricing>
      <price-display>
        <currency>$</currency>
        <amount>79</amount>
        <period>/month</period>
      </price-display>

      <annual-savings v-if="annualSelected">
        <strikethrough>$948/year</strikethrough>
        <discount>$758/year (save $190)</discount>
      </annual-savings>

      <value-statement>
        <strong>Best Value:</strong> $1.58 per user/month
      </value-statement>

      <billing-note>Billed monthly. Cancel anytime.</billing-note>
    </pricing>

    <features>
      <h4>Everything in Basic, plus:</h4>

      <feature-list>
        <feature>
          <icon>✓</icon>
          <text><strong>Unlimited projects</strong></text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text><strong>50 GB storage</strong></text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text><strong>Advanced analytics & reporting</strong></text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text><strong>Priority email & chat support</strong></text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text><strong>Team collaboration (up to 50 users)</strong></text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text>Custom branding</text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text>API access</text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text>Integrations with 50+ tools</text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text>Advanced security features</text>
        </feature>
      </feature-list>
    </features>

    <cta>
      <button class="primary">Start Free Trial</button>
      <trial-info>14-day free trial. No credit card required.</trial-info>
    </cta>
  </pricing-card>

  <!-- ENTERPRISE PLAN -->
  <pricing-card class="enterprise">
    <header>
      <plan-name>Enterprise</plan-name>
      <tagline>For large organizations with custom needs</tagline>
    </header>

    <pricing>
      <price-display>
        <amount-text>Custom Pricing</amount-text>
      </price-display>

      <contact-sales>Let's talk about your needs</contact-sales>
    </pricing>

    <features>
      <h4>Everything in Pro, plus:</h4>

      <feature-list>
        <feature>
          <icon>✓</icon>
          <text><strong>Unlimited storage</strong></text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text><strong>Unlimited users</strong></text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text><strong>Dedicated account manager</strong></text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text><strong>24/7 phone support</strong></text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text><strong>Custom integrations</strong></text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text>SLA guarantee (99.9% uptime)</text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text>Advanced security & compliance (SOC 2, HIPAA)</text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text>Onboarding & training</text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text>Volume discounts</text>
        </feature>

        <feature>
          <icon>✓</icon>
          <text>Custom contract terms</text>
        </feature>
      </feature-list>
    </features>

    <cta>
      <button class="secondary">Contact Sales</button>
      <contact-info>
        or call: 1-800-XXX-XXXX
      </contact-info>
    </cta>
  </pricing-card>
</section>
```

#### Annual vs Monthly Toggle Implementation:

```javascript
// Pricing toggle functionality
const pricingPlans = {
  basic: {
    monthly: 29,
    annual: 279, // $23.25/month
    savings: 69
  },
  pro: {
    monthly: 79,
    annual: 758, // $63.17/month
    savings: 190
  },
  enterprise: {
    monthly: 'Custom',
    annual: 'Custom',
    savings: 0
  }
};

function toggleBilling(period) {
  const isAnnual = period === 'annual';

  document.querySelectorAll('.pricing-card').forEach(card => {
    const tier = card.dataset.tier;
    const price = pricingPlans[tier][period];

    // Update displayed price
    card.querySelector('.amount').textContent = price;

    // Show/hide annual savings
    card.querySelector('.annual-savings').style.display =
      isAnnual ? 'block' : 'none';

    // Update CTA button text
    const button = card.querySelector('button.primary, button.secondary');
    button.textContent = isAnnual
      ? 'Start Free Trial (Annual)'
      : 'Start Free Trial';
  });
}

// Add toggle listeners
document.querySelector('.billing-toggle').addEventListener('click', (e) => {
  if (e.target.classList.contains('monthly')) {
    toggleBilling('monthly');
  } else if (e.target.classList.contains('annual')) {
    toggleBilling('annual');
  }
});
```

### 3. Feature Comparison Matrix

```html
<section class="feature-comparison">
  <header>
    <h2>Compare Plans</h2>
    <subtitle>See what's included in each plan</subtitle>
  </header>

  <comparison-table>
    <table>
      <thead>
        <tr>
          <th class="feature-column">Features</th>
          <th class="plan-column">
            <plan-name>Basic</plan-name>
            <price>$29/mo</price>
          </th>
          <th class="plan-column featured">
            <badge>Most Popular</badge>
            <plan-name>Pro</plan-name>
            <price>$79/mo</price>
          </th>
          <th class="plan-column">
            <plan-name>Enterprise</plan-name>
            <price>Custom</price>
          </th>
        </tr>
      </thead>

      <tbody>
        <!-- SECTION: Core Features -->
        <tr class="section-header">
          <td colspan="4">
            <h3>Core Features</h3>
          </td>
        </tr>

        <tr>
          <td class="feature-name">
            Projects
            <tooltip>Create and manage projects</tooltip>
          </td>
          <td class="basic">Up to 10</td>
          <td class="pro">Unlimited</td>
          <td class="enterprise">Unlimited</td>
        </tr>

        <tr>
          <td class="feature-name">
            Storage
            <tooltip>File storage capacity</tooltip>
          </td>
          <td class="basic">5 GB</td>
          <td class="pro">50 GB</td>
          <td class="enterprise">Unlimited</td>
        </tr>

        <tr>
          <td class="feature-name">Users</td>
          <td class="basic">1</td>
          <td class="pro">Up to 50</td>
          <td class="enterprise">Unlimited</td>
        </tr>

        <tr>
          <td class="feature-name">Mobile App</td>
          <td class="basic"><icon class="check">✓</icon></td>
          <td class="pro"><icon class="check">✓</icon></td>
          <td class="enterprise"><icon class="check">✓</icon></td>
        </tr>

        <!-- SECTION: Analytics & Reporting -->
        <tr class="section-header">
          <td colspan="4">
            <h3>Analytics & Reporting</h3>
          </td>
        </tr>

        <tr>
          <td class="feature-name">Basic Reports</td>
          <td class="basic"><icon class="check">✓</icon></td>
          <td class="pro"><icon class="check">✓</icon></td>
          <td class="enterprise"><icon class="check">✓</icon></td>
        </tr>

        <tr>
          <td class="feature-name">Advanced Analytics</td>
          <td class="basic"><icon class="x">—</icon></td>
          <td class="pro"><icon class="check">✓</icon></td>
          <td class="enterprise"><icon class="check">✓</icon></td>
        </tr>

        <tr>
          <td class="feature-name">Custom Dashboards</td>
          <td class="basic"><icon class="x">—</icon></td>
          <td class="pro"><icon class="check">✓</icon></td>
          <td class="enterprise"><icon class="check">✓</icon></td>
        </tr>

        <tr>
          <td class="feature-name">Export Reports</td>
          <td class="basic">PDF only</td>
          <td class="pro">PDF, CSV, Excel</td>
          <td class="enterprise">All formats + API</td>
        </tr>

        <!-- SECTION: Collaboration -->
        <tr class="section-header">
          <td colspan="4">
            <h3>Collaboration</h3>
          </td>
        </tr>

        <tr>
          <td class="feature-name">Comments & Mentions</td>
          <td class="basic"><icon class="x">—</icon></td>
          <td class="pro"><icon class="check">✓</icon></td>
          <td class="enterprise"><icon class="check">✓</icon></td>
        </tr>

        <tr>
          <td class="feature-name">File Sharing</td>
          <td class="basic">Basic</td>
          <td class="pro">Advanced</td>
          <td class="enterprise">Advanced + Permissions</td>
        </tr>

        <tr>
          <td class="feature-name">Real-time Collaboration</td>
          <td class="basic"><icon class="x">—</icon></td>
          <td class="pro"><icon class="check">✓</icon></td>
          <td class="enterprise"><icon class="check">✓</icon></td>
        </tr>

        <!-- SECTION: Integrations -->
        <tr class="section-header">
          <td colspan="4">
            <h3>Integrations</h3>
          </td>
        </tr>

        <tr>
          <td class="feature-name">Pre-built Integrations</td>
          <td class="basic">10</td>
          <td class="pro">50+</td>
          <td class="enterprise">All + Custom</td>
        </tr>

        <tr>
          <td class="feature-name">API Access</td>
          <td class="basic"><icon class="x">—</icon></td>
          <td class="pro"><icon class="check">✓</icon></td>
          <td class="enterprise"><icon class="check">✓</icon></td>
        </tr>

        <tr>
          <td class="feature-name">Webhooks</td>
          <td class="basic"><icon class="x">—</icon></td>
          <td class="pro"><icon class="check">✓</icon></td>
          <td class="enterprise"><icon class="check">✓</icon></td>
        </tr>

        <!-- SECTION: Support -->
        <tr class="section-header">
          <td colspan="4">
            <h3>Support</h3>
          </td>
        </tr>

        <tr>
          <td class="feature-name">Email Support</td>
          <td class="basic">Business hours</td>
          <td class="pro">Priority (24/5)</td>
          <td class="enterprise">24/7</td>
        </tr>

        <tr>
          <td class="feature-name">Live Chat</td>
          <td class="basic"><icon class="x">—</icon></td>
          <td class="pro"><icon class="check">✓</icon></td>
          <td class="enterprise"><icon class="check">✓</icon></td>
        </tr>

        <tr>
          <td class="feature-name">Phone Support</td>
          <td class="basic"><icon class="x">—</icon></td>
          <td class="pro"><icon class="x">—</icon></td>
          <td class="enterprise"><icon class="check">✓</icon></td>
        </tr>

        <tr>
          <td class="feature-name">Dedicated Account Manager</td>
          <td class="basic"><icon class="x">—</icon></td>
          <td class="pro"><icon class="x">—</icon></td>
          <td class="enterprise"><icon class="check">✓</icon></td>
        </tr>

        <tr>
          <td class="feature-name">Onboarding & Training</td>
          <td class="basic">Self-service</td>
          <td class="pro">Guided</td>
          <td class="enterprise">White-glove</td>
        </tr>

        <!-- SECTION: Security -->
        <tr class="section-header">
          <td colspan="4">
            <h3>Security & Compliance</h3>
          </td>
        </tr>

        <tr>
          <td class="feature-name">SSL Encryption</td>
          <td class="basic"><icon class="check">✓</icon></td>
          <td class="pro"><icon class="check">✓</icon></td>
          <td class="enterprise"><icon class="check">✓</icon></td>
        </tr>

        <tr>
          <td class="feature-name">Two-Factor Authentication</td>
          <td class="basic"><icon class="x">—</icon></td>
          <td class="pro"><icon class="check">✓</icon></td>
          <td class="enterprise"><icon class="check">✓</icon></td>
        </tr>

        <tr>
          <td class="feature-name">SSO (Single Sign-On)</td>
          <td class="basic"><icon class="x">—</icon></td>
          <td class="pro"><icon class="x">—</icon></td>
          <td class="enterprise"><icon class="check">✓</icon></td>
        </tr>

        <tr>
          <td class="feature-name">Advanced Permissions</td>
          <td class="basic"><icon class="x">—</icon></td>
          <td class="pro">Basic</td>
          <td class="enterprise">Granular</td>
        </tr>

        <tr>
          <td class="feature-name">Compliance (SOC 2, HIPAA)</td>
          <td class="basic"><icon class="x">—</icon></td>
          <td class="pro"><icon class="x">—</icon></td>
          <td class="enterprise"><icon class="check">✓</icon></td>
        </tr>
      </tbody>

      <tfoot>
        <tr>
          <td></td>
          <td><button class="secondary">Start Free Trial</button></td>
          <td><button class="primary">Start Free Trial</button></td>
          <td><button class="secondary">Contact Sales</button></td>
        </tr>
      </tfoot>
    </table>
  </comparison-table>
</section>
```

### 4. FAQ Section (Addressing Objections)

```html
<section class="pricing-faq">
  <header>
    <h2>Frequently Asked Questions</h2>
    <subtitle>Everything you need to know about pricing</subtitle>
  </header>

  <faq-accordion>
    <!-- Payment & Billing -->
    <faq-item>
      <question>
        <icon>💳</icon>
        What payment methods do you accept?
      </question>
      <answer>
        We accept all major credit cards (Visa, Mastercard, American Express),
        PayPal, and ACH transfers for annual plans. Enterprise customers can
        also pay via invoice or wire transfer.
      </answer>
    </faq-item>

    <faq-item>
      <question>
        <icon>🔄</icon>
        Can I change or cancel my plan?
      </question>
      <answer>
        Absolutely! You can upgrade, downgrade, or cancel your plan anytime
        from your account settings. If you upgrade, you'll be charged
        immediately for the prorated difference. If you downgrade, the change
        takes effect at the end of your current billing cycle. No long-term
        contracts or cancellation fees.
      </answer>
    </faq-item>

    <faq-item>
      <question>
        <icon>💰</icon>
        Do you offer refunds?
      </question>
      <answer>
        Yes! We offer a 30-day money-back guarantee. If you're not completely
        satisfied within the first 30 days, contact us for a full refund, no
        questions asked.
      </answer>
    </faq-item>

    <faq-item>
      <question>
        <icon>📅</icon>
        What's the difference between monthly and annual billing?
      </question>
      <answer>
        Annual billing saves you 20% compared to paying monthly. For example,
        the Pro plan is $79/month ($948/year) when billed monthly, but only
        $758/year when billed annually—that's $190 in savings! Plus, you
        avoid the hassle of monthly payments.
      </answer>
    </faq-item>

    <!-- Free Trial -->
    <faq-item>
      <question>
        <icon>🎁</icon>
        How does the free trial work?
      </question>
      <answer>
        Start your 14-day free trial with no credit card required. You'll get
        full access to all features in your chosen plan. We'll send you a
        reminder before your trial ends, and you'll only be charged if you
        decide to continue. Cancel anytime during the trial with no charge.
      </answer>
    </faq-item>

    <faq-item>
      <question>
        <icon>🚀</icon>
        Can I upgrade during my trial?
      </question>
      <answer>
        Yes! You can upgrade from Basic to Pro (or Pro to Enterprise) at any
        time during your trial. Your trial period remains the same, and you'll
        get access to all the features of your new plan immediately.
      </answer>
    </faq-item>

    <!-- Plan Details -->
    <faq-item>
      <question>
        <icon>👥</icon>
        What counts as a "user"?
      </question>
      <answer>
        A user is anyone who has login access to your account. This includes
        team members, collaborators, and administrators. Guests or view-only
        access don't count toward your user limit.
      </answer>
    </faq-item>

    <faq-item>
      <question>
        <icon>📈</icon>
        What happens if I exceed my plan limits?
      </question>
      <answer>
        We'll notify you when you're approaching your limits (storage,
        projects, or users). You can either upgrade to a higher plan or
        manage your usage. We won't cut off your access unexpectedly—you'll
        always have time to adjust.
      </answer>
    </faq-item>

    <faq-item>
      <question>
        <icon>🏢</icon>
        Do you offer discounts for nonprofits or education?
      </question>
      <answer>
        Yes! We offer 25% discounts for registered nonprofits and educational
        institutions. Contact our sales team with your documentation to verify
        eligibility and claim your discount.
      </answer>
    </faq-item>

    <!-- Security & Compliance -->
    <faq-item>
      <question>
        <icon>🔒</icon>
        Is my data secure?
      </question>
      <answer>
        Absolutely. We use bank-level 256-bit SSL encryption, undergo regular
        security audits, and are SOC 2 Type II certified. Your data is
        encrypted at rest and in transit. Enterprise plans include additional
        security features like SSO and advanced permissions.
      </answer>
    </faq-item>

    <faq-item>
      <question>
        <icon>📜</icon>
        Are you GDPR/HIPAA compliant?
      </question>
      <answer>
        We are fully GDPR compliant for all plans. HIPAA compliance is
        available for Enterprise customers who require it. We can sign BAAs
        (Business Associate Agreements) for healthcare clients.
      </answer>
    </faq-item>

    <!-- Enterprise -->
    <faq-item>
      <question>
        <icon>💼</icon>
        How does Enterprise pricing work?
      </question>
      <answer>
        Enterprise pricing is customized based on your specific needs, including
        number of users, storage requirements, custom integrations, and support
        level. Contact our sales team for a personalized quote. Most Enterprise
        contracts start at $299/month.
      </answer>
    </faq-item>

    <faq-item>
      <question>
        <icon>📞</icon>
        Can I talk to someone before purchasing?
      </question>
      <answer>
        Of course! Our team is here to help. You can:
        • Chat with us (bottom right corner)
        • Email us at sales@yourcompany.com
        • Call us at 1-800-XXX-XXXX
        • Schedule a demo: [Link]
      </answer>
    </faq-item>
  </faq-accordion>

  <still-have-questions>
    <h3>Still have questions?</h3>
    <p>We're here to help!</p>
    <button class="primary">Contact Support</button>
    <button class="secondary">Schedule a Call</button>
  </still-have-questions>
</section>
```

### 5. Social Proof Section

```html
<section class="social-proof">
  <header>
    <h2>Trusted by Industry Leaders</h2>
  </header>

  <!-- Customer Logos -->
  <logo-cloud>
    [Company Logo 1]
    [Company Logo 2]
    [Company Logo 3]
    [Company Logo 4]
    [Company Logo 5]
    [Company Logo 6]
    [Company Logo 7]
    [Company Logo 8]
  </logo-cloud>

  <!-- Statistics -->
  <stats-grid>
    <stat>
      <number>10,000+</number>
      <label>Active Customers</label>
    </stat>

    <stat>
      <number>4.9/5</number>
      <label>Average Rating</label>
      <stars>⭐⭐⭐⭐⭐</stars>
    </stat>

    <stat>
      <number>99.9%</number>
      <label>Uptime SLA</label>
    </stat>

    <stat>
      <number>$50M+</number>
      <label>Revenue Processed</label>
    </stat>
  </stats-grid>

  <!-- Testimonials -->
  <testimonials>
    <h3>What Our Customers Say</h3>

    <testimonial-grid>
      <testimonial-card>
        <quote>
          "[Product] has transformed how we [outcome]. We've seen a [metric]
          increase in [KPI] since switching."
        </quote>
        <author>
          <avatar>[Photo]</avatar>
          <info>
            <name>[Full Name]</name>
            <title>[Title], [Company]</title>
          </info>
        </author>
        <rating>⭐⭐⭐⭐⭐</rating>
      </testimonial-card>

      [Repeat 3-6 testimonials]

    </testimonial-grid>
  </testimonials>

  <!-- Reviews -->
  <review-platforms>
    <h3>Rated Excellent Across Platforms</h3>

    <platform-grid>
      <platform>
        <logo>[G2 Logo]</logo>
        <rating>4.8/5 (324 reviews)</rating>
        <link>Read reviews →</link>
      </platform>

      <platform>
        <logo>[Capterra Logo]</logo>
        <rating>4.9/5 (198 reviews)</rating>
        <link>Read reviews →</link>
      </platform>

      <platform>
        <logo>[TrustPilot Logo]</logo>
        <rating>4.7/5 (562 reviews)</rating>
        <link>Read reviews →</link>
      </platform>
    </platform-grid>
  </review-platforms>
</section>
```

### 6. Money-Back Guarantee

```html
<section class="guarantee">
  <badge-icon>
    [Shield/Badge Icon]
  </badge-icon>

  <content>
    <h2>30-Day Money-Back Guarantee</h2>

    <p>
      Try [Product] risk-free for 30 days. If you're not completely satisfied,
      we'll refund your money—no questions asked.
    </p>

    <guarantee-details>
      <detail>
        <icon>✓</icon>
        <text>Full refund within 30 days</text>
      </detail>

      <detail>
        <icon>✓</icon>
        <text>No questions asked</text>
      </detail>

      <detail>
        <icon>✓</icon>
        <text>Cancel anytime</text>
      </detail>

      <detail>
        <icon>✓</icon>
        <text>Keep all your data</text>
      </detail>
    </guarantee-details>

    <testimonial>
      "I was skeptical at first, but the 30-day guarantee made it a no-brainer
      to try. Best decision ever!"
      <author>— [Customer Name], [Title]</author>
    </testimonial>
  </content>
</section>
```

### 7. Calculator or ROI Tool

```html
<section class="roi-calculator">
  <header>
    <h2>Calculate Your ROI</h2>
    <subtitle>See how much you could save with [Product]</subtitle>
  </header>

  <calculator-form>
    <input-group>
      <label>
        How many [projects/users/hours] per month?
        <input type="number" id="quantity" value="10" />
      </label>
    </input-group>

    <input-group>
      <label>
        Average [cost/time] per [unit]?
        <input type="number" id="cost" value="50" />
      </label>
    </input-group>

    <input-group>
      <label>
        Expected efficiency gain with [Product]?
        <select id="efficiency">
          <option value="0.2">20% faster</option>
          <option value="0.3" selected>30% faster</option>
          <option value="0.5">50% faster</option>
        </select>
      </label>
    </input-group>

    <button onclick="calculateROI()">Calculate Savings</button>
  </calculator-form>

  <results-display id="roiResults" style="display:none;">
    <result-card>
      <label>Monthly Savings</label>
      <value id="monthlySavings">$1,500</value>
    </result-card>

    <result-card>
      <label>Annual Savings</label>
      <value id="annualSavings">$18,000</value>
    </result-card>

    <result-card>
      <label>ROI</label>
      <value id="roiPercentage">1,900%</value>
    </result-card>

    <result-card>
      <label>Payback Period</label>
      <value id="paybackPeriod">< 1 week</value>
    </result-card>

    <cta>
      <h3>Ready to start saving?</h3>
      <button class="primary">Start Free Trial</button>
    </cta>
  </results-display>
</section>

<script>
function calculateROI() {
  const quantity = parseFloat(document.getElementById('quantity').value);
  const cost = parseFloat(document.getElementById('cost').value);
  const efficiency = parseFloat(document.getElementById('efficiency').value);

  const currentMonthlyCost = quantity * cost;
  const monthlySavings = currentMonthlyCost * efficiency;
  const annualSavings = monthlySavings * 12;

  const planCost = 79; // Pro plan monthly cost
  const netMonthlySavings = monthlySavings - planCost;
  const roi = ((netMonthlySavings * 12) / (planCost * 12)) * 100;
  const paybackDays = Math.ceil((planCost / monthlySavings) * 30);

  document.getElementById('monthlySavings').textContent = `$${Math.round(monthlySavings).toLocaleString()}`;
  document.getElementById('annualSavings').textContent = `$${Math.round(annualSavings).toLocaleString()}`;
  document.getElementById('roiPercentage').textContent = `${Math.round(roi)}%`;
  document.getElementById('paybackPeriod').textContent = paybackDays < 7 ? '< 1 week' : `${paybackDays} days`;

  document.getElementById('roiResults').style.display = 'grid';
}
</script>
```

### 8. CTA Optimization

#### Final CTA Section:

```html
<section class="final-cta">
  <container>
    <h2>Ready to Get Started?</h2>
    <subtitle>
      Join 10,000+ businesses already using [Product] to [achieve outcome]
    </subtitle>

    <cta-buttons>
      <button class="primary large">
        Start Your Free Trial
        <subtext>14 days free. No credit card required.</subtext>
      </button>

      <button class="secondary large">
        Schedule a Demo
        <subtext>See [Product] in action</subtext>
      </button>
    </cta-buttons>

    <trust-indicators>
      <indicator>
        <icon>✓</icon>
        <text>No credit card required</text>
      </indicator>

      <indicator>
        <icon>✓</icon>
        <text>Cancel anytime</text>
      </indicator>

      <indicator>
        <icon>✓</icon>
        <text>30-day money-back guarantee</text>
      </indicator>

      <indicator>
        <icon>✓</icon>
        <text>Setup in 5 minutes</text>
      </indicator>
    </trust-indicators>
  </container>
</section>
```

### 9. A/B Testing Setup

#### Elements to Test:

**Test 1: Pricing Display**
- **Variant A:** Monthly price prominent
- **Variant B:** Annual price prominent (with savings)
- **Variant C:** "Starting at $X/day"

**Test 2: Plan Emphasis**
- **Variant A:** Pro plan highlighted (most popular badge)
- **Variant B:** No highlighting
- **Variant C:** All plans equal emphasis

**Test 3: CTA Button Text**
- **Variant A:** "Start Free Trial"
- **Variant B:** "Get Started Free"
- **Variant C:** "Try [Product] Free"
- **Variant D:** "Start Saving Today"

**Test 4: Guarantee Placement**
- **Variant A:** Above pricing cards
- **Variant B:** Below pricing cards
- **Variant C:** In sidebar (sticky)

**Test 5: Comparison Table**
- **Variant A:** Full table above fold
- **Variant B:** Collapsed, "Show Full Comparison"
- **Variant C:** No table, just pricing cards

**Test 6: Annual Toggle**
- **Variant A:** Toggle defaulting to monthly
- **Variant B:** Toggle defaulting to annual
- **Variant C:** No toggle, show both prices

**Implementation:**
```javascript
// Google Optimize or VWO integration
if (window.google_optimize !== undefined) {
  const variant = google_optimize.get('EXPERIMENT_ID');

  switch(variant) {
    case '0': // Control
      // Original pricing page
      break;
    case '1': // Variant A
      showAnnualPricingFirst();
      break;
    case '2': // Variant B
      emphasizeProPlan();
      break;
  }
}

// Track conversions
function trackPricingPageConversion(plan, billingCycle) {
  gtag('event', 'purchase_intent', {
    'event_category': 'Pricing',
    'event_label': `${plan}-${billingCycle}`,
    'value': getPlanValue(plan)
  });

  // Google Optimize
  google_optimize.event('pricing_page_conversion');
}
```

## Output Format

Provide:

1. **Complete Pricing Page HTML** (fully functional with all sections)
2. **CSS Stylesheet** (responsive design, mobile-optimized)
3. **JavaScript Functionality** (annual toggle, calculator, comparisons)
4. **3 Pricing Tiers** (complete with features, pricing, CTAs)
5. **Feature Comparison Matrix** (comprehensive table with 50+ features)
6. **15+ FAQ Items** (addressing all common objections)
7. **Social Proof Section** (testimonials, logos, statistics)
8. **ROI Calculator** (interactive tool with custom logic)
9. **A/B Testing Plan** (6+ test variations with hypotheses)
10. **Analytics Tracking** (conversion events, heatmaps, scroll tracking)
11. **Mobile-Responsive Design** (optimized for all devices)

Ask clarifying questions about the product/service, target audience, competitive pricing, value proposition, existing customers, conversion goals, and technical platform before creating the pricing page.
