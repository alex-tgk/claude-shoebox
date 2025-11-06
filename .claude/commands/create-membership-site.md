# Membership Site Platform Creator

Create a complete membership platform with authentication, content delivery, community features, payment processing, and admin controls for the membership program specified by the user.

## Instructions

Build a comprehensive membership site including:

### 1. Membership Site Strategy

#### Program Definition:
- Membership name and positioning
- Target audience and avatar
- Content type (courses, resources, community, tools)
- Membership tiers/levels
- Pricing model (monthly, annual, lifetime)
- Value proposition and benefits
- Launch strategy

#### Membership Tiers:

**Example Structure:**
```
FREE (Lead Magnet):
- 3 sample lessons
- Community access (read-only)
- Monthly newsletter
- Price: $0

BASIC ($29/month or $290/year):
- Full course library access
- Community access (full participation)
- Monthly live Q&A
- Resource downloads
- Email support

PRO ($99/month or $990/year):
- Everything in Basic
- Weekly coaching calls
- Private Slack/Discord channel
- Priority support
- Monthly expert interviews
- Done-for-you templates

VIP ($299/month or $2,990/year):
- Everything in Pro
- 1-on-1 monthly coaching session
- Annual in-person meetup
- Early access to new content
- Review/feedback on your work
- Direct messaging access
```

### 2. User Authentication & Profiles

#### Authentication System:

**Registration Flow:**
```
Landing Page
  ↓
Sign Up Form (email, password, name)
  ↓
Email Verification
  ↓
Plan Selection
  ↓
Payment (if paid tier)
  ↓
Welcome to Dashboard
```

**Features:**
- Email/password authentication
- Social login (Google, Facebook, LinkedIn optional)
- Email verification required
- Password reset flow
- Remember me functionality
- 2FA optional (for higher tiers)
- Session management
- Logout all devices

**Tech Implementation (React + Node.js example):**
```javascript
// User registration endpoint
POST /api/auth/register
{
  "email": "user@example.com",
  "password": "securepass123",
  "firstName": "John",
  "lastName": "Doe",
  "tier": "basic"
}

// JWT token generation
const token = jwt.sign(
  {
    userId: user.id,
    email: user.email,
    tier: user.tier
  },
  process.env.JWT_SECRET,
  {expiresIn: '7d'}
);
```

#### User Profile System:

**Profile Information:**
- Display name
- Profile photo (upload or Gravatar)
- Bio/About me
- Location
- Website/social links
- Skills/interests
- Membership tier badge
- Join date
- Activity stats (courses completed, posts made)

**Privacy Settings:**
- Profile visibility (public, members-only, private)
- Show/hide email
- Show/hide activity
- Email notification preferences
- Search visibility

**Progress Tracking:**
- Courses in progress
- Courses completed (%)
- Lessons completed
- Certificates earned
- Total time spent
- Streak tracking (consecutive days active)
- Points/badges earned

### 3. Content Organization & Delivery

#### Content Structure:

**Hierarchical Organization:**
```
Membership Site
  ├── Courses
  │   ├── Course 1
  │   │   ├── Module 1
  │   │   │   ├── Lesson 1.1 (video)
  │   │   │   ├── Lesson 1.2 (video + worksheet)
  │   │   │   └── Quiz 1
  │   │   ├── Module 2
  │   │   └── Module 3
  │   └── Course 2
  ├── Resources
  │   ├── Templates
  │   ├── Checklists
  │   ├── Worksheets
  │   └── Tools
  ├── Community
  │   ├── Discussion Forums
  │   ├── Member Directory
  │   └── Events Calendar
  └── Live Sessions
      ├── Upcoming
      ├── Recordings
      └── Transcripts
```

#### Course/Lesson Types:

**Video Lessons:**
- Video player (Vimeo, Wistia, custom)
- Progress tracking (watched X%)
- Playback speed control
- Subtitles/captions
- Download option (for higher tiers)
- Notes section below video
- Resources/attachments
- Next lesson auto-play option

**Text Lessons:**
- Rich text editor content
- Embedded media
- Code snippets with syntax highlighting
- Downloadable PDFs
- Estimated reading time
- Print-friendly version

**Audio Lessons:**
- Audio player with controls
- Downloadable MP3
- Transcript
- Show notes

**Quiz/Assessment:**
- Multiple choice
- True/false
- Fill in the blank
- Essay/open-ended
- Instant feedback
- Score tracking
- Certificate upon passing
- Retake options

**Assignments:**
- Upload submissions
- Peer review option
- Instructor feedback
- Grading rubric
- Due dates
- Revision submission

#### Content Metadata:

For each lesson/resource:
- Title and description
- Duration/length
- Difficulty level
- Prerequisites
- Tags/categories
- Free preview (yes/no)
- Tier access level
- Publish date
- Last updated
- Author/instructor

### 4. Drip Content Functionality

#### Scheduling Methods:

**1. Date-Based Drip:**
```
Example: 30-Day Onboarding Course

Day 1: Module 1 unlocked
Day 7: Module 2 unlocked
Day 14: Module 3 unlocked
Day 21: Module 4 unlocked
Day 30: Final module + certificate
```

**2. Sequential/Completion-Based:**
```
Unlock next module when:
- Previous module completed (all lessons watched)
- Quiz passed (70%+ score)
- Assignment submitted
- X days since starting previous module
```

**3. Manual Release:**
- Admin controls when content goes live
- Scheduled releases
- Event-based releases

**4. Membership Duration-Based:**
```
Month 1: Foundation content
Month 2: Intermediate content
Month 3: Advanced content
Ongoing: Monthly new lessons
```

#### Implementation:

**Database Schema:**
```sql
CREATE TABLE content_access (
  id SERIAL PRIMARY KEY,
  user_id INTEGER REFERENCES users(id),
  content_id INTEGER REFERENCES content(id),
  unlocked_at TIMESTAMP,
  completed_at TIMESTAMP,
  progress_percent INTEGER DEFAULT 0
);

CREATE TABLE content_rules (
  id SERIAL PRIMARY KEY,
  content_id INTEGER REFERENCES content(id),
  unlock_type VARCHAR(50), -- days_after_join, complete_previous, date_based
  unlock_value TEXT, -- number of days, prerequisite ID, or date
  tier_required VARCHAR(50)
);
```

**Logic:**
```javascript
async function checkContentAccess(userId, contentId) {
  const user = await getUser(userId);
  const content = await getContent(contentId);
  const rule = await getContentRule(contentId);

  // Check tier access
  if (!hasTierAccess(user.tier, content.tier_required)) {
    return {access: false, reason: 'upgrade_required'};
  }

  // Check drip rules
  switch (rule.unlock_type) {
    case 'days_after_join':
      const daysSinceJoin = daysBetween(user.joined_date, now());
      if (daysSinceJoin >= rule.unlock_value) {
        return {access: true};
      }
      return {
        access: false,
        reason: 'not_yet_available',
        availableIn: rule.unlock_value - daysSinceJoin + ' days'
      };

    case 'complete_previous':
      const previousCompleted = await checkCompletion(
        userId,
        rule.unlock_value
      );
      if (previousCompleted) {
        return {access: true};
      }
      return {access: false, reason: 'complete_previous_first'};

    case 'date_based':
      if (new Date() >= new Date(rule.unlock_value)) {
        return {access: true};
      }
      return {
        access: false,
        reason: 'scheduled_release',
        availableDate: rule.unlock_value
      };

    default:
      return {access: true};
  }
}
```

### 5. Discussion Forum / Community

#### Forum Structure:

**Categories:**
- General Discussion
- Questions & Answers
- Success Stories
- Feature Requests
- Course-Specific (one per course)
- Off-Topic
- Introductions

**Post Types:**
- Discussion (standard post)
- Question (can mark answer as "Solved")
- Poll
- Announcement (admin only)
- Event

**Features:**
- Rich text editor (formatting, links, images)
- File attachments
- Code blocks with syntax highlighting
- @mentions (notifications)
- Emoji reactions
- Threaded replies (nested comments)
- Upvote/downvote or like system
- Best answer marking
- Pin important posts
- Lock threads
- Tags/categories
- Search functionality

**Moderation:**
- Report post/comment
- Admin approval queue (optional)
- Auto-moderation (spam detection)
- Ban users
- Edit/delete posts
- Move threads to different categories
- Moderator roles

**Gamification:**
- Post count displayed
- Reputation/points system
- Badges (Helpful, Popular Post, 100 Posts, etc.)
- Top contributors leaderboard
- Trust levels (unlock abilities with activity)

#### Member Directory:

**Features:**
- Searchable member list
- Filter by tier, location, interests
- Profile previews
- Direct messaging option
- Follow/connect functionality
- Activity feed

### 6. Payment Integration (Recurring Subscriptions)

#### Supported Payment Methods:

**Stripe Integration (Primary):**
```javascript
// Create customer and subscription
const customer = await stripe.customers.create({
  email: user.email,
  payment_method: paymentMethodId,
  invoice_settings: {
    default_payment_method: paymentMethodId
  }
});

const subscription = await stripe.subscriptions.create({
  customer: customer.id,
  items: [{
    price: 'price_basic_monthly' // Stripe price ID
  }],
  trial_period_days: 14, // optional
  metadata: {
    userId: user.id,
    tier: 'basic'
  }
});

// Save subscription ID to database
await updateUser(user.id, {
  stripe_customer_id: customer.id,
  stripe_subscription_id: subscription.id,
  tier: 'basic',
  subscription_status: 'active'
});
```

**Webhook Handling:**
```javascript
// Handle Stripe webhooks for subscription events
app.post('/webhook/stripe', async (req, res) => {
  const event = stripe.webhooks.constructEvent(
    req.body,
    req.headers['stripe-signature'],
    process.env.STRIPE_WEBHOOK_SECRET
  );

  switch (event.type) {
    case 'customer.subscription.created':
      await activateMembership(event.data.object);
      break;

    case 'customer.subscription.updated':
      await updateMembership(event.data.object);
      break;

    case 'customer.subscription.deleted':
      await cancelMembership(event.data.object);
      break;

    case 'invoice.payment_failed':
      await handlePaymentFailure(event.data.object);
      break;

    case 'invoice.payment_succeeded':
      await confirmPayment(event.data.object);
      break;
  }

  res.json({received: true});
});
```

#### Subscription Features:

**Plan Management:**
- Upgrade/downgrade between tiers
- Proration handling (Stripe automatic)
- Annual discount (save 15-20%)
- Pause subscription (optional)
- Cancel anytime
- Reactivation flow
- Failed payment recovery

**Billing Portal:**
- View current plan
- Update payment method
- View invoice history
- Download receipts
- Update billing information
- Manage subscriptions
- Cancel or change plan

**Trial Periods:**
- 7, 14, or 30-day free trials
- Credit card required or not
- Trial expiration emails
- Automatic conversion to paid

**Coupons & Discounts:**
- Percentage off
- Fixed amount off
- First month free
- Extended trial
- Lifetime deals
- Affiliate/referral discounts

### 7. Member Dashboard

#### Dashboard Layout:

**Welcome Section:**
```
Welcome back, [First Name]!

Membership: [BASIC] badge
Member since: [Date]
Streak: 🔥 7 days

Quick Actions:
[Continue Learning] [Browse Courses] [Community] [Support]
```

**Progress Overview:**
```
Your Progress

Courses in Progress (2):
- [Course Name] ████████░░ 78% complete
  → Continue to Lesson 12
- [Course Name] ███░░░░░░░ 32% complete
  → Continue to Lesson 5

Completed Courses (3):
- [Course Name] ✓
- [Course Name] ✓
- [Course Name] ✓
```

**Recent Activity Feed:**
```
Recent Activity

• New lesson available: "Advanced Techniques"
• Sarah Johnson replied to your post
• You earned the "7-Day Streak" badge
• New resources added to Templates library
• Upcoming live session: Tomorrow at 2pm
```

**Recommendations:**
```
Recommended For You

Based on your progress and interests:

[Course Card] [Course Card] [Course Card]
```

**Upcoming Events:**
```
Upcoming Live Sessions

📅 Nov 8, 2:00 PM EST - Monthly Q&A
📅 Nov 15, 12:00 PM EST - Workshop: XYZ
📅 Nov 22, 3:00 PM EST - Guest Expert Interview

[View Calendar]
```

**Community Highlights:**
```
Latest From the Community

💬 "How do I implement X?" - 5 replies
💬 "Just completed Course Y!" - 12 likes
💬 "Looking for accountability partner" - New

[Visit Community]
```

### 8. Admin Panel for Content Management

#### Admin Dashboard Features:

**Member Management:**
- View all members (table with filters)
- Search by name, email, tier
- View individual member details
- Manual tier upgrades/downgrades
- Grant lifetime access
- Comp subscriptions
- Send direct messages
- Ban/suspend members
- Export member list
- Bulk actions

**Content Management:**
```
Courses & Lessons:
- Create/edit/delete courses
- Drag-and-drop lesson reordering
- Bulk upload videos
- Set access rules
- Schedule releases
- Mark as free preview
- Clone courses
- Import/export content
```

**Categories & Organization:**
- Create course categories
- Add tags
- Set difficulty levels
- Featured content selection
- Content ordering

**Video Management:**
- Upload to integrated hosting (Vimeo/Wistia)
- Embed external videos
- Generate thumbnails
- Add captions/subtitles
- Set player options
- Analytics integration

**Resource Library:**
- Upload files (PDFs, docs, templates)
- Organize in folders
- Set download permissions
- Track downloads
- File version control

**Analytics & Reports:**
```
Key Metrics:
- Total active members
- New members (this month)
- Churn rate
- MRR (Monthly Recurring Revenue)
- LTV (Lifetime Value)
- Course completion rates
- Most popular content
- Engagement metrics
- Revenue by tier
- Cohort analysis
```

**Financial Dashboard:**
```
Revenue Overview:
- Monthly revenue
- Annual revenue
- Failed payments
- Refunds
- Churn analysis
- Revenue projections
- Payment method breakdown

Charts:
- Revenue over time (line chart)
- Members by tier (pie chart)
- Churn cohorts (table)
- MRR movement (waterfall)
```

**Email Center:**
- Broadcast emails to all members
- Segment by tier
- Drip email campaigns
- Transactional email templates
- Email analytics (open, click rates)

**Settings:**
- Site information
- Branding (logo, colors)
- Email configurations
- Payment gateway settings
- Access rules configuration
- Integrations
- Security settings
- SEO settings

### 9. Email Notifications System

#### Automated Emails:

**1. Welcome Series (New Members):**

**Email 1 - Immediate:**
```
Subject: Welcome to [Membership Name]! Let's get started 🎉

Hi [First Name],

Welcome to [Membership]! We're thrilled to have you.

Here's what to do first:
→ Complete your profile
→ Explore the course library
→ Introduce yourself in the community
→ Bookmark your dashboard: [Link]

Ready to dive in? Start with our Quick Start Guide: [Link]

If you have any questions, just reply to this email.

Welcome aboard!
[Your Name]
```

**Email 2 - Day 2:**
- Feature highlight
- Course recommendation
- Community introduction

**Email 3 - Day 5:**
- Progress check-in
- Tips for success
- Available resources

**Email 4 - Day 10:**
- Case study/success story
- Advanced features
- Exclusive benefit reminder

**2. Engagement Emails:**
- New content available
- Course completion congratulations
- Inactivity nudge (7, 14, 30 days)
- Streak milestones (7, 30, 100 days)
- Community activity digest (weekly)
- Upcoming live events

**3. Transactional Emails:**
- Payment successful
- Payment failed (with action steps)
- Subscription expiring soon
- Subscription renewed
- Plan upgrade/downgrade confirmed
- Receipt/invoice
- Cancellation confirmation
- Password reset
- Email address verification

**4. Retention Emails:**
- Monthly value reminder
- Unused benefits highlight
- Personalized recommendations
- Win-back campaign (cancelled members)
- Upgrade prompts (for lower tiers)

### 10. Mobile-Responsive Design

#### Design Principles:

**Mobile-First Approach:**
- Touch-friendly buttons (44x44px minimum)
- Simplified navigation (hamburger menu)
- Collapsible sections
- Swipe gestures
- Responsive video players
- Optimized images
- Fast loading times

**Breakpoints:**
- Mobile: < 768px
- Tablet: 768px - 1024px
- Desktop: > 1024px
- Large desktop: > 1440px

**Mobile-Specific Features:**
- Offline mode (download lessons)
- Push notifications (optional)
- Native app feel (PWA)
- Quick access toolbar
- Bottom navigation

**Technical Implementation:**
```css
/* Responsive grid */
.course-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
}

@media (max-width: 768px) {
  .course-grid {
    grid-template-columns: 1fr;
    gap: 1rem;
  }
}
```

### 11. Additional Features

#### Certificates:
- Auto-generated upon course completion
- Custom design with branding
- Include member name, course name, date
- Unique verification code
- PDF download
- Shareable link
- LinkedIn integration

#### Live Events Integration:
- Zoom or WebinarJam integration
- Calendar integration (iCal, Google)
- Event registration
- Email reminders (1 week, 1 day, 1 hour before)
- Recording access
- Event replay section

#### Gamification:
- Points for activities (login, complete lesson, post in forum)
- Badges for achievements
- Levels/ranks
- Leaderboard (optional, privacy-sensitive)
- Challenges and quests
- Rewards for streaks

#### Search Functionality:
- Global search (courses, lessons, posts, members)
- Filters (type, tier, category)
- Autocomplete
- Search history
- Popular searches

#### Integrations:
- Zapier (connect to 1000+ apps)
- Slack/Discord (community alternative)
- Google Analytics
- Facebook Pixel
- Email marketing (Mailchimp, ConvertKit)
- CRM (HubSpot, Salesforce)
- Customer support (Intercom, Help Scout)

#### API Access (for developers):
- RESTful API
- Webhooks
- Zapier integration
- Custom integrations

### 12. Database Schema

```sql
-- Core tables
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  email VARCHAR(255) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  first_name VARCHAR(100),
  last_name VARCHAR(100),
  tier VARCHAR(50) DEFAULT 'free',
  status VARCHAR(50) DEFAULT 'active',
  stripe_customer_id VARCHAR(255),
  stripe_subscription_id VARCHAR(255),
  joined_date TIMESTAMP DEFAULT NOW(),
  last_login TIMESTAMP
);

CREATE TABLE courses (
  id SERIAL PRIMARY KEY,
  title VARCHAR(255) NOT NULL,
  slug VARCHAR(255) UNIQUE,
  description TEXT,
  instructor_id INTEGER REFERENCES users(id),
  tier_required VARCHAR(50),
  status VARCHAR(50) DEFAULT 'draft',
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE modules (
  id SERIAL PRIMARY KEY,
  course_id INTEGER REFERENCES courses(id),
  title VARCHAR(255),
  order_index INTEGER,
  unlock_rule TEXT
);

CREATE TABLE lessons (
  id SERIAL PRIMARY KEY,
  module_id INTEGER REFERENCES modules(id),
  title VARCHAR(255),
  content_type VARCHAR(50), -- video, text, quiz, assignment
  content TEXT,
  video_url VARCHAR(500),
  duration_seconds INTEGER,
  order_index INTEGER,
  free_preview BOOLEAN DEFAULT FALSE
);

CREATE TABLE user_progress (
  id SERIAL PRIMARY KEY,
  user_id INTEGER REFERENCES users(id),
  lesson_id INTEGER REFERENCES lessons(id),
  progress_percent INTEGER DEFAULT 0,
  completed BOOLEAN DEFAULT FALSE,
  last_accessed TIMESTAMP,
  UNIQUE(user_id, lesson_id)
);

CREATE TABLE forum_posts (
  id SERIAL PRIMARY KEY,
  user_id INTEGER REFERENCES users(id),
  category VARCHAR(100),
  title VARCHAR(255),
  content TEXT,
  post_type VARCHAR(50),
  likes_count INTEGER DEFAULT 0,
  replies_count INTEGER DEFAULT 0,
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE forum_replies (
  id SERIAL PRIMARY KEY,
  post_id INTEGER REFERENCES forum_posts(id),
  user_id INTEGER REFERENCES users(id),
  content TEXT,
  is_solution BOOLEAN DEFAULT FALSE,
  created_at TIMESTAMP DEFAULT NOW()
);
```

## Output Format

Provide:

1. **Complete Application Codebase** (React/Next.js frontend + Node.js backend, or detailed specifications)
2. **Database Schema** (full SQL with all tables and relationships)
3. **Authentication System** (registration, login, JWT implementation)
4. **Payment Integration** (Stripe setup with subscriptions)
5. **Content Management System** (admin panel for courses and lessons)
6. **Drip Content Engine** (scheduling logic and rules)
7. **Forum/Community Platform** (discussion board with moderation)
8. **Email Templates** (all 15+ automated emails)
9. **Member Dashboard** (wireframes and component structure)
10. **Mobile Responsive Design** (CSS framework and breakpoints)
11. **Deployment Guide** (hosting, domain, SSL, database setup)
12. **Documentation** (user guides for members and admins)

Ask clarifying questions about the membership content type, target audience, pricing structure, existing content, desired features, technical preferences, and budget before building the membership site.
