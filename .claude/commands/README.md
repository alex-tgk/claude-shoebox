# Custom Slash Commands

This directory contains 30 high-quality custom slash commands for Claude Code that supercharge your development workflow.

## 📊 Overview

- **Total Commands**: 30
- **Categories**: Development (15) + Business/Marketing (15)
- **Usage**: Type `/{command-name}` to invoke
- **Format**: Markdown files with detailed prompts

## 🛠️ Development Commands (15)

### Component & Code Generation

**`/new-component`** (2.9KB)
- Generate React component with TypeScript, Storybook, and tests
- Includes TailwindCSS styling and accessibility features
- Usage: `/new-component` → Follow prompts for component details

**`/new-api`** (3.6KB)
- Scaffold REST API endpoint with TypeScript/Express or Go
- Includes validation, error handling, tests, and OpenAPI docs
- Usage: `/new-api` → Specify endpoint details

**`/microservice`** (9.2KB)
- Scaffold complete microservice with Docker, API, database
- Includes health checks, monitoring, logging, tests
- Usage: `/microservice` → Define service requirements

### Testing & Quality

**`/add-tests`** (3.9KB)
- Generate comprehensive test suites (unit, integration, component)
- Targets 85%+ code coverage with edge cases
- Usage: `/add-tests` → Point to code needing tests

**`/refactor`** (4.7KB)
- Analyze and refactor code for better maintainability
- Applies SOLID principles and reduces complexity
- Usage: `/refactor` → Identify code to improve

**`/optimize`** (5.7KB)
- Find and fix performance bottlenecks
- Frontend (React) and backend (queries, algorithms) optimization
- Usage: `/optimize` → Describe performance issue

**`/security-scan`** (7.0KB)
- Comprehensive security vulnerability analysis
- Identifies injection, auth issues, sensitive data exposure
- Usage: `/security-scan` → Scan codebase or specific files

### Documentation

**`/add-docs`** (6.3KB)
- Generate JSDoc/TSDoc/Godoc comments and README files
- Creates comprehensive documentation with examples
- Usage: `/add-docs` → Specify what needs documentation

### Type Safety & Code Quality

**`/type-safety`** (8.6KB)
- Add/improve TypeScript types across codebase
- Eliminates `any`, adds generics, enables strict mode
- Usage: `/type-safety` → Enhance type coverage

**`/error-handling`** (16KB)
- Add comprehensive error handling and logging
- Custom errors, middleware, structured logging, monitoring
- Usage: `/error-handling` → Improve error resilience

### Database & Data

**`/database-schema`** (12KB)
- Design and generate database schema from requirements
- Includes migrations, ORM models, indexes, seed data
- Usage: `/database-schema` → Describe data model

### API & Integration

**`/api-client`** (13KB)
- Generate TypeScript SDK from OpenAPI/Swagger spec
- Type-safe client with error handling, retry logic
- Usage: `/api-client` → Provide API specification

### Infrastructure & Deployment

**`/deploy-config`** (16KB)
- Create Docker, Kubernetes, and CI/CD configurations
- Multi-stage builds, health checks, autoscaling
- Usage: `/deploy-config` → Define deployment requirements

**`/setup-storybook`** (15KB)
- Initialize Storybook with TailwindCSS integration
- Includes dark mode, a11y addon, interaction testing
- Usage: `/setup-storybook` → Set up component library

**`/setup-monorepo`** (13KB)
- Add new package/app to Nx monorepo
- Configures TypeScript paths, build targets, dependencies
- Usage: `/setup-monorepo` → Expand monorepo structure

## 💼 Business & Marketing Commands (15)

### Product Management

**`/write-prd`** (2.0KB)
- Generate comprehensive Product Requirements Document
- Includes user stories, requirements, metrics, timeline
- Usage: `/write-prd` → Describe product/feature

**`/user-personas`** (3.0KB)
- Create 3-5 detailed user personas with demographics, goals, pain points
- Usage: `/user-personas` → Define target market

**`/user-interview`** (11KB)
- Generate interview scripts with 50-75 questions
- Screening, discovery, validation, usability testing
- Usage: `/user-interview` → Specify research goals

**`/product-launch`** (11KB)
- Create detailed launch checklist and timeline (12-16 weeks)
- Covers product, marketing, sales, PR, technical readiness
- Usage: `/product-launch` → Plan product launch

**`/metrics-dashboard`** (11KB)
- Define KPIs and analytics tracking plan
- AARRR metrics, dashboards by role, event specifications
- Usage: `/metrics-dashboard` → Set up analytics

### Market Research & Strategy

**`/market-research`** (2.3KB)
- Conduct comprehensive market analysis (TAM/SAM/SOM)
- Industry trends, competitive landscape, opportunities
- Usage: `/market-research` → Research product idea

**`/competitor-analysis`** (2.5KB)
- Analyze competitors with comparison matrices
- SWOT analysis, positioning maps, strategic recommendations
- Usage: `/competitor-analysis` → Identify competitors

**`/pricing-strategy`** (2.7KB)
- Design pricing tiers and monetization strategy
- Cost analysis, value-based pricing, tier structure
- Usage: `/pricing-strategy` → Determine pricing model

### Marketing & Growth

**`/marketing-plan`** (3.8KB)
- Generate complete marketing strategy (7Ps framework)
- Channel strategy, content plan, budget allocation
- Usage: `/marketing-plan` → Create marketing strategy

**`/content-calendar`** (4.0KB)
- Create 30-90 day content calendar for blog/social
- Platform-specific strategies and repurposing plan
- Usage: `/content-calendar` → Plan content schedule

**`/seo-strategy`** (5.6KB)
- Develop SEO strategy with 50-100 keyword recommendations
- Technical SEO, content strategy, link building
- Usage: `/seo-strategy` → Optimize for search

**`/email-campaign`** (5.6KB)
- Create email marketing campaign with 5-8 email sequences
- Segmentation, personalization, deliverability optimization
- Usage: `/email-campaign` → Design email funnel

**`/landing-page-copy`** (6.3KB)
- Write high-converting landing page copy
- Headlines, features/benefits, social proof, CTAs
- Usage: `/landing-page-copy` → Create landing page

**`/growth-hacks`** (9.6KB)
- Generate 30-50 creative growth tactics
- Organized by AARRR funnel with 90-day roadmap
- Usage: `/growth-hacks` → Accelerate growth

**`/pitch-deck`** (14KB)
- Create investor or client pitch deck (15 slides)
- Storytelling framework, design guidelines, Q&A prep
- Usage: `/pitch-deck` → Prepare presentation

## 🎯 How to Use

### Basic Usage
```bash
# Simply type the command in Claude Code
/new-component

# Claude will execute the prompt and guide you through the process
```

### Best Practices

1. **Have context ready** - Know what you want to build/analyze
2. **Be specific** - Provide detailed requirements when prompted
3. **Review outputs** - Commands generate comprehensive results, review carefully
4. **Iterate** - Refine and adjust based on initial output
5. **Combine commands** - Use multiple commands in sequence for complex tasks

### Example Workflow

```bash
# Starting a new feature
/write-prd              # Define requirements
/database-schema        # Design data model
/new-api                # Create backend endpoints
/new-component          # Build frontend components
/add-tests              # Add test coverage
/security-scan          # Check for vulnerabilities
/deploy-config          # Set up deployment
/product-launch         # Plan launch strategy
```

## 📋 Command Categories

### Quick Reference

**Code Generation** (3 commands)
- `/new-component`, `/new-api`, `/microservice`

**Testing & Quality** (4 commands)
- `/add-tests`, `/refactor`, `/optimize`, `/security-scan`

**Documentation** (1 command)
- `/add-docs`

**Type Safety & Errors** (2 commands)
- `/type-safety`, `/error-handling`

**Database** (1 command)
- `/database-schema`

**API & Integration** (1 command)
- `/api-client`

**Infrastructure** (3 commands)
- `/deploy-config`, `/setup-storybook`, `/setup-monorepo`

**Product Management** (5 commands)
- `/write-prd`, `/user-personas`, `/user-interview`, `/product-launch`, `/metrics-dashboard`

**Market Research** (3 commands)
- `/market-research`, `/competitor-analysis`, `/pricing-strategy`

**Marketing & Growth** (7 commands)
- `/marketing-plan`, `/content-calendar`, `/seo-strategy`, `/email-campaign`, `/landing-page-copy`, `/growth-hacks`, `/pitch-deck`

## 🔧 Customization

Each command is a markdown file that can be edited to fit your specific needs:

1. Navigate to `.claude/commands/{command-name}.md`
2. Edit the prompt instructions
3. Add project-specific context or requirements
4. Save and use immediately

## 💡 Pro Tips

- **Chain commands** - Use output from one command as input to another
- **Create variants** - Copy and customize commands for specific use cases
- **Add your own** - Create new commands following the same markdown format
- **Version control** - Commands are just markdown files, commit them to git
- **Share with team** - Great commands can be shared across projects

## 📚 Related Resources

- **PRDs**: See `docs/prds/` for business ideas and project templates
- **Skills**: See `.claude/skills/` for specialized development expertise
- **Agents**: See `.claude/agents/` for autonomous task automation
- **Prompts**: See `docs/prompts/` for AI-assisted development templates

---

**Total Commands**: 30
**Total Size**: ~240KB
**Last Updated**: 2025-11-05
