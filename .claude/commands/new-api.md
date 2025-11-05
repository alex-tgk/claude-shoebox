# Scaffold New REST API Endpoint

You are tasked with scaffolding a new REST API endpoint with TypeScript/Express or Go, following best practices and industry standards.

## Instructions

1. **Gather Requirements**
   - Ask for the endpoint path (e.g., "/api/users", "/api/products/:id")
   - Determine HTTP methods needed (GET, POST, PUT, PATCH, DELETE)
   - Understand the data model and business logic
   - Ask which package/service this belongs to
   - Identify authentication/authorization requirements
   - Confirm the tech stack (TypeScript/Express vs Go)

2. **TypeScript/Express API Structure**

   Create the following files:
   - `{resource}.routes.ts` - Route definitions
   - `{resource}.controller.ts` - Request handlers
   - `{resource}.service.ts` - Business logic
   - `{resource}.model.ts` - Data models/interfaces
   - `{resource}.validation.ts` - Request validation schemas (Zod/Joi)
   - `{resource}.test.ts` - Integration tests

3. **Go API Structure**

   Create the following files:
   - `{resource}_handler.go` - HTTP handlers
   - `{resource}_service.go` - Business logic
   - `{resource}_model.go` - Data structures
   - `{resource}_repository.go` - Database operations
   - `{resource}_handler_test.go` - Tests

4. **Implementation Requirements**

   **Routes/Handlers:**
   - Define clear route paths following REST conventions
   - Use appropriate HTTP status codes
   - Implement proper request validation
   - Add authentication/authorization middleware
   - Include rate limiting if needed
   - Add request logging

   **Controllers/Handlers:**
   - Parse and validate request data
   - Call service layer for business logic
   - Format responses consistently
   - Handle errors gracefully
   - Return appropriate status codes

   **Service Layer:**
   - Implement core business logic
   - Keep it database-agnostic
   - Add transaction handling where needed
   - Implement caching if applicable
   - Add comprehensive error handling

   **Models:**
   - Define TypeScript interfaces or Go structs
   - Include validation rules
   - Add JSDoc/godoc comments
   - Define request/response DTOs

   **Validation:**
   - Use Zod (TypeScript) or validator package (Go)
   - Validate all input data
   - Provide clear error messages
   - Check for required fields, types, formats

5. **Error Handling**
   - Create custom error classes/types
   - Use consistent error response format
   - Log errors appropriately
   - Don't expose sensitive information in errors
   - Handle edge cases (null values, invalid IDs, etc.)

6. **Testing**
   - Write integration tests for all endpoints
   - Test successful responses
   - Test error cases (400, 401, 403, 404, 500)
   - Test validation failures
   - Test authentication/authorization
   - Mock external dependencies
   - Aim for >85% code coverage

7. **Documentation**
   - Add OpenAPI/Swagger annotations
   - Document request/response schemas
   - Include example requests and responses
   - Document authentication requirements
   - Add inline code comments for complex logic

8. **Security Considerations**
   - Validate and sanitize all inputs
   - Use parameterized queries to prevent SQL injection
   - Implement rate limiting
   - Add CORS configuration
   - Use helmet.js (Express) for security headers
   - Validate content-type headers
   - Implement proper authentication checks

9. **After Creation**
   - Register routes with the main app/router
   - Run tests and ensure they pass
   - Test endpoints manually with curl or Postman
   - Update API documentation
   - Provide usage examples to the user

Complete all steps and confirm successful creation with the user.
