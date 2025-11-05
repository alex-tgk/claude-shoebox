# Testing Prompts

A collection of prompt templates for test generation, test strategy, and quality assurance tasks.

---

## Unit Testing

### 1. Generate Unit Tests

**Purpose:** Create comprehensive unit tests for a function or class.

**Prompt:**
```
Generate unit tests for this [LANGUAGE] code:
[CODE_BLOCK]

Test requirements:
- Testing framework: [JEST/PYTEST/JUNIT/ETC]
- Coverage target: [PERCENTAGE]
- Test cases to include:
  - Happy path scenarios
  - Edge cases: [SPECIFIC_EDGES]
  - Error conditions: [EXPECTED_ERRORS]
  - Boundary values
- Mock dependencies: [DEPENDENCIES_TO_MOCK]
- Assertion style: [STYLE_PREFERENCE]

Organize tests with clear descriptions and use AAA pattern (Arrange, Act, Assert).
```

**Example:**
```
Generate unit tests for this TypeScript authentication service:
[AuthService class with login, logout, validateToken methods]

Test requirements:
- Testing framework: Jest with @testing-library
- Coverage target: 95%
- Test cases to include:
  - Happy path: successful login, logout, valid token
  - Edge cases: empty credentials, malformed tokens, expired tokens
  - Error conditions: network failures, invalid credentials, rate limiting
  - Boundary values: minimum password length, token expiration timing
- Mock dependencies: HTTP client, token generator, cache
- Assertion style: expect() with jest matchers

Organize tests with clear descriptions and use AAA pattern (Arrange, Act, Assert).
```

---

### 2. Test Data Builders

**Purpose:** Create test data builders and factories.

**Prompt:**
```
Create test data builders for [ENTITY]:

Entity structure:
[SCHEMA/INTERFACE]

Generate:
- Builder class with fluent API
- Factory function for common scenarios:
  - Valid default instance
  - Minimal valid instance
  - Edge case variations: [SPECIFIC_CASES]
- Random data generation for properties
- Relationship handling: [FOREIGN_KEYS]
- Framework: [LANGUAGE/LIBRARY]

Make builders chainable and easy to customize for different test scenarios.
```

**Example:**
```
Create test data builders for User and Order entities:

Entity structure:
User: { id, email, name, role, createdAt, orders[] }
Order: { id, userId, items[], total, status, orderDate }

Generate:
- Builder classes with fluent API (.withEmail(), .withRole(), etc.)
- Factory functions:
  - createValidUser(), createAdminUser(), createGuestUser()
  - createPendingOrder(), createCompletedOrder()
- Random but valid email, name, amounts
- Relationship handling: user.orders populated correctly
- Framework: TypeScript with faker.js

Make builders chainable like: createUser().withRole('admin').withOrders(3).build()
```

---

### 3. Parameterized Test Generation

**Purpose:** Create parameterized/table-driven tests.

**Prompt:**
```
Create parameterized tests for [FUNCTION]:
[CODE_BLOCK]

Test matrix:
- Input parameters: [PARAMETER_LIST]
- Variations to test: [INPUT_COMBINATIONS]
- Expected outputs: [OUTPUT_MAPPING]

Generate:
- Test cases table with inputs and expected outputs
- Parameterized test implementation using [FRAMEWORK_FEATURE]
- Clear test case descriptions
- Coverage of all combinations: [EXHAUSTIVE/REPRESENTATIVE]

Format as [TEST_FRAMEWORK] parameterized tests.
```

**Example:**
```
Create parameterized tests for discount calculation function:
calculateDiscount(orderTotal, customerType, promoCode) -> discountAmount

Test matrix:
- orderTotal: [0, 50, 100, 500, 1000]
- customerType: ['regular', 'premium', 'vip']
- promoCode: [null, 'SAVE10', 'SAVE20', 'INVALID']

Generate:
- Test cases table covering representative combinations (not all 60)
- Parameterized test using Jest's test.each()
- Descriptive test names like "should apply 10% discount for regular customer with SAVE10"
- Coverage of boundary conditions and common scenarios

Format as Jest parameterized tests with table at top.
```

---

## Integration Testing

### 4. API Integration Tests

**Purpose:** Create integration tests for API endpoints.

**Prompt:**
```
Create integration tests for these API endpoints:
[API_SPECIFICATION]

Test coverage:
- HTTP methods: [GET/POST/PUT/DELETE]
- Authentication/authorization scenarios
- Request validation (valid/invalid inputs)
- Response status codes and bodies
- Error handling
- Side effects (database changes, etc.)
- Performance expectations: [RESPONSE_TIME]

Use:
- Testing framework: [SUPERTEST/REQUESTS/ETC]
- Test database: [STRATEGY]
- Authentication: [MOCK/REAL]
- Setup/teardown for data consistency

Include both success and failure scenarios.
```

**Example:**
```
Create integration tests for user management API:
- POST /api/users (create)
- GET /api/users/:id (read)
- PUT /api/users/:id (update)
- DELETE /api/users/:id (delete)
- GET /api/users (list with pagination)

Test coverage:
- All CRUD operations with valid data
- Authentication required for all except GET
- Request validation: missing fields, invalid email, weak password
- Status codes: 200, 201, 400, 401, 404, 409
- Error messages in proper format
- Database reflects changes correctly
- Response time < 200ms for reads

Use:
- Supertest with Express app
- Separate test database, reset between tests
- JWT tokens for authentication tests
- beforeEach/afterEach for data setup/cleanup

Include success paths and all error scenarios.
```

---

### 5. Database Integration Tests

**Purpose:** Test database operations and queries.

**Prompt:**
```
Create database integration tests for [REPOSITORY/DAO]:
[CODE_BLOCK]

Test scenarios:
- CRUD operations for [ENTITY]
- Complex queries: [SPECIFIC_QUERIES]
- Transactions and rollbacks
- Constraints: [FOREIGN_KEYS/UNIQUE/ETC]
- Concurrent access scenarios
- Data migration validation

Setup:
- Database: [TYPE_AND_VERSION]
- Test data fixtures: [APPROACH]
- Isolation strategy: [TRANSACTION_ROLLBACK/TRUNCATE]
- Framework: [ORM/QUERY_BUILDER]

Verify both data correctness and query performance.
```

**Example:**
```
Create database integration tests for OrderRepository:
[OrderRepository with methods: create, findById, findByUser, updateStatus, delete]

Test scenarios:
- CRUD operations for Order entity
- Complex queries: findOrdersWithItems, getRevenueByPeriod
- Transaction: creating order with items should be atomic
- Constraints: userId foreign key, unique order number
- Concurrent access: two requests updating same order
- Verify indexes exist for common queries

Setup:
- PostgreSQL 14 in Docker container
- Fixtures: seed users and products before each test
- Transaction rollback for isolation
- TypeORM for database access

Verify data correctness, foreign key constraints, and query time < 100ms for indexed queries.
```

---

## End-to-End Testing

### 6. E2E User Journey Tests

**Purpose:** Create end-to-end tests for user journeys.

**Prompt:**
```
Create E2E tests for [USER_JOURNEY]:

Journey steps:
1. [STEP_1]
2. [STEP_2]
3. [STEP_3]
...

Test requirements:
- Testing tool: [PLAYWRIGHT/CYPRESS/SELENIUM]
- Environment: [STAGING/LOCAL]
- Test data: [STRATEGY]
- Authentication: [APPROACH]
- Assertions at each step
- Handle async operations
- Screenshot on failure
- Test cleanup

Write tests that verify both UI interactions and resulting system state.
```

**Example:**
```
Create E2E tests for e-commerce checkout journey:

Journey steps:
1. User logs in
2. Browses products and adds items to cart
3. Views cart and updates quantities
4. Proceeds to checkout
5. Enters shipping information
6. Enters payment information
7. Reviews order
8. Confirms order
9. Sees order confirmation

Test requirements:
- Playwright with TypeScript
- Local development environment
- Test user with known credentials
- Test credit card from payment gateway
- Assert cart total, shipping calculation, order total
- Wait for payment processing (async)
- Screenshot on any failure
- Delete test order after test

Verify UI shows correct information and order is created in database.
```

---

### 7. Visual Regression Tests

**Purpose:** Create visual regression tests for UI components.

**Prompt:**
```
Create visual regression tests for [COMPONENT/PAGE]:

Components to test:
- [COMPONENT_LIST]

Test scenarios:
- Default state
- Interactive states: [HOVER/FOCUS/ACTIVE]
- Different data: [EMPTY/LOADING/ERROR/FULL]
- Responsive breakpoints: [MOBILE/TABLET/DESKTOP]
- Theme variations: [LIGHT/DARK]
- Accessibility states: [HIGH_CONTRAST]

Setup:
- Tool: [PERCY/CHROMATIC/BACKSTOP]
- Browsers: [BROWSER_LIST]
- Viewport sizes: [SIZES]
- Baseline management: [STRATEGY]

Organize tests by component and state.
```

**Example:**
```
Create visual regression tests for Dashboard page and Card component:

Components to test:
- Dashboard with various widget layouts
- Card in different sizes and content

Test scenarios:
- Default: dashboard with all widgets, card with standard content
- Interactive: card hover effect, dashboard with expanded widget
- Data variations: empty dashboard, card with long text, card with image
- Responsive: mobile (375px), tablet (768px), desktop (1920px)
- Themes: light and dark mode
- Loading and error states

Setup:
- Percy with Storybook stories
- Chrome, Firefox, Safari
- Three viewport sizes
- Main branch as baseline for comparison

Capture 20+ visual snapshots covering all state combinations.
```

---

## Test Strategy

### 8. Test Plan Creation

**Purpose:** Create comprehensive test plan for a feature.

**Prompt:**
```
Create a test plan for [FEATURE]:

Feature description:
[DETAILED_DESCRIPTION]

Test plan should include:
- Test scope and objectives
- Testing types: [UNIT/INTEGRATION/E2E/PERFORMANCE]
- Test environments: [DEV/STAGING/PROD]
- Entry and exit criteria
- Test cases organized by priority
- Test data requirements
- Risk analysis: [HIGH_RISK_AREAS]
- Resource requirements: [TOOLS/PEOPLE/TIME]
- Success metrics: [COVERAGE/DEFECT_RATE]
- Schedule and milestones

Format as structured document.
```

**Example:**
```
Create a test plan for Multi-factor Authentication (MFA) feature:

Feature description:
Add SMS and authenticator app-based MFA to user accounts. Users can enable/disable MFA,
with enforcement for admin accounts. Includes backup codes.

Test plan should include:
- Scope: MFA enrollment, authentication, recovery, admin enforcement
- Testing types: Unit (30%), Integration (40%), E2E (20%), Security (10%)
- Environments: Dev, staging with test SMS gateway, production with gradual rollout
- Entry: Feature complete in dev. Exit: 90% coverage, no P1/P2 bugs, security audit passed
- Test cases by priority: P0 (core auth flow), P1 (edge cases), P2 (UI/UX)
- Test data: test phone numbers, test authenticator seeds, various user scenarios
- Risk: SMS delivery failures, time sync issues, lockout scenarios
- Resources: 2 QA engineers, Twilio test credentials, 2 weeks
- Success: 90%+ coverage, <2% auth failure rate, security audit approval
- Schedule: Week 1 unit/integration, Week 2 E2E/security

Format as markdown document with sections.
```

---

### 9. Test Coverage Analysis

**Purpose:** Analyze and improve test coverage.

**Prompt:**
```
Analyze test coverage for [MODULE/APPLICATION]:

Current coverage:
- Overall: [PERCENTAGE]
- By type: [UNIT/INTEGRATION/E2E_PERCENTAGES]
- By module: [MODULE_BREAKDOWN]

Coverage report:
[COVERAGE_DATA or FILE_PATH]

Provide:
- Identification of untested/under-tested code
- Risk assessment for uncovered areas
- Recommended test additions prioritized by risk
- Strategy to reach [TARGET_COVERAGE]%
- Tests that can be removed (redundant/low-value)
- Coverage improvements beyond line coverage (branch, path)

Focus on meaningful coverage, not just metrics.
```

**Example:**
```
Analyze test coverage for payment processing module:

Current coverage:
- Overall: 72%
- Unit: 85%, Integration: 60%, E2E: 40%
- By module: PaymentService 95%, RefundService 45%, WebhookHandler 30%

Coverage report:
[Path to coverage HTML report]

Provide:
- Uncovered: RefundService edge cases, webhook retry logic, error handling
- Risk: HIGH for webhook handling (financial data), MEDIUM for refunds
- Recommendations:
  1. Add webhook failure/retry tests (HIGH priority)
  2. Add refund scenario tests (HIGH)
  3. Add integration tests for payment gateway timeouts (MEDIUM)
  4. Add E2E tests for full refund flow (MEDIUM)
- Strategy: Focus on high-risk areas first, aim for 85% overall with 100% on critical paths
- Remove: Redundant constructor tests, trivial getter tests
- Improve: Add branch coverage analysis for complex conditionals

Target meaningful 85% coverage with 100% on payment/refund critical paths.
```

---

## Performance Testing

### 10. Load Test Scenarios

**Purpose:** Create load testing scenarios.

**Prompt:**
```
Create load test scenarios for [APPLICATION]:

Performance requirements:
- Expected load: [USERS/REQUESTS]
- Response time: [P95/P99_TARGETS]
- Throughput: [REQUESTS_PER_SECOND]
- Concurrent users: [NUMBER]

Test scenarios:
1. Baseline: [NORMAL_LOAD]
2. Peak load: [EXPECTED_MAXIMUM]
3. Stress test: [BEYOND_CAPACITY]
4. Spike test: [SUDDEN_INCREASES]
5. Endurance: [SUSTAINED_LOAD]

For each scenario provide:
- Test configuration (users, duration, ramp-up)
- Specific endpoints/operations to test
- Success criteria
- Tool: [K6/JMETER/GATLING]

Include realistic user behavior patterns.
```

**Example:**
```
Create load test scenarios for e-commerce API:

Performance requirements:
- Expected: 1000 concurrent users, 5000 req/sec
- Response time: p95 < 200ms, p99 < 500ms
- Throughput: 5000 RPS sustained
- Peak concurrent: 2000 users (holiday sales)

Test scenarios:
1. Baseline: 500 users, 30 min, normal traffic mix
2. Peak: 2000 users, 1 hour, heavy on product search and checkout
3. Stress: 5000 users, ramp until failure to find breaking point
4. Spike: 500 to 3000 users in 1 minute, test auto-scaling
5. Endurance: 1000 users, 4 hours, check for memory leaks

For each:
- K6 configuration with virtual users, duration, stages
- Traffic: 50% browse, 30% search, 15% add to cart, 5% checkout
- Success: meet response time SLOs, <1% error rate, no degradation
- Use K6 scripts with realistic think time (1-5 seconds)

Model realistic user journeys: browse → search → view product → add to cart → checkout.
```

---

### 11. Performance Benchmark Tests

**Purpose:** Create performance benchmarks.

**Prompt:**
```
Create performance benchmarks for [COMPONENT/FUNCTION]:

Code to benchmark:
[CODE_BLOCK]

Benchmark requirements:
- Operations to measure: [OPERATIONS]
- Input sizes: [DATA_SIZE_VARIATIONS]
- Iterations: [NUMBER_FOR_STATISTICAL_VALIDITY]
- Metrics: [LATENCY/THROUGHPUT/MEMORY/CPU]
- Comparison baseline: [PREVIOUS_VERSION/ALTERNATIVE_IMPL]
- Environment: [HARDWARE_SPECS]

Generate:
- Benchmark setup code
- Multiple test cases with varying inputs
- Statistical analysis (mean, median, percentiles)
- Performance regression detection
- Framework: [BENCHMARK_LIBRARY]

Include warmup runs and multiple iterations for accuracy.
```

**Example:**
```
Create performance benchmarks for JSON serialization implementations:

Code to benchmark:
[JSON.stringify vs custom serializer vs library]

Benchmark requirements:
- Operations: serialize object to JSON string
- Input sizes: small (10 fields), medium (100 fields), large (10k fields), nested
- Iterations: 10k runs per test for statistical validity
- Metrics: ops/sec, mean latency, p95 latency, memory allocation
- Baseline: JSON.stringify (native)
- Environment: Node.js 18, 4 CPU cores, 8GB RAM

Generate:
- Benchmark using tinybench or benchmark.js
- Test cases for each input size × implementation
- Calculate mean, median, p95, p99
- Report: "Custom serializer is 2.3x faster for large objects"
- Fail CI if performance regresses >10%

Include 1000 warmup iterations before measurement runs.
```

---

## Test Maintenance

### 12. Flaky Test Investigation

**Purpose:** Identify and fix flaky tests.

**Prompt:**
```
Investigate this flaky test:
[TEST_CODE]

Flakiness data:
- Pass rate: [PERCENTAGE]
- Failure pattern: [INTERMITTENT/TIME_BASED/ENV_BASED]
- Error messages: [COMMON_ERRORS]
- Environment: [TEST_ENVIRONMENT]

Analyze for common flakiness causes:
- Timing issues (race conditions, insufficient waits)
- Test dependencies (shared state, order dependency)
- External dependencies (APIs, databases)
- Non-deterministic data (random values, timestamps)
- Resource contention
- Environment differences

Provide:
- Root cause identification
- Fix recommendation
- Prevention strategies
```

**Example:**
```
Investigate this flaky E2E test:
[Login test that sometimes fails]

Flakiness data:
- Pass rate: 75% (fails 1 in 4 runs)
- Failure pattern: intermittent, seems worse on CI
- Error: "Element not found: #submit-button"
- Environment: Playwright on CI runners

Analyze for:
- Timing: Page not fully loaded before clicking submit
- Dependencies: None, test runs in isolation
- External: Authenticates against staging API
- Non-deterministic: None obvious
- Resource: CI runners might be slower
- Environment: Different network latency on CI

Provide:
- Root cause: Race condition - test clicks before page hydration complete
- Fix: Use waitFor with proper selector, increase timeout, wait for network idle
- Prevention: Use Playwright's auto-waiting, avoid fixed sleep(), use explicit waits
- Example: await page.waitForSelector('#submit-button', { state: 'visible', timeout: 10000 })
```

---

### 13. Test Refactoring

**Purpose:** Refactor tests for maintainability.

**Prompt:**
```
Refactor these tests for better maintainability:
[TEST_CODE]

Issues to address:
- Code duplication: [REPEATED_PATTERNS]
- Poor test organization: [STRUCTURE_ISSUES]
- Unclear test intent: [NAMING/DESCRIPTION_ISSUES]
- Hard-coded values: [MAGIC_NUMBERS/STRINGS]
- Complex setup: [SETUP_COMPLEXITY]
- Brittle assertions: [OVER_SPECIFIED_TESTS]

Apply:
- Extract common setup to fixtures/helpers
- Use Page Object Model for UI tests
- Create custom matchers/assertions
- Implement test data builders
- Follow AAA pattern consistently
- Improve test names for clarity
- DRY principle for test utilities

Maintain test coverage while improving readability.
```

**Example:**
```
Refactor these React component tests:
[Multiple tests with duplicated render and query logic]

Issues:
- Duplication: Every test renders same component with similar props
- Organization: All tests in one file, no logical grouping
- Intent: Test names like "test1", "test2" not descriptive
- Hard-coded: Strings like "john@example.com" repeated
- Setup: Complex prop objects recreated in each test
- Brittle: Tests assert on implementation details (state, class names)

Apply:
- Extract renderComponent helper with default props
- Use describe blocks to group related tests
- Rename: "renders error when email invalid" vs "test1"
- Create TEST_USER constant for test data
- Create createUserProps() builder function
- Assert on user-visible behavior, use Testing Library queries
- Create custom matcher toBeValidEmail()

Result: Reduce duplication by 60%, make tests easier to understand and modify.
```

---

## Specialized Testing

### 14. Security Testing

**Purpose:** Create security-focused tests.

**Prompt:**
```
Create security tests for [APPLICATION/FEATURE]:

Security concerns:
- Authentication/authorization bypasses
- Input validation vulnerabilities
- Injection attacks: [SQL/XSS/COMMAND]
- Sensitive data exposure
- CSRF/SSRF vulnerabilities
- Rate limiting effectiveness
- [SPECIFIC_THREATS]

Test cases:
- Malicious inputs: [SPECIFIC_PAYLOADS]
- Authentication edge cases
- Authorization boundary testing
- Session management security
- Secure communication (HTTPS, headers)
- Dependency vulnerabilities

Use [SECURITY_TESTING_TOOL] and provide:
- Test scenarios with attack vectors
- Expected security controls
- Verification of proper error handling (no info disclosure)
```

**Example:**
```
Create security tests for API authentication and user data endpoints:

Security concerns:
- Auth bypass by JWT manipulation
- Authorization: users accessing other users' data
- SQL injection in search parameters
- XSS in user-generated content
- Sensitive data (passwords, tokens) in responses
- Rate limiting on login endpoint
- CSRF on state-changing operations

Test cases:
- JWT: expired token, modified signature, invalid issuer, missing claims
- Authz: User A tries to access User B's /api/users/B/profile
- Injection: SQL payloads in search query, escape characters
- XSS: Script tags in user bio, test output encoding
- Exposure: Verify password hashes never in responses
- Rate limit: 100 failed logins → should block
- CSRF: State-changing requests require CSRF token

Use OWASP ZAP for automated scanning and Jest for specific test cases.
Verify proper 401/403 responses without leaking information.
```

---

### 15. Accessibility Testing

**Purpose:** Create accessibility tests for web applications.

**Prompt:**
```
Create accessibility tests for [APPLICATION/COMPONENT]:

WCAG compliance target: [A/AA/AAA]

Test areas:
- Keyboard navigation (tab order, focus management)
- Screen reader compatibility
- Color contrast ratios
- Alternative text for images
- Form labels and error messages
- ARIA attributes
- Heading hierarchy
- Focus indicators
- [SPECIFIC_REQUIREMENTS]

Generate tests using:
- Automated tools: [AXE/LIGHTHOUSE/PA11Y]
- Manual test scenarios
- Keyboard-only interaction tests
- Screen reader announcement verification

Provide both automated and manual test procedures.
```

**Example:**
```
Create accessibility tests for checkout form:

WCAG 2.1 Level AA compliance

Test areas:
- Keyboard: Tab through entire form, submit with Enter
- Screen reader: All fields announced with labels
- Contrast: Error messages meet 4.5:1 ratio
- Alt text: Payment icons have meaningful descriptions
- Labels: All inputs associated with labels
- ARIA: Live regions for error announcements, required fields marked
- Headings: Logical h1-h3 structure
- Focus: Visible focus indicator on all interactive elements
- Error handling: Clear error messages linked to fields

Using:
- jest-axe for automated WCAG checks in React tests
- Manual: Test with NVDA/JAWS screen reader
- Keyboard test: Complete checkout without mouse
- Verify error announcements are polite (not assertive)

Automated tests catch 30-40% of issues; include manual test checklist for rest.
```

---

## Additional Resources

- **Related:** See [prompt-engineering-guide.md](./prompt-engineering-guide.md) for writing effective testing prompts
- **Implementation:** See [coding-prompts.md](./coding-prompts.md) for implementing test code
- **Documentation:** See [documentation-prompts.md](./documentation-prompts.md) for test documentation
