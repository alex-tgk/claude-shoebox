# Documentation Prompts

A collection of prompt templates for generating documentation, comments, README files, and technical writing.

---

## Code Documentation

### 1. Generate Function Documentation

**Purpose:** Create comprehensive documentation for functions/methods.

**Prompt:**
```
Generate documentation for this [LANGUAGE] function:
[CODE_BLOCK]

Include:
- Purpose/description
- Parameters with types and descriptions
- Return value with type and description
- Exceptions/errors that may be thrown
- Usage examples (1-2 simple cases)
- Complexity: time and space
- Edge cases and special behaviors
- Related functions/methods
- [DOCSTRING_STYLE: JSDoc/Sphinx/Javadoc/etc]

Write clear, concise documentation suitable for API references.
```

**Example:**
```
Generate documentation for this TypeScript function:
async function fetchUserOrders(userId: string, options?: FetchOptions): Promise<Order[]>

Include:
- Purpose: What this function does
- Parameters: userId (UUID string), options (optional FetchOptions object)
- Return: Promise resolving to array of Order objects
- Throws: ValidationError, NotFoundError, NetworkError
- Examples: Basic fetch, fetch with pagination options
- Complexity: O(n) for n orders
- Edge cases: Empty results, pagination boundaries
- Related: fetchUserById, createOrder
- Use JSDoc format with TypeScript types

Write clear API documentation for TypeScript developers.
```

---

### 2. Generate Class Documentation

**Purpose:** Document classes with all their members.

**Prompt:**
```
Generate comprehensive documentation for this [LANGUAGE] class:
[CODE_BLOCK]

Documentation structure:
- Class overview and purpose
- Usage examples showing common patterns
- Constructor parameters
- Public properties with types and descriptions
- Public methods (full documentation for each)
- Events/callbacks (if applicable)
- Inheritance/interface information
- Thread safety / concurrency notes
- [DOCSTRING_STYLE]

Include class-level examples showing typical usage patterns.
```

**Example:**
```
Generate documentation for this Python UserRepository class:
[Class with methods for CRUD operations on users]

Documentation structure:
- Overview: Repository pattern for user data access
- Examples: Creating repository, fetching users, updating users
- Constructor: database_connection, cache_client
- Properties: connection_pool, cache_ttl
- Methods: create, get_by_id, update, delete, find_by_email (document each)
- No events
- Implements Repository[User] interface
- Thread-safe for reads, requires external locking for writes
- Google-style docstrings

Include example showing initialization and common operations.
```

---

### 3. Add Inline Code Comments

**Purpose:** Add helpful inline comments to complex code.

**Prompt:**
```
Add clear, helpful inline comments to this code:
[CODE_BLOCK]

Comment guidelines:
- Explain WHY, not WHAT (code shows what)
- Comment complex logic and non-obvious decisions
- Explain algorithms and mathematical operations
- Document assumptions and constraints
- Highlight potential gotchas or edge cases
- Keep comments concise and up-to-date with code
- Use [COMMENT_STYLE]
- Avoid obvious comments

Focus on helping future developers understand the reasoning.
```

**Example:**
```
Add clear, helpful inline comments to this code:
[Complex algorithm for calculating shipping costs with multiple conditions]

Comment guidelines:
- Explain the business logic behind shipping tiers
- Why certain weight/distance thresholds were chosen
- Complex calculations (explain the formula)
- Document assumption: prices in cents to avoid float errors
- Highlight: international shipping requires different calculation
- Keep concise, one line per complex step
- Use // for single-line comments
- Don't comment obvious things like variable assignments

Help future developers understand the shipping logic and business rules.
```

---

## API Documentation

### 4. Generate API Endpoint Documentation

**Purpose:** Document REST API endpoints.

**Prompt:**
```
Generate API documentation for [ENDPOINT]:

Endpoint details:
- Method: [GET/POST/PUT/DELETE/PATCH]
- Path: [URL_PATH]
- Purpose: [DESCRIPTION]

Document:
- Endpoint description
- Authentication requirements
- Path parameters
- Query parameters
- Request body schema
- Response schema (success cases)
- Error responses with status codes
- Example requests (curl, JS, etc.)
- Example responses
- Rate limiting
- Related endpoints

Format: [OPENAPI/MARKDOWN/CUSTOM]
```

**Example:**
```
Generate API documentation for user creation endpoint:

Endpoint:
- Method: POST
- Path: /api/v1/users
- Purpose: Create a new user account

Document:
- Description: Registers new user with email and password
- Authentication: None required (public endpoint)
- No path parameters
- No query parameters
- Request body: { email, password, firstName, lastName }
- Response 201: { user: {id, email, firstName, lastName}, token }
- Errors: 400 (validation), 409 (duplicate email), 500 (server)
- Examples: curl and JavaScript fetch()
- Response examples for success and error cases
- Rate limit: 5 requests/minute per IP
- Related: POST /api/v1/auth/login, GET /api/v1/users/:id

Format as Markdown for docs site.
```

---

### 5. Generate GraphQL Schema Documentation

**Purpose:** Document GraphQL types and operations.

**Prompt:**
```
Generate documentation for GraphQL schema:
[SCHEMA_DEFINITION]

Document:
- Type descriptions for all types
- Field descriptions
- Argument descriptions with validation rules
- Enum values
- Interface/union usage
- Queries: purpose, arguments, return types
- Mutations: purpose, arguments, return types, side effects
- Subscriptions: purpose, events
- Example queries and mutations
- Error handling approach
- Pagination strategy
- Authentication/authorization notes

Use GraphQL description syntax and include examples.
```

**Example:**
```
Generate documentation for User and Post types:
[Schema with User, Post types, userById query, createPost mutation]

Document:
- User type: Represents user account with profile
- Fields: id (unique), email (unique), posts (related posts)
- Post type: User-generated content
- userById query: Fetch user by ID, null if not found
- Arguments: id (required UUID)
- createPost mutation: Create new post
- Arguments: title (max 200), content (required), userId
- Returns: Created post or validation errors
- No subscriptions
- Example: Query user with posts, create post mutation
- Errors: Return null or specific error type
- Pagination: Cursor-based on posts connection
- Auth: Mutations require valid JWT token

Use """ description strings in schema and provide example queries.
```

---

## Project Documentation

### 6. Generate README File

**Purpose:** Create comprehensive README for a project.

**Prompt:**
```
Generate a README.md for [PROJECT_NAME]:

Project details:
- Type: [LIBRARY/APPLICATION/TOOL]
- Purpose: [WHAT_IT_DOES]
- Tech stack: [TECHNOLOGIES]
- Target users: [DEVELOPERS/END_USERS]

Include sections:
- Project title and description
- Badges (build status, coverage, version, etc.)
- Key features
- Installation instructions
- Quick start / usage examples
- Configuration options
- API documentation link
- Contributing guidelines link
- Testing instructions
- Deployment guide link
- License
- Credits/acknowledgments

Write in engaging, clear language. Use proper markdown formatting.
```

**Example:**
```
Generate a README.md for FastAPI microservice template:

Project:
- Type: Application template/boilerplate
- Purpose: Production-ready FastAPI microservice with best practices
- Tech: Python 3.11, FastAPI, PostgreSQL, Docker, pytest
- Target: Backend developers building microservices

Include:
- Title: FastAPI Production Template
- Description: What problems it solves
- Badges: Build status, coverage, Python version
- Features: Auth, database, tests, Docker, CI/CD setup
- Installation: Clone, Docker Compose up, or pip install
- Quick start: Run server, hit /docs endpoint
- Configuration: Environment variables, config files
- API docs: Link to OpenAPI docs at /docs
- Contributing: Link to CONTRIBUTING.md
- Testing: pytest commands, coverage
- Deployment: Docker deployment guide link
- License: MIT
- Credits: Libraries and inspirations

Make it welcoming for new contributors, clear for quick setup.
```

---

### 7. Generate CONTRIBUTING Guide

**Purpose:** Create contribution guidelines.

**Prompt:**
```
Generate CONTRIBUTING.md for [PROJECT]:

Project context:
- Type: [OPEN_SOURCE/INTERNAL]
- Tech stack: [TECHNOLOGIES]
- Team size: [SIZE]
- Development workflow: [WORKFLOW]

Include:
- Welcome message
- Code of conduct reference
- Ways to contribute (code, docs, issues, etc.)
- Development setup instructions
- Coding standards and style guide
- Branch naming conventions
- Commit message format
- Pull request process
- Testing requirements
- Documentation requirements
- Review process and timelines
- Issue reporting guidelines
- Recognition for contributors

Make it welcoming and clear about expectations.
```

**Example:**
```
Generate CONTRIBUTING.md for open-source React component library:

Project:
- Type: Open source, accepting contributions
- Tech: React, TypeScript, Storybook, Jest
- Team: 3 core maintainers + community
- Workflow: Fork, feature branch, PR with review

Include:
- Warm welcome to new contributors
- Link to CODE_OF_CONDUCT.md
- Ways to help: new components, bug fixes, docs, examples, issues
- Setup: Fork, clone, npm install, npm start
- Standards: TypeScript strict, ESLint rules, Prettier
- Branches: feature/component-name, fix/issue-description
- Commits: Conventional commits (feat:, fix:, docs:)
- PR: Fill template, link issue, request review
- Tests: 80% coverage required, Storybook stories for components
- Docs: JSDoc for props, README updates
- Review: Within 48 hours, 2 approvals needed
- Issues: Use templates, provide reproduction
- Contributors listed in README, swag for major contributions

Friendly tone, encourage first-time contributors.
```

---

### 8. Generate Changelog

**Purpose:** Create or update a changelog file.

**Prompt:**
```
Generate/update CHANGELOG.md for [PROJECT]:

Recent changes:
[LIST_OF_CHANGES_OR_GIT_LOG]

Format:
- Follow Keep a Changelog format
- Version: [VERSION_NUMBER]
- Release date: [DATE]
- Categories:
  - Added: New features
  - Changed: Changes to existing features
  - Deprecated: Soon-to-be removed features
  - Removed: Removed features
  - Fixed: Bug fixes
  - Security: Security fixes

For each item:
- User-facing description (not technical internals)
- Link to issue/PR
- Breaking changes clearly marked
- Migration guide for breaking changes

Write for end users, not just developers.
```

**Example:**
```
Update CHANGELOG.md for version 2.0.0 of authentication library:

Recent changes:
- Switched to JWT from session cookies (breaking)
- Added MFA support with TOTP
- Fixed token refresh race condition
- Removed deprecated loginWithUsername (breaking)
- Improved error messages
- Updated dependencies

Format:
- Keep a Changelog style
- Version 2.0.0
- Date: 2024-01-15

Group as:
- Added: MFA with TOTP authenticator support (#123)
- Changed: [BREAKING] JWT tokens replace session cookies (#124) - see migration guide
- Removed: [BREAKING] Deprecated loginWithUsername method (#125)
- Fixed: Race condition in token refresh (#126)
- Security: Updated jsonwebtoken to 9.0.0 (#127)

Include migration guide section for breaking changes.
Write so users understand impact without reading code.
```

---

## Technical Documentation

### 9. Generate Architecture Documentation

**Purpose:** Document system architecture.

**Prompt:**
```
Generate architecture documentation for [SYSTEM]:

System overview:
[DESCRIPTION]

Document:
- Architecture overview (high-level)
- Component diagram description
- Key components and responsibilities
- Data flow through system
- Technology stack rationale
- Design patterns used
- Scalability considerations
- Security architecture
- Deployment architecture
- Integration points
- Trade-offs and alternatives considered
- Future considerations
- Diagrams: [INCLUDE_DESCRIPTIONS]

Write for technical audience (developers, architects).
```

**Example:**
```
Generate architecture documentation for microservices e-commerce platform:

System:
Product catalog, shopping cart, orders, payments, inventory services

Document:
- Overview: Event-driven microservices with API gateway
- Component diagram: 5 services + gateway + message broker
- Components: Each service's purpose and boundaries
- Data flow: User request → Gateway → Services → Events
- Stack: Node.js, PostgreSQL per service, RabbitMQ, Redis
- Patterns: CQRS for orders, saga for distributed transactions
- Scalability: Horizontal scaling, stateless services, caching
- Security: OAuth at gateway, service-to-service JWT, encrypted events
- Deployment: Kubernetes, service mesh for communication
- Integrations: Payment gateway API, shipping providers
- Trade-offs: Eventual consistency vs complexity
- Future: Add recommendation service, move to event sourcing
- Include descriptions of: architecture diagram, service map, data flow

Write for new team members and external architects.
```

---

### 10. Generate Database Schema Documentation

**Purpose:** Document database schema and design.

**Prompt:**
```
Generate database schema documentation:

Schema:
[DDL_STATEMENTS or DESCRIPTION]

Document:
- Database overview and purpose
- Entity-Relationship description
- Table descriptions with purpose
- Column details (type, nullable, defaults, constraints)
- Relationships and foreign keys
- Indexes and their purpose
- Triggers and stored procedures
- Data integrity rules
- Partitioning strategy (if any)
- Migration history approach
- Sample queries for common operations
- Diagram description

Format as [MARKDOWN/DBML/SQL_COMMENTS]
```

**Example:**
```
Generate schema documentation for e-commerce database:

Schema:
Users, Products, Orders, OrderItems, Reviews tables with relationships

Document:
- Overview: E-commerce transactional database, PostgreSQL
- ER: Users ←→ Orders ←→ OrderItems → Products, Users → Reviews → Products
- Tables:
  - Users: Customer accounts (id, email unique, password_hash, created_at)
  - Products: Catalog (id, name, description, price decimal, stock int)
  - Orders: Purchase records (id, user_id FK, status, total, created_at)
  - OrderItems: Line items (order_id FK, product_id FK, quantity, price)
  - Reviews: Product reviews (user_id FK, product_id FK, rating 1-5, comment)
- Indexes: email unique, product_id on orderitems, created_at on orders
- No triggers, using application logic
- Constraints: Positive prices, valid status enum, ratings 1-5
- Partitioning: orders by created_at (monthly) for performance
- Migrations: Numbered migration files with up/down
- Sample: Get user orders with items, calculate product rating

Format as Markdown with table sections.
```

---

## User Documentation

### 11. Generate User Guide

**Purpose:** Create end-user documentation.

**Prompt:**
```
Generate user guide for [FEATURE/PRODUCT]:

Target audience: [USER_TYPE]
Feature overview: [DESCRIPTION]

Include:
- Introduction: What is it and why use it
- Prerequisites / requirements
- Step-by-step tutorials for common tasks
- Screenshots/diagrams descriptions
- Tips and best practices
- Troubleshooting common issues
- FAQ section
- Glossary of terms
- Video tutorial links (if available)
- Support contact information

Write in clear, non-technical language. Use second person (you).
```

**Example:**
```
Generate user guide for multi-factor authentication feature:

Target audience: Non-technical end users
Feature: Setting up and using MFA for account security

Include:
- Intro: What MFA is, why it makes account more secure
- Prerequisites: Have smartphone with authenticator app
- Tutorials:
  1. Enable MFA on your account (step by step)
  2. Scan QR code with authenticator app
  3. Enter verification code
  4. Save backup codes
  5. Login with MFA code
- Screenshots: Settings page, QR code screen, code entry
- Tips: Use backup codes safely, recommended apps
- Troubleshooting: Lost phone, codes not working, time sync issues
- FAQ: Can I disable MFA? What if I lose backup codes?
- Glossary: MFA, TOTP, authenticator app, backup codes
- Video: Link to 2-minute setup video
- Support: security@company.com for MFA issues

Use simple language, assume no technical knowledge.
```

---

### 12. Generate Tutorial

**Purpose:** Create step-by-step tutorial.

**Prompt:**
```
Create a tutorial for [TASK]:

Tutorial details:
- Goal: [WHAT_USER_WILL_ACCOMPLISH]
- Audience: [SKILL_LEVEL]
- Prerequisites: [REQUIRED_KNOWLEDGE/TOOLS]
- Estimated time: [DURATION]

Structure:
- Introduction: What they'll learn and build
- Prerequisites list
- Step-by-step instructions (numbered)
- Code snippets or examples for each step
- Expected output/result after each major step
- Explanations of WHY, not just HOW
- Common mistakes to avoid
- Next steps / further learning
- Complete code/project link

Make it easy to follow, test each step works.
```

**Example:**
```
Create tutorial: "Build a REST API with Express.js and PostgreSQL"

Goal: Working API with CRUD operations for blog posts
Audience: Intermediate JavaScript developers
Prerequisites: Node.js installed, basic SQL knowledge, Postman or curl
Time: 60 minutes

Structure:
- Intro: You'll build a blog post API with database persistence
- Prerequisites: Node 18+, PostgreSQL 14+, code editor
- Steps:
  1. Initialize Node project (npm init, install packages)
  2. Set up Express server
  3. Configure PostgreSQL connection
  4. Create database schema
  5. Implement GET /posts endpoint
  6. Implement POST /posts endpoint
  7. Add validation middleware
  8. Test with Postman (expected responses)
  9. Add error handling
  10. Deploy to Heroku
- Explanations: Why connection pooling, why validation matters
- Common mistakes: Forgetting error handling, SQL injection risks
- Next: Add authentication, pagination, unit tests
- Complete code: GitHub repo link

Test every step yourself before publishing.
```

---

## Comment Quality

### 13. Improve Code Comments

**Purpose:** Review and improve existing comments.

**Prompt:**
```
Review and improve comments in this code:
[CODE_WITH_COMMENTS]

Evaluate comments for:
- Accuracy (do they match the code?)
- Usefulness (explain WHY, not WHAT)
- Clarity (easy to understand?)
- Completeness (missing important context?)
- Conciseness (too verbose?)
- Outdated (need updates?)

Provide:
- Comments to remove (obvious/outdated)
- Comments to improve (rewritten versions)
- Missing comments to add
- General comment quality feedback

Follow [COMMENT_STYLE_GUIDE].
```

**Example:**
```
Review and improve comments in this user service code:
[Code with mix of good and poor comments]

Evaluate:
- Accuracy: Comment says "returns user" but function returns Promise<User>
- Usefulness: Comment "i++" doesn't help, need WHY we iterate
- Clarity: Comment "handles edge cases" - which ones?
- Completeness: No comment on why we retry 3 times
- Conciseness: Comment spans 10 lines for simple validation
- Outdated: References old field name "userName" (now "email")

Provide:
- Remove: Obvious comments like "increment i"
- Improve: "Retries 3 times because API is flaky" vs "Retry logic"
- Add: Explain business rule for user validation
- Feedback: 60% comments are obvious, need more architecture explanations

Use JSDoc style, focus on business logic and architectural decisions.
```

---

### 14. Generate Code Examples

**Purpose:** Create code examples for documentation.

**Prompt:**
```
Generate code examples for [LIBRARY/API/FEATURE]:

Documentation context:
[API/FEATURE_DESCRIPTION]

Create examples for:
- Basic usage (simplest case)
- Common use cases (2-3 scenarios)
- Advanced usage (complex scenario)
- Error handling
- Edge cases
- Best practices demonstration
- Anti-patterns (what NOT to do)

For each example provide:
- Description of what it demonstrates
- Complete, runnable code
- Expected output/behavior
- Explanatory comments
- Language: [PROGRAMMING_LANGUAGE]

Examples should be realistic and useful.
```

**Example:**
```
Generate code examples for React useQuery hook documentation:

Context:
Custom hook for data fetching with loading, error, and caching

Examples for:
- Basic: Fetch user data on component mount
- Common: Fetch with parameters, refetch on button click, paginated list
- Advanced: Dependent queries, optimistic updates
- Error: Handle network errors, display error message
- Edge: Empty results, stale data handling
- Best practices: Use query keys properly, handle loading states
- Anti-patterns: Don't fetch in useEffect, don't ignore errors

For each:
- "Example: Fetching user profile data"
- TypeScript code with full component
- "Displays loading spinner, then user name, or error message"
- Comments explaining key parts
- Language: TypeScript/React

Make examples copy-pasteable and realistic (not foo/bar examples).
```

---

### 15. Generate Error Message Documentation

**Purpose:** Document error codes and messages.

**Prompt:**
```
Generate error documentation for [SYSTEM/API]:

Errors to document:
[ERROR_LIST or ERROR_CODE_DEFINITIONS]

For each error include:
- Error code/name
- HTTP status code (if API)
- Error message (user-facing)
- Description (technical details)
- Cause (why this error occurs)
- Resolution (how to fix)
- Example scenario
- Related errors
- Severity (warning/error/critical)

Format as [MARKDOWN_TABLE/DETAILED_SECTIONS]

Make error messages actionable for developers.
```

**Example:**
```
Generate error documentation for payment processing API:

Errors:
INVALID_CARD, INSUFFICIENT_FUNDS, PAYMENT_DECLINED, EXPIRED_CARD, RATE_LIMIT_EXCEEDED

For each:
- Error code: INSUFFICIENT_FUNDS
- Status: 402 Payment Required
- Message: "Payment failed: insufficient funds"
- Description: Customer's account balance too low for transaction
- Cause: Bank declined due to insufficient balance in account
- Resolution: Ask customer to use different payment method or add funds
- Example: Purchase $100 with $50 available
- Related: PAYMENT_DECLINED (generic decline)
- Severity: Error (expected, not system failure)

Format as markdown table with expandable details sections.

Make it clear what developers should do when they encounter each error.
```

---

## Additional Resources

- **Related:** See [prompt-engineering-guide.md](./prompt-engineering-guide.md) for writing effective documentation prompts
- **Code:** See [coding-prompts.md](./coding-prompts.md) for code that needs documentation
- **API Design:** See [architecture-prompts.md](./architecture-prompts.md) for API architecture
