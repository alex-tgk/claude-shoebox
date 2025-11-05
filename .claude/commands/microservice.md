# Scaffold New Microservice

You are tasked with scaffolding a complete new microservice with API, database, Docker configuration, testing, and documentation.

## Instructions

1. **Gather Requirements**
   - Ask for the microservice name
   - Understand the service's purpose and responsibilities
   - Determine tech stack (Node.js/TypeScript, Go, etc.)
   - Identify database needs (PostgreSQL, MongoDB, etc.)
   - Determine API type (REST, GraphQL, gRPC)
   - Ask about authentication/authorization needs
   - Understand integration points with other services
   - Confirm deployment target (Kubernetes, Docker, etc.)

2. **Project Structure**

   **Node.js/TypeScript Microservice:**
   ```
   service-name/
   ├── src/
   │   ├── api/           # API routes and controllers
   │   ├── services/      # Business logic
   │   ├── repositories/  # Data access layer
   │   ├── models/        # Data models
   │   ├── middleware/    # Express middleware
   │   ├── config/        # Configuration
   │   ├── utils/         # Utility functions
   │   └── index.ts       # Entry point
   ├── tests/
   │   ├── unit/
   │   ├── integration/
   │   └── e2e/
   ├── Dockerfile
   ├── docker-compose.yml
   ├── .env.example
   ├── package.json
   ├── tsconfig.json
   └── README.md
   ```

   **Go Microservice:**
   ```
   service-name/
   ├── cmd/
   │   └── server/
   │       └── main.go
   ├── internal/
   │   ├── handlers/
   │   ├── services/
   │   ├── repository/
   │   ├── models/
   │   └── middleware/
   ├── pkg/              # Public packages
   ├── config/
   ├── migrations/
   ├── tests/
   ├── Dockerfile
   ├── docker-compose.yml
   ├── go.mod
   └── README.md
   ```

3. **API Layer**

   **REST API (Express/TypeScript):**
   - Set up Express server
   - Configure middleware (CORS, helmet, compression)
   - Create route definitions
   - Implement controllers
   - Add request validation (Zod/Joi)
   - Add authentication middleware (JWT)
   - Add rate limiting
   - Add request logging
   - Add error handling middleware
   - Set up OpenAPI/Swagger documentation

   **REST API (Go):**
   - Set up HTTP server (net/http or Gin/Echo)
   - Define routes and handlers
   - Add middleware (CORS, logging, recovery)
   - Implement handlers
   - Add validation
   - Add authentication middleware
   - Add rate limiting
   - Generate Swagger docs

4. **Service Layer**

   - Implement core business logic
   - Keep services database-agnostic
   - Handle business validations
   - Implement transaction management
   - Add error handling
   - Use dependency injection
   - Make services testable

5. **Repository/Data Access Layer**

   **TypeScript/Node.js:**
   - Choose ORM (TypeORM, Prisma, Sequelize)
   - Define database models/entities
   - Implement repository pattern
   - Create database migrations
   - Add connection pooling
   - Implement query optimization

   **Go:**
   - Use sqlx or GORM
   - Define structs for models
   - Implement repository interfaces
   - Create migrations (golang-migrate)
   - Add connection pooling
   - Use prepared statements

6. **Database Setup**

   **PostgreSQL:**
   - Create database schema
   - Set up migrations
   - Add indexes for performance
   - Configure connection pooling
   - Set up backup strategy

   **MongoDB:**
   - Design document schema
   - Set up indexes
   - Configure connection
   - Add validation rules

   **Redis (if needed):**
   - Set up for caching
   - Configure session storage
   - Implement pub/sub if needed

7. **Configuration Management**

   - Create .env.example file
   - Use environment variables
   - Implement config loader
   - Support multiple environments (dev, staging, prod)
   - Validate configuration on startup
   - Document all config options

   **Example .env:**
   ```
   NODE_ENV=development
   PORT=3000
   DATABASE_URL=postgresql://user:pass@localhost:5432/dbname
   REDIS_URL=redis://localhost:6379
   JWT_SECRET=your-secret-key
   API_KEY=your-api-key
   LOG_LEVEL=info
   ```

8. **Docker Configuration**

   **Dockerfile:**
   ```dockerfile
   # Multi-stage build for Node.js
   FROM node:20-alpine AS builder
   WORKDIR /app
   COPY package*.json ./
   RUN npm ci
   COPY . .
   RUN npm run build

   FROM node:20-alpine
   WORKDIR /app
   COPY --from=builder /app/dist ./dist
   COPY --from=builder /app/node_modules ./node_modules
   COPY package*.json ./
   EXPOSE 3000
   USER node
   CMD ["node", "dist/index.js"]
   ```

   **docker-compose.yml:**
   ```yaml
   version: '3.8'
   services:
     api:
       build: .
       ports:
         - "3000:3000"
       environment:
         - DATABASE_URL=postgresql://user:pass@db:5432/dbname
       depends_on:
         - db
         - redis
     db:
       image: postgres:15-alpine
       environment:
         POSTGRES_USER: user
         POSTGRES_PASSWORD: pass
         POSTGRES_DB: dbname
       volumes:
         - postgres_data:/var/lib/postgresql/data
     redis:
       image: redis:7-alpine
   volumes:
     postgres_data:
   ```

9. **Middleware**

   Implement essential middleware:
   - Authentication (JWT verification)
   - Authorization (role/permission checks)
   - Request logging
   - Error handling
   - Rate limiting
   - CORS
   - Security headers (helmet)
   - Request validation
   - Compression
   - Timeout handling

10. **Error Handling**

    - Create custom error classes
    - Implement global error handler
    - Use consistent error response format
    - Log errors appropriately
    - Don't expose sensitive info in errors
    - Handle async errors properly

11. **Logging**

    - Set up structured logging (Winston, Pino, or Zap)
    - Log levels (debug, info, warn, error)
    - Request/response logging
    - Error logging
    - Performance logging
    - Avoid logging sensitive data
    - Configure log rotation

12. **Health Checks and Monitoring**

    Implement health check endpoints:
    ```typescript
    // GET /health
    {
      "status": "healthy",
      "timestamp": "2024-01-01T00:00:00Z",
      "uptime": 123456,
      "checks": {
        "database": "healthy",
        "redis": "healthy"
      }
    }

    // GET /metrics (Prometheus format)
    ```

13. **Testing**

    **Unit Tests:**
    - Test services in isolation
    - Mock dependencies
    - Test business logic
    - Aim for >80% coverage

    **Integration Tests:**
    - Test API endpoints
    - Use test database
    - Test database operations
    - Test middleware

    **E2E Tests:**
    - Test complete workflows
    - Use docker-compose for dependencies
    - Test with realistic data

14. **API Documentation**

    - Generate OpenAPI/Swagger spec
    - Document all endpoints
    - Include request/response examples
    - Document error responses
    - Add authentication docs
    - Set up Swagger UI endpoint

15. **Security**

    - Implement authentication (JWT)
    - Add authorization checks
    - Validate all inputs
    - Sanitize outputs
    - Use parameterized queries
    - Add rate limiting
    - Use security headers
    - Encrypt sensitive data
    - Use HTTPS in production
    - Implement CORS properly
    - Add secrets management

16. **CI/CD Configuration**

    Create CI/CD pipeline:
    - Run linting
    - Run tests
    - Build Docker image
    - Push to registry
    - Deploy to environment

    **Example GitHub Actions:**
    ```yaml
    name: CI/CD
    on: [push]
    jobs:
      test:
        runs-on: ubuntu-latest
        steps:
          - uses: actions/checkout@v2
          - uses: actions/setup-node@v2
          - run: npm ci
          - run: npm test
          - run: npm run build
      docker:
        needs: test
        runs-on: ubuntu-latest
        steps:
          - uses: docker/build-push-action@v2
    ```

17. **README Documentation**

    Create comprehensive README:
    - Service overview
    - Architecture diagram
    - Prerequisites
    - Installation instructions
    - Configuration guide
    - Running locally
    - Running with Docker
    - API documentation link
    - Testing instructions
    - Deployment guide
    - Contributing guidelines

18. **Additional Files**

    Create:
    - .gitignore
    - .dockerignore
    - .eslintrc (if TypeScript)
    - .prettierrc (if TypeScript)
    - LICENSE
    - CHANGELOG.md

19. **Final Checklist**

    Ensure:
    - [ ] All code compiles/builds
    - [ ] All tests pass
    - [ ] Docker image builds successfully
    - [ ] docker-compose up works
    - [ ] Health checks work
    - [ ] API documentation is accessible
    - [ ] README is comprehensive
    - [ ] Environment variables are documented
    - [ ] Security best practices followed
    - [ ] Logging is configured
    - [ ] Error handling is comprehensive

20. **Deliverables**

    Provide summary including:
    - Complete project structure
    - All files created
    - How to run locally
    - How to run with Docker
    - API endpoints available
    - Testing instructions
    - Next steps for deployment
    - Integration points with other services

Complete the microservice scaffolding and ensure it's production-ready.
