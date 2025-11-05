# AI-Assisted Development Prompt Library

This directory contains 150+ prompt templates for AI-assisted development across all phases of the software development lifecycle.

## 📊 Overview

- **Total Files**: 9 (8 category files + 1 guide)
- **Total Prompts**: 150+
- **Total Lines**: 10,565
- **Total Size**: 290KB
- **Coverage**: Coding, architecture, testing, docs, business, UI/UX, data, DevOps

## 📚 Prompt Categories

### 1. **coding-prompts.md** (25+ prompts, 1,043 lines)

Prompts for code generation, refactoring, and debugging.

**Sample Topics**:
- Generate functions from specifications
- Refactor code for better structure
- Debug and fix issues
- Optimize algorithms and data structures
- Add error handling and logging
- Security audit and vulnerability fixes
- Code review and improvement suggestions
- Convert between languages/frameworks

**Example Prompt**:
```
Generate a [LANGUAGE] function called [FUNCTION_NAME] that:
- Takes [INPUT_PARAMETERS] as parameters
- Returns [RETURN_TYPE]
- [SPECIFIC_FUNCTIONALITY]
- Handles edge cases: [EDGE_CASES]
- Follows [STYLE_GUIDE] conventions
```

---

### 2. **architecture-prompts.md** (15+ prompts, 882 lines)

Prompts for system design and architecture decisions.

**Sample Topics**:
- Design system architecture
- Microservices decomposition
- Database architecture design
- API design and contracts
- Technology stack selection
- Scalability and performance planning
- Security architecture
- Architecture Decision Records (ADRs)

**Example Prompt**:
```
Design a system architecture for [APPLICATION_NAME]:
- Scale: [EXPECTED_USERS/LOAD]
- Key features: [MAIN_FEATURES]
- Performance requirements: [LATENCY/THROUGHPUT]

Provide:
- Component breakdown with responsibilities
- Technology stack recommendations
- Scalability strategy
- Trade-offs and alternatives considered
```

---

### 3. **testing-prompts.md** (15+ prompts, 828 lines)

Prompts for test generation and test strategy.

**Sample Topics**:
- Generate unit tests
- Create integration tests
- E2E test scenarios
- Load and performance testing
- Security testing
- Accessibility testing
- Test strategy and planning
- Mocking and test data generation

**Example Prompt**:
```
Generate unit tests for this [LANGUAGE] code:
[CODE_BLOCK]

Test requirements:
- Testing framework: [JEST/PYTEST/JUNIT]
- Coverage target: [PERCENTAGE]
- Test cases: Happy path, edge cases, error conditions
- Mock dependencies: [DEPENDENCIES_TO_MOCK]

Organize tests with clear descriptions using AAA pattern.
```

---

### 4. **documentation-prompts.md** (15+ prompts, 833 lines)

Prompts for docs, comments, and technical writing.

**Sample Topics**:
- Function documentation (JSDoc, TSDoc, Godoc)
- API endpoint documentation
- README file generation
- Inline code comments
- Architecture documentation
- User guides and tutorials
- Change logs and release notes
- API reference docs

**Example Prompt**:
```
Generate documentation for this [LANGUAGE] function:
[CODE_BLOCK]

Include:
- Purpose/description
- Parameters with types and descriptions
- Return value with type
- Usage examples (1-2 simple cases)
- [DOCSTRING_STYLE: JSDoc/Sphinx/Javadoc]
```

---

### 5. **business-prompts.md** (20+ prompts, 1,213 lines)

Prompts for PRDs, marketing, and business strategy.

**Sample Topics**:
- Product Requirements Documents (PRDs)
- Competitive analysis
- Go-to-market strategy
- Customer journey mapping
- Value proposition design
- Business model canvas
- Market sizing and TAM/SAM/SOM
- Pricing strategy
- Feature prioritization

**Example Prompt**:
```
Create a Product Requirements Document for [FEATURE_NAME]:
- Target users: [USER_SEGMENTS]
- Business goal: [OBJECTIVE]
- Success metrics: [KPIS]

Include:
- Problem Statement
- User Stories and Use Cases
- Functional & Non-Functional Requirements
- Timeline and Milestones
```

---

### 6. **ui-ux-prompts.md** (15+ prompts, 1,678 lines)

Prompts for design, UX, and component creation.

**Sample Topics**:
- Component specifications
- User flow design
- Responsive layout strategy
- Design tokens definition
- Accessibility requirements
- Wireframes and mockups
- Design system creation
- Interaction patterns
- Usability improvements

**Example Prompt**:
```
Create a component specification for [COMPONENT_NAME]:

Include:
- Visual design description
- States (default, hover, focus, disabled, loading, error)
- Variants (sizes, styles, themes)
- Props/attributes and their types
- Accessibility requirements (ARIA, keyboard navigation)
- Responsive considerations
```

---

### 7. **data-prompts.md** (15+ prompts, 1,375 lines)

Prompts for data analysis, SQL, and database design.

**Sample Topics**:
- Generate SQL queries
- Optimize slow queries
- Database schema design
- Data migration scripts
- Exploratory data analysis
- Data visualization
- ETL pipeline design
- Data modeling

**Example Prompt**:
```
Write a SQL query for [DATABASE_TYPE]:
- Goal: [WHAT_YOU_WANT_TO_RETRIEVE]
- Tables: [TABLE_NAMES_AND_SCHEMAS]
- Conditions: [FILTERS_AND_CRITERIA]

Provide:
- SQL query (formatted and commented)
- Explanation of key parts
- Performance considerations
- Indexes needed for optimization
```

---

### 8. **devops-prompts.md** (15+ prompts, 1,893 lines)

Prompts for CI/CD, deployment, and infrastructure.

**Sample Topics**:
- CI/CD pipeline generation
- Deployment strategies (blue-green, canary)
- Terraform/IaC configuration
- Docker and Kubernetes setup
- Monitoring and alerting
- Logging infrastructure
- Backup and disaster recovery
- Security hardening

**Example Prompt**:
```
Create a CI/CD pipeline for [PROJECT]:
- Tech stack: [LANGUAGES/FRAMEWORKS]
- CI/CD platform: [GITHUB_ACTIONS/JENKINS]

Pipeline stages:
- Build, Test, Security scans, Deploy
- Trigger on: [PUSH/PR/TAG]
- Deployment strategy: [BLUE_GREEN/CANARY/ROLLING]

Provide complete pipeline configuration with comments.
```

---

### 9. **prompt-engineering-guide.md** (820 lines)

Comprehensive guide on writing effective prompts for AI coding assistants.

**Contents**:
- **Core Principles**: Be specific, provide context, define success criteria
- **Prompt Structure**: Templates and frameworks
- **Best Practices**: Tech stack specification, code style, testing
- **Common Patterns**: Generation, review, debugging, architecture
- **Anti-Patterns to Avoid**: Vague requests, missing context
- **Domain-Specific Tips**: Frontend, backend, data/ML, DevOps
- **Advanced Techniques**: Chain-of-thought, few-shot learning, role-based prompting

---

## 🎯 How to Use This Library

### 1. Find the Right Category

Identify which category matches your task:
- **Code task?** → `coding-prompts.md`
- **Architecture decision?** → `architecture-prompts.md`
- **Need tests?** → `testing-prompts.md`
- **Writing docs?** → `documentation-prompts.md`
- **Business planning?** → `business-prompts.md`
- **UI/UX design?** → `ui-ux-prompts.md`
- **Data/database work?** → `data-prompts.md`
- **Deployment/infra?** → `devops-prompts.md`

### 2. Browse Prompts in That Category

Each file is organized with:
- Clear headings for each prompt
- Detailed prompt templates
- Example usage
- Expected outputs

### 3. Copy and Customize

1. Copy the prompt template
2. Replace `[PLACEHOLDERS]` with your specifics
3. Paste into your AI assistant (Claude, ChatGPT, etc.)
4. Get high-quality results

### 4. Iterate and Refine

- Review the output
- Adjust the prompt if needed
- Build a library of your own refined prompts

## 💡 Prompt Engineering Tips

### Make Prompts Specific

❌ **Vague**: "Write a function for users"

✅ **Specific**: "Write a TypeScript function that validates user email addresses using regex, returns boolean, handles edge cases like invalid formats and empty strings"

### Provide Context

Include:
- **Tech stack** (languages, frameworks)
- **Coding style** (functional, OOP, conventions)
- **Constraints** (performance, security, compatibility)
- **Success criteria** (what defines a good result)

### Use Examples

Show the AI what you want:
```
Generate API endpoints following this pattern:

Example:
GET /api/users/:id
Returns: { id, name, email, createdAt }
Status: 200 (success), 404 (not found)

Now create endpoints for [RESOURCE]...
```

### Request Explanations

Ask for:
- **Why** certain decisions were made
- **Trade-offs** considered
- **Alternatives** available
- **Best practices** followed

### Iterate Incrementally

Start simple, then enhance:
1. "Create basic component"
2. "Add error handling"
3. "Add loading states"
4. "Add accessibility features"

## 🔧 Customization

### Creating Your Own Prompts

1. **Start with a template** from this library
2. **Customize** for your project/team
3. **Test** with your AI assistant
4. **Refine** based on results
5. **Document** successful prompts
6. **Share** with your team

### Building a Team Library

```
/docs/prompts/
  ├── coding-prompts.md          (from this library)
  ├── custom-react-prompts.md    (your team's React patterns)
  ├── custom-go-prompts.md       (your Go service patterns)
  └── custom-domain-prompts.md   (domain-specific prompts)
```

## 📊 Prompt Effectiveness

### High-Quality Prompts Have:

✅ **Clear objective** - What you want to achieve
✅ **Specific constraints** - Tech stack, style, requirements
✅ **Context** - Relevant background information
✅ **Examples** - Show what you want
✅ **Success criteria** - How to measure success
✅ **Output format** - Structure of expected result

### Low-Quality Prompts Lack:

❌ Specificity - Too vague or general
❌ Context - Missing background information
❌ Constraints - No technical requirements
❌ Examples - No guidance on expected output

## 🎓 Learning Resources

### Read First
Start with `prompt-engineering-guide.md` for foundational principles

### Practice
Use prompts from this library and observe results

### Iterate
Refine prompts based on what works

### Share
Contribute successful prompts back to the library

## 📚 Related Resources

- **Slash Commands**: See `.claude/commands/` for pre-built executable commands
- **Skills**: See `.claude/skills/` for specialized domain expertise
- **Agents**: See `.claude/agents/` for autonomous task automation
- **PRDs**: See `docs/prds/` for business project templates

## 🚀 Advanced Usage

### Chaining Prompts

Combine multiple prompts for complex tasks:

```
1. Use architecture-prompts.md → Design system
2. Use coding-prompts.md → Implement components
3. Use testing-prompts.md → Add test coverage
4. Use documentation-prompts.md → Document code
5. Use devops-prompts.md → Deploy to production
```

### Prompt Templates for Your Domain

Create specialized templates:

```markdown
# E-Commerce Checkout Flow

Generate a checkout flow for [PLATFORM]:
- Payment methods: [STRIPE/PAYPAL/etc]
- Shipping: [CALCULATION_METHOD]
- Tax: [TAX_RULES]

Include:
- Cart review step
- Address validation
- Payment processing
- Order confirmation
- Error handling for each step
```

### AI Pair Programming

Use prompts conversationally:

```
You: [Use coding-prompts.md] "Generate authentication service"
AI: [Generates code]
You: [Use testing-prompts.md] "Add tests for this"
AI: [Generates tests]
You: [Use documentation-prompts.md] "Document the API"
AI: [Generates docs]
```

---

## 📈 Prompt Library Statistics

| Category | Prompts | Lines | Size | Focus Area |
|----------|---------|-------|------|------------|
| Coding | 25+ | 1,043 | 25KB | Implementation |
| Architecture | 15+ | 882 | 26KB | Design |
| Testing | 15+ | 828 | 23KB | Quality |
| Documentation | 15+ | 833 | 23KB | Communication |
| Business | 20+ | 1,213 | 37KB | Strategy |
| UI/UX | 15+ | 1,678 | 46KB | Design |
| Data | 15+ | 1,375 | 41KB | Data Engineering |
| DevOps | 15+ | 1,893 | 46KB | Operations |
| **Total** | **150+** | **10,565** | **290KB** | **Full SDLC** |

---

**Last Updated**: 2025-11-05
**Format**: Markdown with placeholder-based templates
**Compatibility**: Claude, ChatGPT, GitHub Copilot, and other AI assistants
