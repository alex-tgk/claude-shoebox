# Prompt Engineering Guide for AI Coding Assistants

A comprehensive guide to writing effective prompts for AI-assisted software development.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Core Principles](#core-principles)
3. [Prompt Structure](#prompt-structure)
4. [Best Practices](#best-practices)
5. [Common Patterns](#common-patterns)
6. [Anti-Patterns to Avoid](#anti-patterns-to-avoid)
7. [Domain-Specific Tips](#domain-specific-tips)
8. [Advanced Techniques](#advanced-techniques)
9. [Examples](#examples)

---

## Introduction

AI coding assistants like Claude, GitHub Copilot, and ChatGPT can significantly accelerate development when prompted effectively. This guide provides actionable techniques for crafting prompts that generate high-quality, production-ready code.

**Key Benefits of Good Prompting:**
- Faster development with fewer iterations
- More accurate and relevant code
- Better documentation and explanations
- Reduced cognitive load on developers
- Consistent code quality

---

## Core Principles

### 1. Be Specific and Clear

**Poor:** "Write a function for users"
**Better:** "Write a TypeScript function that validates user email addresses using regex, returns boolean"

**Why it matters:** Specificity reduces ambiguity and gives the AI precise constraints to work within.

### 2. Provide Context

**Poor:** "Add error handling"
**Better:** "Add error handling to this Express.js API endpoint. Use try-catch for async operations, return 400 for validation errors, 500 for server errors, and log errors with Winston."

**Why it matters:** Context helps the AI understand your environment, tech stack, and coding standards.

### 3. Define Success Criteria

**Poor:** "Make it better"
**Better:** "Refactor this function to: (1) reduce cyclomatic complexity from 15 to under 10, (2) improve readability with descriptive variable names, (3) add JSDoc comments"

**Why it matters:** Clear success criteria ensure you get what you actually need.

### 4. Use Examples

**Poor:** "Format the output"
**Better:** "Format the output like this example:
```json
{
  \"name\": \"John Doe\",
  \"email\": \"john@example.com\"
}
```
Include name and email fields, use camelCase."

**Why it matters:** Examples eliminate ambiguity about format, style, and structure.

### 5. Iterate and Refine

**Strategy:** Start broad, then narrow down
1. First prompt: General direction
2. Second prompt: Add constraints
3. Third prompt: Refine edge cases

**Why it matters:** Complex requirements are often better achieved through conversation than a single massive prompt.

---

## Prompt Structure

### Template: The Five W's + How

```
WHAT: [What you want the AI to create]
WHY: [The purpose or problem it solves]
WHERE: [The context - file, system, architecture]
WHO: [Target audience - developers, users, etc.]
WHEN: [When it runs - build time, runtime, on event]
HOW: [Specific implementation details, constraints]
```

**Example:**
```
WHAT: Create a React custom hook for debouncing user input
WHY: To reduce API calls when users type in a search box
WHERE: React 18 application, hooks are in src/hooks/
WHO: Used by frontend developers on the team
WHEN: Runs during user input, debounces for 300ms
HOW: Use useRef for timeout, useEffect for cleanup, TypeScript typed
```

### Template: Request-Context-Requirements-Output (RCRO)

```
REQUEST: [Clear statement of what you need]

CONTEXT:
- Technology: [Stack, frameworks, versions]
- Current situation: [What exists now]
- Constraints: [Limitations, requirements]

REQUIREMENTS:
- Functional: [What it must do]
- Non-functional: [Performance, security, etc.]
- Style: [Code standards, patterns]

OUTPUT:
- Format: [Code, documentation, both]
- Details to include: [Examples, tests, comments]
```

**Example:**
```
REQUEST: Generate a database migration to add full-text search

CONTEXT:
- Technology: PostgreSQL 14, Node.js with Knex migrations
- Current: users table exists with name, email, bio fields
- Constraints: Can't drop table, must be reversible

REQUIREMENTS:
- Functional: Add tsvector column, update trigger, GIN index
- Non-functional: Migration must complete in <30s on 1M rows
- Style: Knex.js syntax, use raw SQL for PostgreSQL-specific features

OUTPUT:
- Migration file (up and down methods)
- Inline comments explaining each step
- SQL for testing the search functionality
```

---

## Best Practices

### 1. Specify Technology Stack Explicitly

**Poor:** "Create a REST API"
**Good:** "Create a REST API using Node.js 18, Express 4.x, TypeScript 5.0, following RESTful conventions"

**Benefit:** Ensures code uses correct syntax, APIs, and patterns for your stack.

### 2. Include Code Style Preferences

**Techniques:**
- Reference style guides: "Follow Airbnb JavaScript Style Guide"
- Specify formatters: "Use Prettier with single quotes, 2-space indent"
- Show examples: "Use this pattern: [example code]"

**Example:**
```
Generate a Python class following these style rules:
- Google Python Style Guide
- Type hints for all functions
- Docstrings in Google format
- Max line length 100 characters
- Use dataclasses where appropriate
```

### 3. Request Tests Alongside Code

**Pattern:**
```
Generate [COMPONENT] with:
1. Implementation
2. Unit tests (Jest, 80%+ coverage)
3. Example usage
4. Edge cases handled: [list cases]
```

**Benefit:** Ensures code is testable and catches edge cases early.

### 4. Ask for Explanations

**Techniques:**
- "Explain your approach before writing code"
- "Comment key decisions inline"
- "Provide a summary of how this works"

**Example:**
"Optimize this SQL query. First explain the bottlenecks you identify, then provide the optimized version with comments explaining each optimization."

### 5. Use Placeholders for Variable Parts

**Pattern:**
```
Create [TYPE] for [FEATURE]:
- Name: [NAME]
- Inputs: [INPUTS]
- Outputs: [OUTPUTS]
- Framework: [FRAMEWORK]
```

**Benefit:** Makes prompts reusable across similar tasks.

### 6. Specify Error Handling Requirements

**Example:**
```
Add error handling:
- Use try-catch for async operations
- Validate inputs, throw ValidationError for invalid data
- Return HTTP 400 for client errors, 500 for server errors
- Log errors with correlation ID
- Don't expose stack traces to clients
```

### 7. Request Performance Considerations

**Example:**
```
Implement data fetching with these performance requirements:
- Use caching (Redis, 5-minute TTL)
- Batch database queries (use DataLoader pattern)
- Target: p95 latency < 100ms
- Handle 1000 concurrent requests
```

### 8. Define Security Requirements

**Example:**
```
Generate authentication middleware:
- Validate JWT tokens
- Check token expiration
- Verify signature using RS256
- Extract user claims
- Handle malformed tokens gracefully (return 401, don't crash)
- Rate limit: 100 requests/minute per IP
- OWASP best practices
```

---

## Common Patterns

### Pattern 1: Code Generation

```
Generate [LANGUAGE] [TYPE] for [PURPOSE]:

Specifications:
- [SPEC_1]
- [SPEC_2]
- [SPEC_3]

Include:
- Main implementation
- Type definitions (if applicable)
- Usage example
- Edge case handling

Follow [STYLE_GUIDE] conventions.
```

### Pattern 2: Code Review/Refactoring

```
Review/refactor this code:
[CODE_BLOCK]

Focus on:
- [ASPECT_1: e.g., readability]
- [ASPECT_2: e.g., performance]
- [ASPECT_3: e.g., security]

Provide:
- List of issues found
- Refactored code
- Explanation of changes
```

### Pattern 3: Debugging

```
Debug this [LANGUAGE] code:
[CODE_BLOCK]

Issue:
- Error: [ERROR_MESSAGE]
- Expected: [EXPECTED_BEHAVIOR]
- Actual: [ACTUAL_BEHAVIOR]
- Inputs that fail: [FAILING_INPUTS]

Provide:
- Root cause analysis
- Fixed code
- Explanation of the bug
- How to prevent similar bugs
```

### Pattern 4: Architecture/Design

```
Design [COMPONENT/SYSTEM] for [PURPOSE]:

Requirements:
- [FUNCTIONAL_REQUIREMENTS]
- [NON_FUNCTIONAL_REQUIREMENTS]
- [CONSTRAINTS]

Provide:
- High-level architecture description
- Component breakdown
- Data flow
- Technology recommendations
- Trade-offs considered
```

### Pattern 5: Documentation

```
Generate documentation for:
[CODE_BLOCK or API_SPEC]

Include:
- Overview and purpose
- [SPECIFIC_SECTIONS: parameters, examples, etc.]
- [DOCSTRING_FORMAT: JSDoc, Sphinx, etc.]
- Usage examples
- Common pitfalls or gotchas
```

---

## Anti-Patterns to Avoid

### 1. Vague Requests

**Poor:** "Make it work"
**Problem:** No clear success criteria, AI must guess your intent
**Fix:** "Make this function handle null inputs by returning an empty array instead of throwing an error"

### 2. Missing Context

**Poor:** "Add caching"
**Problem:** Where? What to cache? How long? What technology?
**Fix:** "Add Redis caching to the getUserById function. Cache for 5 minutes. Use user ID as key. Invalidate on user update."

### 3. Unrealistic Expectations

**Poor:** "Build a production-ready e-commerce platform"
**Problem:** Too broad, would take days to implement properly
**Fix:** Break into smaller chunks: "Create a Product model with validation" → "Add product search API" → etc.

### 4. Assuming Prior Knowledge

**Poor:** "Use the same pattern as before"
**Problem:** AI doesn't have memory of previous conversations (unless in same session)
**Fix:** "Use the Repository pattern like this example: [code snippet]"

### 5. Over-Constraining

**Poor:** "Use exactly 47 lines, 3 functions, named func1/func2/func3, using for-loops not while-loops..."
**Problem:** Over-specification limits AI's ability to find good solutions
**Fix:** Focus on essential requirements, let AI decide implementation details

### 6. Not Specifying Language/Framework

**Poor:** "Create a server"
**Problem:** Could be Node.js, Python, Go, Java, etc. - all very different
**Fix:** "Create an Express.js server in Node.js 18 with TypeScript"

### 7. Requesting Incomplete Solutions

**Poor:** "Just give me the function signature"
**Problem:** You'll need to ask for implementation anyway, wasting time
**Fix:** "Give me the complete function implementation with error handling and tests"

### 8. No Error Handling Guidance

**Poor:** "Parse JSON from API"
**Problem:** Will it handle malformed JSON? Network errors? Timeouts?
**Fix:** "Parse JSON from API. Handle network errors (retry 3x), malformed JSON (log and return null), timeouts (5s limit)."

---

## Domain-Specific Tips

### Frontend Development

**Key elements to specify:**
- Framework/library (React, Vue, Angular, etc.) and version
- State management (Redux, Context, Zustand, etc.)
- Styling approach (CSS Modules, Styled Components, Tailwind, etc.)
- Accessibility requirements (WCAG level, screen reader support)
- Browser compatibility targets
- Responsive breakpoints

**Example Prompt:**
```
Create a React 18 component for a data table:
- Use TypeScript with strict mode
- Props: data (array), columns (config), onRowClick (callback)
- Features: Sorting, pagination, search
- Styling: Tailwind CSS, responsive (mobile: stack columns, desktop: full table)
- Accessibility: WCAG AA, keyboard navigation, screen reader labels
- State: Local state with useState, no external library
```

### Backend Development

**Key elements to specify:**
- Language, framework, version
- Database type and ORM/query builder
- Authentication/authorization approach
- API style (REST, GraphQL, gRPC)
- Error handling patterns
- Logging strategy
- Performance requirements

**Example Prompt:**
```
Create a Node.js REST API endpoint:
- Framework: Express 4.x with TypeScript
- Route: POST /api/orders
- Database: PostgreSQL with Prisma ORM
- Auth: JWT validation middleware (existing)
- Input: { userId, items[], shippingAddress }
- Validation: Joi schema, return 400 for invalid input
- Business logic: Check stock, calculate total, create order transaction
- Return: 201 with order object, or 409 if out of stock
- Error handling: Wrap in try-catch, log with Winston, use custom error classes
- Performance: Transaction for atomicity, <200ms target
```

### Data/ML

**Key elements to specify:**
- Data sources and formats
- Preprocessing needs
- Libraries (pandas, numpy, sklearn, pytorch, etc.)
- Expected input/output shapes
- Visualization requirements
- Performance constraints (memory, time)

**Example Prompt:**
```
Create a Python script for exploratory data analysis:
- Data: CSV with 100k rows, 20 columns (user demographics and churn status)
- Libraries: pandas, matplotlib, seaborn
- Analysis: Summary stats, missing values, correlation matrix, churn rate by segment
- Visualizations: 5 charts (distribution, correlation heatmap, etc.)
- Output: Markdown report with findings + PNG charts
- Handle: Missing data (impute or flag), outliers (detect with z-score)
```

### DevOps/Infrastructure

**Key elements to specify:**
- Cloud provider (AWS, GCP, Azure)
- IaC tool (Terraform, CloudFormation, etc.)
- CI/CD platform (GitHub Actions, Jenkins, etc.)
- Environment (dev, staging, prod)
- High availability requirements
- Security/compliance needs

**Example Prompt:**
```
Create Terraform configuration for AWS:
- Resources: VPC, ECS Fargate, RDS PostgreSQL, ALB
- Environment: Production
- Requirements: Multi-AZ, auto-scaling (2-10 tasks), encrypted data
- Networking: Private subnets for compute/DB, public for ALB
- Security: Security groups, IAM roles with least privilege
- Output: Modular structure, variables for configurability
- Follow: AWS Well-Architected Framework
```

---

## Advanced Techniques

### 1. Chain-of-Thought Prompting

Ask the AI to think step-by-step before generating code.

**Technique:**
```
Before implementing [TASK], explain your approach:
1. What are the main components needed?
2. What are potential edge cases?
3. What's the optimal algorithm/pattern?

Then implement based on your analysis.
```

**Benefit:** More thoughtful solutions, catches issues early.

**Example:**
```
Before implementing a rate limiter, explain:
1. What data structure to use (token bucket? sliding window?)
2. How to handle distributed systems (single server vs. multi-server)
3. Edge cases (clock skew, concurrent requests)

Then implement using Redis with sliding window, handling race conditions.
```

### 2. Few-Shot Learning

Provide examples of desired output style.

**Technique:**
```
Generate functions following these examples:

Example 1:
[CODE_EXAMPLE_1]

Example 2:
[CODE_EXAMPLE_2]

Now generate similar function for [NEW_TASK].
```

**Benefit:** AI matches your team's coding style automatically.

**Example:**
```
Follow this error handling pattern:

Example:
async function getUser(id) {
  try {
    const user = await db.query('SELECT * FROM users WHERE id = $1', [id]);
    if (!user) throw new NotFoundError('User not found');
    return user;
  } catch (error) {
    logger.error('Failed to get user', { id, error });
    throw error;
  }
}

Now create getOrder(orderId) following the same pattern.
```

### 3. Role-Based Prompting

Frame the AI as an expert in a specific role.

**Technique:**
```
You are a [ROLE] with expertise in [DOMAIN].
[TASK_DESCRIPTION]

Consider [ROLE_SPECIFIC_FACTORS].
```

**Example:**
```
You are a security engineer reviewing authentication code.

Review this login function for security vulnerabilities:
[CODE]

Consider: SQL injection, timing attacks, password storage, session management, rate limiting, error information disclosure.

Provide: Security issues found (severity), recommended fixes, secure implementation.
```

### 4. Constraint-Based Generation

Use constraints to guide toward better solutions.

**Technique:**
```
Implement [TASK] under these constraints:
- Must complete in O(n log n) time
- Memory usage under 100MB
- No external dependencies
- Thread-safe
- Handle inputs up to 1M items
```

**Benefit:** Forces consideration of performance, scalability, and edge cases.

### 5. Iterative Refinement

Build solutions iteratively with feedback.

**Process:**
1. **Prompt 1:** Basic implementation
2. **Prompt 2:** "Add error handling and input validation"
3. **Prompt 3:** "Optimize for performance, target O(n) time"
4. **Prompt 4:** "Add comprehensive unit tests"

**Benefit:** Allows course-correction and handles complexity incrementally.

### 6. Negative Prompting

Explicitly state what NOT to do.

**Technique:**
```
Implement [TASK]

DO:
- [DESIRED_APPROACH]

DON'T:
- Use eval() or Function() constructor (security risk)
- Make API calls without timeout
- Ignore errors silently
- Use any type in TypeScript
```

### 7. Meta-Prompting

Ask the AI to help you create a better prompt.

**Technique:**
```
I want to [GOAL]. What information do you need to provide the best solution?
```

**Example:**
"I want to create a caching layer for my API. What details about my system, requirements, and constraints do you need to recommend the best approach?"

AI might ask:
- What are you caching (HTML, JSON, database queries)?
- Cache size and eviction policy?
- Cache invalidation strategy?
- Single server or distributed?
- Read/write patterns?

Then you provide those details for a much better response.

---

## Examples

### Example 1: Good vs. Poor Prompts

**POOR Prompt:**
> "Make a login page"

**Why it's poor:**
- No tech stack specified
- No UI/UX requirements
- No security considerations
- No validation requirements
- No error handling guidance

**GOOD Prompt:**
> Create a login page with the following specifications:
>
> **Technology:**
> - React 18 with TypeScript
> - Form handling: React Hook Form with Yup validation
> - Styling: Tailwind CSS
> - API calls: Axios
>
> **Requirements:**
> - Fields: Email, Password
> - Validation:
>   - Email: Valid format, required
>   - Password: Min 8 characters, required
> - Show validation errors below fields
> - Submit button disabled during API call
> - Show loading spinner on button while submitting
>
> **API Integration:**
> - POST to /api/auth/login
> - On success (200): Store JWT in localStorage, redirect to /dashboard
> - On failure (401): Show "Invalid credentials" error
> - On failure (500): Show "Server error, try again" error
> - Handle network errors gracefully
>
> **Accessibility:**
> - WCAG AA compliant
> - Proper labels and ARIA attributes
> - Keyboard navigation support
> - Focus management
>
> **Include:**
> - Complete React component with TypeScript types
> - Yup validation schema
> - Example API service function
> - Tailwind classes for styling

### Example 2: Debugging Prompt

**GOOD Debugging Prompt:**
> Debug this TypeScript function that calculates discounts:
>
> ```typescript
> function calculateDiscount(price: number, discountPercent: number): number {
>   return price - price * discountPercent;
> }
> ```
>
> **Issue:**
> - Input: `calculateDiscount(100, 20)`
> - Expected output: `80` (20% off $100 = $80)
> - Actual output: `2000`
>
> **Additional failing cases:**
> - `calculateDiscount(50, 10)` returns `500` (expected `45`)
> - `calculateDiscount(200, 5)` returns `1000` (expected `190`)
>
> **Provide:**
> 1. Explanation of the bug
> 2. Fixed function
> 3. Test cases to prevent regression
> 4. Input validation (e.g., handle negative prices, percent > 100)

**Expected Response:**
1. **Bug:** `discountPercent` is being treated as a whole number (20) instead of a percentage (0.20). Should divide by 100.
2. **Fixed function:** [corrected code]
3. **Tests:** [unit tests covering edge cases]
4. **Validation:** Check price >= 0, discountPercent between 0-100

### Example 3: Architecture Prompt

**GOOD Architecture Prompt:**
> Design a file upload system for a web application:
>
> **Requirements:**
> - Users upload images (JPEG, PNG) up to 10MB
> - Support 10k concurrent users, 100k uploads/day
> - Generate thumbnails (small, medium, large sizes)
> - Virus scan uploaded files
> - Serve files via CDN
> - 99.9% availability
>
> **Constraints:**
> - Use AWS services
> - Budget: ~$500/month
> - Data retention: 1 year
> - Comply with GDPR (data deletion on request)
>
> **Provide:**
> - High-level architecture diagram (description)
> - Component breakdown (what each service does)
> - Data flow (upload → processing → storage → serving)
> - Technology choices with rationale
> - Scalability strategy
> - Security measures
> - Cost estimation breakdown
> - Failure scenarios and mitigation

---

## Quick Reference Checklist

When crafting a prompt, ask yourself:

**Context:**
- [ ] Have I specified the programming language and version?
- [ ] Have I mentioned the framework/library and version?
- [ ] Have I described the broader system/architecture?

**Requirements:**
- [ ] Have I clearly stated what I want the AI to create?
- [ ] Have I defined success criteria?
- [ ] Have I specified any constraints or limitations?

**Details:**
- [ ] Have I included code style preferences?
- [ ] Have I mentioned error handling requirements?
- [ ] Have I specified input validation needs?
- [ ] Have I requested tests or examples?

**Output:**
- [ ] Have I stated the desired output format?
- [ ] Have I asked for explanations where needed?
- [ ] Have I requested edge case handling?

**Clarity:**
- [ ] Is my prompt specific and unambiguous?
- [ ] Have I provided examples if helpful?
- [ ] Have I avoided jargon or company-specific terms?

---

## Conclusion

Effective prompting is a skill that improves with practice. Key takeaways:

1. **Be specific** - The more detail, the better the output
2. **Provide context** - Help the AI understand your environment
3. **Iterate** - Refine prompts based on responses
4. **Use patterns** - Templates make prompting faster and more consistent
5. **Review output** - AI-generated code should always be reviewed and tested

Remember: AI coding assistants are tools to augment your development, not replace your expertise. Use them to handle boilerplate, explore solutions, and accelerate implementation, but always apply critical thinking to the output.

---

## Additional Resources

- **Related Prompt Libraries:**
  - [coding-prompts.md](./coding-prompts.md) - Code generation and refactoring
  - [architecture-prompts.md](./architecture-prompts.md) - System design
  - [testing-prompts.md](./testing-prompts.md) - Test generation
  - [documentation-prompts.md](./documentation-prompts.md) - Documentation
  - [business-prompts.md](./business-prompts.md) - PRDs and business tasks
  - [ui-ux-prompts.md](./ui-ux-prompts.md) - UI/UX design
  - [data-prompts.md](./data-prompts.md) - Data analysis and SQL
  - [devops-prompts.md](./devops-prompts.md) - CI/CD and infrastructure

- **External Resources:**
  - OpenAI Prompt Engineering Guide
  - Anthropic's Guide to Prompting Claude
  - Prompt Engineering subreddit (r/PromptEngineering)
  - LearnPrompting.org
