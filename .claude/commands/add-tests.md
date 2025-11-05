# Generate Comprehensive Test Suites

You are tasked with generating comprehensive test suites for existing code to ensure quality, reliability, and maintainability.

## Instructions

1. **Analyze Existing Code**
   - Ask the user which file(s) or directory to test
   - Read and understand the code thoroughly
   - Identify all functions, methods, and components
   - Determine the current test coverage (if any)
   - Identify edge cases and error scenarios
   - Check for dependencies that need mocking

2. **Determine Testing Framework**
   - TypeScript/JavaScript: Vitest, Jest, or Mocha
   - React: React Testing Library + Vitest/Jest
   - Node.js APIs: Supertest + Vitest/Jest
   - Go: standard testing package + testify
   - Python: pytest
   - Check existing test files to match the project's conventions

3. **Test File Structure**
   - Create test file with appropriate naming:
     - `{filename}.test.ts` or `{filename}.spec.ts` (TypeScript/JS)
     - `{filename}_test.go` (Go)
     - `test_{filename}.py` (Python)
   - Use descriptive describe/test blocks
   - Group related tests logically
   - Follow AAA pattern: Arrange, Act, Assert

4. **Test Coverage Requirements**

   **Unit Tests:**
   - Test each function/method in isolation
   - Test with valid inputs
   - Test with invalid inputs
   - Test edge cases (empty, null, undefined, zero, negative)
   - Test boundary conditions
   - Test error handling and exceptions
   - Mock external dependencies

   **Integration Tests (if applicable):**
   - Test interactions between modules
   - Test database operations
   - Test API endpoints
   - Test authentication/authorization
   - Use test databases or mocks

   **Component Tests (React/Frontend):**
   - Test rendering with different props
   - Test user interactions (clicks, typing, etc.)
   - Test conditional rendering
   - Test state changes
   - Test hooks behavior
   - Test accessibility
   - Test error boundaries

5. **Testing Best Practices**
   - Write clear, descriptive test names
   - Each test should test one thing
   - Tests should be independent and isolated
   - Use factories or fixtures for test data
   - Mock external services (APIs, databases)
   - Avoid testing implementation details
   - Test behavior, not internals
   - Clean up after tests (afterEach/afterAll)
   - Use meaningful assertions
   - Aim for >85% code coverage

6. **Mocking Strategy**
   - Identify dependencies to mock:
     - External APIs
     - Database calls
     - File system operations
     - Date/time functions
     - Random number generators
   - Use appropriate mocking tools:
     - Vitest: vi.mock, vi.fn
     - Jest: jest.mock, jest.fn
     - Go: interfaces and mock implementations
   - Mock at the boundary, not deep inside

7. **Test Data Management**
   - Create reusable test fixtures
   - Use factories for generating test data
   - Keep test data minimal and focused
   - Avoid hardcoding sensitive data
   - Use realistic but fake data

8. **Assertions**
   - Use specific assertions (toBe, toEqual, toContain, etc.)
   - Check return values
   - Verify side effects
   - Check error messages
   - Validate data types
   - Test async operations properly (await, async/await)

9. **Error and Exception Testing**
   - Test all error paths
   - Verify error messages
   - Test exception handling
   - Test validation failures
   - Test timeout scenarios

10. **Performance and Snapshot Tests (where applicable)**
    - Add snapshot tests for components
    - Test performance-critical functions
    - Add benchmarks for critical paths
    - Test memory usage for large operations

11. **After Creation**
    - Run the test suite and ensure all tests pass
    - Check code coverage report
    - Fix any failing tests
    - Identify gaps in coverage
    - Add missing tests for uncovered code
    - Provide summary of coverage and test results

Complete all steps and provide a detailed summary of the tests created and coverage achieved.
