# Generate TypeScript Client SDK from OpenAPI/Swagger

You are tasked with generating a type-safe TypeScript client SDK from OpenAPI/Swagger specifications for consuming REST APIs.

## Instructions

1. **Gather Requirements**
   - Ask for the OpenAPI/Swagger specification (URL or file path)
   - Determine the output location for generated client
   - Ask about authentication method (API key, Bearer token, OAuth)
   - Understand the target environment (browser, Node.js, both)
   - Ask about additional features (retry logic, caching, etc.)

2. **Validate OpenAPI Specification**
   - Read the OpenAPI/Swagger spec
   - Validate it's valid OpenAPI 3.0+ or Swagger 2.0
   - Check for all required fields
   - Verify operation IDs exist for all endpoints
   - Review response and request schemas
   - Check for security definitions

3. **Choose Generation Strategy**

   **Option 1: Use OpenAPI Generator**
   ```bash
   npx @openapitools/openapi-generator-cli generate \
     -i ./openapi.yaml \
     -g typescript-axios \
     -o ./src/generated/api-client
   ```

   **Option 2: Use openapi-typescript + openapi-fetch**
   ```bash
   npx openapi-typescript ./openapi.yaml -o ./src/generated/api.ts
   ```

   **Option 3: Custom generator with Orval**
   ```bash
   npx orval --config orval.config.ts
   ```

4. **Client Architecture**

   Create structured client with:
   ```
   api-client/
   ├── client/
   │   ├── index.ts           # Main client export
   │   ├── base.ts            # Base HTTP client
   │   ├── config.ts          # Client configuration
   │   └── types.ts           # Shared types
   ├── resources/             # API resource clients
   │   ├── users.ts
   │   ├── posts.ts
   │   └── index.ts
   ├── models/                # Generated types/interfaces
   │   └── index.ts
   ├── errors/                # Error handling
   │   ├── api-error.ts
   │   └── index.ts
   └── index.ts               # Public API
   ```

5. **Base HTTP Client**

   Create base client with common functionality:

   ```typescript
   // client/base.ts
   import axios, { AxiosInstance, AxiosRequestConfig, AxiosResponse } from 'axios';
   import { ApiError } from '../errors/api-error';
   import { ClientConfig } from './config';

   export class BaseClient {
     protected client: AxiosInstance;

     constructor(config: ClientConfig) {
       this.client = axios.create({
         baseURL: config.baseURL,
         timeout: config.timeout || 30000,
         headers: {
           'Content-Type': 'application/json',
           ...config.headers,
         },
       });

       this.setupInterceptors(config);
     }

     private setupInterceptors(config: ClientConfig) {
       // Request interceptor - add auth token
       this.client.interceptors.request.use(
         (requestConfig) => {
           if (config.apiKey) {
             requestConfig.headers['Authorization'] = `Bearer ${config.apiKey}`;
           }
           return requestConfig;
         },
         (error) => Promise.reject(error)
       );

       // Response interceptor - handle errors
       this.client.interceptors.response.use(
         (response) => response,
         (error) => {
           throw new ApiError(
             error.response?.data?.message || error.message,
             error.response?.status,
             error.response?.data
           );
         }
       );
     }

     protected async request<T>(config: AxiosRequestConfig): Promise<T> {
       const response: AxiosResponse<T> = await this.client.request(config);
       return response.data;
     }
   }
   ```

6. **Configuration Interface**

   ```typescript
   // client/config.ts
   export interface ClientConfig {
     baseURL: string;
     apiKey?: string;
     timeout?: number;
     headers?: Record<string, string>;
     retryConfig?: {
       retries: number;
       retryDelay: number;
     };
   }

   export const defaultConfig: Partial<ClientConfig> = {
     timeout: 30000,
     retryConfig: {
       retries: 3,
       retryDelay: 1000,
     },
   };
   ```

7. **Resource Clients**

   Generate typed resource clients:

   ```typescript
   // resources/users.ts
   import { BaseClient } from '../client/base';
   import { User, CreateUserRequest, UpdateUserRequest } from '../models';

   export class UsersResource extends BaseClient {
     /**
      * Get all users
      */
     async list(params?: {
       page?: number;
       limit?: number;
       sort?: string;
     }): Promise<User[]> {
       return this.request<User[]>({
         method: 'GET',
         url: '/users',
         params,
       });
     }

     /**
      * Get user by ID
      * @param id - User ID
      */
     async get(id: string): Promise<User> {
       return this.request<User>({
         method: 'GET',
         url: `/users/${id}`,
       });
     }

     /**
      * Create a new user
      * @param data - User data
      */
     async create(data: CreateUserRequest): Promise<User> {
       return this.request<User>({
         method: 'POST',
         url: '/users',
         data,
       });
     }

     /**
      * Update user
      * @param id - User ID
      * @param data - Updated user data
      */
     async update(id: string, data: UpdateUserRequest): Promise<User> {
       return this.request<User>({
         method: 'PUT',
         url: `/users/${id}`,
         data,
       });
     }

     /**
      * Delete user
      * @param id - User ID
      */
     async delete(id: string): Promise<void> {
       return this.request<void>({
         method: 'DELETE',
         url: `/users/${id}`,
       });
     }
   }
   ```

8. **Type Generation**

   Generate TypeScript types from OpenAPI schemas:

   ```typescript
   // models/index.ts
   /**
    * User object
    */
   export interface User {
     id: string;
     email: string;
     username: string;
     firstName?: string;
     lastName?: string;
     role: 'user' | 'admin' | 'moderator';
     createdAt: string;
     updatedAt: string;
   }

   /**
    * Request body for creating a user
    */
   export interface CreateUserRequest {
     email: string;
     username: string;
     password: string;
     firstName?: string;
     lastName?: string;
   }

   /**
    * Request body for updating a user
    */
   export interface UpdateUserRequest {
     email?: string;
     username?: string;
     firstName?: string;
     lastName?: string;
   }

   /**
    * Paginated response wrapper
    */
   export interface PaginatedResponse<T> {
     data: T[];
     total: number;
     page: number;
     pageSize: number;
   }

   /**
    * API error response
    */
   export interface ErrorResponse {
     message: string;
     code: string;
     details?: Record<string, unknown>;
   }
   ```

9. **Error Handling**

   Create custom error classes:

   ```typescript
   // errors/api-error.ts
   export class ApiError extends Error {
     public readonly statusCode?: number;
     public readonly response?: unknown;
     public readonly isApiError = true;

     constructor(message: string, statusCode?: number, response?: unknown) {
       super(message);
       this.name = 'ApiError';
       this.statusCode = statusCode;
       this.response = response;

       // Maintains proper stack trace
       if (Error.captureStackTrace) {
         Error.captureStackTrace(this, ApiError);
       }
     }

     public is4xx(): boolean {
       return this.statusCode ? this.statusCode >= 400 && this.statusCode < 500 : false;
     }

     public is5xx(): boolean {
       return this.statusCode ? this.statusCode >= 500 : false;
     }
   }

   export class NotFoundError extends ApiError {
     constructor(message = 'Resource not found') {
       super(message, 404);
       this.name = 'NotFoundError';
     }
   }

   export class UnauthorizedError extends ApiError {
     constructor(message = 'Unauthorized') {
       super(message, 401);
       this.name = 'UnauthorizedError';
     }
   }

   export class ValidationError extends ApiError {
     constructor(message = 'Validation failed', details?: unknown) {
       super(message, 400, details);
       this.name = 'ValidationError';
     }
   }
   ```

10. **Main Client Class**

    Create the main API client:

    ```typescript
    // client/index.ts
    import { BaseClient } from './base';
    import { ClientConfig } from './config';
    import { UsersResource } from '../resources/users';
    import { PostsResource } from '../resources/posts';

    export class ApiClient extends BaseClient {
      public users: UsersResource;
      public posts: PostsResource;

      constructor(config: ClientConfig) {
        super(config);
        this.users = new UsersResource(config);
        this.posts = new PostsResource(config);
      }
    }

    // Factory function
    export function createClient(config: ClientConfig): ApiClient {
      return new ApiClient(config);
    }
    ```

11. **Advanced Features**

    **Retry Logic:**
    ```typescript
    import axiosRetry from 'axios-retry';

    axiosRetry(this.client, {
      retries: config.retryConfig?.retries || 3,
      retryDelay: axiosRetry.exponentialDelay,
      retryCondition: (error) => {
        return axiosRetry.isNetworkOrIdempotentRequestError(error) ||
               error.response?.status === 429; // Retry on rate limit
      },
    });
    ```

    **Request Caching:**
    ```typescript
    import { setupCache } from 'axios-cache-adapter';

    const cache = setupCache({
      maxAge: 15 * 60 * 1000, // 15 minutes
    });

    this.client = axios.create({
      adapter: cache.adapter,
    });
    ```

    **Request Cancellation:**
    ```typescript
    const controller = new AbortController();

    async get(id: string, signal?: AbortSignal): Promise<User> {
      return this.request<User>({
        method: 'GET',
        url: `/users/${id}`,
        signal,
      });
    }
    ```

12. **Usage Examples**

    Create comprehensive usage documentation:

    ```typescript
    // Example usage
    import { createClient } from './api-client';

    // Initialize client
    const client = createClient({
      baseURL: 'https://api.example.com',
      apiKey: process.env.API_KEY,
    });

    // Use the client
    async function example() {
      try {
        // List users
        const users = await client.users.list({ page: 1, limit: 10 });

        // Get specific user
        const user = await client.users.get('user-id');

        // Create user
        const newUser = await client.users.create({
          email: 'user@example.com',
          username: 'newuser',
          password: 'secure-password',
        });

        // Update user
        const updated = await client.users.update('user-id', {
          firstName: 'John',
          lastName: 'Doe',
        });

        // Delete user
        await client.users.delete('user-id');
      } catch (error) {
        if (error instanceof ApiError) {
          console.error('API Error:', error.message, error.statusCode);
        }
      }
    }
    ```

13. **Testing**

    Generate tests for the client:

    ```typescript
    // client/users.test.ts
    import { describe, it, expect, vi, beforeEach } from 'vitest';
    import axios from 'axios';
    import { ApiClient } from './client';

    vi.mock('axios');

    describe('UsersResource', () => {
      let client: ApiClient;

      beforeEach(() => {
        client = new ApiClient({
          baseURL: 'https://api.example.com',
          apiKey: 'test-key',
        });
      });

      it('should list users', async () => {
        const mockUsers = [{ id: '1', email: 'test@example.com' }];
        vi.mocked(axios.create).mockReturnValue({
          request: vi.fn().mockResolvedValue({ data: mockUsers }),
        } as any);

        const users = await client.users.list();
        expect(users).toEqual(mockUsers);
      });
    });
    ```

14. **Package Configuration**

    Create package.json for the client:

    ```json
    {
      "name": "@your-org/api-client",
      "version": "1.0.0",
      "description": "TypeScript client for Your API",
      "main": "dist/index.js",
      "types": "dist/index.d.ts",
      "scripts": {
        "build": "tsc",
        "generate": "openapi-typescript ./openapi.yaml -o ./src/generated/api.ts",
        "test": "vitest"
      },
      "dependencies": {
        "axios": "^1.6.0"
      },
      "devDependencies": {
        "@types/node": "^20.0.0",
        "typescript": "^5.3.0",
        "openapi-typescript": "^6.7.0",
        "vitest": "^1.0.0"
      }
    }
    ```

15. **Documentation**

    Create comprehensive README:
    - Installation instructions
    - Configuration options
    - Authentication setup
    - Usage examples for all resources
    - Error handling guide
    - TypeScript examples
    - API reference link

16. **Final Deliverables**

    Provide:
    - Generated client code
    - Type definitions
    - Error classes
    - Usage examples
    - Tests
    - README documentation
    - Build configuration
    - Package.json
    - Integration instructions

Complete the client SDK generation ensuring type safety, error handling, and developer experience.
