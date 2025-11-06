# Resume Optimizer - Product Design Document

## Executive Summary

**Product**: AI-Powered Resume/CV Optimization Service
**Target Market**: Job seekers (recent grads, mid-career professionals)
**Value Proposition**: Get 3x more interviews with AI-optimized, ATS-friendly resumes
**Revenue Model**: Freemium SaaS ($0 → $19/mo → $49/mo → $99/mo)
**Differentiation**: Content-focused optimization vs template-focused competitors

**Key Metrics**:
- Year 1 Target: 10,000 users, 350 paid ($120K ARR)
- Conversion Rate: 3-5% (free → paid)
- Churn: <10% monthly
- CAC Target: <$50

---

## Product Vision

### Problem Statement
- 99% of Fortune 500 use ATS systems, only 25% of resumes pass screening
- Job seekers spend 34 hours/week on applications with 3% interview rate
- Professional resume writers cost $500+, AI tools are expensive ($49-99/mo)
- Current AI tools produce generic content, don't optimize for specific jobs

### Solution
AI-powered resume optimization that:
1. **Scores resumes** 0-100 against ATS and best practices
2. **Matches to job descriptions** with keyword analysis
3. **Improves content** with AI suggestions (not just formatting)
4. **Tracks outcomes** to prove ROI (interview rates)
5. **Fair pricing** with generous free tier and no dark patterns

---

## User Personas

### Primary: Sarah - Recent Graduate
- **Age**: 22-25
- **Goal**: Land first professional job
- **Pain**: Generic resume, no interviews, unsure what to improve
- **Willingness to Pay**: $19/month during job search (2-4 months)
- **Success Metric**: 5+ interviews in first month

### Secondary: Mike - Mid-Career Professional
- **Age**: 30-45
- **Goal**: Career advancement or switch
- **Pain**: Resume doesn't reflect accomplishments, ATS rejections
- **Willingness to Pay**: $49/month for premium features
- **Success Metric**: Interview at target companies within 6 weeks

### Tertiary: Lisa - Career Coach
- **Age**: 35-55
- **Goal**: Help 20-50 clients efficiently
- **Pain**: Time-consuming manual optimization
- **Willingness to Pay**: $99/month for team features
- **Success Metric**: 2x client throughput, better outcomes

---

## Core Features (MVP)

### 1. Resume Editor
**Description**: Rich text editor for creating/editing resumes

**Functionality**:
- Import existing resume (PDF, DOCX)
- Structured sections (Contact, Summary, Experience, Education, Skills)
- Real-time ATS score as you type
- 3-5 ATS-optimized templates (different styles)
- Auto-save every 30 seconds

**Technical**:
- Frontend: Lexical or TipTap editor (React-based)
- Parser: Python microservice (PyMuPDF + pyresparser)
- Storage: PostgreSQL + S3 for PDFs

**Success Criteria**:
- Import 80%+ of resumes successfully
- Parse common formats (Chronological, Functional, Hybrid)
- <2 second load time for existing resumes

---

### 2. AI Resume Scoring
**Description**: 0-100 score evaluating ATS compatibility and best practices

**Scoring Factors** (weighted):
- **ATS Compatibility (40%)**
  - Standard section headings
  - Simple formatting (no tables/columns)
  - Keyword presence
  - File format (PDF vs DOCX)

- **Content Quality (35%)**
  - Action verbs usage
  - Quantifiable achievements
  - Relevant keywords
  - Appropriate length (1-2 pages)

- **Formatting (15%)**
  - Consistent fonts and spacing
  - Proper hierarchy
  - Readability (white space)

- **Impact (10%)**
  - Achievement-focused bullets
  - Industry-specific terminology
  - Skills alignment

**Technical**:
- NLP: spaCy for keyword extraction
- GPT-4 API for content quality analysis
- Rule-based scoring engine
- Caching to reduce API costs

**Success Criteria**:
- Score correlates with interview rate (validate with user data)
- <3 second scoring time
- Actionable improvement suggestions (not just number)

---

### 3. Job Description Matching
**Description**: Match resume to specific job posting, identify gaps

**Functionality**:
- Paste job description
- Calculate match percentage (0-100%)
- Highlight missing keywords
- Suggest additions to improve match
- Track multiple jobs (free: 5, paid: unlimited)

**Matching Algorithm**:
1. Extract key skills and requirements from JD
2. Extract skills and keywords from resume
3. Calculate overlap (Jaccard similarity + weighted keywords)
4. Identify critical gaps (required skills missing)
5. Generate improvement suggestions

**Technical**:
- NLP: spaCy + NLTK for keyword extraction
- Custom weighting for "required" vs "preferred" skills
- GPT-4 for semantic matching (beyond exact keywords)

**Success Criteria**:
- 85%+ accuracy vs human assessment
- Specific, actionable suggestions
- <5 second analysis time

---

### 4. AI Content Improvement
**Description**: AI-powered suggestions to improve resume content

**Suggestion Types**:
- **Strengthen bullets**: Make more impactful with action verbs
- **Quantify achievements**: Add numbers/metrics where missing
- **Add keywords**: Incorporate relevant industry terms
- **Improve clarity**: Simplify complex/jargon-heavy language
- **Fix grammar**: Correct errors and improve readability

**AI Approach**:
- GPT-4 with custom prompts per suggestion type
- Context-aware (knows user's industry, role, experience level)
- Provides 2-3 variations per suggestion
- User accepts/rejects, learning from preferences

**Technical**:
- OpenAI GPT-4 API (gpt-4-turbo for cost)
- Prompt engineering for quality, consistency
- Rate limiting: Free (5 suggestions/month), Pro (unlimited)
- Caching common patterns to reduce costs

**Success Criteria**:
- 70%+ acceptance rate for suggestions
- Suggestions feel personalized, not generic
- <10 second generation time per suggestion

---

### 5. PDF Export
**Description**: Export optimized resume as ATS-friendly PDF

**Features**:
- Multiple templates (Clean, Modern, Professional, Executive)
- Customization (fonts, colors, spacing within ATS-safe bounds)
- Metadata optimization (keywords in PDF metadata)
- File size optimization (<500KB)

**Technical**:
- Server-side rendering (Puppeteer or Playwright)
- LaTeX alternative: React-PDF or Paged.js
- PDF/A standard for maximum compatibility

**Success Criteria**:
- Works with 95%+ ATS systems (test against major ones)
- Professional appearance
- <10 second generation time

---

### 6. Resume Management
**Description**: Store and manage multiple resume versions

**Features**:
- Multiple resumes (Free: 1, Pro: unlimited)
- Version history (track changes over time)
- Duplicate and customize for different jobs
- Organize with tags/labels

**Technical**:
- PostgreSQL for metadata
- S3 for PDF storage
- Soft delete (retain for 30 days)

**Success Criteria**:
- Fast loading (<1 second)
- Easy to find resumes (search, filter)
- No data loss

---

## Technical Architecture

### Frontend Stack
- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript
- **Styling**: Tailwind CSS v4
- **UI Components**: Shadcn/UI
- **Editor**: Lexical (extensible rich text)
- **State**: Zustand (lightweight, simple)
- **Forms**: React Hook Form + Zod
- **API Client**: TanStack Query (caching, optimistic updates)

### Backend Stack
- **API**: Next.js API Routes (serverless)
- **Database**: PostgreSQL (Supabase)
- **File Storage**: S3 (or Supabase Storage)
- **Auth**: Next-Auth v5 (email/password + Google OAuth)
- **Payments**: Stripe (subscriptions)
- **AI**: OpenAI GPT-4 API

### AI/NLP Microservice (Python)
- **Framework**: FastAPI
- **Libraries**: spaCy, NLTK, PyMuPDF, pyresparser
- **Purpose**: PDF parsing, keyword extraction, NLP heavy lifting
- **Deployment**: Fly.io or Railway (containerized)

### Infrastructure
- **Hosting**: Vercel (frontend + API)
- **Database**: Supabase (PostgreSQL)
- **AI Service**: Fly.io (Python FastAPI)
- **CDN**: Cloudflare
- **Monitoring**: Sentry, PostHog
- **Email**: Resend or SendGrid

---

## Database Schema

### users
```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  password_hash VARCHAR(255),
  full_name VARCHAR(255),
  subscription_tier VARCHAR(20) DEFAULT 'free', -- free, pro, premium, team
  subscription_status VARCHAR(20) DEFAULT 'active',
  stripe_customer_id VARCHAR(255),
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);
```

### resumes
```sql
CREATE TABLE resumes (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  title VARCHAR(255) NOT NULL,
  content JSONB NOT NULL, -- structured resume data
  ats_score INTEGER,
  last_scored_at TIMESTAMP,
  template VARCHAR(50) DEFAULT 'clean',
  pdf_url VARCHAR(500),
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_resumes_user_id ON resumes(user_id);
```

### job_matches
```sql
CREATE TABLE job_matches (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  resume_id UUID REFERENCES resumes(id) ON DELETE CASCADE,
  job_title VARCHAR(255),
  company VARCHAR(255),
  job_description TEXT,
  match_score INTEGER,
  missing_keywords TEXT[],
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_job_matches_user_id ON resumes(user_id);
CREATE INDEX idx_job_matches_resume_id ON job_matches(resume_id);
```

### ai_suggestions
```sql
CREATE TABLE ai_suggestions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  resume_id UUID REFERENCES resumes(id) ON DELETE CASCADE,
  section VARCHAR(50), -- summary, experience, skills
  original_text TEXT,
  suggested_text TEXT,
  suggestion_type VARCHAR(50), -- strengthen, quantify, keywords, clarity
  status VARCHAR(20) DEFAULT 'pending', -- pending, accepted, rejected
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_ai_suggestions_resume_id ON ai_suggestions(resume_id);
```

### usage_metrics
```sql
CREATE TABLE usage_metrics (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  action_type VARCHAR(50), -- ai_suggestion, pdf_export, job_match
  metadata JSONB,
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_usage_metrics_user_id ON usage_metrics(user_id);
CREATE INDEX idx_usage_metrics_created_at ON usage_metrics(created_at);
```

---

## API Endpoints

### Authentication
- `POST /api/auth/register` - Create account
- `POST /api/auth/login` - Email/password login
- `GET /api/auth/session` - Get current user
- `POST /api/auth/logout` - End session

### Resumes
- `GET /api/resumes` - List user's resumes
- `POST /api/resumes` - Create new resume
- `GET /api/resumes/:id` - Get resume details
- `PATCH /api/resumes/:id` - Update resume
- `DELETE /api/resumes/:id` - Delete resume
- `POST /api/resumes/:id/score` - Calculate ATS score
- `POST /api/resumes/:id/export` - Generate PDF

### Job Matching
- `POST /api/job-match` - Analyze resume against job description
- `GET /api/job-match/:id` - Get match details
- `GET /api/job-match/resume/:resumeId` - List matches for resume

### AI Suggestions
- `POST /api/suggestions/generate` - Generate AI suggestions
- `GET /api/suggestions/resume/:resumeId` - Get suggestions for resume
- `PATCH /api/suggestions/:id` - Accept/reject suggestion

### Subscriptions
- `GET /api/subscription` - Get current subscription
- `POST /api/subscription/checkout` - Create Stripe checkout session
- `POST /api/subscription/portal` - Access Stripe customer portal
- `POST /api/webhooks/stripe` - Handle Stripe webhooks

---

## Pricing Strategy

### Free Tier
**Price**: $0/month
**Limits**:
- 1 resume
- 5 AI suggestions per month
- 3 PDF exports per month
- 5 job matches per month
- Community support

**Goal**: Convert 3-5% to paid within 30 days

### Pro Tier
**Price**: $29/month or $199/year (31% savings)
**Features**:
- Unlimited resumes
- Unlimited AI suggestions
- Unlimited PDF exports
- Unlimited job matches
- Cover letter generation
- Email support
- Resume review by humans (waitlist)

**Target**: Individual job seekers

### Premium Tier
**Price**: $49/month or $399/year (32% savings)
**Features**:
- Everything in Pro
- Priority AI (faster processing)
- LinkedIn profile optimization
- Interview preparation AI
- Salary negotiation guidance
- Priority email support

**Target**: Serious career changers, executives

### Team Tier (Future)
**Price**: $99/month (up to 5 users)
**Features**:
- Everything in Premium
- Team management
- Collaboration features
- Usage analytics
- Dedicated support

**Target**: Career coaches, recruiting agencies

---

## User Flows

### New User Onboarding
1. Land on homepage → See value prop + social proof
2. Click "Get Started Free"
3. Sign up with email or Google
4. Welcome screen: "Let's create your first resume"
5. Choose: Upload existing resume OR Start from scratch
6. **If upload**: Parse PDF → Show in editor → Run initial score
7. **If scratch**: Fill out structured form → Generate resume
8. Show ATS score with suggestions
9. Prompt: "Want to optimize for a specific job? Paste the job description"
10. Generate job match analysis
11. Show AI suggestions to improve
12. Export first PDF (counts toward free tier limit)
13. Celebrate! "Your optimized resume is ready. Apply with confidence!"

### Resume Optimization Flow
1. User views resume with ATS score (e.g., 67/100)
2. See breakdown: What's good, what needs improvement
3. Click "Get AI Suggestions"
4. AI analyzes resume, generates 5-10 suggestions
5. User reviews suggestions one by one
6. Click to apply suggestion (updates resume instantly)
7. ATS score updates in real-time
8. Repeat until satisfied (target: 85+ score)
9. Export final PDF

### Job Application Flow
1. User finds job posting
2. Copy job description
3. Go to Resume Optimizer → Select resume
4. Click "Match to Job"
5. Paste job description
6. See match score (e.g., 78%)
7. See missing keywords highlighted
8. Get AI suggestions to improve match
9. Apply suggestions
10. Re-score (now 91%)
11. Export tailored resume for this job
12. Track application (external to our tool, but we can add later)

---

## Success Metrics & KPIs

### Acquisition Metrics
- **Signups per day**: Target 30-50 (Month 3), 100+ (Month 6)
- **Traffic sources**: Organic (40%), Reddit (20%), Paid (25%), Other (15%)
- **Landing page conversion**: 3-5%
- **CAC**: <$50

### Activation Metrics
- **% who create first resume**: >70%
- **% who complete resume**: >50%
- **% who run first score**: >80%
- **Time to first value**: <10 minutes

### Engagement Metrics
- **Daily active users (DAU)**: 15-20% of total users
- **Weekly active users (WAU)**: 40-50% of total users
- **Avg resumes per user**: 2-3
- **Avg AI suggestions accepted**: 60-70%

### Monetization Metrics
- **Free → Paid conversion**: 3-5%
- **Time to conversion**: 7-14 days
- **Monthly churn**: <10%
- **LTV:CAC ratio**: >3:1
- **MRR growth**: 15-20% month-over-month

### Product Quality Metrics
- **ATS score improvement**: Avg +15 points
- **User-reported interview rate**: Aim for 3x improvement (3% → 9%)
- **NPS score**: >50
- **5-star reviews**: >4.5/5

---

## Go-to-Market Strategy

### Phase 1: Pre-Launch (Weeks 1-2)
- Build landing page with email capture
- Target 500-1,000 waitlist signups
- Content: "How to beat ATS systems" blog posts (5 articles)
- Reddit engagement on r/resumes, r/jobs (provide value, soft promote)

### Phase 2: Beta Launch (Weeks 3-4)
- Invite 50-100 beta users from waitlist
- Offer: Free Pro for 3 months in exchange for feedback
- Iterate based on feedback
- Collect testimonials and success stories

### Phase 3: Public Launch (Week 5)
- Product Hunt launch (aim for Product of the Day)
- Reddit posts with case studies
- Launch offer: 50% off Pro for first month (urgency)
- Email waitlist: "We're live!"

### Phase 4: Growth (Months 2-12)
**SEO** (40% of acquisition):
- Target keywords: "ats resume checker", "resume optimization", "ai resume builder"
- 2-3 blog posts per week
- Build backlinks through guest posting

**Community** (20%):
- Reddit: r/resumes, r/jobs, r/careerguidance (provide value)
- LinkedIn: Share success stories, resume tips
- Facebook groups: Job seekers, recent grads

**Paid Ads** (25%):
- Google Ads on competitor keywords ("resume.io alternative")
- Facebook/Instagram: Target job seekers (recent grads, layoff victims)
- Budget: $500/month initially, scale with revenue

**Partnerships** (10%):
- University career centers (bulk licenses)
- Recruiting agencies (referral commissions)
- Job boards (Indeed, LinkedIn integration)

**Content** (5%):
- YouTube: Resume tips, ATS hacks
- TikTok: Quick resume tips (viral potential)
- Newsletter: Weekly job search tips

---

## Competitive Differentiation

| Feature | Us | Resume.io | Rezi | Jobscan |
|---------|----|-----------| -----|---------|
| **Pricing** | $29/mo | $24.95/mo | $29/mo | $49.95/mo |
| **Free Tier** | 1 resume, 5 AI/mo | 10 links/mo | Limited | Very limited |
| **AI Content** | ✅ Advanced | ❌ Basic | ✅ Advanced | ❌ None |
| **Job Matching** | ✅ Included | ❌ No | ✅ Included | ✅ Core feature |
| **Auto-renewal** | ❌ Transparent | ⚠️ Complaints | ✅ Clear | ⚠️ Complaints |
| **Focus** | Content + ATS | Templates | AI-first | ATS-only |

**Our Advantages**:
1. **Transparent pricing**: No dark patterns, easy cancellation
2. **Content focus**: Improve what you say, not just how it looks
3. **Generous free tier**: Actually useful, builds trust
4. **Affordable premium**: $29 vs $49-99 competitors
5. **Outcome tracking**: Prove ROI with interview metrics

---

## Risk Mitigation

### Risk: High AI API Costs
**Impact**: Erodes margins, makes unit economics unsustainable
**Probability**: Medium
**Mitigation**:
- Cache common suggestions and patterns
- Use GPT-4 Turbo (cheaper) for most tasks
- Rate limiting on free tier
- Progressive enhancement (simpler AI for lower tiers)
- Monitor cost per user, adjust pricing if needed

### Risk: Low Free → Paid Conversion
**Impact**: Can't achieve revenue targets
**Probability**: Medium
**Mitigation**:
- Make free tier genuinely useful (builds trust)
- Trigger upgrades at key moments (after good score, before important app)
- Time-limited discounts (50% off first month)
- Referral incentives (free month for referrals)
- Email nurture sequence (7 emails over 14 days)

### Risk: Quality of AI Suggestions
**Impact**: Users don't trust/use AI, main feature fails
**Probability**: Low-Medium
**Mitigation**:
- Extensive prompt engineering and testing
- Human review of suggestions (sampling)
- A/B test different prompts, optimize for acceptance rate
- Allow users to provide feedback on suggestions
- Continuously improve based on user feedback

### Risk: ATS Compatibility Issues
**Impact**: Resumes don't pass ATS, damages credibility
**Probability**: Low
**Mitigation**:
- Test against major ATS systems (Taleo, Workday, Greenhouse, etc.)
- Follow established ATS best practices
- Regular testing and validation
- Offer guarantee (if resume doesn't pass ATS, refund)

---

## Development Roadmap

### MVP (Weeks 1-8)
**Week 1-2**: Infrastructure & Auth
- Next.js setup, database, authentication
- User registration/login flows

**Week 3-4**: Core Resume Features
- Resume editor (Lexical)
- PDF import/export
- Template selection

**Week 5-6**: AI Features
- ATS scoring engine
- Job matching algorithm
- AI content suggestions (basic)

**Week 7-8**: Polish & Beta
- UI/UX refinement
- Testing and bug fixes
- Beta user testing

### Post-MVP (Months 3-6)
**Month 3**: Enhanced AI
- Improved suggestion quality
- Cover letter generation
- LinkedIn optimization

**Month 4**: Analytics & Tracking
- User dashboard with metrics
- Interview tracking (self-reported)
- Outcome correlation analysis

**Month 5**: Team Features
- Multi-user accounts
- Collaboration tools
- Admin panel

**Month 6**: Partnerships & Integrations
- Job board integrations (Indeed, LinkedIn)
- Calendar integrations for interview scheduling
- University partnerships

---

## Technical Requirements for TDD

### Test Coverage Goals
- **Unit tests**: 80%+ coverage
- **Integration tests**: All API endpoints
- **E2E tests**: Critical user flows (signup, create resume, export)
- **Performance tests**: API latency, PDF generation time

### Test Framework
- **Unit**: Vitest (fast, modern)
- **Integration**: Supertest + Vitest
- **E2E**: Playwright
- **API Mocking**: MSW (Mock Service Worker)

### Critical Test Scenarios
1. User authentication (signup, login, session)
2. Resume CRUD operations
3. PDF import (various formats)
4. ATS scoring (different resume types)
5. Job matching (edge cases)
6. AI suggestion generation
7. PDF export (all templates)
8. Subscription management
9. Usage limits enforcement
10. Payment webhooks

---

## Success Criteria for Launch

### Technical
- ✅ 80%+ test coverage
- ✅ All critical flows have E2E tests
- ✅ <2s page load times (Lighthouse 90+)
- ✅ <3s API response times (95th percentile)
- ✅ Zero P0/P1 bugs
- ✅ Works on Chrome, Firefox, Safari (desktop + mobile)

### Product
- ✅ 10+ beta users successfully create and export resumes
- ✅ 70%+ accept AI suggestions
- ✅ Average ATS score improvement of 10+ points
- ✅ Users report resumes pass ATS screening
- ✅ 5+ testimonials with measurable outcomes

### Business
- ✅ Landing page converts at 3%+
- ✅ Pricing validated with user interviews
- ✅ CAC model shows path to <$50
- ✅ 3+ distribution channels identified and tested
- ✅ Email nurture sequence ready

---

**Document Version**: 1.0
**Last Updated**: 2025-11-06
**Status**: Ready for implementation
**Next Step**: Write comprehensive test suite following TDD methodology
