# Business Prompts

A collection of prompt templates for PRDs, marketing, strategy, and business-focused development tasks.

---

## Product Requirements

### 1. Generate Product Requirements Document (PRD)

**Purpose:** Create comprehensive PRD for a new feature.

**Prompt:**
```
Create a Product Requirements Document for [FEATURE_NAME]:

Context:
- Product: [PRODUCT_NAME]
- Target users: [USER_SEGMENTS]
- Business goal: [OBJECTIVE]
- Success metrics: [KPIS]

Include sections:
- Executive Summary
- Problem Statement
- Goals and Objectives
- User Stories and Use Cases
- Functional Requirements (detailed)
- Non-Functional Requirements (performance, security, etc.)
- User Experience Requirements
- Technical Considerations
- Dependencies and Integrations
- Success Metrics and KPIs
- Timeline and Milestones
- Out of Scope
- Open Questions
- Appendix (mockups, research, etc.)

Write for engineering, design, and stakeholder audiences.
```

**Example:**
```
Create PRD for Multi-Language Support feature:

Context:
- Product: SaaS project management tool
- Users: Global teams, SMBs to enterprise
- Goal: Expand to non-English markets, increase international revenue by 30%
- Metrics: User adoption in target countries, reduced churn for international users

Sections:
- Summary: Add support for 5 languages (Spanish, French, German, Japanese, Chinese)
- Problem: 40% of trial users from target markets don't convert, cite language barrier
- Goals: Support 5 languages in UI, email, docs; maintain feature parity
- User Stories: As a Spanish user, I want UI in Spanish so I can use product efficiently
- Functional: Language selector, translated strings, date/time localization, RTL for future
- Non-Functional: <100ms translation load, 99.9% translation accuracy, SEO for each language
- UX: Language selector in header, detect browser language, remember preference
- Technical: i18n framework, translation management system, CDN for language bundles
- Dependencies: Hire translators, integrate translation service API
- Metrics: 30% international user growth, 90% of users in target languages
- Timeline: Q2 (dev), Q3 (testing & translation), Q4 (rollout)
- Out of Scope: Customer support in other languages (future), automated translation
- Questions: Professional vs machine translation? Add more languages?

For cross-functional team alignment.
```

---

### 2. Generate User Stories

**Purpose:** Create well-formed user stories from requirements.

**Prompt:**
```
Generate user stories for [FEATURE]:

Feature description:
[DESCRIPTION]

User personas:
[PERSONA_DETAILS]

For each user story provide:
- Title
- Story format: "As a [ROLE], I want [GOAL] so that [BENEFIT]"
- Acceptance criteria (Given/When/Then format)
- Priority (Must Have / Should Have / Could Have / Won't Have)
- Story points estimate
- Dependencies
- Notes/considerations

Generate [NUMBER] user stories covering main workflows.
```

**Example:**
```
Generate user stories for Shopping Cart feature:

Feature: Allow users to add products to cart, modify quantities, and proceed to checkout

Personas:
- Busy parent: Wants quick, efficient shopping
- Budget shopper: Needs to track total, compare prices
- Mobile user: Shops on phone, wants simple interface

Stories:
1. "Add Product to Cart"
   - As a shopper, I want to add products to my cart so I can purchase multiple items together
   - AC: Given I'm on product page, When I click "Add to Cart", Then product added, cart count updates, see confirmation
   - Priority: Must Have
   - Points: 3
   - Dependencies: Product catalog

2. "Update Cart Quantity"
   - As a budget shopper, I want to change item quantities so I can manage my spending
   - AC: Given items in cart, When I change quantity, Then total updates, inventory checked, can't exceed stock
   - Priority: Must Have
   - Points: 2

Generate 10 stories covering: add, remove, update, view cart, proceed to checkout, save for later, apply coupons, mobile optimization, guest checkout, cart persistence.
```

---

### 3. Generate Acceptance Criteria

**Purpose:** Create detailed acceptance criteria for features.

**Prompt:**
```
Generate acceptance criteria for [FEATURE/USER_STORY]:

Feature description:
[DESCRIPTION]

Create acceptance criteria that cover:
- Happy path (successful scenarios)
- Alternative paths (different valid flows)
- Error cases (what happens when things go wrong)
- Edge cases (boundaries, extremes)
- Non-functional aspects (performance, accessibility)
- Integration points
- Data validation rules

Use [GIVEN_WHEN_THEN / CHECKLIST] format.
Make criteria specific, measurable, and testable.
```

**Example:**
```
Generate acceptance criteria for User Login feature:

Feature: Users can log in with email and password to access their account

Criteria covering:
- Happy path: Valid credentials, successful login
- Alternative: Remember me option, password reset flow
- Errors: Invalid email, wrong password, account locked, network error
- Edge cases: Empty fields, SQL injection attempts, very long inputs
- Non-functional: <2 second response time, WCAG AA accessible
- Integration: OAuth providers (Google, GitHub), SSO for enterprise

Format as Given/When/Then:

1. Successful Login
   - Given valid registered email and correct password
   - When user submits login form
   - Then redirect to dashboard, session created, "remember me" respected

2. Invalid Credentials
   - Given registered email and incorrect password
   - When user submits login form
   - Then show "Invalid credentials" error, don't reveal if email exists, log attempt

3. Account Lockout
   - Given 5 failed login attempts in 15 minutes
   - When user tries to login again
   - Then account locked for 30 minutes, show lockout message, send email notification

[Continue with 10+ criteria covering all scenarios]
Make each criterion independently testable.
```

---

## Market Research

### 4. Competitive Analysis

**Purpose:** Analyze competitors and market positioning.

**Prompt:**
```
Conduct competitive analysis for [PRODUCT/FEATURE]:

Context:
- Our product: [DESCRIPTION]
- Target market: [MARKET_SEGMENT]
- Key competitors: [COMPETITOR_LIST]

Analyze:
- Competitor features (comparison matrix)
- Pricing strategies
- Strengths and weaknesses
- Market positioning
- User experience highlights
- Technology stack (if known)
- Marketing approach
- Customer reviews and pain points
- Market share / traction
- Opportunities for differentiation

Provide:
- Feature comparison table
- Strategic recommendations
- Gap analysis (what we should build)
```

**Example:**
```
Competitive analysis for our AI-powered email assistant:

Context:
- Our product: AI email drafting and scheduling tool
- Market: Small business owners, sales professionals
- Competitors: Superhuman, Hey, Spark, Gmail with AI

Analyze:
- Features: All have AI drafting, we add tone adjustment and scheduling
- Pricing: Superhuman $30/mo, Hey $99/yr, Spark free/premium, Gmail free
- Strengths: Superhuman (speed), Hey (workflow), Spark (collab)
- Weaknesses: Superhuman (price), Hey (learning curve), Spark (feature bloat)
- Positioning: Superhuman (premium speed), Hey (email rebel), Spark (team email)
- UX: Superhuman keyboard-first, Hey opinionated, Spark feature-rich
- Tech: Most use Gmail API, AI models vary
- Marketing: Superhuman (referral/exclusivity), Hey (thought leadership)
- Reviews: Users want better mobile, faster AI, affordable pricing
- Share: Superhuman growing in tech, Gmail dominant
- Opportunities: Affordable AI email for SMBs, superior mobile experience, integrations

Comparison table: [Features × Competitors]
Recommendations: Price at $15/mo, focus on mobile, emphasize tone control
Gaps: No competitor has strong mobile + affordable + AI tone control
```

---

### 5. Feature Prioritization

**Purpose:** Prioritize features using frameworks.

**Prompt:**
```
Prioritize these features using [RICE/MoSCoW/VALUE_VS_EFFORT]:

Features:
[FEATURE_LIST]

Context:
- Business goals: [OBJECTIVES]
- Resources: [TEAM_SIZE and TIMELINE]
- User feedback: [KEY_REQUESTS]
- Technical constraints: [LIMITATIONS]

For each feature score/categorize:
- [RICE: Reach, Impact, Confidence, Effort]
- [MoSCoW: Must/Should/Could/Won't]
- [Value vs Effort: High/Medium/Low for each]

Provide:
- Prioritized feature list with rationale
- Quick wins vs long-term investments
- Recommended roadmap order
- Dependencies to consider
```

**Example:**
```
Prioritize features using RICE for project management tool:

Features:
1. Gantt chart view
2. Mobile app
3. Time tracking
4. Advanced reporting
5. Slack integration
6. Custom fields
7. Guest access
8. API access
9. Dark mode
10. Email reminders

Context:
- Goals: Increase user engagement, reduce churn, expand to larger teams
- Resources: 5 engineers, 3-month timeline
- Feedback: Top requests: mobile app, Slack, time tracking
- Constraints: Mobile requires native developers

RICE Scores (Reach × Impact × Confidence / Effort):
1. Email reminders: 8000 × 2 × 90% / 1 = 14,400 (HIGH)
2. Slack integration: 5000 × 3 × 80% / 2 = 6,000 (HIGH)
3. Mobile app: 6000 × 3 × 70% / 8 = 1,575 (MEDIUM)
4. Guest access: 4000 × 2 × 90% / 3 = 2,400 (MEDIUM)
5. Time tracking: 3000 × 2 × 80% / 4 = 1,200 (MEDIUM)
[Continue for all features]

Prioritized: Email reminders, Slack, Guest access, Time tracking, Mobile app
Quick wins: Email reminders (1 week), Dark mode (3 days)
Long-term: Mobile app (2 months), API (1.5 months)
Roadmap: Phase 1 (month 1): Reminders, Slack, Dark mode
         Phase 2 (month 2): Guest access, Time tracking
         Phase 3 (month 3): Start mobile app
```

---

## Marketing Content

### 6. Generate Product Description

**Purpose:** Create compelling product descriptions.

**Prompt:**
```
Write a product description for [PRODUCT]:

Product details:
- What it is: [TYPE]
- Target audience: [USERS]
- Key benefits: [VALUE_PROPOSITIONS]
- Unique features: [DIFFERENTIATORS]
- Use cases: [SCENARIOS]

Create:
- Short description (1-2 sentences for listings)
- Medium description (paragraph for product page)
- Long description (multiple paragraphs with features, benefits, use cases)
- Key feature bullets (5-7 items)
- Call to action

Tone: [PROFESSIONAL/CASUAL/TECHNICAL/PLAYFUL]
Focus on benefits, not just features.
```

**Example:**
```
Product description for AI-powered code review tool:

Product:
- What: Automated code review and quality analysis tool
- Audience: Development teams, CTOs, tech leads
- Benefits: Catch bugs early, improve code quality, save review time
- Unique: AI learns from team's style, integrates with workflow
- Use cases: PR reviews, legacy code audits, onboarding

Short: "AI-powered code review that learns your team's standards and catches bugs before production."

Medium: "CodeGuard uses advanced AI to review your pull requests, catching bugs, security issues, and style inconsistencies before they reach production. Unlike generic linters, CodeGuard learns from your team's past reviews and enforces your specific standards. Integrates seamlessly with GitHub, GitLab, and Bitbucket to provide instant feedback on every commit."

Long: [3 paragraphs covering: problem it solves, how it works, why it's better than alternatives]

Features:
- AI learns your team's coding standards over time
- Catches bugs, security vulnerabilities, and performance issues
- Integrates with GitHub, GitLab, Bitbucket
- Provides fix suggestions, not just error messages
- 10-minute setup, works with any language
- Reduces code review time by 40%
- Enterprise-grade security and compliance

CTA: "Start your free 14-day trial - no credit card required"

Tone: Professional but approachable, technical audience
Focus on time savings and quality improvements, not just features.
```

---

### 7. Landing Page Copy

**Purpose:** Write conversion-focused landing page content.

**Prompt:**
```
Write landing page copy for [PRODUCT/FEATURE]:

Page structure:
- Hero section (headline, subheadline, CTA)
- Problem statement
- Solution overview
- Key features (3-5 with descriptions)
- Social proof (testimonials, logos, stats)
- How it works (3-4 steps)
- Pricing tease
- FAQ section (5-7 questions)
- Final CTA

Product details:
[PRODUCT_INFO]

Target: [AUDIENCE]
Goal: [SIGNUPS/DEMOS/PURCHASES]
Tone: [STYLE]

Focus on clarity, benefits, and conversion.
```

**Example:**
```
Landing page for team collaboration tool:

Product: Real-time workspace for distributed teams with docs, tasks, and video

Structure:

Hero:
- Headline: "Where distributed teams come together"
- Subheadline: "All your team's work in one place. Documents, tasks, and video calls that actually work together."
- CTA: "Start free trial" + "Watch demo"

Problem: "Scattered across Slack, Google Docs, Zoom, Asana? Your team is too."

Solution: "TeamSpace brings everything together. Edit docs while on video. Turn messages into tasks. Never lose context switching between tools."

Features:
1. Real-time collaboration: "Edit documents together, see who's viewing what, and get instant feedback."
2. Integrated video: "Start a call from any document. No switching apps, no lost context."
3. Connected tasks: "Turn any discussion into a task. Track progress without leaving your workflow."

Social Proof: "Trusted by 10,000+ teams at Stripe, Notion, and Figma" + testimonials

How it works:
1. "Create a workspace in 60 seconds"
2. "Invite your team and start collaborating"
3. "Build your workflow with docs, tasks, and video"

Pricing: "Free for small teams. From $10/user for growing teams."

FAQ: "How is this different from Slack?", "Can I import from Google Docs?", etc.

CTA: "Start collaborating today - free for 14 days"

Tone: Friendly, professional, benefit-focused
Emphasize "together", "seamless", "no more switching"
```

---

### 8. Email Campaign Copy

**Purpose:** Write email marketing campaigns.

**Prompt:**
```
Write an email campaign for [CAMPAIGN_PURPOSE]:

Campaign details:
- Goal: [CONVERSION_GOAL]
- Audience: [SEGMENT]
- Sequence: [SINGLE/SERIES]
- Tone: [STYLE]

For each email provide:
- Subject line (with 2-3 alternatives)
- Preview text
- Email body
  - Opening hook
  - Value proposition
  - Social proof (optional)
  - Clear CTA
  - P.S. line
- Mobile optimization notes

Email types: [WELCOME/ONBOARDING/FEATURE_ANNOUNCEMENT/RE_ENGAGEMENT/PROMOTIONAL]

Keep concise, scannable, action-oriented.
```

**Example:**
```
Email campaign: Feature announcement for new analytics dashboard

Campaign:
- Goal: Drive feature adoption, 30% of users try dashboard in 7 days
- Audience: Existing customers, active users
- Sequence: 3-email series
- Tone: Excited but professional

Email 1 (Announcement):
Subject: "Your new analytics dashboard is here ✨" / "See what's working (and what's not)" / "Data you can actually use"
Preview: "Get insights that drive action, not just pretty charts"

Body:
Hook: "Remember when you asked for better analytics? We listened."

Value: "Your new dashboard shows exactly what matters: top-performing content, user trends, and actionable recommendations. No more exporting to spreadsheets or guessing what works."

Features (3 bullets): Real-time updates, custom reports, AI insights

CTA: "Explore your dashboard →"

P.S.: "We're hosting a live walkthrough Tuesday at 2pm PT. Save your spot."

Mobile: Short paragraphs, big CTA button, works without images

[Email 2: Tutorial tips, Email 3: Case study/social proof]

Test subject lines for open rate, keep body under 200 words.
```

---

## Business Strategy

### 9. Go-to-Market Strategy

**Purpose:** Plan product or feature launch strategy.

**Prompt:**
```
Create a go-to-market strategy for [PRODUCT/FEATURE]:

Product:
- Description: [WHAT_IT_IS]
- Target market: [SEGMENTS]
- Positioning: [UNIQUE_VALUE]
- Competition: [KEY_COMPETITORS]

GTM Strategy components:
- Market analysis and sizing
- Target customer profiles
- Value proposition and messaging
- Pricing strategy
- Distribution channels
- Marketing channels and tactics
- Sales strategy
- Launch timeline and phases
- Success metrics and goals
- Budget allocation
- Risk mitigation

Provide actionable plan for first 90 days.
```

**Example:**
```
GTM strategy for AI code completion tool for enterprise:

Product:
- AI-powered code completion trained on company's codebase
- Target: Enterprise development teams (500+ developers)
- Positioning: "GitHub Copilot for your private codebase"
- Competition: Copilot, Tabnine, Codeium

Strategy:

Market: $5B TAM, 50k companies with 500+ devs, 10% addressable ($500M)

Customer profiles:
1. Fortune 500 tech companies (high security needs)
2. Financial services (compliance requirements)
3. Healthcare tech (HIPAA compliance)

Value prop: "40% faster coding with AI that understands YOUR code, not just public GitHub"

Pricing: $50/developer/month, minimum 500 seats ($25k/mo)

Distribution: Direct sales, no self-serve initially

Marketing:
- Content: Security whitepapers, ROI calculators
- Events: KubeCon, AWS re:Invent sponsorships
- Partnerships: IDE vendors, GitHub Enterprise
- Demand gen: LinkedIn ads to CTOs/VPs Engineering

Sales: Enterprise sales team, 3-month sales cycle, POC required

Timeline:
- Month 1: Private beta with 3 design partners
- Month 2: Case studies, sales enablement, soft launch
- Month 3: Public launch, paid campaigns, conference presence

Metrics: 10 enterprise customers, $3M ARR, 30% close rate on POCs

Budget: $500k (50% sales/BD, 30% marketing, 20% partnerships)

Risks: Security concerns (mitigation: SOC 2, on-prem option), slow enterprise sales (offer POC fast-track)
```

---

### 10. Business Case / ROI Analysis

**Purpose:** Build business case for a project or feature.

**Prompt:**
```
Create a business case for [PROJECT]:

Project overview:
- Description: [WHAT_IT_IS]
- Problem it solves: [PAIN_POINTS]
- Proposed solution: [APPROACH]

Business case components:
- Executive summary
- Current situation and problem
- Proposed solution
- Benefits (quantitative and qualitative)
- Cost analysis (development, operations, maintenance)
- ROI calculation
- Risk analysis
- Timeline
- Alternatives considered
- Recommendation
- Success criteria

Use financial metrics: [NPV/IRR/PAYBACK_PERIOD/ROI]
Include assumptions and sensitivity analysis.
```

**Example:**
```
Business case for migrating to microservices architecture:

Overview:
- What: Migrate monolithic app to microservices
- Problem: Slow releases, scaling bottlenecks, developer productivity issues
- Solution: Decompose into 8 microservices, containerized, Kubernetes

Executive Summary:
Migrating to microservices will cost $500k over 6 months but deliver $1.2M in annual benefits through faster time-to-market, reduced infrastructure costs, and improved developer productivity. ROI: 140% in year 1, break-even in 5 months.

Current State:
- 4-week release cycles (too slow for competitive market)
- 99.5% uptime (below 99.9% SLA commitment)
- $50k/month infrastructure costs (over-provisioned for peak)
- 20 developers blocked by monolith architecture

Benefits:
Quantitative:
- Faster releases: 4 weeks → 1 week (3x faster time-to-market, ~$400k value)
- Infrastructure: $50k → $35k/month ($180k annual savings)
- Downtime reduction: 99.5% → 99.95% ($100k prevented losses)
- Developer productivity: 20% improvement ($500k value based on 20 devs × $150k)

Qualitative: Better developer morale, easier to hire, modern tech stack

Costs:
- Development: $300k (6 engineers × 6 months × $20k burdened)
- Infrastructure: $100k (Kubernetes, monitoring, new tools)
- Training: $50k
- Risk buffer: $50k
Total: $500k

ROI: ($1.2M annual benefit - $500k investment) / $500k = 140% first year
Payback: 5 months
NPV (3 years, 10% discount): $2.1M

Risks: Migration complexity (8/10), business disruption (6/10), talent needs (7/10)
Mitigation: Strangler fig pattern, parallel running, external contractors

Alternatives:
1. Stay with monolith: $0 cost, but losing competitive edge, estimated $2M revenue at risk
2. Rewrite from scratch: $1M, 12 months, high risk
3. Hybrid approach: Keep core monolith, extract services gradually ($300k, 9 months)

Recommendation: Full microservices migration with strangler pattern
Success criteria: 1-week releases, 99.95% uptime, $35k infra costs, <10% regression bugs
```

---

### 11. Customer Journey Mapping

**Purpose:** Map customer journey and identify opportunities.

**Prompt:**
```
Create a customer journey map for [USER_PERSONA]:

Persona:
- Name/role: [PERSONA_NAME]
- Goals: [OBJECTIVES]
- Pain points: [CHALLENGES]
- Context: [USAGE_SCENARIO]

Journey stages:
1. [AWARENESS/DISCOVERY]
2. [CONSIDERATION/EVALUATION]
3. [PURCHASE/SIGNUP]
4. [ONBOARDING/FIRST_USE]
5. [ACTIVE_USE/ENGAGEMENT]
6. [RENEWAL/ADVOCACY]

For each stage document:
- User goals and tasks
- Touchpoints (where they interact)
- Thoughts and feelings (emotional state)
- Pain points and frustrations
- Opportunities for improvement
- Key metrics

Identify moments of truth and improvement priorities.
```

**Example:**
```
Customer journey for Sarah, Marketing Manager at 50-person startup:

Persona:
- Sarah, Marketing Manager, 30s, tech-savvy
- Goals: Find better email marketing tool, improve campaign ROI
- Pain points: Current tool expensive, limited automation, poor analytics
- Context: Evaluated Mailchimp, looking for alternatives

Stages:

1. Awareness (Week 0)
   - Goals: Find alternatives to Mailchimp
   - Touchpoints: Google search, G2 reviews, colleague recommendation
   - Feelings: Frustrated with current tool, hopeful about alternatives
   - Pain: Too many options, unclear differentiation
   - Opportunity: Better comparison content, clear pricing
   - Metrics: Website visits, time on pricing page

2. Evaluation (Week 1-2)
   - Goals: Compare features, test ease of use, check pricing
   - Touchpoints: Free trial signup, help docs, demo video, support chat
   - Feelings: Excited about features, concerned about migration
   - Pain: Learning curve, data migration complexity
   - Opportunity: Guided trial, migration assistance, comparison charts
   - Metrics: Trial activation, features tested, support interactions

3. Purchase (Week 3)
   - Goals: Get approval, negotiate pricing, finalize decision
   - Touchpoints: Talk to sales, check reviews, get quotes
   - Feelings: Confident but needs validation, worried about commitment
   - Pain: Budget approval process, contract terms
   - Opportunity: ROI calculator, customer references, flexible terms
   - Metrics: Conversion rate, time to close, discount requests

4. Onboarding (Month 1)
   - Goals: Migrate lists, create first campaign, train team
   - Touchpoints: Onboarding checklist, tutorials, CSM kickoff call
   - Feelings: Overwhelmed with setup, excited to start
   - Pain: Data migration issues, feature parity gaps
   - Opportunity: Personalized onboarding, migration tools, quick wins
   - Metrics: Time to first campaign, activation rate, support tickets

5. Active Use (Months 2-12)
   - Goals: Run campaigns, analyze results, optimize performance
   - Touchpoints: Daily app use, monthly reviews, feature updates
   - Feelings: Satisfied with results, occasionally frustrated
   - Pain: Advanced features hard to find, reporting gaps
   - Opportunity: Proactive tips, advanced training, feature discovery
   - Metrics: Campaigns sent, engagement rates, feature adoption, NPS

6. Renewal (Month 11+)
   - Goals: Evaluate ROI, consider alternatives, renew or switch
   - Touchpoints: Renewal email, account review, competitor outreach
   - Feelings: Evaluating value, open to staying if improvements made
   - Pain: Remembering benefits, comparing to new options
   - Opportunity: Show ROI, introduce new features, long-term discount
   - Metrics: Renewal rate, expansion revenue, churn reasons

Moments of truth:
- First campaign sent (make it easy and successful)
- Data migration (reduce friction and errors)
- Month 3 check-in (prove ROI before renewal consideration)

Priority improvements:
1. Streamline onboarding with personalized checklist and migration tools
2. Better in-app feature discovery and tips
3. Proactive account reviews showing ROI
```

---

## Analytics & Metrics

### 12. Define KPIs and Metrics

**Purpose:** Establish metrics framework for feature or product.

**Prompt:**
```
Define KPIs and metrics for [FEATURE/PRODUCT]:

Context:
- Product/feature: [DESCRIPTION]
- Business goals: [OBJECTIVES]
- User goals: [USER_OUTCOMES]
- Stage: [LAUNCH/GROWTH/MATURITY]

Create metrics framework:
- North Star Metric (single most important metric)
- Primary KPIs (3-5 key metrics)
- Secondary metrics (supporting indicators)
- Counter metrics (ensure quality)
- Input metrics (leading indicators)
- Health metrics (system health)

For each metric specify:
- Definition and calculation
- Target/goal
- Measurement frequency
- Owner
- Data source
- Why it matters

Align metrics with business goals and user value.
```

**Example:**
```
KPIs for new social sharing feature in design tool:

Context:
- Feature: Public gallery where users share designs for feedback
- Business goal: Increase viral growth, improve engagement
- User goal: Get design feedback, find inspiration, grow following
- Stage: New feature launch

Metrics:

North Star: Weekly Active Sharers (users who share at least 1 design/week)
- Why: Balances growth and engagement, indicates feature value
- Target: 10% of active users in month 3
- Frequency: Weekly
- Owner: Product Manager
- Source: Event tracking

Primary KPIs:
1. Share rate: % of users who share designs
   - Target: 25% within 3 months
   - Shows feature discovery and adoption

2. Engagement rate: Views, likes, comments per shared design
   - Target: Average 50 views, 5 likes, 2 comments per design
   - Indicates network effects and value

3. Viral coefficient: New users from shared designs / Sharers
   - Target: 0.3 (each sharer brings 0.3 new users)
   - Measures growth impact

4. Retention lift: Do sharers retain better?
   - Target: 15% improvement in 30-day retention
   - Validates feature value

Secondary:
- Gallery views per user (engagement)
- Follow/follower growth (network building)
- Reshare rate (content quality)
- Time to first share (onboarding friction)

Counter metrics:
- Low-quality share rate (spam prevention)
- Copyright reports (content quality)
- Share→unshare rate (user regret)

Input metrics (leading):
- Share button click rate
- Gallery landing page visits
- Feature awareness (% who know it exists)

Health:
- Share upload success rate
- Gallery page load time
- Moderation queue time

Dashboard: Real-time for engagement, daily for growth, weekly for retention
Review: Weekly growth review, monthly OKR check-in
```

---

### 13. A/B Test Plan

**Purpose:** Design A/B test for a feature or change.

**Prompt:**
```
Create A/B test plan for [FEATURE/CHANGE]:

Hypothesis:
- Change: [WHAT_YOU'RE_CHANGING]
- Expected impact: [PREDICTION]
- Rationale: [WHY_YOU_THINK_THIS]

Test design:
- Primary metric: [KEY_METRIC]
- Secondary metrics: [SUPPORTING_METRICS]
- Success criteria: [MINIMUM_DETECTABLE_EFFECT]
- Sample size calculation: [USERS_NEEDED]
- Test duration: [DAYS/WEEKS]
- Traffic allocation: [CONTROL_VS_VARIANT_%]
- Segmentation: [ANY_SEGMENTS]
- Exclusions: [WHO_NOT_TO_INCLUDE]

Include:
- Detailed variant descriptions
- Potential risks and guardrails
- Analysis plan
- Decision framework (ship/iterate/kill)

Ensure statistical rigor and practical significance.
```

**Example:**
```
A/B test plan: Redesigned pricing page to increase conversions

Hypothesis:
- Change: Simplify pricing page from 4 plans to 3, add annual discount badge
- Impact: 15% increase in paid conversions
- Rationale: User research shows confusion with middle-tier options, annual discount not prominent

Test Design:

Variants:
- Control: Current 4-plan page (Starter/Pro/Business/Enterprise)
- Variant: 3 plans (Starter/Pro/Enterprise), annual savings badge, simplified feature comparison

Primary metric: Paid conversion rate (trial → paid)
- Current: 18%
- Target: 20.7% (15% relative increase)
- MDE: 2% absolute (11% relative) for 80% power

Secondary:
- Plan selection distribution (which plans chosen)
- Annual vs monthly split
- Time on pricing page
- Scroll depth

Success criteria:
- Primary increase by ≥2% with p<0.05
- No decrease in average revenue per customer (ARPC)
- Qualitative: No significant confusion in support tickets

Sample size: 4,860 trial signups per variant (9,720 total)
- Calculation: α=0.05, β=0.20, baseline=18%, MDE=2%

Duration: 3 weeks (estimated based on 450 trials/day)

Traffic: 50/50 split, new trial users only

Segmentation: Analyze separately for SMB vs Enterprise traffic

Exclusions: Users who already visited pricing page, returning users, employees

Risks & guardrails:
- Risk: Removing plan might hurt enterprise customers
- Guardrail: If enterprise conversions drop >5%, stop test
- Risk: Support ticket increase
- Guardrail: Monitor support volume daily

Analysis:
- Daily: Check for anomalies, ensure even split
- Weekly: Interim peek (won't act on it, just monitoring)
- End: Sequential testing or fixed-horizon analysis

Decision framework:
- Ship if: Primary ↑ ≥2%, no secondary degradation, positive qual feedback
- Iterate if: Directionally positive but not significant, or mixed signals
- Kill if: Primary ↔ or ↓, or secondary metrics degraded significantly

Post-test: If shipping, monitor for 2 weeks for novelty effects
```

---

## User Research

### 14. User Research Plan

**Purpose:** Plan user research study.

**Prompt:**
```
Create a user research plan for [RESEARCH_GOAL]:

Research context:
- Goal: [WHAT_YOU_WANT_TO_LEARN]
- Research questions: [SPECIFIC_QUESTIONS]
- Stage: [DISCOVERY/VALIDATION/EVALUATION]
- Timeline: [DURATION]

Plan components:
- Research objectives (3-5 key questions)
- Methodology: [INTERVIEWS/SURVEYS/USABILITY_TESTS/ETC]
- Participant criteria (who to recruit)
- Sample size and rationale
- Screener questions
- Research protocol/script
- Data collection method
- Analysis approach
- Deliverables
- Resources needed

Ensure research is actionable and unbiased.
```

**Example:**
```
User research plan: Understanding why users abandon checkout

Research Context:
- Goal: Identify friction points in checkout flow causing 70% cart abandonment
- Questions: What causes abandonment? Which steps? Why? How to fix?
- Stage: Problem validation before redesign
- Timeline: 3 weeks (recruit, conduct, analyze)

Objectives:
1. Identify main friction points in current checkout flow
2. Understand user expectations and mental models for checkout
3. Discover which checkout step has highest drop-off
4. Validate hypotheses about payment and shipping form issues
5. Prioritize improvements by impact

Methodology:
- Usability testing (moderated, remote, 60 min sessions)
- Screen recording with think-aloud protocol
- Post-task questionnaire (SUS score)
- 15-min follow-up interview
- Analytics review (funnel analysis)

Participants:
- 12-15 recent cart abandoners (last 7 days)
- Mix: 60% mobile, 40% desktop (matches traffic)
- 50% new users, 50% returning
- Diverse: Age, tech-savviness, product types
- Exclude: Employees, researchers' connections

Screener:
1. "Have you shopped online in last 30 days?" (Yes required)
2. "Added items to cart but didn't complete purchase?" (Yes required)
3. "Device used?" (Mix mobile/desktop)
4. "Reason for not completing?" (Open-ended, screener question)

Protocol:
1. Intro and consent (5 min)
2. Background questions (5 min)
3. Task: "Shop for [product] and complete checkout" (25 min)
4. Observe friction points, ask "what are you thinking?"
5. Post-task: SUS questionnaire (5 min)
6. Debrief interview about pain points (15 min)
7. Thank and incentivize ($75 gift card)

Data Collection:
- Zoom recordings (video, screen, transcript)
- Observer notes in shared doc
- Task completion rate, time, error count
- SUS scores
- Quotes and observations

Analysis:
- Affinity mapping of pain points
- Severity rating (high/med/low) by frequency and impact
- Journey map with friction points
- Synthesize into top 5 insights

Deliverables:
- Research summary (2-page executive brief)
- Detailed findings deck (20 slides)
- Video highlights reel (3 min)
- Prioritized recommendations

Resources:
- Researcher (1 week full-time)
- Note-taker for sessions
- $1,125 for participant incentives (15 × $75)
- UserTesting.com or Zoom
- Miro for affinity mapping

Timeline:
- Week 1: Recruit, finalize protocol
- Week 2: Conduct 12-15 sessions
- Week 3: Analysis and report
```

---

### 15. Customer Interview Script

**Purpose:** Create script for customer discovery interviews.

**Prompt:**
```
Create a customer interview script for [INTERVIEW_PURPOSE]:

Interview goal:
[WHAT_YOU_WANT_TO_LEARN]

Interview details:
- Duration: [MINUTES]
- Interviewee type: [PERSONA/ROLE]
- Stage: [DISCOVERY/VALIDATION]
- Method: [IN_PERSON/VIDEO/PHONE]

Script sections:
- Opening and rapport building (5 min)
- Background and context questions (10 min)
- Problem/solution exploration (20-30 min)
- Feature/concept reaction (if applicable)
- Wrap-up and next steps (5 min)

For each question provide:
- Question text
- Why you're asking (researcher note)
- Follow-up probes
- What to listen for

Use open-ended questions, avoid leading questions.
```

**Example:**
```
Customer interview script: Discovering pain points in expense reporting (B2B SaaS)

Goal: Understand current process, pain points, and willingness to pay for solution

Duration: 45 minutes
Interviewee: Finance managers at 50-500 person companies
Stage: Problem discovery
Method: Video call (Zoom)

Script:

Opening (5 min)
"Thanks for joining! I'm researching how companies handle expense reporting. I'd love to learn about your process. There are no right or wrong answers—I just want to understand your experience. We're recording for note-taking; is that okay?"

[Why: Build trust, set expectations, get consent]

Background (10 min)
1. "Tell me about your role and how expense management fits in."
   - Follow-up: "How many employees submit expenses? How often?"
   - Listen for: Team size, volume, frequency, their involvement level

2. "Walk me through what happens when an employee submits an expense."
   - Follow-up: "What tools do you use? Who's involved?"
   - Listen for: Current process, tools, people, steps

3. "How much time does your team spend on expense management weekly?"
   - Follow-up: "Is that more than you'd like? What would ideal be?"
   - Listen for: Time burden, pain intensity

[Why: Understand context before diving into problems]

Problem Exploration (25 min)
4. "What's frustrating about the current process?" [OPEN-ENDED]
   - Don't ask: "Is it slow?" (leading)
   - Follow-up: "Tell me about the last time that happened."
   - Follow-up: "How often does that occur?"
   - Listen for: Specific pain points, frequency, emotion

5. "You mentioned [pain point]—how do you handle that today?"
   - Follow-up: "What have you tried? Why didn't it work?"
   - Listen for: Workarounds, failed solutions, budget for fixes

6. "If you had a magic wand, how would expense reporting work?"
   - Follow-up: "What's most important to you: speed, accuracy, compliance, or something else?"
   - Listen for: Priorities, ideal state, features they'd value

7. "Have you looked for solutions? What did you find?"
   - Follow-up: "What stopped you from buying?"
   - Listen for: Competitive intel, buying barriers, price sensitivity

8. "What would make this problem worth solving with a paid tool?"
   - Follow-up: "How much time/money would you need to save?"
   - Listen for: Value drivers, willingness to pay, ROI expectations

[Why: Deep dive on problems without pitching solution]

Concept Reaction (5 min, optional)
[Show mockup/concept if ready]
9. "We're exploring a tool that does [X]. What's your initial reaction?"
   - Follow-up: "What would make you try it? What concerns do you have?"
   - Listen for: Interest level, objections, must-have features

[Why: Gauge interest without selling]

Wrap-up (5 min)
10. "What did I not ask that I should have?"
    - Listen for: Missed angles, other stakeholders

11. "Can I follow up as we build this? Would you be interested in trying an early version?"
    - Listen for: Engagement level, design partner potential

12. "Know anyone else I should talk to?"
    - Listen for: Referrals

"Thank you so much! This was incredibly helpful. I'll send a $50 gift card as a thanks."

Researcher Notes:
- Ask follow-ups, don't stick rigidly to script
- Pause and give them time to think
- Listen more than talk (80/20 rule)
- Note emotional reactions, not just words
- If they pitch you, redirect: "That's interesting, but first tell me about..."
- Avoid confirmation bias: Don't lead them to your hypothesis
```

---

## Additional Resources

- **Related:** See [prompt-engineering-guide.md](./prompt-engineering-guide.md) for crafting effective business prompts
- **Product:** See [ui-ux-prompts.md](./ui-ux-prompts.md) for design and UX considerations
- **Technical:** See [architecture-prompts.md](./architecture-prompts.md) for technical planning
