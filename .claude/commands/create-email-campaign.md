# Create Email Campaign

Generate a complete, high-converting email marketing campaign with professional HTML templates, compelling copy, and full ESP integration ready for immediate deployment.

## Instructions

You are tasked with creating a COMPLETE, production-ready email marketing campaign. This is a one-shot command that must produce a fully functional, polished email sequence optimized for conversions and revenue generation.

### Step 1: Gather Requirements

First, ask the user these essential questions:
1. **Campaign Goal**: Welcome series, product launch, nurture sequence, or sales funnel?
2. **Target Audience**: Who are the recipients? What's their context?
3. **Product/Service**: What are you selling or promoting?
4. **Sequence Length**: How many emails? (Default: 7-10 emails)
5. **Timeline**: What's the sending cadence? (e.g., Day 0, Day 2, Day 5...)
6. **Brand Voice**: Professional, casual, friendly, authoritative?
7. **Email Service Provider**: Mailchimp, SendGrid, Mailgun, ConvertKit, or other?
8. **Existing Assets**: Do you have product images, testimonials, case studies?
9. **Conversion Goal**: Click to website, book demo, purchase, download?

### Step 2: Complete Email Campaign Structure

Create the following COMPLETE structure:

```
email-campaign/
├── templates/
│   ├── email-01-welcome.html
│   ├── email-02-value-intro.html
│   ├── email-03-education.html
│   ├── email-04-social-proof.html
│   ├── email-05-objection-handler.html
│   ├── email-06-urgency.html
│   ├── email-07-conversion.html
│   ├── email-08-follow-up.html
│   ├── email-09-retention.html
│   ├── email-10-winback.html
│   └── base-template.html
├── images/
│   ├── logo.png
│   ├── hero-01.jpg
│   ├── product-image.jpg
│   ├── testimonial-1.jpg
│   ├── social-icons/
│   └── cta-buttons/
├── copy/
│   ├── subject-lines.md
│   ├── preview-text.md
│   ├── email-copy.md
│   └── ab-test-variants.md
├── integration/
│   ├── sendgrid-setup.js
│   ├── mailchimp-setup.js
│   ├── mailgun-setup.js
│   └── convertkit-setup.js
├── tracking/
│   ├── analytics.js
│   ├── pixels.html
│   └── utm-builder.js
├── compliance/
│   ├── unsubscribe.html
│   ├── preferences.html
│   └── gdpr-consent.js
├── automation/
│   ├── sequence-config.json
│   ├── triggers.js
│   └── segments.js
├── testing/
│   ├── email-validator.js
│   ├── spam-checker.js
│   └── preview-generator.js
├── README.md
└── CAMPAIGN-GUIDE.md
```

### Step 3: Email Sequence Strategy

Create a 7-10 email sequence with strategic timing:

#### Email #1: Welcome Email (Sent immediately)
**Goal**: Build rapport, set expectations, deliver lead magnet

**Subject Lines** (A/B test 3 variants):
- "Welcome! Here's what to expect..."
- "Thanks for joining! Your [Free Resource] is inside"
- "Let's get started → Here's your first step"

**Preview Text**: "Plus: Exclusive tips you won't find anywhere else"

**Content Structure**:
```
- Warm welcome and thank you
- Who you are and why they should listen
- What to expect from this email series
- Deliver promised lead magnet/resource
- Quick win or valuable tip
- CTA to engage (reply, follow, visit site)
- Set expectations for next email
```

#### Email #2: Value Introduction (Day 2)
**Goal**: Demonstrate value, educate on problem

**Subject Lines**:
- "The #1 mistake most people make with [topic]"
- "Here's why [problem] happens (and how to fix it)"
- "Did you know? [Surprising statistic]"

**Preview Text**: "This changed everything for me..."

**Content Structure**:
```
- Hook with relatable problem
- Explain why this problem exists
- Share personal story or case study
- Introduce your solution/approach
- Provide actionable tip or framework
- CTA to learn more
- Tease next email topic
```

#### Email #3: Education & Value (Day 4)
**Goal**: Build authority, deliver massive value

**Subject Lines**:
- "The complete guide to [solving problem]"
- "3 simple steps to [achieve result]"
- "How [customer] achieved [impressive result]"

**Preview Text**: "This is the most important email I'll send you..."

**Content Structure**:
```
- Deep dive into solution
- Step-by-step tutorial or framework
- Real examples and results
- Common mistakes to avoid
- Tools and resources
- CTA to free resource or tool
- Soft mention of paid solution
```

#### Email #4: Social Proof (Day 7)
**Goal**: Build trust with testimonials and case studies

**Subject Lines**:
- "How [customer name] got [result] in [timeframe]"
- "Don't just take my word for it..."
- "Real results from real people"

**Preview Text**: "\"This completely transformed my business\" - Sarah M."

**Content Structure**:
```
- Compelling case study headline
- Customer transformation story
- Specific results and numbers
- What they struggled with before
- How solution helped them
- 3-5 testimonial quotes
- CTA to see more success stories
- Introduce paid offering
```

#### Email #5: Objection Handler (Day 10)
**Goal**: Address common concerns and hesitations

**Subject Lines**:
- "\"But what if...?\" (Your questions answered)"
- "The truth about [common objection]"
- "Is [product] right for you? Let's find out"

**Preview Text**: "I hear this question all the time..."

**Content Structure**:
```
- Acknowledge common objections
- Address "too expensive" concern
- Address "not enough time" concern
- Address "not sure it'll work for me"
- Provide comparison to alternatives
- Risk reversal (guarantee, trial)
- CTA to FAQ or consultation
- Urgency element (bonus expiring)
```

#### Email #6: Urgency & Scarcity (Day 13)
**Goal**: Create FOMO and drive action

**Subject Lines**:
- "⏰ Only 48 hours left for [offer]"
- "Last chance: [Bonus] expires tonight"
- "This won't be available much longer..."

**Preview Text**: "I don't want you to miss out on this"

**Content Structure**:
```
- Clear deadline announcement
- What they're missing out on
- Recap of all benefits
- Limited spots/time remaining
- Bonus if they act now
- What happens after deadline
- Strong CTA with countdown
- P.S. with final urgency reminder
```

#### Email #7: Primary Conversion (Day 14)
**Goal**: Make the sale or conversion

**Subject Lines**:
- "Ready to [achieve outcome]? Start here"
- "Your opportunity to [benefit] starts now"
- "Let's do this 🚀"

**Preview Text**: "Everything you need to get started is inside..."

**Content Structure**:
```
- Direct, confident opening
- Clear value proposition
- "Here's what you get" list
- Pricing (with any discounts)
- Guarantee/risk reversal
- Clear step-by-step what happens next
- Multiple CTAs throughout
- Urgency reminder
- P.S. with objection handling
```

#### Email #8: Follow-Up (Day 16)
**Goal**: Re-engage non-converters

**Subject Lines**:
- "I noticed you haven't [taken action] yet..."
- "What's holding you back?"
- "Can I answer any questions?"

**Preview Text**: "Hit reply and let me know what you need"

**Content Structure**:
```
- Acknowledge they haven't converted
- Ask what's stopping them
- Offer personal help
- Address final objections
- Emphasize money-back guarantee
- Share one more testimonial
- CTA to book call or ask questions
- Last chance reminder
```

#### Email #9: Retention/Engagement (Day 21)
**Goal**: Keep engaged, prevent unsubscribe

**Subject Lines**:
- "Still want to hear from me?"
- "Here's what's coming next..."
- "Let's stay connected"

**Preview Text**: "I have some exciting things planned for you"

**Content Structure**:
```
- Acknowledge they're still subscribed
- Thank them for staying
- Ask what content they want
- Share upcoming value
- Offer alternative free resources
- Keep the relationship warm
- CTA to engage on social
```

#### Email #10: Win-Back (Day 30+)
**Goal**: Re-engage inactive subscribers

**Subject Lines**:
- "Do you still want to hear from me?"
- "I'm breaking up with you..."
- "One last thing before you go"

**Preview Text**: "I'll respect your decision either way"

**Content Structure**:
```
- Acknowledge they haven't engaged
- Offer to unsubscribe them
- Share best content they missed
- Limited-time special offer
- CTA to stay subscribed
- Easy unsubscribe option
- Genuine goodbye if they leave
```

### Step 4: Professional HTML Email Templates

Create COMPLETE, responsive HTML email templates:

#### Base Template Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <title>{{subject}}</title>
  <style>
    /* Email-safe CSS */
    body {
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
      font-size: 16px;
      line-height: 1.6;
      color: #333333;
      background-color: #f4f4f4;
    }

    .email-container {
      max-width: 600px;
      margin: 0 auto;
      background-color: #ffffff;
    }

    .header {
      padding: 30px 40px;
      text-align: center;
      background-color: #ffffff;
    }

    .logo {
      max-width: 150px;
      height: auto;
    }

    .content {
      padding: 40px;
    }

    .hero-image {
      width: 100%;
      max-width: 600px;
      height: auto;
      display: block;
    }

    h1 {
      font-size: 28px;
      font-weight: 700;
      line-height: 1.2;
      margin: 0 0 20px 0;
      color: #111111;
    }

    h2 {
      font-size: 22px;
      font-weight: 600;
      line-height: 1.3;
      margin: 30px 0 15px 0;
      color: #222222;
    }

    p {
      margin: 0 0 15px 0;
      color: #333333;
    }

    .button {
      display: inline-block;
      padding: 16px 32px;
      margin: 20px 0;
      font-size: 16px;
      font-weight: 600;
      text-align: center;
      text-decoration: none;
      color: #ffffff !important;
      background-color: #007AFF;
      border-radius: 6px;
      transition: background-color 0.3s;
    }

    .button:hover {
      background-color: #0051D5;
    }

    .testimonial {
      background-color: #f8f8f8;
      border-left: 4px solid #007AFF;
      padding: 20px;
      margin: 20px 0;
      font-style: italic;
    }

    .testimonial-author {
      font-style: normal;
      font-weight: 600;
      margin-top: 10px;
      color: #666666;
    }

    .benefits-list {
      margin: 20px 0;
    }

    .benefit-item {
      padding: 10px 0;
      padding-left: 30px;
      position: relative;
    }

    .benefit-item:before {
      content: "✓";
      position: absolute;
      left: 0;
      color: #00C853;
      font-weight: bold;
      font-size: 18px;
    }

    .footer {
      padding: 30px 40px;
      background-color: #f8f8f8;
      text-align: center;
      font-size: 14px;
      color: #666666;
    }

    .social-links {
      margin: 20px 0;
    }

    .social-link {
      display: inline-block;
      margin: 0 10px;
    }

    .unsubscribe {
      margin-top: 20px;
      font-size: 12px;
      color: #999999;
    }

    .unsubscribe a {
      color: #999999;
      text-decoration: underline;
    }

    /* Mobile responsive */
    @media only screen and (max-width: 600px) {
      .content {
        padding: 20px !important;
      }

      h1 {
        font-size: 24px !important;
      }

      h2 {
        font-size: 20px !important;
      }

      .button {
        display: block !important;
        padding: 14px 20px !important;
      }
    }
  </style>
</head>
<body>
  <table role="presentation" width="100%" cellspacing="0" cellpadding="0" border="0">
    <tr>
      <td align="center" style="padding: 20px 0;">
        <table class="email-container" role="presentation" cellspacing="0" cellpadding="0" border="0">
          <!-- Header -->
          <tr>
            <td class="header">
              <img src="{{logo_url}}" alt="{{company_name}}" class="logo">
            </td>
          </tr>

          <!-- Hero Image (optional) -->
          {{#if hero_image}}
          <tr>
            <td>
              <img src="{{hero_image}}" alt="Hero" class="hero-image">
            </td>
          </tr>
          {{/if}}

          <!-- Content -->
          <tr>
            <td class="content">
              {{> email_content}}
            </td>
          </tr>

          <!-- Footer -->
          <tr>
            <td class="footer">
              <div class="social-links">
                <a href="{{twitter_url}}" class="social-link">
                  <img src="{{cdn}}/twitter-icon.png" alt="Twitter" width="24" height="24">
                </a>
                <a href="{{linkedin_url}}" class="social-link">
                  <img src="{{cdn}}/linkedin-icon.png" alt="LinkedIn" width="24" height="24">
                </a>
                <a href="{{facebook_url}}" class="social-link">
                  <img src="{{cdn}}/facebook-icon.png" alt="Facebook" width="24" height="24">
                </a>
              </div>

              <p>
                {{company_name}}<br>
                {{company_address}}
              </p>

              <div class="unsubscribe">
                <p>
                  You're receiving this email because you signed up at {{website_url}}
                </p>
                <p>
                  <a href="{{unsubscribe_url}}">Unsubscribe</a> |
                  <a href="{{preferences_url}}">Update preferences</a>
                </p>
              </div>

              <!-- Tracking Pixel -->
              <img src="{{tracking_pixel_url}}" alt="" width="1" height="1" border="0" style="display:none">
            </td>
          </tr>
        </table>
      </td>
    </tr>
  </table>
</body>
</html>
```

### Step 5: Email Service Provider Integration

Implement COMPLETE integration with chosen ESP:

#### SendGrid Integration

```javascript
// integration/sendgrid-setup.js
const sgMail = require('@sendgrid/mail');
sgMail.setApiKey(process.env.SENDGRID_API_KEY);

// Send single email
const sendEmail = async ({ to, templateId, dynamicData }) => {
  const msg = {
    to,
    from: {
      email: 'hello@yourdomain.com',
      name: 'Your Company'
    },
    templateId,
    dynamicTemplateData: dynamicData,
    trackingSettings: {
      clickTracking: { enable: true },
      openTracking: { enable: true }
    },
    customArgs: {
      campaign: 'welcome_series',
      source: 'landing_page'
    }
  };

  try {
    await sgMail.send(msg);
    console.log('Email sent successfully');
  } catch (error) {
    console.error('Error sending email:', error);
    throw error;
  }
};

// Create automation sequence
const createAutomation = async () => {
  const sequence = [
    { delay: 0, templateId: 'd-xxx1', name: 'Welcome' },
    { delay: 172800, templateId: 'd-xxx2', name: 'Value Intro' },
    { delay: 345600, templateId: 'd-xxx3', name: 'Education' },
    { delay: 604800, templateId: 'd-xxx4', name: 'Social Proof' },
    { delay: 864000, templateId: 'd-xxx5', name: 'Objection Handler' },
    { delay: 1123200, templateId: 'd-xxx6', name: 'Urgency' },
    { delay: 1209600, templateId: 'd-xxx7', name: 'Conversion' }
  ];

  return sequence;
};

// Add to list
const addToList = async (email, firstName, lastName, customFields = {}) => {
  const client = require('@sendgrid/client');
  client.setApiKey(process.env.SENDGRID_API_KEY);

  const data = {
    contacts: [{
      email,
      first_name: firstName,
      last_name: lastName,
      custom_fields: customFields
    }]
  };

  const request = {
    url: '/v3/marketing/contacts',
    method: 'PUT',
    body: data
  };

  try {
    await client.request(request);
    console.log('Contact added successfully');
  } catch (error) {
    console.error('Error adding contact:', error);
    throw error;
  }
};

module.exports = { sendEmail, createAutomation, addToList };
```

#### Mailchimp Integration

```javascript
// integration/mailchimp-setup.js
const Mailchimp = require('@mailchimp/mailchimp_marketing');

Mailchimp.setConfig({
  apiKey: process.env.MAILCHIMP_API_KEY,
  server: process.env.MAILCHIMP_SERVER_PREFIX
});

// Add subscriber to list
const addSubscriber = async (email, firstName, lastName, tags = []) => {
  const listId = process.env.MAILCHIMP_LIST_ID;

  try {
    const response = await Mailchimp.lists.addListMember(listId, {
      email_address: email,
      status: 'subscribed',
      merge_fields: {
        FNAME: firstName,
        LNAME: lastName
      },
      tags: tags
    });

    console.log('Subscriber added successfully');
    return response;
  } catch (error) {
    console.error('Error adding subscriber:', error);
    throw error;
  }
};

// Create automation
const createAutomationWorkflow = async () => {
  const workflowId = 'welcome_series_01';

  const automation = {
    recipients: {
      list_id: process.env.MAILCHIMP_LIST_ID
    },
    settings: {
      title: 'Welcome Series',
      from_name: 'Your Company',
      reply_to: 'hello@yourdomain.com'
    },
    trigger_settings: {
      workflow_type: 'emailAdded'
    }
  };

  try {
    const response = await Mailchimp.automations.create(automation);
    console.log('Automation created successfully');
    return response;
  } catch (error) {
    console.error('Error creating automation:', error);
    throw error;
  }
};

// Send campaign
const sendCampaign = async (subject, templateId, segmentId) => {
  try {
    // Create campaign
    const campaign = await Mailchimp.campaigns.create({
      type: 'regular',
      recipients: {
        list_id: process.env.MAILCHIMP_LIST_ID,
        segment_opts: {
          saved_segment_id: segmentId
        }
      },
      settings: {
        subject_line: subject,
        from_name: 'Your Company',
        reply_to: 'hello@yourdomain.com',
        template_id: templateId
      }
    });

    // Send campaign
    await Mailchimp.campaigns.send(campaign.id);
    console.log('Campaign sent successfully');

    return campaign;
  } catch (error) {
    console.error('Error sending campaign:', error);
    throw error;
  }
};

module.exports = { addSubscriber, createAutomationWorkflow, sendCampaign };
```

#### ConvertKit Integration

```javascript
// integration/convertkit-setup.js
const axios = require('axios');

const API_KEY = process.env.CONVERTKIT_API_KEY;
const API_SECRET = process.env.CONVERTKIT_API_SECRET;
const BASE_URL = 'https://api.convertkit.com/v3';

// Add subscriber to form
const addToForm = async (email, firstName, formId, tags = []) => {
  try {
    const response = await axios.post(
      `${BASE_URL}/forms/${formId}/subscribe`,
      {
        api_key: API_KEY,
        email,
        first_name: firstName,
        tags
      }
    );

    console.log('Subscriber added successfully');
    return response.data;
  } catch (error) {
    console.error('Error adding subscriber:', error);
    throw error;
  }
};

// Create sequence
const addToSequence = async (email, sequenceId) => {
  try {
    const response = await axios.post(
      `${BASE_URL}/sequences/${sequenceId}/subscribe`,
      {
        api_key: API_KEY,
        email
      }
    );

    console.log('Added to sequence successfully');
    return response.data;
  } catch (error) {
    console.error('Error adding to sequence:', error);
    throw error;
  }
};

// Tag subscriber
const tagSubscriber = async (email, tagId) => {
  try {
    const response = await axios.post(
      `${BASE_URL}/tags/${tagId}/subscribe`,
      {
        api_key: API_KEY,
        email
      }
    );

    console.log('Tag added successfully');
    return response.data;
  } catch (error) {
    console.error('Error adding tag:', error);
    throw error;
  }
};

module.exports = { addToForm, addToSequence, tagSubscriber };
```

### Step 6: Personalization & Dynamic Content

```javascript
// Personalization tokens
const personalizeEmail = (template, subscriber) => {
  const tokens = {
    '{{first_name}}': subscriber.firstName || 'there',
    '{{last_name}}': subscriber.lastName || '',
    '{{email}}': subscriber.email,
    '{{company}}': subscriber.company || '',
    '{{signup_date}}': formatDate(subscriber.signupDate),
    '{{days_since_signup}}': getDaysSince(subscriber.signupDate),
    '{{product_interest}}': subscriber.productInterest || '',
    '{{last_clicked}}': subscriber.lastClicked || '',
    '{{engagement_score}}': subscriber.engagementScore || 0
  };

  let personalizedTemplate = template;

  Object.keys(tokens).forEach(token => {
    personalizedTemplate = personalizedTemplate.replace(
      new RegExp(token, 'g'),
      tokens[token]
    );
  });

  return personalizedTemplate;
};

// Dynamic content based on behavior
const getDynamicContent = (subscriber) => {
  // Show different content based on engagement
  if (subscriber.engagementScore > 80) {
    return {
      cta: 'Ready to upgrade to Pro?',
      offer: 'exclusive-vip-discount'
    };
  } else if (subscriber.engagementScore > 50) {
    return {
      cta: 'Learn more about our features',
      offer: 'standard-discount'
    };
  } else {
    return {
      cta: 'See how it works',
      offer: 'getting-started-guide'
    };
  }
};
```

### Step 7: Analytics & Tracking

```javascript
// tracking/analytics.js

// Track email opens
const trackOpen = (emailId, subscriberId) => {
  // Log to database
  logEvent({
    event: 'email_open',
    emailId,
    subscriberId,
    timestamp: new Date()
  });

  // Send to analytics
  analytics.track('Email Opened', {
    email_id: emailId,
    subscriber_id: subscriberId
  });
};

// Track email clicks
const trackClick = (emailId, subscriberId, linkUrl) => {
  logEvent({
    event: 'email_click',
    emailId,
    subscriberId,
    linkUrl,
    timestamp: new Date()
  });

  analytics.track('Email Link Clicked', {
    email_id: emailId,
    subscriber_id: subscriberId,
    link_url: linkUrl
  });
};

// Track conversions
const trackConversion = (emailId, subscriberId, conversionType, value) => {
  logEvent({
    event: 'email_conversion',
    emailId,
    subscriberId,
    conversionType,
    value,
    timestamp: new Date()
  });

  analytics.track('Email Conversion', {
    email_id: emailId,
    subscriber_id: subscriberId,
    conversion_type: conversionType,
    value
  });
};

// UTM parameter builder
const buildUTMUrl = (baseUrl, emailName, linkName) => {
  const params = new URLSearchParams({
    utm_source: 'email',
    utm_medium: 'email',
    utm_campaign: emailName,
    utm_content: linkName
  });

  return `${baseUrl}?${params.toString()}`;
};

// Email performance dashboard data
const getEmailMetrics = async (campaignId) => {
  return {
    sent: 1000,
    delivered: 980,
    opens: 245,
    uniqueOpens: 220,
    clicks: 89,
    uniqueClicks: 75,
    conversions: 23,
    revenue: 2300,
    openRate: 22.4,
    clickRate: 7.6,
    conversionRate: 2.3,
    revenuePerEmail: 2.30
  };
};
```

### Step 8: Compliance & GDPR

```html
<!-- compliance/unsubscribe.html -->
<!DOCTYPE html>
<html>
<head>
  <title>Unsubscribe</title>
  <style>
    body {
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
      max-width: 600px;
      margin: 50px auto;
      padding: 20px;
      text-align: center;
    }
    .button {
      display: inline-block;
      padding: 12px 24px;
      margin: 10px;
      background-color: #007AFF;
      color: white;
      text-decoration: none;
      border-radius: 6px;
    }
  </style>
</head>
<body>
  <h1>We're sorry to see you go</h1>
  <p>Are you sure you want to unsubscribe from our emails?</p>

  <form action="/unsubscribe/confirm" method="POST">
    <input type="hidden" name="email" value="{{email}}">
    <input type="hidden" name="token" value="{{token}}">

    <p>
      <label>
        <input type="checkbox" name="reason" value="too_frequent">
        Emails are too frequent
      </label>
    </p>
    <p>
      <label>
        <input type="checkbox" name="reason" value="not_relevant">
        Content isn't relevant
      </label>
    </p>
    <p>
      <label>
        <input type="checkbox" name="reason" value="other">
        Other reason
      </label>
    </p>

    <p>
      <button type="submit" class="button">Unsubscribe</button>
      <a href="/" class="button" style="background-color: #666;">Keep me subscribed</a>
    </p>
  </form>

  <p style="margin-top: 40px; font-size: 14px; color: #666;">
    Or <a href="/preferences">update your email preferences</a> instead
  </p>
</body>
</html>
```

```javascript
// compliance/gdpr-consent.js
const recordConsent = async (email, consentType, ipAddress) => {
  await database.consents.create({
    email,
    consentType, // 'marketing', 'transactional', 'newsletter'
    consentGiven: true,
    consentDate: new Date(),
    ipAddress,
    userAgent: request.headers['user-agent'],
    source: 'landing_page_signup'
  });
};

const getConsentStatus = async (email) => {
  return await database.consents.findOne({
    where: { email },
    order: [['consentDate', 'DESC']]
  });
};

const revokeConsent = async (email, reason) => {
  await database.consents.update({
    consentGiven: false,
    revokeDate: new Date(),
    revokeReason: reason
  }, {
    where: { email }
  });
};
```

### Step 9: A/B Testing

```javascript
// Create A/B test variants
const abTestConfig = {
  email_02: {
    subject_lines: [
      "The #1 mistake most people make with [topic]",
      "Here's why [problem] happens (and how to fix it)",
      "Did you know? [Surprising statistic]"
    ],
    cta_buttons: [
      "Learn More",
      "Get Started Now",
      "Show Me How"
    ],
    send_times: [
      '09:00', // 9 AM
      '14:00', // 2 PM
      '19:00'  // 7 PM
    ]
  }
};

// Split test implementation
const sendABTest = async (subscribers, variants) => {
  const splitSize = Math.floor(subscribers.length / variants.length);

  for (let i = 0; i < variants.length; i++) {
    const segment = subscribers.slice(i * splitSize, (i + 1) * splitSize);

    await sendBulkEmail({
      to: segment,
      subject: variants[i].subject,
      template: variants[i].template,
      variant: `variant_${String.fromCharCode(65 + i)}` // A, B, C...
    });
  }
};

// Analyze test results
const analyzeABTest = async (testId) => {
  const results = await database.emailStats.findAll({
    where: { testId },
    group: ['variant']
  });

  return results.map(r => ({
    variant: r.variant,
    sent: r.sent,
    openRate: (r.opens / r.sent * 100).toFixed(2),
    clickRate: (r.clicks / r.sent * 100).toFixed(2),
    conversionRate: (r.conversions / r.sent * 100).toFixed(2),
    winner: r.conversionRate === Math.max(...results.map(x => x.conversionRate))
  }));
};
```

### Step 10: Testing & Quality Assurance

```javascript
// testing/email-validator.js

// Validate email content
const validateEmail = (html, text) => {
  const issues = [];

  // Check for spam trigger words
  const spamWords = ['free', 'click here', 'act now', 'limited time', '!!!'];
  spamWords.forEach(word => {
    if (text.toLowerCase().includes(word)) {
      issues.push(`Potential spam word: "${word}"`);
    }
  });

  // Check for required elements
  if (!html.includes('unsubscribe')) {
    issues.push('Missing unsubscribe link');
  }

  if (!html.includes('{{company_address}}')) {
    issues.push('Missing company address (CAN-SPAM requirement)');
  }

  // Check for broken links
  const links = html.match(/href="([^"]*)"/g) || [];
  links.forEach(link => {
    if (link.includes('href="#"') || link.includes('href=""')) {
      issues.push('Broken or empty link found');
    }
  });

  // Check image alt tags
  const images = html.match(/<img[^>]*>/g) || [];
  images.forEach(img => {
    if (!img.includes('alt=')) {
      issues.push('Image missing alt tag');
    }
  });

  return {
    valid: issues.length === 0,
    issues
  };
};

// Test email rendering across clients
const testRendering = async (html) => {
  // Use Litmus or Email on Acid API
  const clients = [
    'gmail_chrome',
    'outlook_2019',
    'iphone_13',
    'android_gmail'
  ];

  const results = await Promise.all(
    clients.map(client => renderTest(html, client))
  );

  return results;
};

// Spam score checker
const checkSpamScore = async (html, text, subject) => {
  // Use SpamAssassin or similar
  const score = await spamChecker.analyze({
    html,
    text,
    subject,
    from: 'hello@yourdomain.com'
  });

  return {
    score: score.score,
    threshold: 5.0,
    passed: score.score < 5.0,
    issues: score.details
  };
};
```

### Step 11: Automation & Sequences

```javascript
// automation/sequence-config.json
{
  "sequences": [
    {
      "id": "welcome_series",
      "name": "Welcome Series",
      "trigger": "form_submission",
      "emails": [
        {
          "id": "welcome_01",
          "delay": 0,
          "subject": "Welcome! Here's what to expect...",
          "template": "email-01-welcome.html"
        },
        {
          "id": "value_02",
          "delay": 172800,
          "subject": "The #1 mistake most people make",
          "template": "email-02-value-intro.html",
          "conditions": {
            "opened": "welcome_01"
          }
        },
        {
          "id": "education_03",
          "delay": 345600,
          "subject": "The complete guide to...",
          "template": "email-03-education.html"
        }
      ]
    },
    {
      "id": "abandoned_cart",
      "name": "Abandoned Cart Recovery",
      "trigger": "cart_abandoned",
      "emails": [
        {
          "delay": 3600,
          "subject": "You left something behind...",
          "template": "cart-01.html"
        },
        {
          "delay": 86400,
          "subject": "Still interested? Here's 10% off",
          "template": "cart-02.html"
        },
        {
          "delay": 259200,
          "subject": "Last chance: Your cart expires soon",
          "template": "cart-03.html"
        }
      ]
    }
  ]
}
```

### Step 12: Complete Documentation

```markdown
# Email Campaign Documentation

## Campaign Overview
- **Name**: Welcome Series
- **Goal**: Convert new subscribers to customers
- **Length**: 7-10 emails over 30 days
- **Expected Conversion Rate**: 5-8%

## Setup Instructions

### 1. Email Service Provider Setup
1. Create account with [ESP name]
2. Add API key to `.env` file
3. Verify sender domain
4. Import email templates
5. Create automation workflow

### 2. Upload Email Templates
\`\`\`bash
# Upload to SendGrid
node scripts/upload-templates.js

# Upload to Mailchimp
node scripts/sync-mailchimp.js
\`\`\`

### 3. Configure Automation
1. Set trigger: Form submission
2. Add 7-10 emails to sequence
3. Set delays between emails
4. Configure conditions (if/else branching)
5. Test automation with test email

### 4. Testing Checklist
- [ ] Test email rendering on all major clients
- [ ] Check all links work
- [ ] Verify personalization tokens
- [ ] Test unsubscribe link
- [ ] Check spam score (<5.0)
- [ ] Send test emails to team
- [ ] Verify tracking pixels
- [ ] Test mobile rendering

### 5. Launch
1. Import subscriber list
2. Activate automation
3. Monitor first sends
4. Check deliverability
5. Watch analytics dashboard

## Email Sequence Overview

| Email | Day | Subject | Goal | Expected Open % | Expected Click % |
|-------|-----|---------|------|----------------|-----------------|
| #1 | 0 | Welcome! | Build rapport | 40-50% | 10-15% |
| #2 | 2 | #1 Mistake | Educate | 25-35% | 8-12% |
| #3 | 4 | Complete Guide | Provide value | 20-30% | 7-10% |
| #4 | 7 | Case Study | Build trust | 20-25% | 6-9% |
| #5 | 10 | Objections | Handle concerns | 18-23% | 5-8% |
| #6 | 13 | Urgency | Create FOMO | 20-28% | 8-12% |
| #7 | 14 | Conversion | Make sale | 22-30% | 10-15% |

## Optimization Tips

### Subject Lines
- Keep under 50 characters
- Use emojis sparingly (test first)
- Include numbers when possible
- Ask questions
- Create curiosity
- Personalize with first name

### Content
- Keep paragraphs short (2-3 lines)
- Use bullet points for scannability
- Include clear CTA buttons
- Add social proof
- Use conversational tone
- Address reader directly ("you")

### Timing
- Test send times (morning vs evening)
- Avoid Mondays and Fridays
- Consider time zones
- Respect frequency (don't over-send)

## Analytics & KPIs

Track these metrics:
- **Delivery Rate**: >98%
- **Open Rate**: >20%
- **Click Rate**: >3%
- **Conversion Rate**: >2%
- **Unsubscribe Rate**: <0.5%
- **Spam Complaints**: <0.1%
- **Revenue Per Email**: $1-5+

## Troubleshooting

### Low Open Rates
- Test different subject lines
- Clean email list (remove inactive)
- Improve sender reputation
- Try different send times

### Low Click Rates
- Make CTAs more prominent
- Reduce number of links
- Improve content relevance
- Test different copy

### High Unsubscribe Rate
- Reduce email frequency
- Improve content quality
- Better audience targeting
- Set clear expectations

## Compliance
- ✅ Include unsubscribe link
- ✅ Add physical address
- ✅ Honor opt-outs within 10 days
- ✅ Don't use deceptive subject lines
- ✅ Clearly identify as advertisement
- ✅ Obtain consent before sending
- ✅ Keep consent records

## Next Steps
1. Launch campaign
2. Monitor performance daily
3. A/B test elements weekly
4. Optimize based on data
5. Scale to more subscribers
```

### Success Criteria

The command is successful when you deliver:
✅ Complete 7-10 email sequence with compelling copy
✅ Professional HTML email templates (responsive)
✅ Subject lines and preview text (with A/B variants)
✅ Email service provider integration (working code)
✅ Personalization and dynamic content
✅ Analytics and tracking implementation
✅ Compliance features (unsubscribe, GDPR)
✅ Automation/sequence configuration
✅ Testing tools (spam checker, validator)
✅ Complete documentation and setup guide
✅ Performance benchmarks and KPIs
✅ Optimization recommendations

This should be a COMPLETE, PROFESSIONAL email campaign ready for immediate deployment and revenue generation.
