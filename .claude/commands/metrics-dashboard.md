# KPIs & Analytics Tracking Plan

Define comprehensive KPIs and create an analytics tracking implementation plan for the product or business specified by the user.

## Instructions

Create a complete metrics and analytics strategy including:

### 1. Analytics Strategy Overview
- Business objectives
- Key questions to answer with data
- Target audience and stakeholders
- Current analytics maturity
- Analytics tools in use
- Reporting frequency and format

### 2. North Star Metric

Define the single most important metric:
- North Star Metric selection and rationale
- Why this metric matters to the business
- How it connects to business value
- Leading indicators for the North Star
- Target benchmarks
- Historical trends (if available)

### 3. Framework Selection

Choose appropriate metrics framework:
- **AARRR (Pirate Metrics):** Acquisition, Activation, Retention, Revenue, Referral
- **HEART Framework:** Happiness, Engagement, Adoption, Retention, Task Success
- **Dave McClure's Startup Metrics:** Customer acquisition, activation, retention, revenue, referral
- Custom framework for your business model

### 4. Key Performance Indicators (KPIs) by Category

#### Acquisition Metrics:
- Website visitors (unique, total, by source)
- Traffic sources breakdown (organic, direct, referral, social, paid)
- Top landing pages
- New vs. returning visitors
- Sign-ups / registrations
- Lead generation (by channel)
- Cost per acquisition (CPA) by channel
- Customer acquisition cost (CAC)
- Lead conversion rate
- Marketing qualified leads (MQLs)
- Sales qualified leads (SQLs)

#### Activation Metrics:
- Time to first value
- Onboarding completion rate
- Steps completed in onboarding
- "Aha moment" achievement rate
- Feature adoption rate (key features)
- Profile completion rate
- Setup completion rate
- First action completion rate
- Day 1, 3, 7 activation rates

#### Engagement Metrics:
- Daily Active Users (DAU)
- Weekly Active Users (WAU)
- Monthly Active Users (MAU)
- DAU/MAU ratio (stickiness)
- Session frequency
- Session duration
- Pages per session
- Feature usage frequency
- Time spent in product
- User actions per session
- Depth of engagement score

#### Retention Metrics:
- Day 1, 7, 30, 90 retention rates
- Cohort retention analysis
- Churn rate (customer churn, revenue churn)
- Monthly/Annual recurring revenue retained
- Customer lifetime (average)
- Resurrection rate (returned churned users)
- Net Revenue Retention (NRR)
- Gross Revenue Retention (GRR)

#### Revenue Metrics:
- Monthly Recurring Revenue (MRR)
- Annual Recurring Revenue (ARR)
- Revenue growth rate
- Average Revenue Per User (ARPU)
- Customer Lifetime Value (CLV or LTV)
- LTV:CAC ratio
- Payback period
- Average contract value (ACV)
- Total Contract Value (TCV)
- Expansion revenue
- Contraction revenue
- Revenue by segment
- Revenue by plan/tier

#### Referral Metrics:
- Referral rate
- Viral coefficient (K-factor)
- Invites sent per user
- Invite acceptance rate
- Time to referral
- Referral source tracking
- Net Promoter Score (NPS)
- Word-of-mouth attribution

#### Customer Satisfaction Metrics:
- Net Promoter Score (NPS)
- Customer Satisfaction Score (CSAT)
- Customer Effort Score (CES)
- Product-Market Fit Score
- Support ticket volume
- Average resolution time
- First response time
- Customer health score

#### Product Performance Metrics:
- Page load time
- Time to interactive
- Error rates
- API response times
- Uptime percentage
- Bug count and severity
- Feature request volume
- Technical debt metrics

#### Sales Metrics (if applicable):
- Sales pipeline value
- Sales cycle length
- Win rate
- Average deal size
- Sales quota attainment
- Lead-to-opportunity conversion
- Opportunity-to-close conversion
- Sales velocity

#### Marketing Metrics:
- Marketing Qualified Leads (MQLs)
- Lead-to-customer conversion rate
- Cost per lead (CPL)
- Return on Ad Spend (ROAS)
- Marketing ROI
- Brand awareness metrics
- Share of voice
- Content engagement
- Email open rates
- Email click-through rates
- Social media engagement
- Organic search rankings

### 5. Metrics Dashboard Design

#### Executive Dashboard (for leadership):
- North Star Metric
- Revenue metrics (MRR, ARR, growth rate)
- Customer metrics (new customers, churn, NRR)
- Unit economics (CAC, LTV, LTV:CAC)
- Cash and runway
- Team headcount
- Update frequency: Weekly/Monthly

#### Product Dashboard:
- Active users (DAU, WAU, MAU)
- Activation rate
- Retention cohorts
- Feature adoption
- User engagement scores
- Product-market fit score
- Update frequency: Daily/Weekly

#### Marketing Dashboard:
- Traffic sources and volume
- Lead generation by channel
- Conversion rates by channel
- CAC by channel
- Campaign performance
- Content performance
- SEO rankings
- Update frequency: Daily/Weekly

#### Sales Dashboard:
- Pipeline value
- Sales velocity
- Win rate
- Average deal size
- Sales cycle length
- Quota attainment
- Top performing reps
- Update frequency: Daily/Weekly

#### Customer Success Dashboard:
- Customer health scores
- Onboarding progress
- Support ticket metrics
- NPS trends
- Churn risk accounts
- Expansion opportunities
- Update frequency: Weekly

### 6. Event Tracking Plan

#### Core Events to Track:
- User signed up
- User logged in
- Profile completed
- Feature X used
- Content created
- Content shared
- Invite sent
- Payment initiated
- Purchase completed
- Subscription started
- Subscription upgraded
- Subscription canceled
- Support ticket created
- Feature requested

For each event, specify:
- Event name
- When it fires
- User properties to track
- Event properties to track
- Expected frequency
- Why it matters

### 7. User Properties to Track

#### Identity Properties:
- User ID (unique identifier)
- Email
- Name
- Sign-up date
- Sign-up source

#### Demographic Properties:
- Company/organization
- Industry
- Company size
- Role/job title
- Location (country, city)

#### Behavioral Properties:
- Last login date
- Total sessions
- Total time spent
- Features used (list)
- Subscription plan
- Payment method
- Lifetime value
- Referral source

#### Engagement Properties:
- Engagement score
- Activation status
- Power user flag
- Days since last active
- Email engagement
- Feature adoption score

### 8. Analytics Implementation Plan

#### Technical Setup:
- Analytics tools selection (Google Analytics, Mixpanel, Amplitude, Segment, etc.)
- Event tracking implementation
- User identification setup
- Cross-domain tracking
- Conversion tracking
- Custom dimensions and metrics
- Data layer implementation
- Tag management system (Google Tag Manager)

#### Data Collection:
- Frontend tracking (JavaScript SDK)
- Backend tracking (server-side events)
- Mobile app tracking
- Email tracking (opens, clicks)
- Marketing automation integration
- CRM integration
- Payment provider integration

#### Data Quality:
- Naming conventions
- Event taxonomy
- Data validation rules
- Testing procedures
- Documentation standards
- Change management process

### 9. Cohort Analysis Framework

Define cohorts by:
- Sign-up date (daily, weekly, monthly)
- Acquisition channel
- User segment
- Plan/tier
- Geographic region
- Company size

Analyze cohorts for:
- Retention over time
- Revenue expansion
- Feature adoption
- Engagement patterns
- Churn patterns

### 10. Funnel Analysis

Key funnels to track:
- Sign-up funnel
- Onboarding funnel
- Purchase/conversion funnel
- Feature adoption funnel
- Upgrade funnel
- Referral funnel

For each funnel:
- Steps in the funnel
- Conversion rate at each step
- Drop-off points
- Time to complete
- Segment-specific performance

### 11. Segmentation Strategy

Segment users by:
- Acquisition channel
- User behavior (power users, casual users, dormant)
- Value (high-value, medium, low)
- Plan type
- Industry/vertical
- Company size
- Geographic location
- Product usage patterns
- Lifecycle stage

### 12. Attribution Modeling

- Attribution model selection (last-click, first-click, linear, time-decay, position-based)
- Multi-touch attribution setup
- Marketing channel attribution
- Feature attribution (what drives retention)
- Referral attribution

### 13. A/B Testing and Experimentation

Framework for:
- Hypothesis formation
- Success metrics selection
- Sample size calculation
- Test duration
- Statistical significance threshold
- Results analysis
- Learning documentation

### 14. Reporting and Communication

#### Report Types:
- Daily snapshot
- Weekly business review
- Monthly board report
- Quarterly business review
- Annual retrospective

#### Report Contents:
- Executive summary
- Metrics trends (vs. last period, vs. goal)
- Key insights and analysis
- Wins and concerns
- Action items
- Forecast and projections

#### Distribution:
- Automated dashboards
- Email reports
- Slack/Teams notifications
- Presentation decks
- Data warehouse access

### 15. Data Governance

- Data access policies
- Privacy compliance (GDPR, CCPA)
- Data retention policies
- PII handling procedures
- Security measures
- Audit logs
- Data backup procedures

### 16. Analytics Tools Stack

Recommend tools for:
- Web analytics (Google Analytics, Plausible)
- Product analytics (Mixpanel, Amplitude, Heap)
- Customer data platform (Segment, Rudderstack)
- Business intelligence (Tableau, Looker, Metabase)
- Session replay (FullStory, Hotjar)
- Heatmaps (Hotjar, Crazy Egg)
- A/B testing (Optimizely, VWO, Google Optimize)
- Survey tools (Typeform, SurveyMonkey)
- NPS tracking (Delighted, Promoter.io)

### 17. Benchmarks and Goals

Set targets for:
- Industry benchmarks by metric
- Company-specific goals
- Quarterly targets
- Annual objectives
- Stretch goals

### 18. Data Analysis Playbooks

Create playbooks for:
- Weekly metrics review
- Monthly deep dives
- Churn analysis procedure
- Growth opportunity identification
- Feature success evaluation
- Campaign performance analysis

### 19. Metrics Maturity Roadmap

#### Phase 1 (Months 1-3): Foundation
- Basic tracking implementation
- Core KPIs defined
- Simple dashboards built
- Weekly reporting cadence

#### Phase 2 (Months 4-6): Expansion
- Advanced event tracking
- Cohort analysis
- Funnel optimization
- A/B testing framework

#### Phase 3 (Months 7-12): Sophistication
- Predictive analytics
- Advanced segmentation
- Custom models
- AI/ML integration

## Output Format

Provide:
1. Complete KPI list organized by category
2. Metrics dashboard mockups (description)
3. Event tracking specification sheet
4. Analytics implementation checklist
5. Reporting templates
6. 90-day implementation roadmap
7. Metrics definitions glossary
8. Calculation formulas for each metric

Create tables for:
- KPI summary (metric name, definition, target, frequency)
- Event tracking (event name, properties, when it fires)
- Dashboard views (audience, metrics included, update frequency)
- Tool recommendations (purpose, tool options, cost range)

Ask clarifying questions about the business model, product maturity, current analytics setup, team size, and specific goals before creating the metrics plan.