# Create Sales Funnel

Generate a complete, high-converting sales funnel system with landing pages, email sequences, sales pages, upsells, payment integration, and conversion optimization.

## Instructions

You are tasked with creating a COMPLETE, revenue-optimized sales funnel. This is a one-shot command that must produce a fully functional funnel system ready for immediate deployment and revenue generation.

### Step 1: Gather Requirements

First, ask the user these essential questions:
1. **Product/Service**: What are you selling?
2. **Price Point**: Main offer price? Upsells? Downsells?
3. **Target Audience**: Who is your ideal customer?
4. **Lead Magnet**: What will attract leads? (ebook, checklist, video, webinar)
5. **Traffic Source**: Where will traffic come from? (ads, organic, partnerships)
6. **Email Service**: Which ESP? (Mailchimp, ConvertKit, ActiveCampaign)
7. **Payment Processor**: Stripe, PayPal, or other?
8. **Goal**: Revenue target per month?

### Step 2: Complete Funnel Structure

```
sales-funnel/
├── pages/
│   ├── 01-landing-page/
│   │   ├── index.html
│   │   ├── styles.css
│   │   ├── script.js
│   │   └── assets/
│   ├── 02-thank-you-page/
│   │   ├── index.html
│   │   └── tripwire-offer.html
│   ├── 03-sales-page/
│   │   ├── index.html
│   │   ├── long-form.html
│   │   └── vsl-page.html
│   ├── 04-order-form/
│   │   ├── checkout.html
│   │   └── order-bump.html
│   ├── 05-upsell-pages/
│   │   ├── upsell-1.html
│   │   ├── upsell-2.html
│   │   └── downsell.html
│   ├── 06-confirmation/
│   │   ├── success.html
│   │   └── onboarding.html
│   └── 07-cart-abandonment/
│       └── recovery.html
├── emails/
│   ├── sequences/
│   │   ├── welcome-series/
│   │   ├── nurture-sequence/
│   │   ├── sales-sequence/
│   │   └── post-purchase/
│   └── templates/
├── copy/
│   ├── headlines.md
│   ├── bullet-points.md
│   ├── testimonials.md
│   └── faqs.md
├── integrations/
│   ├── stripe-setup.js
│   ├── email-integration.js
│   ├── analytics.js
│   └── crm-sync.js
├── tracking/
│   ├── pixel-setup.html
│   ├── conversion-tracking.js
│   └── funnel-analytics.md
├── optimization/
│   ├── ab-tests.md
│   ├── conversion-checklist.md
│   └── optimization-plan.md
└── README.md
```

### Step 3: Funnel Flow Architecture

```markdown
# Sales Funnel Architecture

## Traffic Sources → Landing Page
**Sources**:
- Facebook Ads ($500/month budget)
- Google Ads ($300/month budget)
- Instagram Ads ($200/month budget)
- Organic (SEO, content marketing)
- Partnerships (affiliate, JVs)

**Landing Page Goal**: Capture email with lead magnet
**Conversion Target**: 40-50%

↓

## Step 1: Landing Page (Lead Capture)
**Offer**: Free [Lead Magnet] worth $47
**Elements**:
- Compelling headline
- 3-5 key benefits
- Social proof (testimonials/numbers)
- Lead magnet preview
- Email capture form
- Exit-intent popup

**Traffic**: 1,000 visitors/day
**Expected Conversions**: 400-500 leads/day
**Cost per Lead**: $2-3

↓

## Step 2: Thank You Page + Tripwire
**Offer**: Limited-time $7 tripwire offer
**Purpose**: Indoctrinate, ascend, monetize
**Elements**:
- Deliver lead magnet
- Video explaining tripwire
- Time-limited discount (20 min timer)
- 1-click purchase
- Risk reversal (money-back guarantee)

**Conversion Target**: 10-15% of leads
**Revenue**: $280-525/day from tripwire

↓

## Step 3: Email Nurture Sequence (5-7 days)
**Purpose**: Build trust, demonstrate value, sell main offer
**Sequence**:
1. Welcome + deliver lead magnet
2. Quick win / case study
3. Overcome objection #1
4. Social proof / testimonials
5. Overcome objection #2
6. Scarcity / urgency
7. Last chance / pitch main offer

**Open Rate Target**: 35-45%
**Click Rate Target**: 10-15%

↓

## Step 4: Sales Page (Main Offer)
**Offer**: [Main Product] at $297
**Format**: Long-form VSL or written sales letter
**Elements**:
- Hook (problem → agitation)
- Story (relatability)
- Solution (product reveal)
- Value demonstration
- Social proof (10+ testimonials)
- Guarantee
- Bonuses ($500+ value)
- FAQ
- Multiple CTAs
- Scarcity/urgency

**Conversion Target**: 3-5% of email list
**Revenue**: $3,564-5,940/day

↓

## Step 5: Order Form + Order Bump
**Order Form**: Stripe checkout
**Order Bump**: Add [Complement Product] for $47 (30% take rate)
**Total Order Value**: $297 + $14 (avg) = $311

↓

## Step 6: Upsell Sequence
**Upsell #1**: Premium version at $497 (25% take rate)
**Upsell #2**: Done-for-you service at $997 (10% take rate)
**Downsell**: Payment plan - 3 payments of $117 (40% take rate)

**Average Order Value**: $450

↓

## Step 7: Order Confirmation + Onboarding
**Purpose**: Deliver product, set expectations, reduce refunds
**Elements**:
- Order confirmation
- Access credentials
- Welcome video
- Quick start guide
- Support information
- Community invitation

↓

## Step 8: Post-Purchase Sequence
**Purpose**: Onboard, engage, retain, refer
**Emails**:
1. Welcome + access (immediate)
2. Getting started guide (Day 1)
3. Quick win tip (Day 3)
4. Check-in + support (Day 7)
5. Success story (Day 14)
6. Referral request (Day 30)

## Funnel Math

**Daily Traffic**: 1,000 visitors
**Lead Capture Rate**: 45% = 450 leads
**Tripwire Conversion**: 12% × 450 = 54 sales × $7 = $378

**Main Offer Conversion**: 4% × 450 = 18 sales × $311 = $5,598
**Upsells**: 18 × $150 (avg upsell) = $2,700

**Daily Revenue**: $378 + $5,598 + $2,700 = $8,676
**Monthly Revenue**: $260,280

**Ad Spend**: $1,000/day
**Revenue**: $8,676/day
**Profit**: $7,676/day
**ROI**: 768%
```

### Step 4: Landing Page (Lead Magnet)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Get Your Free [Lead Magnet] ($47 Value)</title>

    <!-- Meta Tags for SEO & Social -->
    <meta name="description" content="Download our free [lead magnet] and learn how to [achieve result] in [timeframe]">
    <meta property="og:title" content="Free [Lead Magnet] - Limited Time">
    <meta property="og:description" content="Discover the secrets to [benefit]">
    <meta property="og:image" content="/images/og-image.jpg">

    <!-- CSS -->
    <link rel="stylesheet" href="styles.css">

    <!-- Tracking Pixels -->
    <!-- Facebook Pixel -->
    <script>
        !function(f,b,e,v,n,t,s)
        {if(f.fbq)return;n=f.fbq=function(){n.callMethod?
        n.callMethod.apply(n,arguments):n.queue.push(arguments)};
        if(!f._fbq)f._fbq=n;n.push=n;n.loaded=!0;n.version='2.0';
        n.queue=[];t=b.createElement(e);t.async=!0;
        t.src=v;s=b.getElementsByTagName(e)[0];
        s.parentNode.insertBefore(t,s)}(window, document,'script',
        'https://connect.facebook.net/en_US/fbevents.js');
        fbq('init', 'YOUR_PIXEL_ID');
        fbq('track', 'PageView');
        fbq('track', 'ViewContent');
    </script>

    <!-- Google Analytics -->
    <script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
    <script>
        window.dataLayer = window.dataLayer || [];
        function gtag(){dataLayer.push(arguments);}
        gtag('js', new Date());
        gtag('config', 'GA_MEASUREMENT_ID');
    </script>
</head>
<body>
    <!-- Above Fold Section -->
    <section class="hero">
        <div class="container">
            <!-- Headline -->
            <h1 class="headline">
                Discover The Secret To
                <span class="highlight">[Achieving Desired Result]</span>
                In Just [Timeframe]
            </h1>

            <h2 class="subheadline">
                FREE: Download Our [Lead Magnet] and Get Instant Access
                To [Specific Benefit] ($47 Value - Yours Free Today)
            </h2>

            <!-- Lead Magnet Preview -->
            <div class="preview-section">
                <div class="preview-image">
                    <img src="/images/lead-magnet-preview.png" alt="Lead Magnet Preview">
                    <div class="value-badge">$47 VALUE</div>
                </div>

                <div class="benefits">
                    <h3>Inside You'll Discover:</h3>
                    <ul class="benefit-list">
                        <li>
                            <span class="checkmark">✓</span>
                            <strong>[Benefit #1]:</strong> How to [specific outcome] without [pain point]
                        </li>
                        <li>
                            <span class="checkmark">✓</span>
                            <strong>[Benefit #2]:</strong> The exact [strategy/system] that helped [social proof]
                        </li>
                        <li>
                            <span class="checkmark">✓</span>
                            <strong>[Benefit #3]:</strong> [Number] proven [methods/tactics] to [achieve result]
                        </li>
                        <li>
                            <span class="checkmark">✓</span>
                            <strong>[Benefit #4]:</strong> Secret [technique] used by [authority figures]
                        </li>
                        <li>
                            <span class="checkmark">✓</span>
                            <strong>[Benefit #5]:</strong> How to avoid [common mistake] that [negative outcome]
                        </li>
                    </ul>
                </div>
            </div>

            <!-- Opt-in Form -->
            <div class="optin-form-container">
                <div class="form-header">
                    <h3>Get Instant Access Now - 100% Free</h3>
                    <p>Enter your email below to download immediately</p>
                </div>

                <form id="leadForm" class="optin-form">
                    <input
                        type="email"
                        name="email"
                        placeholder="Enter your best email address"
                        required
                        class="email-input"
                    >
                    <button type="submit" class="cta-button">
                        GET INSTANT ACCESS
                        <span class="arrow">→</span>
                    </button>
                    <p class="privacy-note">
                        🔒 We respect your privacy. Unsubscribe at any time.
                    </p>
                </form>

                <div class="trust-badges">
                    <img src="/images/badge-secure.png" alt="Secure">
                    <img src="/images/badge-privacy.png" alt="Privacy Protected">
                    <img src="/images/badge-spam-free.png" alt="Spam Free">
                </div>
            </div>
        </div>
    </section>

    <!-- Social Proof Section -->
    <section class="social-proof">
        <div class="container">
            <div class="stats">
                <div class="stat">
                    <div class="stat-number">10,000+</div>
                    <div class="stat-label">Downloads</div>
                </div>
                <div class="stat">
                    <div class="stat-number">4.9/5</div>
                    <div class="stat-label">Rating</div>
                </div>
                <div class="stat">
                    <div class="stat-number">94%</div>
                    <div class="stat-label">Recommend It</div>
                </div>
            </div>

            <h2>What People Are Saying</h2>

            <div class="testimonials">
                <div class="testimonial">
                    <div class="stars">⭐⭐⭐⭐⭐</div>
                    <p class="quote">
                        "[Specific result achieved]. This [lead magnet] completely changed
                        the way I [do something]. Highly recommended!"
                    </p>
                    <div class="author">
                        <img src="/images/testimonial-1.jpg" alt="Customer">
                        <div>
                            <strong>Jane Smith</strong>
                            <span>CEO, Company Inc.</span>
                        </div>
                    </div>
                </div>

                <div class="testimonial">
                    <div class="stars">⭐⭐⭐⭐⭐</div>
                    <p class="quote">
                        "I've tried [alternatives] but this is by far the best. I saw
                        [specific result] in just [timeframe]."
                    </p>
                    <div class="author">
                        <img src="/images/testimonial-2.jpg" alt="Customer">
                        <div>
                            <strong>John Doe</strong>
                            <span>Marketing Director</span>
                        </div>
                    </div>
                </div>

                <div class="testimonial">
                    <div class="stars">⭐⭐⭐⭐⭐</div>
                    <p class="quote">
                        "Worth every penny... except it's FREE! The value in this
                        [lead magnet] is incredible. Don't miss out."
                    </p>
                    <div class="author">
                        <img src="/images/testimonial-3.jpg" alt="Customer">
                        <div>
                            <strong>Sarah Johnson</strong>
                            <span>Entrepreneur</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- As Seen On Section -->
    <section class="featured-in">
        <div class="container">
            <h3>As Featured In:</h3>
            <div class="logos">
                <img src="/images/logo-forbes.png" alt="Forbes">
                <img src="/images/logo-techcrunch.png" alt="TechCrunch">
                <img src="/images/logo-entrepreneur.png" alt="Entrepreneur">
                <img src="/images/logo-inc.png" alt="Inc">
            </div>
        </div>
    </section>

    <!-- About Author Section -->
    <section class="about-author">
        <div class="container">
            <div class="author-content">
                <img src="/images/author.jpg" alt="Author" class="author-image">
                <div class="author-bio">
                    <h2>Hi, I'm [Your Name]</h2>
                    <p>
                        I've helped [X number] people [achieve result]. After [years/experience],
                        I discovered [key insight] that changed everything.
                    </p>
                    <p>
                        Now I'm sharing everything I know in this free [lead magnet] so you can
                        [benefit] without [pain point].
                    </p>
                    <div class="credentials">
                        <div class="credential">✓ [Credential 1]</div>
                        <div class="credential">✓ [Credential 2]</div>
                        <div class="credential">✓ [Credential 3]</div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Final CTA Section -->
    <section class="final-cta">
        <div class="container">
            <h2>Ready to [Achieve Desired Result]?</h2>
            <p>Join [X] others who have downloaded this [lead magnet]</p>

            <form id="leadFormBottom" class="optin-form">
                <input
                    type="email"
                    name="email"
                    placeholder="Enter your email address"
                    required
                    class="email-input"
                >
                <button type="submit" class="cta-button">
                    YES! SEND ME THE FREE [LEAD MAGNET]
                </button>
            </form>

            <p class="urgency-text">
                ⏰ Limited time offer - Download now before it's gone!
            </p>
        </div>
    </section>

    <!-- Footer -->
    <footer>
        <div class="container">
            <p>&copy; 2024 Your Company. All rights reserved.</p>
            <div class="footer-links">
                <a href="/privacy">Privacy Policy</a>
                <a href="/terms">Terms of Service</a>
                <a href="/contact">Contact</a>
            </div>
        </div>
    </footer>

    <!-- Exit Intent Popup -->
    <div id="exitPopup" class="popup-overlay">
        <div class="popup">
            <button class="close-popup">&times;</button>
            <h2>⚠️ WAIT! Don't Leave Empty-Handed</h2>
            <p>Before you go, grab your FREE [Lead Magnet]!</p>

            <form id="exitForm" class="optin-form">
                <input
                    type="email"
                    name="email"
                    placeholder="Enter your email"
                    required
                >
                <button type="submit" class="cta-button">
                    GET IT NOW
                </button>
            </form>

            <p class="popup-subtext">
                Available for a limited time only
            </p>
        </div>
    </div>

    <!-- JavaScript -->
    <script src="script.js"></script>

    <script>
        // Form submission handler
        document.querySelectorAll('form').forEach(form => {
            form.addEventListener('submit', async (e) => {
                e.preventDefault();

                const email = form.querySelector('input[name="email"]').value;

                // Track conversion
                fbq('track', 'Lead');
                gtag('event', 'generate_lead', {
                    'currency': 'USD',
                    'value': 47
                });

                // Submit to backend
                const response = await fetch('/api/subscribe', {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ email })
                });

                if (response.ok) {
                    // Redirect to thank you page
                    window.location.href = '/thank-you?email=' + encodeURIComponent(email);
                } else {
                    alert('Something went wrong. Please try again.');
                }
            });
        });

        // Exit intent popup
        let exitIntentShown = false;

        document.addEventListener('mouseout', (e) => {
            if (!exitIntentShown && e.clientY < 50) {
                document.getElementById('exitPopup').style.display = 'flex';
                exitIntentShown = true;
            }
        });

        document.querySelector('.close-popup').addEventListener('click', () => {
            document.getElementById('exitPopup').style.display = 'none';
        });
    </script>
</body>
</html>
```

### Step 5: Thank You Page + Tripwire

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Check Your Email - Download Link Inside</title>
    <link rel="stylesheet" href="styles.css">

    <!-- Tracking -->
    <script>
        fbq('track', 'Lead');
        gtag('event', 'conversion', {
            'send_to': 'AW-CONVERSION_ID/CONVERSION_LABEL'
        });
    </script>
</head>
<body class="thank-you-page">
    <section class="thank-you-hero">
        <div class="container">
            <!-- Success Message -->
            <div class="success-icon">✓</div>
            <h1>Success! Check Your Email</h1>
            <p class="lead">
                Your [Lead Magnet] is on its way to <strong id="userEmail"></strong>
            </p>

            <div class="next-steps">
                <h3>What happens next:</h3>
                <ol>
                    <li>Check your inbox (and spam folder) for an email from us</li>
                    <li>Click the link to download your [Lead Magnet]</li>
                    <li>Start implementing what you learn today!</li>
                </ol>
            </div>
        </div>
    </section>

    <!-- Tripwire Offer -->
    <section class="tripwire-offer">
        <div class="container">
            <div class="offer-badge">⚡ SPECIAL ONE-TIME OFFER ⚡</div>

            <h2>
                Before You Go... Want To
                <span class="highlight">[Achieve Bigger Result]</span>
                10X Faster?
            </h2>

            <p class="subheadline">
                You just got [Lead Magnet]... but what if you could have
                [Premium Product] for just $7 (normally $47)?
            </p>

            <!-- Countdown Timer -->
            <div class="countdown-timer">
                <div class="timer-text">This offer expires in:</div>
                <div id="countdown" class="timer">
                    <div class="time-unit">
                        <span id="minutes">19</span>
                        <span class="label">Minutes</span>
                    </div>
                    <div class="time-separator">:</div>
                    <div class="time-unit">
                        <span id="seconds">59</span>
                        <span class="label">Seconds</span>
                    </div>
                </div>
            </div>

            <!-- Product Preview -->
            <div class="product-preview">
                <img src="/images/product-mockup.png" alt="Product">

                <div class="what-you-get">
                    <h3>Here's What You Get:</h3>
                    <ul class="checklist">
                        <li>✓ [Component #1] - $17 value</li>
                        <li>✓ [Component #2] - $15 value</li>
                        <li>✓ [Component #3] - $10 value</li>
                        <li>✓ [Bonus #1] - $5 value</li>
                    </ul>

                    <div class="value-stack">
                        <div class="original-price">
                            <span class="label">Regular Price:</span>
                            <span class="amount"><del>$47</del></span>
                        </div>
                        <div class="special-price">
                            <span class="label">Your Price Today:</span>
                            <span class="amount">$7</span>
                        </div>
                        <div class="savings">You Save: $40 (85% OFF!)</div>
                    </div>
                </div>
            </div>

            <!-- CTA Button -->
            <button class="tripwire-cta" onclick="processTripwire()">
                ✓ YES! Give Me [Product] For Just $7
            </button>

            <div class="guarantee">
                <img src="/images/guarantee-badge.png" alt="Money Back Guarantee">
                <p>
                    <strong>30-Day Money-Back Guarantee</strong><br>
                    If you're not satisfied, we'll refund every penny. No questions asked.
                </p>
            </div>

            <!-- No Thanks Link -->
            <a href="/main-funnel" class="no-thanks">
                No thanks, I don't want to [miss out on benefit]
            </a>
        </div>
    </section>

    <script>
        // Display user email
        const urlParams = new URLSearchParams(window.location.search);
        const email = urlParams.get('email');
        if (email) {
            document.getElementById('userEmail').textContent = email;
        }

        // Countdown timer
        let timeLeft = 20 * 60; // 20 minutes in seconds

        function updateCountdown() {
            const minutes = Math.floor(timeLeft / 60);
            const seconds = timeLeft % 60;

            document.getElementById('minutes').textContent = String(minutes).padStart(2, '0');
            document.getElementById('seconds').textContent = String(seconds).padStart(2, '0');

            if (timeLeft > 0) {
                timeLeft--;
                setTimeout(updateCountdown, 1000);
            } else {
                // Redirect or hide offer
                document.querySelector('.tripwire-offer').innerHTML = '<p>Offer expired!</p>';
            }
        }

        updateCountdown();

        // Process tripwire purchase
        async function processTripwire() {
            // Track conversion
            fbq('track', 'InitiateCheckout', {
                value: 7,
                currency: 'USD'
            });

            // Redirect to Stripe checkout
            const response = await fetch('/api/create-checkout-session', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({
                    product: 'tripwire',
                    price: 7,
                    email: email
                })
            });

            const data = await response.json();
            window.location.href = data.url;
        }
    </script>
</body>
</html>
```

### Step 6: Email Sequences

```markdown
# Email Sequences

## Welcome Series (7 emails over 7 days)

### Email 1: Welcome + Deliver Lead Magnet (Immediate)

**Subject**: Your [Lead Magnet] is here! 🎉

**Preview**: Plus: How to get results in just [timeframe]...

**Body**:
```
Hey [First Name],

Welcome! 👋

Thanks for downloading [Lead Magnet]. Here's your download link:

👉 [DOWNLOAD BUTTON]

Quick Start Tip:
Start with [specific section] - it's the fastest way to see results.

I'll be sending you more valuable content over the next few days to help you [achieve goal].

Tomorrow, I'll share a case study of how [customer] used these exact strategies to [achieve impressive result].

Talk soon!

[Your Name]

P.S. Hit reply if you have any questions. I read every email!
```

### Email 2: Quick Win (Day 1)

**Subject**: [First Name], try this quick win today

**Preview**: Takes 15 minutes, delivers instant results...

**Body**:
```
Hey [First Name],

Yesterday I sent you [Lead Magnet]. Did you download it yet?

[DOWNLOAD LINK]

Today, I want to share a QUICK WIN you can implement in the next 15 minutes:

[Specific actionable tip]

Here's exactly how to do it:

Step 1: [Clear instruction]
Step 2: [Clear instruction]
Step 3: [Clear instruction]

Why this works:
[Explanation + proof/data]

Try it today and let me know how it goes!

Reply and tell me your results.

[Your Name]

P.S. Tomorrow I'm sharing how [customer name] achieved [impressive result] using this exact method. Stay tuned!
```

### Email 3: Case Study (Day 2)

**Subject**: How [Customer] got [impressive result]

**Preview**: (You can do this too)

**Body**:
```
[First Name],

Let me tell you about [Customer Name].

[Customer] was struggling with [problem] just like you.

They tried [common solutions] but nothing worked.

Then they discovered [your solution/method].

Here's what happened:

📊 Result #1: [Specific metric]
📊 Result #2: [Specific metric]
📊 Result #3: [Specific metric]

Total time: Just [timeframe]!

Want to know their secret?

It's actually simple: [Key insight/strategy]

[Customer] says:
"[Compelling testimonial quote]"

Now, you might be thinking...

"That's great for [Customer], but will it work for ME?"

Short answer: YES.

Here's why: [Explanation of why it's replicable]

Ready to get similar results?

I've created a complete system that shows you exactly how to [achieve result]:

👉 [LINK TO SALES PAGE]

Inside, you'll discover:
• [Benefit 1]
• [Benefit 2]
• [Benefit 3]

Check it out here: [LINK]

[Your Name]

P.S. Have questions? Just hit reply!
```

### Email 4: Objection Handler (Day 3)

**Subject**: "But what if [common objection]?"

**Preview**: Let me address this concern...

**Body**:
```
Hey [First Name],

I get this question ALL the time:

"[Common objection/concern]"

It's a totally valid concern.

Let me address it head-on:

[Detailed explanation of why objection isn't valid]

Here's the truth:
[Counter-argument with proof]

Still not convinced?

Look at what [Customer] said:

"[Testimonial addressing this objection]"

And [Another Customer]:

"[Another testimonial]"

The bottom line:
[Summary of why they shouldn't worry]

If you're ready to [achieve result], here's what to do next:

👉 [LINK TO SALES PAGE]

You'll get:
✓ [Feature/benefit 1]
✓ [Feature/benefit 2]
✓ [Feature/benefit 3]

Plus my 30-day money-back guarantee.

If it doesn't work, you get a full refund. No questions asked.

See you on the inside!

[Your Name]
```

### Email 5: Social Proof Tsunami (Day 4)

**Subject**: What 500+ customers are saying...

**Preview**: ⭐⭐⭐⭐⭐ (Real reviews inside)

**Body**:
```
[First Name],

Don't take MY word for it...

Here's what 500+ customers are saying:

⭐⭐⭐⭐⭐
"[Specific result]. This is the best investment I've made!"
- [Name, Title]

⭐⭐⭐⭐⭐
"I was skeptical at first, but [impressive result] in just [timeframe]."
- [Name, Title]

⭐⭐⭐⭐⭐
"Finally something that actually works! Highly recommended."
- [Name, Title]

[Include 5-7 more testimonials]

Average rating: 4.9/5 from 500+ reviews

These are REAL people getting REAL results.

You could be next.

Join them here: [LINK TO SALES PAGE]

[Your Name]

P.S. This offer won't last forever. Secure your spot now!
```

### Email 6: Urgency + Scarcity (Day 5)

**Subject**: [First Name], time is running out...

**Preview**: Only 48 hours left for [bonus/discount]

**Body**:
```
Hey [First Name],

I have some bad news...

The [discount/bonus/offer] expires in 48 hours.

After that, [consequence of not acting]:
❌ Price increases to $[higher price]
❌ Bonuses worth $[value] disappear
❌ You'll be back to [pain point]

Look, I get it.

You're busy. Life happens.

But here's the thing:

[Timeframe] from now, where will you be?

Option A: Still struggling with [problem]
Option B: Already seeing [results] like our customers

The choice is yours.

But you have to decide NOW.

👉 Click here to join: [LINK]

Time is ticking...

[Your Name]

P.S. Remember my 30-day guarantee. Zero risk to you.
```

### Email 7: Last Chance (Day 6)

**Subject**: LAST CHANCE: Expires tonight at midnight

**Preview**: Don't miss out on [benefit]...

**Body**:
```
[First Name],

This is it.

FINAL CALL.

The [offer] expires tonight at midnight.

After that, it's gone.

⏰ Time left: [Countdown]

If you've been on the fence...

If you've been "thinking about it"...

NOW is the time to act.

Here's what you're getting:

✓ [Main product] - $[value]
✓ [Bonus 1] - $[value]
✓ [Bonus 2] - $[value]
✓ [Bonus 3] - $[value]

Total Value: $[total value]
Your Investment Today: $[price]

You save: $[savings]

Plus 30-day money-back guarantee.

Click here before midnight: [LINK]

Don't let this opportunity slip away.

[Your Name]

P.S. After tonight, this offer is GONE. Don't have regrets. Click now: [LINK]
```
```

### Success Criteria

The command is successful when you deliver:
✅ Complete sales funnel with all pages
✅ Landing page optimized for conversions
✅ Thank you page with tripwire offer
✅ 7-day email nurture sequence
✅ Long-form sales page
✅ Order form with order bump
✅ Upsell/downsell sequence
✅ Payment integration (Stripe)
✅ Analytics tracking throughout
✅ Conversion optimization elements
✅ Complete funnel math and projections

This should be a COMPLETE, HIGH-CONVERTING sales funnel ready for immediate deployment and revenue generation.
