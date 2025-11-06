# Webinar Funnel Builder

Create a complete webinar sales funnel with registration page, presentation slides and script, webinar platform setup, replay system, and post-webinar email sequence for the product or service specified by the user.

## Instructions

Build a comprehensive webinar funnel including:

### 1. Webinar Strategy & Planning

#### Webinar Types:

**Live Webinar:**
- Scheduled date and time
- Interactive Q&A
- Live engagement
- Can go off-script
- Higher urgency
- Technical risk

**Automated/Evergreen:**
- On-demand viewing
- Simulated live experience
- Pre-recorded video
- Scalable
- No technical stress
- Lower urgency (need to engineer)

**Hybrid:**
- Recorded presentation
- Live Q&A segment
- Best of both worlds

#### Webinar Format (60-90 minutes):

**Standard Structure:**
```
0:00-5:00   Pre-webinar (wait music, engagement)
5:00-10:00  Introduction & credibility
10:00-15:00 Promise & outcome preview
15:00-45:00 Teaching content (3-4 major points)
45:00-60:00 The offer & pitch
60:00-75:00 Q&A and objection handling
75:00-90:00 Final CTA and closing
```

### 2. Registration Landing Page

#### Page Structure:

**Above the Fold:**
```html
<header>
  [Logo]
  [Phone number or trust indicator]
</header>

<hero-section>
  <headline>
    [Free Webinar]: [Compelling Promise]
  </headline>

  <subheadline>
    Discover [Outcome] in just [timeframe] without [pain point]
  </subheadline>

  <webinar-details>
    📅 [Day], [Month] [Date]
    🕐 [Time] [Timezone]
    ⏱️ [Duration] minutes
  </webinar-details>

  <registration-form>
    [First Name] *
    [Email] *
    [Phone] (optional)

    [Button: "Yes! Save My Seat" or "Register Now FREE"]

    No credit card required
  </registration-form>

  <urgency>
    ⚠️ Limited to [number] attendees - [X] spots remaining
    or
    ⏰ Registration closes in [countdown timer]
  </urgency>
</hero-section>
```

**Example Headlines:**
- "How to [Achieve Outcome] in [Timeframe] (Without [Pain Point])"
- "The [Adjective] Way to [Result] - Free Webinar"
- "[Number] Secrets to [Desirable Outcome] Revealed"
- "Master [Skill/Topic]: Free Live Training"

**Below the Fold:**

**What You'll Learn:**
```html
<section class="what-youll-learn">
  <h2>Here's What You'll Discover:</h2>

  <benefits-list>
    ✓ [Specific takeaway 1] - [brief elaboration]
    ✓ [Specific takeaway 2] - [brief elaboration]
    ✓ [Specific takeaway 3] - [brief elaboration]
    ✓ [Specific takeaway 4] - [brief elaboration]
    ✓ [Specific takeaway 5] - [brief elaboration]

    Plus: [Bonus insight or resource]
  </benefits-list>

  [CTA Button: "Register for Free"]
</section>
```

**Who This Is For:**
```html
<section class="ideal-for">
  <h2>This Free Training Is Perfect If You're:</h2>

  <avatar-list>
    ✅ [Type of person 1]
    ✅ [Type of person 2]
    ✅ [Type of person 3]
    ✅ [Type of person 4]

    Even if you [common objection], this will work for you.
  </avatar-list>
</section>
```

**About the Host:**
```html
<section class="about-host">
  [Photo - professional but approachable]

  <h2>Meet Your Instructor: [Name]</h2>

  [2-3 paragraph bio highlighting:]
  • Relevant credentials
  • Results achieved
  • Why they're qualified to teach this
  • Personal touch/relatability

  [Media logos or achievements]
  [Social proof numbers]
</section>
```

**Social Proof:**
```html
<section class="testimonials">
  <h2>What Past Attendees Are Saying:</h2>

  <testimonial-grid>
    <testimonial>
      "[Quote highlighting transformation]"
      — [Name], [Title/Location]
    </testimonial>

    [Repeat 3-6 times]
  </testimonial-grid>

  <stats>
    Join [10,000+] people who have attended
    ⭐⭐⭐⭐⭐ [4.9/5] average rating
  </stats>
</section>
```

**Final CTA:**
```html
<section class="final-cta">
  <h2>Ready to [Achieve Outcome]?</h2>

  <urgency-reminder>
    Don't miss this free training!
    [Spots remaining or registration deadline]
  </urgency-reminder>

  [Registration Form Repeated]

  <guarantee>
    100% Free. No Credit Card Required.
    Can't attend live? Register anyway - we'll send the replay.
  </guarantee>
</section>
```

#### Technical Implementation:

**Platforms:**
- WebinarJam/EverWebinar (all-in-one)
- Zoom + Custom landing page
- Demio (modern, user-friendly)
- Livestorm (browser-based)
- GoToWebinar (enterprise)
- ClickFunnels (funnel + webinar)

**Form Integration:**
- Zapier connection to email provider
- Custom webhook
- Native integration
- Double opt-in (optional)
- Timezone detection automatic
- Calendar invite sent

**Conversion Optimization:**
- Exit-intent popup (last chance to register)
- Scroll-triggered sticky header with CTA
- Social proof notifications (recent registrations)
- Live chat or chatbot
- Mobile-responsive design
- Fast loading (< 3 seconds)

### 3. Webinar Presentation (Slides + Script)

#### Slide-by-Slide Structure:

**Slide 1: Title Slide (0:00-5:00)**
```
[Webinar Title]
[Subtitle/Promise]

Presented by: [Your Name]
[Logo/Brand]

[Pre-webinar chat prompts:]
"Where are you joining from? Type in the chat!"
"What's your #1 challenge with [topic]?"
"On a scale of 1-10, how important is [outcome] to you?"
```

**Speaker Script:**
```
[While waiting for start time]

Hey everyone! Great to see you joining.

We'll be starting in just a couple minutes at [time] sharp.

In the meantime, I'd love to get to know you:
• Drop in the chat where you're joining from
• What's your biggest challenge with [topic]?

I'll be reading these and we'll address as many as possible today...
```

---

**Slide 2-3: Introduction & Credibility (5:00-10:00)**

**Slide 2:**
```
Welcome!

[Your photo]

I'm [Name],
[One-line description of who you are]
```

**Slide 3:**
```
Why Listen to Me?

[Credential 1 with visual]
[Credential 2 with visual]
[Credential 3 with visual]
[Key results/social proof]

Not bragging, just showing you're in good hands...
```

**Speaker Script:**
```
Hey everyone! Welcome to [Webinar Title].

I'm [Name], and I'm [description].

Now, you might be wondering why you should listen to me...

[Share credentials quickly - 30 seconds max]

But here's the thing - this isn't about me.

This is about YOU and [outcome you want].

So let's dive in...
```

---

**Slide 4: The Promise (10:00-12:00)**

```
Today You'll Discover:

✓ [Big promise 1]
✓ [Big promise 2]
✓ [Big promise 3]

By the end of this training, you'll have [clear outcome].
```

**Speaker Script:**
```
Here's what we're covering today:

[Go through each bullet with brief elaboration]

And at the end, I'll share a special opportunity to
[take this further / implement this with help / etc.]

So grab a pen and paper because you'll want to take notes...
```

---

**Slide 5: Believability Story (12:00-15:00)**

```
[Photo of you before/struggling]

Where I Was [X] Years Ago...

[Relatable struggle story]
```

**Speaker Script:**
```
Before we get into the content, I want to share a quick story...

[X years ago], I was exactly where you might be now.

[Tell story of struggle, failure, frustration]

I tried [failed solution 1], [failed solution 2], [failed solution 3]...

Nothing worked. I was [emotion: frustrated/overwhelmed/ready to give up].

But then I discovered [key insight that changed everything]...

And that's what I'm sharing with you today.

Let's get into it...
```

---

**Slides 6-20: Teaching Content (15:00-45:00)**

**Framework: 3-4 Major Principles/Steps**

**Pattern for Each Section:**
```
SECTION 1: [Principle/Step]

Content Slides:
• The Mistake (what people do wrong)
• Why It Doesn't Work
• The Better Way (your method)
• How It Works
• Example/Case Study
• Key Takeaway
```

**Example Section:**

**Slide 6:**
```
PART 1:

[Principle Name - Big Idea]

[Visual/icon representing the concept]
```

**Slide 7:**
```
The Common Mistake:

Most people [describe what they do wrong]

[Visual showing wrong way - X over it]
```

**Slide 8:**
```
Why That Doesn't Work:

• [Reason 1]
• [Reason 2]
• [Reason 3]

[Diagram or visual]
```

**Slide 9:**
```
The Solution:

[Your Method/Framework]

[Visual diagram showing your way]

This works because [key insight].
```

**Slide 10:**
```
Case Study:

[Photo of customer]

[Name] used this method and:
• [Result 1]
• [Result 2]
• [Result 3]

"[Testimonial quote]"
```

**Slide 11:**
```
Key Takeaway:

[One-sentence summary]

[Action step or implementation tip]
```

**[Repeat this pattern for 2-3 more major sections]**

---

**Transition to Offer (45:00-47:00)**

**Slide 21:**
```
Now, Here's the Challenge...

[Identify the GAP between knowledge and implementation]

You now know:
✓ [Thing learned 1]
✓ [Thing learned 2]
✓ [Thing learned 3]

But knowing is different from DOING.
```

**Speaker Script:**
```
So we've covered a lot today.

You now understand [recap 3 main points].

But here's the challenge I see all the time...

Knowing this information is one thing.

Actually implementing it - and getting results - is another.

That's where most people get stuck.

[Describe common obstacles]

And that's exactly why I created [Your Solution]...
```

---

**Slides 22-35: The Offer (47:00-60:00)**

**Slide 22:**
```
Introducing:

[PRODUCT/PROGRAM NAME]

[One-line description of what it is]
[Logo or product visual]
```

**Slide 23:**
```
What Is [Product]?

[Product Name] is [type of offering]:

A [duration] program that [core promise]

[Show product packaging or overview]
```

**Slide 24-30: What's Included (Value Stack)**

```
Here's Everything You Get:

COMPONENT 1: [Name] (Value: $X)
[What it is and benefit]
[Visual]

COMPONENT 2: [Name] (Value: $X)
[What it is and benefit]
[Visual]

[Continue for all components]

BONUS 1: [Name] (Value: $X)
[What it is and why it matters]

BONUS 2: [Name] (Value: $X)
[What it is and why it matters]

BONUS 3: [Name] (Value: $X)
[What it is and why it matters]
```

**Slide 31:**
```
Total Value: $[High Number]

But You're Not Paying That Today...
```

**Slide 32:**
```
[SPECIAL WEBINAR PRICING]

Regular Price: $[Higher Price]

Today Only: $[Discounted Price]

Save $[Amount] when you join today!

[Visual showing price comparison]
```

**Slide 33:**
```
100% Money-Back Guarantee

[Guarantee Badge]

[30/60/90] Day Guarantee:

[Detailed guarantee terms]

You risk absolutely nothing.
```

**Slide 34:**
```
Plus, if you join in the next [15 minutes]:

FAST-ACTION BONUS:

[Additional bonus] (Value: $X)

[What it is and why it's valuable]

[Timer showing countdown]
```

**Slide 35:**
```
Here's How to Get Started:

1. Click the button below this video
2. Fill out your information
3. Get instant access

[BUTTON: "YES! I WANT THIS"]

Questions? Keep watching - we'll do Q&A next.
```

**Speaker Script (Pitch Delivery):**
```
[Introduce the solution with enthusiasm]

Alright, so let me show you what I've put together to help you...

[Present each component with value and benefits]

This is normally [higher price].

But for webinar attendees only, I'm doing something special...

[Reveal price with emphasis on savings]

Plus, you're covered by my [guarantee].

[Explain guarantee thoroughly]

And if you take action in the next [15 minutes], I'll also include...

[Present fast-action bonus]

So here's what to do right now...

[Clear instructions for ordering]

I'll give you a few minutes to get signed up, and then we'll do Q&A...
```

---

**Slides 36-40: Q&A Section (60:00-75:00)**

**Slide 36:**
```
Q&A TIME

Let's answer your questions!

[Drop your questions in the chat]

[Button still visible: "Join Now"]
```

**Handle Common Questions:**
- "How long do I have access?"
- "Is there a payment plan?"
- "What if it doesn't work for me?"
- "How much time does this take?"
- "Will this work for [my situation]?"

**Objection-Handling Framework:**
```
1. Acknowledge the question
2. Reframe if needed
3. Answer directly
4. Tie back to value/guarantee
5. CTA reminder
```

---

**Slide 41: Final CTA (75:00-85:00)**

```
Last Call!

Fast-Action Bonus expires in [X] minutes

Click below to join now:

[BUTTON: "CLAIM MY SPOT NOW"]

Guarantee: [Brief reminder]
```

**Final Speaker Script:**
```
Alright everyone, we're coming up on time.

If you haven't grabbed your spot yet, now's the time.

Remember, you're getting:
[Quick recap of offer]

Plus the [fast-action bonus] if you join before [time].

And you're fully protected by the [guarantee].

This truly is a no-brainer.

Click the button below and I'll see you on the inside!

For those who have questions about [objection], let me address that real quick...

[Handle final objections]

Okay, last call - click the button now if you want in!

Thanks so much for joining today. Talk soon!
```

---

**Slide 42: Thank You**
```
Thank You!

See you in [Product Name]!

Questions? Email: [support email]

[Social media links]
```

### 4. Webinar Platform Setup

#### Zoom Webinar Configuration:

**Settings:**
- Enable registration
- Require registration fields (name, email)
- Send confirmation email
- Set timezone
- Enable Q&A
- Enable chat
- Disable screen sharing for attendees
- Enable recording
- Practice session (dry run)

**Custom Questions:**
- Phone number (optional)
- What's your biggest challenge with [topic]?
- How did you hear about this webinar?

**Branding:**
- Custom background
- Logo display
- Branded email templates

#### WebinarJam/Demio Setup:

**Registration Page:**
- Connect domain
- Customize form fields
- Set up thank you page redirect
- Email integrations

**Webinar Room:**
- Upload presentation slides
- Set up offer buttons/links
- Configure chat and Q&A
- Test audio/video
- Set up polls
- Inject CTA buttons

**Automated Features:**
- Chat triggers (auto-messages)
- Offer reveal timing
- Countdown timers
- Notification settings

### 5. Replay Page with Scarcity

#### Replay Page Structure:

**Header:**
```
WEBINAR REPLAY:
[Webinar Title]

⚠️ Replay available for [48 hours only]
[Countdown Timer]
```

**Video Player:**
```
[Embedded Replay Video]

[Special Offer Expires: Countdown Timer]
```

**CTA Section (Always Visible):**
```
Ready to Join [Product Name]?

Special Webinar Pricing: $[Price]
Expires in: [Countdown Timer]

[BUTTON: "Get Instant Access Now"]

[Trust badges]
[Guarantee reminder]
```

**Below Video:**

```
<section class="quick-links">
  <h3>Jump to Section:</h3>
  <a href="#timestamp">Introduction (5:00)</a>
  <a href="#timestamp">Part 1 (15:00)</a>
  <a href="#timestamp">Part 2 (25:00)</a>
  <a href="#timestamp">Part 3 (35:00)</a>
  <a href="#timestamp">The Offer (45:00)</a>
</section>

<section class="recap">
  <h3>What's Included:</h3>
  [Bullet list of components]
  [Value stack reminder]
  [CTA button]
</section>

<section class="faq">
  <h3>Frequently Asked Questions:</h3>
  [Accordion FAQ list]
  [Each FAQ ends with CTA]
</section>

<section class="final-cta">
  [Last chance messaging]
  [Timer]
  [Order button]
</section>
```

#### Scarcity Engineering:

**Genuine Scarcity:**
- Bonus expires in 48-72 hours
- Price increases after webinar period
- Limited coaching spots
- Enrollment closes at [date]

**Evergreen Scarcity (for automated):**
- Countdown based on registration date
- "Next webinar not scheduled for 2 weeks"
- Bonuses expire after viewing
- Deadlines relative to user

**Technical Implementation:**
```javascript
// Set deadline based on registration
const registrationDate = new Date(user.registered_at);
const deadline = new Date(registrationDate.getTime() + (48 * 60 * 60 * 1000)); // 48 hours

// Display countdown
function updateCountdown() {
  const now = new Date();
  const timeLeft = deadline - now;

  if (timeLeft <= 0) {
    // Offer expired - show different message
    showExpiredOffer();
  } else {
    // Calculate hours, minutes, seconds
    displayCountdown(timeLeft);
  }
}

setInterval(updateCountdown, 1000);
```

### 6. Order Form and Upsells

#### Order Page Structure:

**Header:**
```
Complete Your Order

[Product Name]

[Security badges]
```

**Order Summary:**
```
Your Order:

[Product Name] - $[Price]
[Bonus 1] - Included
[Bonus 2] - Included
[Bonus 3] - Included

Total Today: $[Price]

[Discount code field]
```

**Payment Form:**
```
Billing Information:
[Name]
[Email]
[Phone] (optional)

Payment Method:
[Credit Card Fields]
or
[PayPal Button]

[Checkbox] I agree to the terms and conditions

[BUTTON: "Complete My Order Now"]

[Security badges]
[Money-back guarantee image]
[Offer expires: Timer]
```

**Trust Elements:**
- SSL certificate badge
- Money-back guarantee seal
- Payment processor logos (Stripe, PayPal)
- BBB accreditation (if applicable)
- Testimonials below form
- Customer count social proof

#### Upsell Sequence:

**Upsell #1: (Immediately after purchase)**
```
WAIT! Special One-Time Offer

Since you just joined [Product],
I want to offer you something special...

[Complementary Product/Upgrade]

[Benefits - why this enhances main offer]

Regular Price: $[Higher]
Today Only: $[Discount] (Save $[Amount])

This offer won't be available again.

[YES - Add to My Order] [NO - Continue to Dashboard]
```

**Upsell #2: (If they take upsell 1)**
```
One More Thing...

[Another Complementary Offer]

[Benefits]

Only $[Price] when added to your order today

[YES - Add This Too] [NO - That's All For Me]
```

**Downsell: (If they decline upsell)**
```
No Problem!

How about this instead:

[Smaller/Cheaper Version]

Just $[Lower Price]

[YES - I'll Take This] [NO - Continue]
```

### 7. Post-Webinar Email Sequence

#### Email 1: Immediate (Registered, Didn't Attend)
```
Subject: "Sorry we missed you on the webinar"

Hi [Name],

I noticed you weren't able to make it to today's webinar on [topic].

No worries - I've got you covered!

Here's the full replay:
[Replay Link]

The special offer I presented is still available for the next [48 hours]:
→ [Product Name] for $[Price]
→ Includes [key bonuses]
→ [Guarantee]

Watch the replay and grab your spot here:
[Link]

This pricing expires [Date/Time]

Talk soon,
[Your Name]
```

---

#### Email 2: +12 Hours (Attended, Didn't Buy)
```
Subject: "Quick question about [Product]..."

Hi [Name],

Thanks for joining yesterday's webinar!

I wanted to follow up because you didn't grab your spot in [Product] yet.

Do you have any questions I can answer?

Just reply to this email and I'll help you out.

As a reminder, the special webinar pricing expires in [time remaining]:

[Product Name] - Just $[Price]
Includes: [Recap benefits]

Click here to join now: [Link]

[Your Name]

P.S. Don't forget about the [fast-action bonus] - that expires today at [time]!
```

---

#### Email 3: +24 Hours (FAQ Focused)
```
Subject: "The #1 question I'm getting about [Product]"

Hi [Name],

After the webinar, I've been getting tons of questions about [Product].

The most common one is: "[Common Objection]"

Here's my answer:

[Address objection thoroughly]

Does that help?

If you're ready to join, you can still get the webinar pricing here:
[Link]

But hurry - this special offer ends tomorrow.

[Your Name]
```

---

#### Email 4: +36 Hours (Social Proof)
```
Subject: "[Name] just joined - here's what happened"

Hi [Name],

I wanted to share something cool...

[Customer Name] joined [Product] right after the webinar.

They just sent me this message:

"[Testimonial about quick win or great experience]"

This is exactly what I mean when I say [Product] works.

Want to see results like this?

Join here before the deadline tomorrow:
[Link]

[Your Name]
```

---

#### Email 5: +44 Hours (Final Warning)
```
Subject: "FINAL HOURS: Webinar offer expires tonight"

Hi [Name],

This is it - the final reminder.

The special webinar pricing for [Product] expires in [X hours] at [specific time].

After that:
❌ Price increases to $[Regular Price]
❌ Bonuses are gone
❌ Payment plan option disappears

Here's what you're getting:
[Bullet list recap]

Protected by [Guarantee]

This is your last chance:
[Link]

Don't let this pass you by.

[Your Name]

P.S. Seriously - [time]. Don't miss this.
```

---

#### Email 6: +48 Hours (Offer Expired)
```
Subject: "The webinar offer has closed"

Hi [Name],

Just wanted to let you know - the special webinar offer has officially closed.

[Product Name] is still available at the regular price of $[Higher Price] if you're interested:
[Link]

Otherwise, I'll keep you on my email list and share valuable content with you.

Thanks for joining the webinar!

[Your Name]
```

---

#### Email 7: +7 Days (Re-engagement)
```
Subject: "Can I ask you something?"

Hi [Name],

I wanted to reach out because you attended my webinar on [topic] last week.

I'm curious - what stopped you from joining [Product]?

I'd genuinely love to know. Just hit reply and let me know:

• Was it the price?
• Not the right time?
• Still have questions?
• Something else?

I read every response and would love to help if I can.

[Your Name]
```

### 8. Analytics and Conversion Tracking

#### Metrics Dashboard:

**Registration Page:**
- Page views
- Registrations
- Conversion rate (reg / views)
- Traffic sources
- Exit rate

**Webinar Attendance:**
- Registrations
- Attendees (showed up)
- Show-up rate %
- Average watch time
- Drop-off points
- Peak attendance
- Chat engagement

**Offer Conversion:**
- Sales during live
- Sales from replay
- Total sales
- Conversion rate (sales / attendees)
- Revenue
- Average order value
- Upsell take rate

**Email Performance:**
- Open rates
- Click rates
- Conversion rates by email
- Revenue per email

**Overall Funnel:**
```
1000 Visitors → 400 Registrations (40%) →
160 Attendees (40%) → 32 Sales (20%) →
$64,000 Revenue (at $2000 offer)

Cost per Registration: $[X]
Cost per Attendee: $[Y]
Cost per Sale: $[Z]
ROI: [%]
```

## Output Format

Provide:

1. **Complete Registration Landing Page** (HTML/copy with all sections)
2. **Full Presentation Deck** (40+ slides with speaker notes)
3. **Webinar Script** (word-for-word for entire presentation)
4. **Platform Setup Guide** (Zoom/WebinarJam configuration steps)
5. **Replay Page** (HTML/copy with scarcity elements)
6. **Order Form Pages** (checkout + 2 upsells + downsell)
7. **7-Email Post-Webinar Sequence** (complete with subject lines)
8. **Analytics Dashboard Template** (key metrics and tracking setup)
9. **Technical Checklist** (every setup step from start to launch)

Ask clarifying questions about the product/service being sold, target audience, price point, existing content, webinar platform preference, and timeline before creating the webinar funnel.
