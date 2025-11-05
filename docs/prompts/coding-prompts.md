# Coding Prompts

A collection of prompt templates for code generation, refactoring, and debugging tasks.

---

## Code Generation

### 1. Generate Function from Specification

**Purpose:** Create a new function based on detailed requirements.

**Prompt:**
```
Create a [LANGUAGE] function called [FUNCTION_NAME] that:
- Takes [INPUT_PARAMETERS] as parameters
- Returns [RETURN_TYPE]
- [SPECIFIC_FUNCTIONALITY]
- Handles edge cases: [EDGE_CASES]
- Follows [STYLE_GUIDE] conventions

Include comprehensive error handling and input validation.
```

**Example:**
```
Create a TypeScript function called calculateShippingCost that:
- Takes orderTotal (number), destination (string), and weight (number) as parameters
- Returns a number representing the shipping cost
- Calculates cost based on weight tiers and destination zones
- Handles edge cases: negative values, invalid destinations
- Follows Airbnb TypeScript style guide conventions

Include comprehensive error handling and input validation.
```

---

### 2. Implement Class/Module

**Purpose:** Generate a complete class or module structure.

**Prompt:**
```
Implement a [LANGUAGE] [CLASS/MODULE] called [NAME] that:
- Purpose: [DESCRIPTION]
- Properties: [LIST_PROPERTIES]
- Methods: [LIST_METHODS]
- Implements interface/extends: [INHERITANCE]
- Design patterns: [PATTERNS_TO_USE]
- Dependencies: [EXTERNAL_DEPENDENCIES]

Use [ARCHITECTURAL_STYLE] and include appropriate typing/documentation.
```

**Example:**
```
Implement a Python class called UserRepository that:
- Purpose: Manages user data persistence and retrieval
- Properties: database_connection, cache_client
- Methods: create_user, get_user_by_id, update_user, delete_user, find_users_by_criteria
- Implements interface: Repository
- Design patterns: Repository pattern, Singleton for connection
- Dependencies: SQLAlchemy, Redis

Use clean architecture principles and include appropriate typing/documentation.
```

---

### 3. API Endpoint Implementation

**Purpose:** Create a complete API endpoint with routing, validation, and error handling.

**Prompt:**
```
Create a [FRAMEWORK] API endpoint for [RESOURCE]:
- HTTP Method: [GET/POST/PUT/DELETE]
- Route: [URL_PATH]
- Request body/params: [EXPECTED_INPUT]
- Response format: [OUTPUT_STRUCTURE]
- Authentication: [AUTH_METHOD]
- Validation rules: [VALIDATION_REQUIREMENTS]
- Error responses: [ERROR_CODES_AND_MESSAGES]

Include middleware for [MIDDLEWARE_NEEDS] and follow REST best practices.
```

**Example:**
```
Create an Express.js API endpoint for user registration:
- HTTP Method: POST
- Route: /api/v1/users/register
- Request body: { email, password, firstName, lastName }
- Response format: { user: { id, email, firstName, lastName }, token: string }
- Authentication: None (public endpoint)
- Validation rules: email format, password min 8 chars with special char, required fields
- Error responses: 400 for validation errors, 409 for duplicate email, 500 for server errors

Include middleware for rate limiting and input sanitization and follow REST best practices.
```

---

## Refactoring

### 4. Extract Reusable Component/Function

**Purpose:** Identify and extract repeated code into reusable components.

**Prompt:**
```
Analyze this code and extract reusable [COMPONENT/FUNCTION]:
[CODE_BLOCK]

Identify repeated patterns and create:
- Reusable abstractions that follow DRY principles
- Appropriate parameter interfaces
- Proper separation of concerns
- Name suggestions following [NAMING_CONVENTION]

Refactor the original code to use these new abstractions.
```

**Example:**
```
Analyze this code and extract reusable functions:
[code showing repeated form validation logic]

Identify repeated patterns and create:
- Reusable abstractions that follow DRY principles
- Appropriate parameter interfaces
- Proper separation of concerns
- Name suggestions following verb-noun naming convention

Refactor the original code to use these new abstractions.
```

---

### 5. Modernize Legacy Code

**Purpose:** Update old code to use modern patterns and features.

**Prompt:**
```
Modernize this [LANGUAGE] code from [OLD_VERSION] to [NEW_VERSION]:
[CODE_BLOCK]

Apply these improvements:
- Use modern syntax features: [SPECIFIC_FEATURES]
- Replace deprecated APIs with: [NEW_APIS]
- Improve type safety with [TYPING_IMPROVEMENTS]
- Enhance performance using [OPTIMIZATION_TECHNIQUES]
- Maintain backward compatibility: [YES/NO]

Explain each significant change made.
```

**Example:**
```
Modernize this JavaScript code from ES5 to ES2022:
[code using var, function callbacks, manual promise chains]

Apply these improvements:
- Use modern syntax features: const/let, arrow functions, async/await
- Replace deprecated APIs with current standards
- Improve type safety with JSDoc annotations
- Enhance performance using optional chaining and nullish coalescing
- Maintain backward compatibility: NO

Explain each significant change made.
```

---

### 6. Reduce Code Complexity

**Purpose:** Simplify complex code and reduce cyclomatic complexity.

**Prompt:**
```
Simplify this complex [LANGUAGE] code:
[CODE_BLOCK]

Goals:
- Reduce cyclomatic complexity from [CURRENT] to under [TARGET]
- Extract nested logic into separate functions
- Replace complex conditionals with [PREFERRED_PATTERN]
- Improve readability while maintaining functionality
- Add clear variable/function names

Provide before/after complexity metrics.
```

**Example:**
```
Simplify this complex Python code:
[code with deeply nested if-else, multiple loops]

Goals:
- Reduce cyclomatic complexity from 15 to under 10
- Extract nested logic into separate functions
- Replace complex conditionals with guard clauses and early returns
- Improve readability while maintaining functionality
- Add clear variable/function names

Provide before/after complexity metrics.
```

---

### 7. Apply Design Pattern

**Purpose:** Refactor code to implement a specific design pattern.

**Prompt:**
```
Refactor this code to implement the [PATTERN_NAME] pattern:
[CODE_BLOCK]

Requirements:
- Maintain existing functionality
- Follow [PATTERN_NAME] pattern structure
- Improve [SPECIFIC_QUALITIES: flexibility/testability/maintainability]
- Add appropriate interfaces/abstractions
- Include usage examples

Explain why this pattern improves the code.
```

**Example:**
```
Refactor this code to implement the Strategy pattern:
[code with multiple if-else for different payment methods]

Requirements:
- Maintain existing functionality
- Follow Strategy pattern structure
- Improve flexibility and extensibility
- Add appropriate interfaces/abstractions
- Include usage examples

Explain why this pattern improves the code.
```

---

## Debugging

### 8. Debug Runtime Error

**Purpose:** Identify and fix runtime errors.

**Prompt:**
```
Debug this [LANGUAGE] code that produces the following error:

Error: [ERROR_MESSAGE]
Stack trace: [STACK_TRACE]

Code:
[CODE_BLOCK]

Context:
- Input that causes error: [EXAMPLE_INPUT]
- Expected behavior: [EXPECTED_OUTPUT]
- Environment: [RUNTIME_ENVIRONMENT]

Identify the root cause, explain why it occurs, and provide a fix with test cases.
```

**Example:**
```
Debug this Python code that produces the following error:

Error: IndexError: list index out of range
Stack trace: File "process.py", line 42, in process_data

Code:
[code snippet]

Context:
- Input that causes error: Empty list []
- Expected behavior: Should return 0 for empty lists
- Environment: Python 3.11

Identify the root cause, explain why it occurs, and provide a fix with test cases.
```

---

### 9. Fix Logic Bug

**Purpose:** Identify and correct logical errors in code.

**Prompt:**
```
This code has a logic bug - it produces incorrect results:

Code:
[CODE_BLOCK]

Issue:
- Input: [TEST_INPUT]
- Current output: [ACTUAL_OUTPUT]
- Expected output: [EXPECTED_OUTPUT]

Analyze the logic flow, identify where the bug occurs, explain the faulty logic, and provide a corrected version with explanation.
```

**Example:**
```
This code has a logic bug - it produces incorrect results:

Code:
[function calculating discounts]

Issue:
- Input: orderTotal = 100, discountPercent = 20
- Current output: 120
- Expected output: 80

Analyze the logic flow, identify where the bug occurs, explain the faulty logic, and provide a corrected version with explanation.
```

---

### 10. Memory Leak Investigation

**Purpose:** Find and fix memory leaks.

**Prompt:**
```
This [LANGUAGE] application has a memory leak:

Symptoms:
- Memory usage: [GROWTH_PATTERN]
- Occurs when: [TRIGGERING_CONDITIONS]
- Environment: [RUNTIME_DETAILS]

Code areas involved:
[CODE_BLOCK]

Analyze for common memory leak patterns:
- Event listeners not removed
- Circular references
- Unclosed resources
- Growing caches/collections

Identify the leak source and provide a fix.
```

**Example:**
```
This JavaScript React application has a memory leak:

Symptoms:
- Memory usage: Increases by 50MB every minute
- Occurs when: Navigating between pages repeatedly
- Environment: React 18, Chrome browser

Code areas involved:
[component with useEffect and event listeners]

Analyze for common memory leak patterns:
- Event listeners not removed
- Circular references
- Unclosed resources
- Growing caches/collections

Identify the leak source and provide a fix.
```

---

### 11. Performance Bottleneck Analysis

**Purpose:** Identify and optimize performance issues.

**Prompt:**
```
This code has performance issues:

Performance data:
- Current execution time: [CURRENT_TIME]
- Target execution time: [TARGET_TIME]
- Dataset size: [DATA_SIZE]
- Profiling results: [PROFILER_OUTPUT]

Code:
[CODE_BLOCK]

Analyze for:
- Algorithmic complexity (current Big-O)
- Unnecessary operations/iterations
- Inefficient data structures
- I/O optimization opportunities

Provide optimized version with complexity analysis.
```

**Example:**
```
This code has performance issues:

Performance data:
- Current execution time: 5 seconds
- Target execution time: < 500ms
- Dataset size: 10,000 items
- Profiling results: 80% time in nested loop

Code:
[nested loop searching algorithm]

Analyze for:
- Algorithmic complexity (current Big-O)
- Unnecessary operations/iterations
- Inefficient data structures
- I/O optimization opportunities

Provide optimized version with complexity analysis.
```

---

## Code Review

### 12. Security Audit

**Purpose:** Identify security vulnerabilities in code.

**Prompt:**
```
Perform a security audit on this [LANGUAGE] code:
[CODE_BLOCK]

Check for:
- Input validation and sanitization
- SQL injection vulnerabilities
- XSS vulnerabilities
- Authentication/authorization issues
- Sensitive data exposure
- Dependency vulnerabilities
- [SPECIFIC_SECURITY_CONCERNS]

For each issue found, provide:
- Severity level (Critical/High/Medium/Low)
- Explanation of the vulnerability
- Exploitation scenario
- Recommended fix
```

**Example:**
```
Perform a security audit on this Node.js Express code:
[API endpoint code]

Check for:
- Input validation and sanitization
- SQL injection vulnerabilities
- XSS vulnerabilities
- Authentication/authorization issues
- Sensitive data exposure
- Dependency vulnerabilities
- Rate limiting and CSRF protection

For each issue found, provide:
- Severity level (Critical/High/Medium/Low)
- Explanation of the vulnerability
- Exploitation scenario
- Recommended fix
```

---

### 13. Code Quality Review

**Purpose:** Evaluate code quality and suggest improvements.

**Prompt:**
```
Review this code for quality and best practices:
[CODE_BLOCK]

Evaluate:
- Readability and maintainability
- Code organization and structure
- Naming conventions
- Error handling
- Documentation/comments
- SOLID principles adherence
- [LANGUAGE]-specific best practices
- Test coverage considerations

Provide specific recommendations with examples.
```

**Example:**
```
Review this code for quality and best practices:
[Python class implementation]

Evaluate:
- Readability and maintainability
- Code organization and structure
- Naming conventions
- Error handling
- Documentation/comments
- SOLID principles adherence
- Python PEP 8 best practices
- Test coverage considerations

Provide specific recommendations with examples.
```

---

## Code Conversion

### 14. Language Migration

**Purpose:** Convert code from one programming language to another.

**Prompt:**
```
Convert this [SOURCE_LANGUAGE] code to [TARGET_LANGUAGE]:
[CODE_BLOCK]

Requirements:
- Maintain exact functionality
- Use idiomatic [TARGET_LANGUAGE] patterns
- Follow [TARGET_LANGUAGE] conventions
- Update data types appropriately
- Adapt to [TARGET_LANGUAGE] standard library
- Include necessary imports/dependencies

Highlight any concepts that don't translate directly.
```

**Example:**
```
Convert this Python code to Go:
[Python class with methods]

Requirements:
- Maintain exact functionality
- Use idiomatic Go patterns
- Follow Go conventions and error handling
- Update data types appropriately
- Adapt to Go standard library
- Include necessary imports/dependencies

Highlight any concepts that don't translate directly.
```

---

### 15. Framework Migration

**Purpose:** Migrate code between frameworks.

**Prompt:**
```
Migrate this code from [OLD_FRAMEWORK] to [NEW_FRAMEWORK]:
[CODE_BLOCK]

Translation needs:
- Component/module structure
- State management approach
- Routing implementation
- Lifecycle methods/hooks
- Event handling
- Styling approach
- [SPECIFIC_FEATURES]

Provide equivalent [NEW_FRAMEWORK] implementation with explanatory comments.
```

**Example:**
```
Migrate this code from Angular to React:
[Angular component with services]

Translation needs:
- Component structure
- Dependency injection to hooks
- RxJS observables to React Query
- Lifecycle methods to useEffect
- Event handling
- CSS approach
- Form validation

Provide equivalent React implementation with explanatory comments.
```

---

## Code Generation Utilities

### 16. Generate Boilerplate

**Purpose:** Create standard boilerplate code structures.

**Prompt:**
```
Generate [LANGUAGE] boilerplate for [PROJECT_TYPE]:

Requirements:
- Project structure: [FOLDER_ORGANIZATION]
- Configuration files: [CONFIG_NEEDS]
- Entry points: [MAIN_FILES]
- Common utilities: [UTILITY_FUNCTIONS]
- Error handling setup
- Logging configuration
- Environment variable handling
- [SPECIFIC_REQUIREMENTS]

Follow [STYLE_GUIDE] and include README with setup instructions.
```

**Example:**
```
Generate Node.js boilerplate for REST API microservice:

Requirements:
- Project structure: MVC pattern with routes, controllers, services, models
- Configuration files: ESLint, Prettier, tsconfig.json, Docker
- Entry points: server.ts with Express setup
- Common utilities: logger, error handler, validation middleware
- Error handling setup
- Logging configuration with Winston
- Environment variable handling with dotenv
- Health check and metrics endpoints

Follow TypeScript strict mode and include README with setup instructions.
```

---

### 17. Generate CRUD Operations

**Purpose:** Create complete CRUD functionality.

**Prompt:**
```
Generate complete CRUD operations for [ENTITY]:

Entity schema:
[SCHEMA_DEFINITION]

Include:
- Database model/schema
- API endpoints (Create, Read, Update, Delete, List)
- Validation logic
- Error handling
- Database queries/ORM methods
- Request/response DTOs
- Authentication/authorization checks
- Pagination for list endpoint
- Framework: [FRAMEWORK_NAME]
- Database: [DATABASE_TYPE]

Follow REST conventions and include example requests.
```

**Example:**
```
Generate complete CRUD operations for Product:

Entity schema:
- id: UUID (auto-generated)
- name: string (required, max 100 chars)
- description: text (optional)
- price: decimal (required, positive)
- category: string (required)
- stock: integer (required, non-negative)
- createdAt, updatedAt: timestamps

Include:
- Database model/schema
- API endpoints (Create, Read, Update, Delete, List)
- Validation logic
- Error handling
- Database queries/ORM methods
- Request/response DTOs
- Authentication/authorization checks
- Pagination for list endpoint
- Framework: NestJS
- Database: PostgreSQL with TypeORM

Follow REST conventions and include example requests.
```

---

### 18. Generate Type Definitions

**Purpose:** Create comprehensive type definitions.

**Prompt:**
```
Generate [TYPESCRIPT/FLOW/ETC] type definitions for:
[API_SPEC or JSON_SCHEMA or DESCRIPTION]

Requirements:
- Complete type coverage
- Proper use of unions, intersections, generics
- Utility types where appropriate
- Strict null checking compatibility
- Readonly properties where immutability needed
- Documentation comments
- Export statements

Make types as specific and type-safe as possible.
```

**Example:**
```
Generate TypeScript type definitions for:
User management API with endpoints for users, roles, and permissions

Requirements:
- Complete type coverage for all entities and API responses
- Proper use of unions, intersections, generics
- Utility types where appropriate
- Strict null checking compatibility
- Readonly properties for IDs and timestamps
- JSDoc documentation comments
- Export statements

Make types as specific and type-safe as possible.
```

---

## Advanced Techniques

### 19. Implement Algorithm

**Purpose:** Create an implementation of a specific algorithm.

**Prompt:**
```
Implement the [ALGORITHM_NAME] algorithm in [LANGUAGE]:

Requirements:
- Input: [INPUT_DESCRIPTION]
- Output: [OUTPUT_DESCRIPTION]
- Time complexity target: [BIG_O]
- Space complexity target: [BIG_O]
- Handle edge cases: [EDGE_CASES]
- Constraints: [SPECIFIC_CONSTRAINTS]

Include:
- Clean, readable implementation
- Inline comments explaining key steps
- Example usage
- Unit test cases
```

**Example:**
```
Implement the Dijkstra's shortest path algorithm in Python:

Requirements:
- Input: Graph as adjacency list, start node, end node
- Output: Shortest path as list of nodes and total distance
- Time complexity target: O((V + E) log V)
- Space complexity target: O(V)
- Handle edge cases: disconnected graph, negative weights, same start/end
- Constraints: Works with weighted directed graphs

Include:
- Clean, readable implementation
- Inline comments explaining key steps
- Example usage with sample graph
- Unit test cases for edge cases
```

---

### 20. Optimize Data Structure Usage

**Purpose:** Choose and implement optimal data structures.

**Prompt:**
```
Analyze this code and optimize data structure usage:
[CODE_BLOCK]

Current issues:
- Operations performed: [LIST_OPERATIONS]
- Current data structure: [CURRENT_DS]
- Performance problems: [ISSUES]

Recommend optimal data structure(s) based on:
- Operation frequency and patterns
- Time complexity requirements
- Space complexity constraints
- [SPECIFIC_REQUIREMENTS]

Provide refactored code with the new data structure and complexity analysis.
```

**Example:**
```
Analyze this code and optimize data structure usage:
[code using array for frequent lookups and insertions]

Current issues:
- Operations performed: 90% lookups by key, 5% insertions, 5% deletions
- Current data structure: Array with linear search
- Performance problems: O(n) lookups causing slowdowns with 10k+ items

Recommend optimal data structure(s) based on:
- Operation frequency (lookups dominant)
- Time complexity requirements: O(1) for lookups
- Space complexity constraints: Reasonable tradeoff for speed
- Need to maintain insertion order

Provide refactored code with the new data structure and complexity analysis.
```

---

### 21. Generate Mock Data

**Purpose:** Create realistic mock/test data.

**Prompt:**
```
Generate realistic mock data for [ENTITY/SCENARIO]:

Schema:
[DATA_STRUCTURE]

Requirements:
- Generate [NUMBER] records
- Data characteristics: [REALISTIC_PATTERNS]
- Include edge cases: [EDGE_CASES]
- Relationships: [FOREIGN_KEYS/REFERENCES]
- Format: [JSON/SQL/CSV/CODE]
- Use realistic values (names, emails, dates, etc.)

Ensure data is diverse and represents real-world scenarios.
```

**Example:**
```
Generate realistic mock data for e-commerce orders:

Schema:
- orderId, userId, products[], totalAmount, status, orderDate, shippingAddress

Requirements:
- Generate 50 records
- Data characteristics: Various statuses, realistic prices, recent dates
- Include edge cases: cancelled orders, high-value orders, multiple items
- Relationships: Users can have multiple orders
- Format: TypeScript array of objects
- Use realistic values (names, emails, addresses, product names)

Ensure data is diverse and represents real-world scenarios.
```

---

### 22. Add Comprehensive Error Handling

**Purpose:** Enhance code with proper error handling.

**Prompt:**
```
Add comprehensive error handling to this code:
[CODE_BLOCK]

Implement:
- Try-catch blocks at appropriate levels
- Specific error types/classes for different failures
- Meaningful error messages with context
- Error logging with [LOGGING_FRAMEWORK]
- Graceful degradation where possible
- User-friendly error responses
- Retry logic for [TRANSIENT_ERRORS]
- Error boundary/global handler integration

Follow [LANGUAGE] error handling best practices.
```

**Example:**
```
Add comprehensive error handling to this code:
[database access code without error handling]

Implement:
- Try-catch blocks for database operations
- Specific error types: ValidationError, DatabaseError, NotFoundError
- Meaningful error messages with context (entity, operation, reason)
- Error logging with Winston
- Graceful degradation with circuit breaker pattern
- User-friendly error responses (don't expose internal details)
- Retry logic for connection timeout errors
- Error middleware integration for Express

Follow Node.js async/await error handling best practices.
```

---

### 23. Add Logging and Observability

**Purpose:** Instrument code with logging and monitoring.

**Prompt:**
```
Add logging and observability to this code:
[CODE_BLOCK]

Requirements:
- Logging framework: [LOGGER_NAME]
- Log levels: DEBUG, INFO, WARN, ERROR
- Structured logging with context
- Performance metrics: [KEY_OPERATIONS]
- Tracing for [DISTRIBUTED_OPERATIONS]
- Include correlation IDs
- Sanitize sensitive data
- Log format: [JSON/TEXT]

Add logs at key decision points, errors, and performance-critical operations.
```

**Example:**
```
Add logging and observability to this code:
[API request handler code]

Requirements:
- Logging framework: Pino
- Log levels: DEBUG for detailed flow, INFO for requests, WARN for retries, ERROR for failures
- Structured logging with userId, requestId, endpoint
- Performance metrics: request duration, database query time
- Tracing for external API calls
- Include correlation IDs for request tracking
- Sanitize sensitive data (passwords, tokens)
- Log format: JSON

Add logs at key decision points, errors, and performance-critical operations.
```

---

### 24. Parallelize Sequential Operations

**Purpose:** Convert sequential operations to parallel for better performance.

**Prompt:**
```
Optimize this code by parallelizing operations:
[CODE_BLOCK]

Identify:
- Independent operations that can run in parallel
- Current sequential bottlenecks
- Synchronization points needed

Refactor to use:
- [ASYNC_PATTERN: Promise.all/async-await/goroutines/threads]
- Proper error handling for parallel operations
- Result aggregation
- Rate limiting if needed: [CONCURRENCY_LIMIT]

Estimate performance improvement and explain trade-offs.
```

**Example:**
```
Optimize this code by parallelizing operations:
[code making multiple API calls sequentially]

Identify:
- Independent API calls that can run in parallel
- Current sequential bottlenecks (waiting for each API response)
- Synchronization points needed (need all results before proceeding)

Refactor to use:
- Promise.all with async/await
- Proper error handling (fail fast vs. partial success)
- Result aggregation into combined response
- Rate limiting: max 10 concurrent requests

Estimate performance improvement and explain trade-offs.
```

---

### 25. Add Caching Layer

**Purpose:** Implement caching to improve performance.

**Prompt:**
```
Add a caching layer to this code:
[CODE_BLOCK]

Requirements:
- Cache type: [MEMORY/REDIS/CDN/etc]
- Cache expensive operations: [OPERATIONS_TO_CACHE]
- TTL strategy: [TIME_BASED/EVENT_BASED]
- Cache invalidation: [INVALIDATION_RULES]
- Cache key generation: [KEY_STRATEGY]
- Handle cache misses gracefully
- Consider cache stampede prevention
- Metrics: hit/miss rates

Implement cache-aside pattern with appropriate error handling.
```

**Example:**
```
Add a caching layer to this code:
[database query code for user profiles]

Requirements:
- Cache type: Redis
- Cache expensive operations: getUserProfile, getUserPermissions
- TTL strategy: 15 minutes for profiles, 5 minutes for permissions
- Cache invalidation: On user update/delete events
- Cache key generation: user:{userId}:profile, user:{userId}:permissions
- Handle cache misses by querying database
- Use locking to prevent cache stampede
- Metrics: track hit/miss rates with StatsD

Implement cache-aside pattern with appropriate error handling.
```

---

## Additional Resources

- **Related:** See [prompt-engineering-guide.md](./prompt-engineering-guide.md) for tips on writing effective prompts
- **Testing:** See [testing-prompts.md](./testing-prompts.md) for test generation prompts
- **Documentation:** See [documentation-prompts.md](./documentation-prompts.md) for documentation prompts
