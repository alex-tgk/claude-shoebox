# Affiliate Program System Creator

Create a complete affiliate marketing program with dashboard, tracking, payment processing, marketing materials, and fraud prevention for the product or service specified by the user.

## Instructions

Build a comprehensive affiliate system including:

### 1. Affiliate Program Strategy

#### Program Structure:
- **Program name and branding**
- Target affiliate profile (bloggers, influencers, courses, etc.)
- Commission structure and tiers
- Cookie duration (30, 60, 90 days)
- Payment terms and schedule
- Program goals (revenue, reach, partners)

#### Commission Models:

**Revenue Share:**
- Percentage per sale (typical: 20-50%)
- Tiered commissions based on performance
- Recurring commissions (for subscriptions)
- Lifetime commissions (vs first purchase only)

**Flat Rate:**
- Fixed amount per sale
- Fixed amount per lead
- Hybrid (base + percentage)

**Performance Tiers:**
```
Bronze (0-10 sales): 25% commission
Silver (11-50 sales): 30% commission
Gold (51-100 sales): 35% commission
Platinum (101+ sales): 40% commission + bonuses
```

### 2. Affiliate Dashboard (Full Application)

#### Tech Stack Recommendations:

**Frontend:**
- React or Next.js
- Tailwind CSS or Material-UI
- Chart.js or Recharts (analytics)
- Responsive design

**Backend:**
- Node.js (Express) or Python (Django/Flask)
- PostgreSQL or MySQL database
- Redis for caching
- RESTful API or GraphQL

**Authentication:**
- JWT tokens
- OAuth integration (Google, Facebook)
- Email verification
- 2FA optional

#### Dashboard Features:

**1. Overview/Home Page:**
```
Components:
- Welcome message with affiliate name
- Quick stats cards:
  * Total earnings (all-time)
  * This month's earnings
  * Pending commissions
  * Clicks this month
  * Conversions this month
  * Conversion rate
- Recent activity feed
- Performance chart (last 30 days)
- Top performing links
- Leaderboard position
- Announcements from admin
```

**2. Links & Creatives Page:**
```
Features:
- Generate unique affiliate links
- Link shortener integration
- Deep linking to specific products/pages
- QR code generation
- Social share buttons
- Link performance by URL
- Copy-to-clipboard functionality
- Link categorization/tagging

Display:
- Product image
- Product name
- Commission rate
- Your unique link
- Copy button
- Share buttons (Twitter, Facebook, LinkedIn)
- Performance stats (clicks, conversions)
```

**3. Marketing Materials Library:**
```
Categories:
- Banner ads (all sizes: 728x90, 300x250, 160x600, etc.)
- Social media graphics (Instagram, Facebook, Twitter)
- Email swipe copy (3-5 pre-written emails)
- Social media captions
- Product images (high-res)
- Video assets
- Blog post templates
- Case studies
- Sales scripts

Format:
- Preview thumbnail
- Download button
- Dimensions/specs
- Usage tips
- Performance data (if used by others)
```

**4. Earnings & Reports Page:**
```
Views:
- Earnings summary (total, paid, pending, upcoming)
- Earnings chart (daily, weekly, monthly views)
- Transaction history table:
  * Date
  * Order ID
  * Customer (anonymized)
  * Product
  * Sale amount
  * Commission earned
  * Status (pending, approved, paid)
  * Payment date

Filters:
- Date range
- Product
- Status
- Payment method

Export:
- CSV download
- PDF reports
- Tax documents
```

**5. Analytics & Performance:**
```
Metrics:
- Clicks (total, unique, by source)
- Conversions (count, rate, value)
- Click-to-conversion funnel
- Top traffic sources
- Top converting products
- Geographic data
- Device breakdown (mobile, desktop)
- Time-of-day analysis
- Seasonal trends

Visualizations:
- Line charts for trends
- Pie charts for breakdowns
- Funnel visualization
- Heat map calendar
```

**6. Payment Settings:**
```
Configuration:
- Payment method selection:
  * PayPal
  * Bank transfer (ACH)
  * Wire transfer
  * Cryptocurrency (optional)
  * Check by mail
- Payment threshold (minimum payout)
- Payment schedule preference
- Tax information (W-9, VAT, etc.)
- Invoicing preferences

Security:
- Encrypted storage
- 2FA for payment changes
- Email verification for updates
```

**7. Account Settings:**
```
Profile:
- Personal information
- Profile photo
- Bio/description
- Website URL
- Social media links
- Niche/category

Preferences:
- Email notifications (toggle by type)
- Dashboard language
- Timezone
- Currency display

API Access:
- API key generation
- Webhook configuration
- Documentation link
```

**8. Support & Resources:**
```
Sections:
- FAQ database
- Video tutorials
- Best practices guide
- Success stories
- Contact support form
- Community forum link
- Affiliate agreement
- Terms and conditions
```

### 3. Commission Tracking System

#### Database Schema:

```sql
-- Affiliates table
CREATE TABLE affiliates (
  id SERIAL PRIMARY KEY,
  user_id INTEGER REFERENCES users(id),
  affiliate_code VARCHAR(50) UNIQUE NOT NULL,
  status VARCHAR(20) DEFAULT 'active',
  tier VARCHAR(20) DEFAULT 'bronze',
  total_earnings DECIMAL(10,2) DEFAULT 0,
  paid_earnings DECIMAL(10,2) DEFAULT 0,
  pending_earnings DECIMAL(10,2) DEFAULT 0,
  total_clicks INTEGER DEFAULT 0,
  total_conversions INTEGER DEFAULT 0,
  joined_date TIMESTAMP DEFAULT NOW(),
  payment_email VARCHAR(255),
  payment_method VARCHAR(50),
  tax_id VARCHAR(50)
);

-- Clicks table
CREATE TABLE affiliate_clicks (
  id SERIAL PRIMARY KEY,
  affiliate_id INTEGER REFERENCES affiliates(id),
  clicked_at TIMESTAMP DEFAULT NOW(),
  ip_address VARCHAR(45),
  user_agent TEXT,
  referrer TEXT,
  landing_page TEXT,
  device_type VARCHAR(20),
  country VARCHAR(2),
  converted BOOLEAN DEFAULT FALSE
);

-- Conversions/Sales table
CREATE TABLE affiliate_conversions (
  id SERIAL PRIMARY KEY,
  affiliate_id INTEGER REFERENCES affiliates(id),
  click_id INTEGER REFERENCES affiliate_clicks(id),
  order_id VARCHAR(100) UNIQUE,
  customer_email VARCHAR(255),
  product_id INTEGER,
  sale_amount DECIMAL(10,2),
  commission_amount DECIMAL(10,2),
  commission_rate DECIMAL(5,2),
  status VARCHAR(20) DEFAULT 'pending', -- pending, approved, paid, refunded
  converted_at TIMESTAMP DEFAULT NOW(),
  approved_at TIMESTAMP,
  paid_at TIMESTAMP
);

-- Payouts table
CREATE TABLE affiliate_payouts (
  id SERIAL PRIMARY KEY,
  affiliate_id INTEGER REFERENCES affiliates(id),
  amount DECIMAL(10,2),
  payment_method VARCHAR(50),
  transaction_id VARCHAR(255),
  status VARCHAR(20) DEFAULT 'pending',
  requested_at TIMESTAMP DEFAULT NOW(),
  processed_at TIMESTAMP,
  notes TEXT
);

-- Commission rules table
CREATE TABLE commission_rules (
  id SERIAL PRIMARY KEY,
  product_id INTEGER,
  tier VARCHAR(20),
  commission_type VARCHAR(20), -- percentage, fixed
  commission_value DECIMAL(10,2),
  recurring BOOLEAN DEFAULT FALSE,
  active BOOLEAN DEFAULT TRUE
);
```

#### Tracking Implementation:

**JavaScript Tracking Code:**
```javascript
// Embed on all pages of main site
(function() {
  // Check for affiliate cookie
  const urlParams = new URLSearchParams(window.location.search);
  const affCode = urlParams.get('ref') || urlParams.get('aff');

  if (affCode) {
    // Set cookie for 30 days (or configured duration)
    document.cookie = `aff_ref=${affCode}; path=/; max-age=2592000; SameSite=Lax`;

    // Track click via API
    fetch('/api/affiliate/track-click', {
      method: 'POST',
      headers: {'Content-Type': 'application/json'},
      body: JSON.stringify({
        affiliateCode: affCode,
        referrer: document.referrer,
        landingPage: window.location.href,
        userAgent: navigator.userAgent
      })
    });
  }
})();
```

**Conversion Tracking:**
```javascript
// Fire on checkout success page
function trackAffiliateConversion(orderData) {
  const affCode = getCookie('aff_ref');

  if (affCode) {
    fetch('/api/affiliate/track-conversion', {
      method: 'POST',
      headers: {'Content-Type': 'application/json'},
      body: JSON.stringify({
        affiliateCode: affCode,
        orderId: orderData.orderId,
        amount: orderData.total,
        products: orderData.products
      })
    });
  }
}
```

### 4. Payment Processing Integration

#### Payment Workflow:

**1. Commission Approval Process:**
```
Sale Made → Pending (awaiting refund window)
  ↓ (30 days or custom)
Approved → Ready for payout
  ↓ (on payment schedule)
Paid → Commission distributed
```

**2. Automated Payout System:**

**PayPal Mass Pay Integration:**
```python
# Example using PayPal SDK
def process_affiliate_payouts():
    # Get affiliates ready for payout
    affiliates = get_payouts_ready()

    paypal_batch = []
    for affiliate in affiliates:
        if affiliate.balance >= MINIMUM_PAYOUT:
            paypal_batch.append({
                'recipient_email': affiliate.paypal_email,
                'amount': affiliate.balance,
                'note': f'Affiliate commission - {current_month}',
                'sender_item_id': f'AFF-{affiliate.id}-{timestamp}'
            })

    # Send batch payment
    response = paypal.payout.create(paypal_batch)

    # Update database
    for payout in response.payouts:
        record_payout(payout)
```

**Stripe Connect (for direct deposits):**
```javascript
// Create connected account for affiliate
async function setupAffiliateStripe(affiliateId, bankAccount) {
  const account = await stripe.accounts.create({
    type: 'express',
    country: 'US',
    email: affiliate.email,
    capabilities: {
      transfers: {requested: true}
    }
  });

  // Save account ID
  await updateAffiliate(affiliateId, {
    stripe_account_id: account.id
  });
}

// Process payout
async function payAffiliate(affiliateId, amount) {
  const affiliate = await getAffiliate(affiliateId);

  const transfer = await stripe.transfers.create({
    amount: amount * 100, // Convert to cents
    currency: 'usd',
    destination: affiliate.stripe_account_id,
    description: 'Affiliate commission payout'
  });

  return transfer;
}
```

**Manual Payment Options:**
- Bank transfer (ACH) via Plaid or Stripe
- Wire transfer for international
- Cryptocurrency (using Coinbase Commerce)
- Check by mail (automated check printing)

#### Payment Reporting:
- Monthly payout reports via email
- 1099 generation (for US affiliates)
- International tax compliance
- Payment history CSV exports

### 5. Marketing Materials for Affiliates

#### Email Swipe Copy (5 Pre-Written Emails):

**Email 1: Introduction**
```
Subject: Discovered something you'll want to see

Hey [First Name],

I recently came across [Product Name] and had to share it with you.

[Brief problem statement]

[Product Name] solves this by [key benefit].

I've been using it for [timeframe] and [personal result/testimonial].

Check it out here: [Affiliate Link]

[Your Name]

P.S. They're offering [special offer/guarantee] right now.
```

**Email 2: Problem-Focused**
**Email 3: Story-Based**
**Email 4: Urgency/Scarcity**
**Email 5: FAQ/Objection Handler**

#### Social Media Post Templates:

**Twitter/X:**
```
🔥 Hot take: [Opinion about problem]

That's why I use [Product Name].

[One-line benefit]

Try it: [Short Link]

#[RelevantHashtags]
```

**Instagram Caption:**
```
[Attention-grabbing first line]

If you're struggling with [problem], you need to see this.

[Product Name] has helped me [specific result] and I think it could help you too.

Here's what I love about it:
✅ [Benefit 1]
✅ [Benefit 2]
✅ [Benefit 3]

Link in bio to check it out 👆

#[Hashtags]
```

**Facebook Post:**
```
[Personal story introduction]

I've been using [Product Name] for [timeframe] now and wanted to share my experience.

[2-3 paragraphs about results and benefits]

If you're interested, you can learn more here: [Link]

Feel free to ask me any questions in the comments!
```

**LinkedIn:**
```
Professional version focusing on business results and ROI
```

#### Banner Ad Specifications:

**Sizes to Provide:**
- Leaderboard: 728x90
- Medium Rectangle: 300x250
- Wide Skyscraper: 160x600
- Large Rectangle: 336x280
- Half Page: 300x600
- Mobile Banner: 320x50
- Mobile Leaderboard: 320x100

**Design Variations:**
- 3-5 different designs per size
- Animated GIFs (3-frame max)
- Static images
- Multiple color schemes
- A/B tested versions

**Banner Elements:**
- Product image or logo
- Compelling headline
- Key benefit
- Call-to-action button
- Trust indicator (rating, users count)

#### Video Assets:
- 30-second product demo
- 60-second testimonial compilation
- 15-second social media teasers
- Unboxing videos (if physical product)
- Tutorial/how-to videos

### 6. Affiliate Agreement and Terms

#### Key Agreement Sections:

**1. Program Overview:**
- How the program works
- Commission structure
- Payment terms and schedule
- Cookie duration

**2. Affiliate Responsibilities:**
- Ethical promotion guidelines
- Prohibited marketing methods:
  * Spam
  * Trademark bidding (PPC)
  * False claims
  * Incentivized traffic
  * Cookie stuffing
- Content quality standards
- Disclosure requirements (FTC compliance)

**3. Company Rights:**
- Right to reject affiliate applications
- Right to terminate affiliates
- Right to modify commission rates
- Right to reverse fraudulent commissions
- Right to withhold payment for violations

**4. Payment Terms:**
- Payment schedule (monthly, bi-weekly)
- Minimum payout threshold
- Payment methods available
- Tax documentation required
- Refund/chargeback policies

**5. Liability and Warranties:**
- Limitation of liability
- No warranties on earnings
- Independent contractor relationship
- Indemnification clause

**6. Termination:**
- Termination rights (both parties)
- Unpaid commission handling
- Post-termination obligations

**7. Compliance:**
- FTC endorsement guidelines
- GDPR compliance (EU affiliates)
- CAN-SPAM compliance
- State-specific regulations

### 7. Admin Panel for Management

#### Admin Dashboard Features:

**Affiliate Management:**
- View all affiliates (searchable, filterable)
- Approve/reject applications
- Change affiliate tiers
- Suspend/ban affiliates
- Contact affiliates (email tool)
- Add internal notes
- View affiliate profile and performance

**Commission Management:**
- Approve/reject conversions
- Adjust commission amounts
- Process refunds
- Mass approve pending commissions
- Set commission rules by product
- Override specific commissions

**Payout Management:**
- View pending payouts
- Process payouts (batch or individual)
- Export payout data for accounting
- View payout history
- Handle payout disputes
- Generate tax documents

**Analytics & Reporting:**
- Total program performance
- Top performing affiliates
- Revenue by affiliate
- Conversion rates
- Traffic sources
- Fraud detection alerts
- ROI calculations

**Content Management:**
- Upload marketing materials
- Update affiliate resources
- Manage FAQ content
- Post announcements
- Update terms and conditions

**Settings:**
- Commission structure configuration
- Payment schedule settings
- Cookie duration
- Email template customization
- Fraud detection rules
- API key management

### 8. Fraud Detection & Prevention

#### Detection Methods:

**1. Click Fraud Detection:**
```javascript
// Red flags to monitor
const fraudIndicators = {
  // Too many clicks from same IP
  clicksPerIP: {threshold: 10, timeWindow: '1 hour'},

  // Clicks with no user engagement
  bounceRate: {threshold: 95},

  // Suspicious user agents or patterns
  botDetection: true,

  // Referrer anomalies
  suspiciousReferrers: ['spam-site.com', 'fake-traffic.com'],

  // Click-to-conversion time (too fast = suspicious)
  conversionSpeed: {min: '10 seconds'},

  // Geographic inconsistencies
  ipCountryMismatch: true
};
```

**2. Conversion Fraud Detection:**
- Self-referral detection (affiliate's own orders)
- Cookie stuffing detection
- Duplicate order checking
- Abandoned cart manipulation
- Test card usage patterns
- VPN/proxy detection

**3. Traffic Quality Monitoring:**
```
Good traffic indicators:
- Varied IP addresses
- Reasonable bounce rates (30-70%)
- Normal session duration
- Multiple page views
- Organic-looking referrers

Bad traffic indicators:
- Clustered IP ranges
- 90%+ bounce rate
- <5 second sessions
- Direct traffic with affiliate cookie
- Bot user agents
```

**4. Automated Fraud Prevention:**
```python
def check_for_fraud(conversion):
    risk_score = 0

    # Check IP against affiliate's IP
    if conversion.ip == affiliate.ip:
        risk_score += 50

    # Check time from click to conversion
    if conversion.time - click.time < 10: # seconds
        risk_score += 30

    # Check for duplicate email
    if email_used_before(conversion.email):
        risk_score += 40

    # Check for suspicious patterns
    if suspicious_email_pattern(conversion.email):
        risk_score += 20

    # High risk = flag for manual review
    if risk_score >= 70:
        flag_for_review(conversion)
        return False

    return True
```

**5. Affiliate Screening:**
- Application review process
- Website quality check
- Social media verification
- Previous program participation
- Traffic source declaration
- Background check for high-tier

### 9. Gamification & Leaderboards

#### Leaderboard System:

**Public Leaderboard (Dashboard):**
```
Top Affiliates This Month:

1. 🥇 [Affiliate Name] - $45,230 earnings | 523 sales
2. 🥈 [Affiliate Name] - $38,105 earnings | 442 sales
3. 🥉 [Affiliate Name] - $31,890 earnings | 387 sales
...
10. [Affiliate Name] - $18,340 earnings | 215 sales

Your Rank: #23 out of 1,847 affiliates
```

**Categories:**
- Top earners (overall)
- Most sales (volume)
- Highest conversion rate
- Fastest growing
- Most clicks
- Rookie of the month (new affiliates)

#### Gamification Elements:

**Badges & Achievements:**
- First Sale 🎉
- 10 Sales Club 🔟
- 100 Sales Club 💯
- $1K Earned 💰
- $10K Earned 💎
- $100K Earned 👑
- Perfect Month (100% approval rate) ⭐
- Top 10 Finisher 🏆
- Referral Master (recruited affiliates) 🤝

**Challenges & Contests:**
```
Monthly Challenge: Summer Sales Blast

Goal: 50 sales in July
Reward: $500 bonus + Platinum status upgrade

Progress: [■■■■■■■■□□] 38/50 sales

Time Remaining: 8 days
```

**Bonus Structures:**
- Milestone bonuses ($1K, $5K, $10K earned)
- Contest prizes (top 3 affiliates)
- Seasonal promotions (double commissions week)
- Referral bonuses (recruit other affiliates)

### 10. Integration & API

#### RESTful API Endpoints:

```
Authentication:
POST /api/auth/login
POST /api/auth/register
POST /api/auth/refresh

Affiliate Operations:
GET /api/affiliate/profile
PUT /api/affiliate/profile
GET /api/affiliate/stats
GET /api/affiliate/earnings
GET /api/affiliate/links
POST /api/affiliate/generate-link

Tracking:
POST /api/track/click
POST /api/track/conversion
GET /api/track/analytics

Payouts:
GET /api/payouts/history
POST /api/payouts/request
GET /api/payouts/methods

Resources:
GET /api/resources/banners
GET /api/resources/emails
GET /api/resources/creatives
```

#### Webhook Support:
```javascript
// Notify affiliates of events
webhooks = {
  'sale.created': 'https://affiliate-site.com/webhook',
  'commission.approved': 'https://affiliate-site.com/webhook',
  'payout.processed': 'https://affiliate-site.com/webhook'
};

// Payload example
{
  "event": "sale.created",
  "timestamp": "2025-11-06T10:30:00Z",
  "data": {
    "affiliate_id": "AFF123",
    "order_id": "ORD-45678",
    "commission": 45.00,
    "status": "pending"
  }
}
```

### 11. Compliance & Legal

#### FTC Compliance:
- Require disclosure in affiliate content
- Provide disclosure templates
- Monitor compliance (spot checks)
- Terminate non-compliant affiliates

**Disclosure Template:**
```
"I may earn a commission if you purchase through my link.
This comes at no extra cost to you."
```

#### GDPR Compliance:
- Cookie consent for EU visitors
- Data processing agreements with affiliates
- Right to data deletion
- Data export functionality

#### Tax Compliance:
- Collect W-9 (US) or W-8 (international)
- Generate 1099-NEC forms (US)
- Track thresholds ($600 US)
- Provide tax documentation

### 12. Launch & Recruitment Strategy

#### Finding Affiliates:

**Outreach Channels:**
- Direct outreach to relevant bloggers/influencers
- Affiliate network listings (ShareASale, CJ, Impact)
- Social media recruitment campaigns
- Existing customer conversion (turn customers into affiliates)
- Competitor affiliate poaching (ethical)
- Affiliate recruiting agencies

**Application Funnel:**
```
Landing Page: "Join Our Affiliate Program"
  ↓
Application Form
  ↓
Auto-response: "Application received"
  ↓
Manual Review (approve/reject)
  ↓
Welcome Email + Dashboard Access
  ↓
Onboarding Sequence (5 emails)
  ↓
Active Affiliate
```

**Onboarding Email Sequence:**
1. Welcome + Dashboard tour
2. How to create your first link
3. Marketing materials library tour
4. Best practices & tips
5. Payment setup reminder

## Output Format

Provide:

1. **Complete Affiliate Dashboard** (React + Node.js codebase or detailed wireframes)
2. **Database Schema** (SQL with all tables and relationships)
3. **Tracking System** (JavaScript tracking code + backend API)
4. **Commission Rules Engine** (configuration and logic)
5. **Marketing Materials Pack** (5 email swipes, 20+ social posts, 10+ banner ads)
6. **Affiliate Agreement** (complete legal document)
7. **Admin Panel Specification** (features and wireframes)
8. **Fraud Detection System** (rules and implementation)
9. **Payment Integration Code** (PayPal + Stripe setup)
10. **API Documentation** (endpoints, authentication, examples)
11. **Launch Strategy Document** (recruitment and onboarding plan)

Ask clarifying questions about the product/service, commission structure, existing payment infrastructure, target affiliate profile, and budget before building the affiliate program.
