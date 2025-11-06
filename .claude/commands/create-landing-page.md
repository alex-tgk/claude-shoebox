# Create Landing Page

Generate a complete, high-converting landing page with professional design, SEO optimization, analytics, and conversion tools ready for immediate deployment.

## Instructions

You are tasked with creating a COMPLETE, production-ready landing page optimized for conversions. This is a one-shot command that must produce a fully functional, polished product ready for immediate deployment and revenue generation.

### Step 1: Gather Requirements

First, ask the user these essential questions:
1. **Product/Service**: What are you selling/promoting?
2. **Target Audience**: Who is your ideal customer?
3. **Unique Value Proposition**: What makes you different?
4. **Primary Goal**: Email signup, product purchase, demo booking, or download?
5. **Pricing**: Do you have pricing tiers? (If applicable)
6. **Social Proof**: Do you have testimonials, reviews, or case studies?
7. **Brand Assets**: Logo, colors, fonts? (Or should I create a professional theme?)
8. **Call-to-Action**: What's the primary button text? ("Get Started", "Buy Now", etc.)
9. **Tech Stack**: Next.js, React, or vanilla HTML?
10. **Deployment Target**: Vercel, Netlify, or other?

### Step 2: Complete Landing Page Structure

Create the following COMPLETE page structure:

```
landing-page/
├── public/
│   ├── images/
│   │   ├── logo.svg
│   │   ├── hero-image.jpg
│   │   ├── feature-1.svg
│   │   ├── feature-2.svg
│   │   ├── feature-3.svg
│   │   ├── testimonial-1.jpg
│   │   ├── testimonial-2.jpg
│   │   ├── testimonial-3.jpg
│   │   ├── og-image.jpg
│   │   └── favicon.ico
│   ├── robots.txt
│   ├── sitemap.xml
│   └── manifest.json
├── src/
│   ├── components/
│   │   ├── Hero.jsx
│   │   ├── Features.jsx
│   │   ├── Benefits.jsx
│   │   ├── HowItWorks.jsx
│   │   ├── Pricing.jsx
│   │   ├── Testimonials.jsx
│   │   ├── FAQ.jsx
│   │   ├── CTA.jsx
│   │   ├── Footer.jsx
│   │   ├── Header.jsx
│   │   └── EmailCapture.jsx
│   ├── utils/
│   │   ├── analytics.js
│   │   ├── tracking.js
│   │   └── validation.js
│   ├── styles/
│   │   └── globals.css
│   └── pages/
│       ├── index.jsx
│       ├── thank-you.jsx
│       └── privacy-policy.jsx
├── .env.example
├── .env.local
├── tailwind.config.js
├── next.config.js (or vite.config.js)
├── package.json
├── vercel.json (or netlify.toml)
└── README.md
```

### Step 3: Implement ALL Sections

#### 1. Header/Navigation

Create a professional, sticky header:

```jsx
// components/Header.jsx
- Logo (left side)
- Navigation links (Features, Pricing, About, Contact)
- CTA button (right side, highlighted)
- Mobile hamburger menu
- Smooth scroll to sections
- Transparent on top, solid on scroll
- Responsive design
```

**Features:**
- Sticky positioning
- Background change on scroll
- Mobile-responsive menu
- Smooth animations
- High contrast CTA button

#### 2. Hero Section

Create a compelling above-the-fold section:

```jsx
// components/Hero.jsx
<Hero>
  <Headline>
    [Compelling H1 with main benefit - under 10 words]
  </Headline>
  <Subheadline>
    [Supporting text explaining the value - 1-2 sentences]
  </Subheadline>
  <CTAButtons>
    <PrimaryButton>[Main CTA]</PrimaryButton>
    <SecondaryButton>[Secondary action]</SecondaryButton>
  </CTAButtons>
  <HeroImage>
    [Product screenshot/illustration - high quality]
  </HeroImage>
  <SocialProof>
    [Trust indicators: "Trusted by 10,000+ users" or logos]
  </SocialProof>
</Hero>
```

**Must Include:**
- Attention-grabbing headline (benefit-focused)
- Clear subheadline
- Prominent CTA buttons
- High-quality hero image/video
- Social proof (users, ratings, logos)
- Value proposition
- Responsive layout (image + text side-by-side on desktop)
- Animations (fade in, slide up)

#### 3. Social Proof Bar

Add immediate credibility:

```jsx
// components/SocialProof.jsx
- Customer logos (6-8 recognizable brands)
- OR user testimonials count
- OR ratings (5-star with count)
- OR media mentions
- Scrolling animation on mobile
```

#### 4. Features Section

Showcase 6-9 key features:

```jsx
// components/Features.jsx
<Features>
  <SectionHeader>
    <PreHeadline>Features</PreHeadline>
    <Headline>Everything you need to [achieve goal]</Headline>
    <Description>[Supporting text]</Description>
  </SectionHeader>

  <FeatureGrid>
    {features.map(feature => (
      <FeatureCard key={feature.id}>
        <Icon>{feature.icon}</Icon>
        <Title>{feature.title}</Title>
        <Description>{feature.description}</Description>
      </FeatureCard>
    ))}
  </FeatureGrid>
</Features>
```

**Each Feature Must Have:**
- Icon (SVG, professional design)
- Clear title (3-5 words)
- Description (2-3 sentences)
- Benefit-focused copy
- Consistent layout
- Hover effects

#### 5. Benefits/Value Proposition Section

Show the transformation (Before → After):

```jsx
// components/Benefits.jsx
<Benefits>
  <Split>
    <Visual>[Screenshot/illustration]</Visual>
    <Content>
      <Headline>[Benefit-focused headline]</Headline>
      <BenefitList>
        <BenefitItem icon="check">
          [Specific benefit #1]
        </BenefitItem>
        <BenefitItem icon="check">
          [Specific benefit #2]
        </BenefitItem>
        <BenefitItem icon="check">
          [Specific benefit #3]
        </BenefitItem>
      </BenefitList>
      <CTAButton>[Action]</CTAButton>
    </Content>
  </Split>

  [Repeat 2-3 times with alternating layout]
</Benefits>
```

#### 6. How It Works Section

Show the process (3-4 steps):

```jsx
// components/HowItWorks.jsx
<HowItWorks>
  <SectionHeader>
    <Headline>Get started in 3 simple steps</Headline>
  </SectionHeader>

  <StepsList>
    <Step number="1">
      <Icon>[Relevant icon]</Icon>
      <Title>[Action title]</Title>
      <Description>[What to do]</Description>
    </Step>
    <Step number="2">
      <Icon>[Relevant icon]</Icon>
      <Title>[Action title]</Title>
      <Description>[What to do]</Description>
    </Step>
    <Step number="3">
      <Icon>[Relevant icon]</Icon>
      <Title>[Action title]</Title>
      <Description>[What to do]</Description>
    </Step>
  </StepsList>
</HowItWorks>
```

#### 7. Pricing Section

Create compelling pricing tiers:

```jsx
// components/Pricing.jsx
<Pricing>
  <SectionHeader>
    <Headline>Simple, transparent pricing</Headline>
    <Description>Choose the plan that's right for you</Description>
  </SectionHeader>

  <BillingToggle>
    <Option active>Monthly</Option>
    <Option>Annual (Save 20%)</Option>
  </BillingToggle>

  <PricingGrid>
    <PricingCard tier="basic">
      <Name>Starter</Name>
      <Price>
        <Amount>$29</Amount>
        <Period>/month</Period>
      </Price>
      <Description>Perfect for individuals</Description>
      <FeaturesList>
        <Feature included>Feature 1</Feature>
        <Feature included>Feature 2</Feature>
        <Feature included>Feature 3</Feature>
        <Feature excluded>Feature 4</Feature>
      </FeaturesList>
      <CTAButton>Start Free Trial</CTAButton>
    </PricingCard>

    <PricingCard tier="pro" featured>
      <Badge>Most Popular</Badge>
      <Name>Professional</Name>
      <Price>
        <Amount>$79</Amount>
        <Period>/month</Period>
      </Price>
      <Description>For growing teams</Description>
      <FeaturesList>
        <Feature included>Everything in Starter</Feature>
        <Feature included>Feature 4</Feature>
        <Feature included>Feature 5</Feature>
        <Feature included>Feature 6</Feature>
      </FeaturesList>
      <CTAButton primary>Start Free Trial</CTAButton>
    </PricingCard>

    <PricingCard tier="enterprise">
      <Name>Enterprise</Name>
      <Price>
        <Amount>Custom</Amount>
      </Price>
      <Description>For large organizations</Description>
      <FeaturesList>
        <Feature included>Everything in Pro</Feature>
        <Feature included>Feature 7</Feature>
        <Feature included>Feature 8</Feature>
        <Feature included>Dedicated support</Feature>
      </FeaturesList>
      <CTAButton>Contact Sales</CTAButton>
    </PricingCard>
  </PricingGrid>

  <Guarantees>
    <Guarantee icon="shield">30-day money-back guarantee</Guarantee>
    <Guarantee icon="card">No credit card required</Guarantee>
    <Guarantee icon="cancel">Cancel anytime</Guarantee>
  </Guarantees>
</Pricing>
```

**Pricing Best Practices:**
- 3 tiers (good, better, best)
- Highlight recommended option
- Annual discount option
- Clear feature comparison
- Trust badges (money-back guarantee)
- No credit card required message
- Start with a free trial

#### 8. Testimonials Section

Build trust with social proof:

```jsx
// components/Testimonials.jsx
<Testimonials>
  <SectionHeader>
    <Headline>Loved by thousands of users</Headline>
    <Rating>
      <Stars count={5} />
      <Text>4.9 out of 5 stars from 2,000+ reviews</Text>
    </Rating>
  </SectionHeader>

  <TestimonialGrid>
    <TestimonialCard>
      <Quote>
        "[Specific result or transformation achieved]"
      </Quote>
      <Author>
        <Avatar src="[photo]" />
        <Name>John Doe</Name>
        <Title>CEO, Company Inc.</Title>
      </Author>
      <Rating stars={5} />
    </TestimonialCard>

    [6-9 more testimonials]
  </TestimonialGrid>

  <VideoTestimonials>
    [Optional: 1-2 video testimonials with thumbnails]
  </VideoTestimonials>
</Testimonials>
```

**Testimonial Requirements:**
- 6-12 testimonials minimum
- Real photos (or professional avatars)
- Specific results/numbers
- Company names and titles
- 5-star ratings
- Mix of lengths (short and detailed)
- Video testimonials (optional)

#### 9. FAQ Section

Answer objections preemptively:

```jsx
// components/FAQ.jsx
<FAQ>
  <SectionHeader>
    <Headline>Frequently Asked Questions</Headline>
  </SectionHeader>

  <FAQList>
    <FAQItem>
      <Question>How does [product] work?</Question>
      <Answer>[Clear, concise answer]</Answer>
    </FAQItem>

    [8-12 more Q&As covering:]
    - How it works
    - Pricing questions
    - Trial/cancellation
    - Security/privacy
    - Support/training
    - Integration options
    - Comparison to alternatives
  </FAQList>

  <ContactCTA>
    <Text>Still have questions?</Text>
    <Button>Contact Support</Button>
  </ContactCTA>
</FAQ>
```

#### 10. Final CTA Section

Strong call-to-action before footer:

```jsx
// components/CTA.jsx
<CTA>
  <Container>
    <Headline>Ready to [achieve benefit]?</Headline>
    <Description>
      Join [X] companies already using [product]
    </Description>
    <CTAButton size="large">
      [Primary Action]
    </CTAButton>
    <Subtext>
      No credit card required · 14-day free trial
    </Subtext>
  </Container>
</CTA>
```

#### 11. Footer

Complete, professional footer:

```jsx
// components/Footer.jsx
<Footer>
  <TopSection>
    <CompanyInfo>
      <Logo />
      <Description>[Short company description]</Description>
      <SocialLinks>
        <Link icon="twitter" href="#" />
        <Link icon="linkedin" href="#" />
        <Link icon="facebook" href="#" />
        <Link icon="instagram" href="#" />
      </SocialLinks>
    </CompanyInfo>

    <LinkColumns>
      <Column>
        <Title>Product</Title>
        <Link>Features</Link>
        <Link>Pricing</Link>
        <Link>Integrations</Link>
        <Link>Changelog</Link>
      </Column>

      <Column>
        <Title>Company</Title>
        <Link>About</Link>
        <Link>Blog</Link>
        <Link>Careers</Link>
        <Link>Contact</Link>
      </Column>

      <Column>
        <Title>Resources</Title>
        <Link>Help Center</Link>
        <Link>API Docs</Link>
        <Link>Community</Link>
        <Link>Status</Link>
      </Column>

      <Column>
        <Title>Legal</Title>
        <Link>Privacy</Link>
        <Link>Terms</Link>
        <Link>Security</Link>
        <Link>Cookies</Link>
      </Column>
    </LinkColumns>
  </TopSection>

  <BottomSection>
    <Copyright>© 2024 Company Name. All rights reserved.</Copyright>
    <LanguageSelector>
      <Select>[English ▼]</Select>
    </LanguageSelector>
  </BottomSection>
</Footer>
```

### Step 4: Email Capture Integration

Implement COMPLETE email capture system:

```jsx
// components/EmailCapture.jsx
import { useState } from 'react';

const EmailCapture = ({ source }) => {
  const [email, setEmail] = useState('');
  const [status, setStatus] = useState('idle'); // idle, loading, success, error
  const [message, setMessage] = useState('');

  const handleSubmit = async (e) => {
    e.preventDefault();
    setStatus('loading');

    try {
      // Validate email
      if (!isValidEmail(email)) {
        throw new Error('Please enter a valid email');
      }

      // Send to email service
      await subscribeUser({
        email,
        source,
        timestamp: new Date().toISOString()
      });

      // Track conversion
      trackEvent('email_capture', { source });

      setStatus('success');
      setMessage('Thanks! Check your email for confirmation.');

      // Redirect to thank you page
      setTimeout(() => {
        window.location.href = '/thank-you';
      }, 2000);

    } catch (error) {
      setStatus('error');
      setMessage(error.message);
    }
  };

  return (
    <Form onSubmit={handleSubmit}>
      <Input
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
        placeholder="Enter your email"
        disabled={status === 'loading'}
        required
      />
      <Button type="submit" disabled={status === 'loading'}>
        {status === 'loading' ? 'Subscribing...' : 'Get Started'}
      </Button>
      {status === 'success' && <SuccessMessage>{message}</SuccessMessage>}
      {status === 'error' && <ErrorMessage>{message}</ErrorMessage>}
    </Form>
  );
};
```

**Integrate with Email Service Provider:**

```javascript
// utils/emailService.js

// MAILCHIMP Integration
export const subscribeToMailchimp = async ({ email, source }) => {
  const response = await fetch('/api/subscribe', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      email,
      tags: [source, 'landing-page'],
      timestamp: new Date().toISOString()
    })
  });

  if (!response.ok) throw new Error('Subscription failed');
  return response.json();
};

// CONVERTKIT Integration
export const subscribeToConvertKit = async ({ email, source }) => {
  const API_KEY = process.env.CONVERTKIT_API_KEY;
  const FORM_ID = process.env.CONVERTKIT_FORM_ID;

  const response = await fetch(
    `https://api.convertkit.com/v3/forms/${FORM_ID}/subscribe`,
    {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        api_key: API_KEY,
        email,
        tags: [source]
      })
    }
  );

  if (!response.ok) throw new Error('Subscription failed');
  return response.json();
};

// SENDGRID Integration
export const subscribeToSendGrid = async ({ email, source }) => {
  const response = await fetch('https://api.sendgrid.com/v3/marketing/contacts', {
    method: 'PUT',
    headers: {
      'Authorization': `Bearer ${process.env.SENDGRID_API_KEY}`,
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      contacts: [{
        email,
        custom_fields: {
          source,
          signup_date: new Date().toISOString()
        }
      }]
    })
  });

  if (!response.ok) throw new Error('Subscription failed');
  return response.json();
};
```

### Step 5: SEO Optimization

Implement COMPLETE SEO strategy:

#### Meta Tags (in every page):

```jsx
// components/SEO.jsx
import Head from 'next/head';

const SEO = ({
  title = 'Product Name - Headline with Benefit',
  description = 'Clear description with keywords and value prop (150-160 chars)',
  image = '/og-image.jpg',
  url = 'https://yoursite.com'
}) => (
  <Head>
    {/* Primary Meta Tags */}
    <title>{title}</title>
    <meta name="title" content={title} />
    <meta name="description" content={description} />
    <meta name="keywords" content="keyword1, keyword2, keyword3" />

    {/* Open Graph / Facebook */}
    <meta property="og:type" content="website" />
    <meta property="og:url" content={url} />
    <meta property="og:title" content={title} />
    <meta property="og:description" content={description} />
    <meta property="og:image" content={image} />

    {/* Twitter */}
    <meta property="twitter:card" content="summary_large_image" />
    <meta property="twitter:url" content={url} />
    <meta property="twitter:title" content={title} />
    <meta property="twitter:description" content={description} />
    <meta property="twitter:image" content={image} />

    {/* Additional Meta */}
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="robots" content="index, follow" />
    <link rel="canonical" href={url} />
    <link rel="icon" href="/favicon.ico" />

    {/* Structured Data */}
    <script
      type="application/ld+json"
      dangerouslySetInnerHTML={{
        __html: JSON.stringify({
          "@context": "https://schema.org",
          "@type": "SoftwareApplication",
          "name": "Product Name",
          "description": description,
          "applicationCategory": "BusinessApplication",
          "offers": {
            "@type": "Offer",
            "price": "29",
            "priceCurrency": "USD"
          },
          "aggregateRating": {
            "@type": "AggregateRating",
            "ratingValue": "4.9",
            "ratingCount": "2000"
          }
        })
      }}
    />
  </Head>
);
```

#### robots.txt:

```
User-agent: *
Allow: /
Disallow: /api/
Disallow: /admin/

Sitemap: https://yoursite.com/sitemap.xml
```

#### sitemap.xml:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://yoursite.com/</loc>
    <lastmod>2024-01-01</lastmod>
    <changefreq>weekly</changefreq>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://yoursite.com/pricing</loc>
    <lastmod>2024-01-01</lastmod>
    <changefreq>monthly</changefreq>
    <priority>0.8</priority>
  </url>
</urlset>
```

### Step 6: Analytics & Tracking

Implement COMPLETE analytics tracking:

```javascript
// utils/analytics.js

// GOOGLE ANALYTICS 4
export const initGA4 = () => {
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', process.env.NEXT_PUBLIC_GA4_ID);
};

// PLAUSIBLE
export const initPlausible = () => {
  const script = document.createElement('script');
  script.defer = true;
  script.data-domain = 'yoursite.com';
  script.src = 'https://plausible.io/js/plausible.js';
  document.head.appendChild(script);
};

// TRACK EVENTS
export const trackEvent = (eventName, properties = {}) => {
  // Google Analytics
  if (window.gtag) {
    window.gtag('event', eventName, properties);
  }

  // Plausible
  if (window.plausible) {
    window.plausible(eventName, { props: properties });
  }

  // Facebook Pixel
  if (window.fbq) {
    window.fbq('track', eventName, properties);
  }

  // Custom tracking
  console.log('[Analytics]', eventName, properties);
};

// TRACK PAGE VIEWS
export const trackPageView = (url) => {
  trackEvent('page_view', { page: url });
};

// TRACK CONVERSIONS
export const trackConversion = (type, value) => {
  trackEvent('conversion', { type, value });

  // Facebook Conversion
  if (window.fbq) {
    window.fbq('track', 'Lead');
  }
};

// TRACK SCROLL DEPTH
export const trackScrollDepth = () => {
  const depths = [25, 50, 75, 100];
  let tracked = [];

  window.addEventListener('scroll', () => {
    const percent = (window.scrollY / (document.body.scrollHeight - window.innerHeight)) * 100;

    depths.forEach(depth => {
      if (percent >= depth && !tracked.includes(depth)) {
        trackEvent('scroll_depth', { depth });
        tracked.push(depth);
      }
    });
  });
};

// TRACK CLICKS
export const trackClick = (element, label) => {
  element.addEventListener('click', () => {
    trackEvent('click', { label });
  });
};

// TRACK FORM SUBMISSIONS
export const trackFormSubmit = (formName) => {
  trackEvent('form_submit', { form: formName });
  trackConversion('lead', 1);
};
```

**Track These Events:**
- Page views
- Button clicks (all CTAs)
- Form submissions
- Email captures
- Scroll depth (25%, 50%, 75%, 100%)
- Time on page
- Video plays
- Link clicks
- Pricing plan selections
- FAQ expansions

### Step 7: A/B Testing Setup

```javascript
// utils/abtest.js

export const ABTest = ({ name, variants, children }) => {
  const [variant, setVariant] = useState(null);

  useEffect(() => {
    // Get or assign variant
    let userVariant = localStorage.getItem(`ab_${name}`);

    if (!userVariant) {
      // Randomly assign variant
      userVariant = variants[Math.floor(Math.random() * variants.length)];
      localStorage.setItem(`ab_${name}`, userVariant);
    }

    setVariant(userVariant);

    // Track variant view
    trackEvent('ab_test_view', {
      test: name,
      variant: userVariant
    });
  }, [name, variants]);

  if (!variant) return null;

  return children(variant);
};

// Usage:
<ABTest name="hero_headline" variants={['A', 'B']}>
  {(variant) => (
    variant === 'A'
      ? <h1>Original Headline</h1>
      : <h1>Alternative Headline</h1>
  )}
</ABTest>
```

**A/B Test These Elements:**
- Headlines
- CTA button text/colors
- Hero images
- Pricing display
- Social proof placement
- Form length

### Step 8: Performance Optimization

Implement ALL performance optimizations:

```javascript
// next.config.js
module.exports = {
  images: {
    domains: ['yourdomain.com'],
    formats: ['image/avif', 'image/webp'],
  },
  compiler: {
    removeConsole: process.env.NODE_ENV === 'production',
  },
  swcMinify: true,
};

// Image Optimization
import Image from 'next/image';

<Image
  src="/hero.jpg"
  alt="Hero"
  width={1200}
  height={600}
  priority // for above-fold images
  placeholder="blur"
  blurDataURL="data:image/..."
/>

// Lazy Loading
import dynamic from 'next/dynamic';

const Testimonials = dynamic(() => import('./components/Testimonials'), {
  loading: () => <LoadingSpinner />,
  ssr: false
});

// Code Splitting
const FAQ = dynamic(() => import('./components/FAQ'));
const Footer = dynamic(() => import('./components/Footer'));
```

**Performance Checklist:**
- ✅ Image optimization (WebP, lazy loading)
- ✅ Code splitting (lazy load below fold)
- ✅ Minification (CSS, JS)
- ✅ Compression (Gzip/Brotli)
- ✅ Caching headers
- ✅ CDN delivery
- ✅ Font optimization
- ✅ Critical CSS inline
- ✅ Defer non-critical JS
- ✅ Preload critical resources

**Target Metrics:**
- Lighthouse Score: 95+
- First Contentful Paint: < 1.5s
- Largest Contentful Paint: < 2.5s
- Time to Interactive: < 3.5s
- Cumulative Layout Shift: < 0.1

### Step 9: Deployment Configuration

Create deployment-ready configurations:

#### Vercel (vercel.json):

```json
{
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        {
          "key": "X-Content-Type-Options",
          "value": "nosniff"
        },
        {
          "key": "X-Frame-Options",
          "value": "DENY"
        },
        {
          "key": "X-XSS-Protection",
          "value": "1; mode=block"
        }
      ]
    }
  ],
  "redirects": [
    {
      "source": "/home",
      "destination": "/",
      "permanent": true
    }
  ]
}
```

#### Netlify (netlify.toml):

```toml
[build]
  command = "npm run build"
  publish = "out"

[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "DENY"
    X-XSS-Protection = "1; mode=block"
    X-Content-Type-Options = "nosniff"
    Referrer-Policy = "strict-origin-when-cross-origin"

[[redirects]]
  from = "/home"
  to = "/"
  status = 301

[[plugins]]
  package = "@netlify/plugin-lighthouse"
```

### Step 10: Complete Documentation

Provide comprehensive README:

```markdown
# [Product Name] Landing Page

## Overview
High-converting landing page built with [Next.js/React] and TailwindCSS.

## Features
✅ Responsive design
✅ SEO optimized
✅ Analytics integrated
✅ Email capture
✅ A/B testing ready
✅ Performance optimized
✅ Accessibility compliant

## Setup

### Prerequisites
- Node.js 18+
- npm or yarn

### Installation
\`\`\`bash
npm install
\`\`\`

### Environment Variables
Create `.env.local`:
\`\`\`
NEXT_PUBLIC_GA4_ID=G-XXXXXXXXXX
MAILCHIMP_API_KEY=your_key
MAILCHIMP_LIST_ID=your_list_id
\`\`\`

### Development
\`\`\`bash
npm run dev
\`\`\`

### Build
\`\`\`bash
npm run build
npm start
\`\`\`

## Deployment

### Vercel
\`\`\`bash
vercel --prod
\`\`\`

### Netlify
\`\`\`bash
netlify deploy --prod
\`\`\`

## Customization

### Content
Edit content in `/src/data/content.js`

### Styling
Modify theme in `/tailwind.config.js`

### Analytics
Configure in `/utils/analytics.js`

## Performance
- Lighthouse Score: 98
- FCP: 1.2s
- LCP: 1.8s

## License
MIT
```

### Success Criteria

The command is successful when you deliver:
✅ Complete, production-ready landing page
✅ All sections fully implemented (Hero, Features, Pricing, Testimonials, FAQ, CTA, Footer)
✅ Professional, responsive design
✅ SEO fully optimized (meta tags, structured data, sitemap)
✅ Analytics integrated (GA4, Plausible, custom events)
✅ Email capture working with ESP integration
✅ A/B testing setup and ready
✅ Performance optimized (95+ Lighthouse score)
✅ Deployment configuration ready
✅ Complete documentation
✅ Conversion-optimized copy
✅ Mobile-responsive
✅ Accessibility compliant

This should be a COMPLETE, HIGH-CONVERTING landing page ready for immediate deployment and lead generation.
