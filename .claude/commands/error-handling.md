# Add Comprehensive Error Handling and Logging

You are tasked with implementing comprehensive error handling and logging throughout the codebase to improve reliability, debugging, and monitoring.

## Instructions

1. **Analyze Current State**
   - Ask which file(s) or directory to improve
   - Identify existing error handling patterns
   - Check current logging implementation
   - Review error scenarios (network, database, validation, etc.)
   - Identify missing error handling

2. **Error Handling Strategy**

   **Define Error Categories:**
   - Operational errors (expected, recoverable)
   - Programming errors (bugs, should crash)
   - Network errors
   - Database errors
   - Validation errors
   - Authentication/Authorization errors
   - External service errors
   - User errors

3. **Custom Error Classes (TypeScript/JavaScript)**

   Create a hierarchy of custom error classes:

   ```typescript
   // errors/base.error.ts
   export abstract class BaseError extends Error {
     public readonly name: string;
     public readonly httpCode: number;
     public readonly isOperational: boolean;
     public readonly timestamp: Date;

     constructor(
       name: string,
       httpCode: number,
       description: string,
       isOperational: boolean
     ) {
       super(description);
       Object.setPrototypeOf(this, new.target.prototype);

       this.name = name;
       this.httpCode = httpCode;
       this.isOperational = isOperational;
       this.timestamp = new Date();

       Error.captureStackTrace(this);
     }
   }

   // errors/api.error.ts
   export class ApiError extends BaseError {
     constructor(
       name: string,
       httpCode = 500,
       description = 'Internal server error',
       isOperational = true
     ) {
       super(name, httpCode, description, isOperational);
     }
   }

   // errors/validation.error.ts
   export class ValidationError extends ApiError {
     public readonly errors: Record<string, string[]>;

     constructor(errors: Record<string, string[]>) {
       super('VALIDATION_ERROR', 400, 'Validation failed', true);
       this.errors = errors;
     }
   }

   // errors/not-found.error.ts
   export class NotFoundError extends ApiError {
     constructor(resource: string, id?: string) {
       const message = id
         ? `${resource} with id ${id} not found`
         : `${resource} not found`;
       super('NOT_FOUND', 404, message, true);
     }
   }

   // errors/unauthorized.error.ts
   export class UnauthorizedError extends ApiError {
     constructor(message = 'Unauthorized') {
       super('UNAUTHORIZED', 401, message, true);
     }
   }

   // errors/forbidden.error.ts
   export class ForbiddenError extends ApiError {
     constructor(message = 'Forbidden') {
       super('FORBIDDEN', 403, message, true);
     }
   }

   // errors/conflict.error.ts
   export class ConflictError extends ApiError {
     constructor(message: string) {
       super('CONFLICT', 409, message, true);
     }
   }

   // errors/database.error.ts
   export class DatabaseError extends ApiError {
     constructor(message: string, originalError?: Error) {
       super('DATABASE_ERROR', 500, message, true);
       if (originalError) {
         this.stack = originalError.stack;
       }
     }
   }

   // errors/external-service.error.ts
   export class ExternalServiceError extends ApiError {
     public readonly service: string;

     constructor(service: string, message: string) {
       super('EXTERNAL_SERVICE_ERROR', 502, message, true);
       this.service = service;
     }
   }
   ```

4. **Error Handler Middleware (Express)**

   ```typescript
   // middleware/error-handler.ts
   import { Request, Response, NextFunction } from 'express';
   import { BaseError } from '../errors/base.error';
   import { logger } from '../utils/logger';

   export function errorHandler(
     err: Error,
     req: Request,
     res: Response,
     next: NextFunction
   ): void {
     // Log error
     logger.error('Error occurred', {
       error: err.message,
       stack: err.stack,
       path: req.path,
       method: req.method,
       ip: req.ip,
       userId: req.user?.id,
     });

     // Handle custom errors
     if (err instanceof BaseError) {
       res.status(err.httpCode).json({
         success: false,
         error: {
           name: err.name,
           message: err.message,
           ...(err instanceof ValidationError && { errors: err.errors }),
         },
       });
       return;
     }

     // Handle specific error types
     if (err.name === 'CastError') {
       res.status(400).json({
         success: false,
         error: {
           name: 'INVALID_ID',
           message: 'Invalid ID format',
         },
       });
       return;
     }

     if (err.name === 'JsonWebTokenError') {
       res.status(401).json({
         success: false,
         error: {
           name: 'INVALID_TOKEN',
           message: 'Invalid authentication token',
         },
       });
       return;
     }

     // Handle unknown errors
     res.status(500).json({
       success: false,
       error: {
         name: 'INTERNAL_ERROR',
         message: process.env.NODE_ENV === 'production'
           ? 'An unexpected error occurred'
           : err.message,
       },
     });
   }

   // middleware/async-handler.ts
   export function asyncHandler(
     fn: (req: Request, res: Response, next: NextFunction) => Promise<any>
   ) {
     return (req: Request, res: Response, next: NextFunction) => {
       Promise.resolve(fn(req, res, next)).catch(next);
     };
   }
   ```

5. **Error Handling in Services**

   ```typescript
   // services/user.service.ts
   import { NotFoundError, ValidationError, DatabaseError } from '../errors';
   import { logger } from '../utils/logger';

   export class UserService {
     async getUser(id: string): Promise<User> {
       try {
         const user = await this.userRepository.findById(id);

         if (!user) {
           throw new NotFoundError('User', id);
         }

         return user;
       } catch (error) {
         if (error instanceof NotFoundError) {
           throw error;
         }

         logger.error('Failed to get user', { id, error });
         throw new DatabaseError('Failed to retrieve user');
       }
     }

     async createUser(data: CreateUserDto): Promise<User> {
       // Validate input
       const validationErrors = this.validateUserData(data);
       if (Object.keys(validationErrors).length > 0) {
         throw new ValidationError(validationErrors);
       }

       try {
         // Check for existing user
         const existingUser = await this.userRepository.findByEmail(data.email);
         if (existingUser) {
           throw new ConflictError('User with this email already exists');
         }

         return await this.userRepository.create(data);
       } catch (error) {
         if (error instanceof ConflictError) {
           throw error;
         }

         logger.error('Failed to create user', { data, error });
         throw new DatabaseError('Failed to create user');
       }
     }
   }
   ```

6. **Structured Logging (Winston)**

   ```typescript
   // utils/logger.ts
   import winston from 'winston';

   const levels = {
     error: 0,
     warn: 1,
     info: 2,
     http: 3,
     debug: 4,
   };

   const colors = {
     error: 'red',
     warn: 'yellow',
     info: 'green',
     http: 'magenta',
     debug: 'blue',
   };

   winston.addColors(colors);

   const format = winston.format.combine(
     winston.format.timestamp({ format: 'YYYY-MM-DD HH:mm:ss' }),
     winston.format.errors({ stack: true }),
     winston.format.json(),
     winston.format.metadata(),
     winston.format.colorize({ all: true }),
     winston.format.printf((info) => {
       const { timestamp, level, message, metadata } = info;

       let log = `${timestamp} [${level}]: ${message}`;

       if (metadata && Object.keys(metadata).length > 0) {
         log += ` ${JSON.stringify(metadata)}`;
       }

       return log;
     })
   );

   const transports = [
     new winston.transports.Console(),
     new winston.transports.File({
       filename: 'logs/error.log',
       level: 'error',
       maxsize: 5242880, // 5MB
       maxFiles: 5,
     }),
     new winston.transports.File({
       filename: 'logs/combined.log',
       maxsize: 5242880,
       maxFiles: 5,
     }),
   ];

   export const logger = winston.createLogger({
     level: process.env.LOG_LEVEL || 'info',
     levels,
     format,
     transports,
     exitOnError: false,
   });

   // Stream for Morgan HTTP logging
   export const stream = {
     write: (message: string) => {
       logger.http(message.trim());
     },
   };
   ```

7. **Request Logging Middleware**

   ```typescript
   // middleware/request-logger.ts
   import morgan from 'morgan';
   import { logger, stream } from '../utils/logger';

   // Custom token for user ID
   morgan.token('user-id', (req: any) => req.user?.id || 'anonymous');

   export const requestLogger = morgan(
     ':method :url :status :response-time ms - :user-id',
     { stream }
   );

   // Detailed request logger
   export function logRequest(req: Request, res: Response, next: NextFunction) {
     const start = Date.now();

     res.on('finish', () => {
       const duration = Date.now() - start;

       logger.info('HTTP Request', {
         method: req.method,
         url: req.url,
         status: res.statusCode,
         duration: `${duration}ms`,
         userAgent: req.get('user-agent'),
         ip: req.ip,
         userId: req.user?.id,
       });
     });

     next();
   }
   ```

8. **Try-Catch Patterns**

   ```typescript
   // Good: Specific error handling
   async function fetchUserData(userId: string): Promise<UserData> {
     try {
       const response = await fetch(`/api/users/${userId}`);

       if (!response.ok) {
         throw new ExternalServiceError(
           'UserAPI',
           `Failed to fetch user: ${response.statusText}`
         );
       }

       return await response.json();
     } catch (error) {
       if (error instanceof ExternalServiceError) {
         throw error;
       }

       logger.error('Unexpected error fetching user data', { userId, error });
       throw new ExternalServiceError(
         'UserAPI',
         'An unexpected error occurred while fetching user data'
       );
     }
   }

   // Good: Resource cleanup
   async function processFile(filePath: string): Promise<void> {
     const fileHandle = await fs.open(filePath, 'r');

     try {
       const data = await fileHandle.readFile('utf-8');
       await processData(data);
     } catch (error) {
       logger.error('Error processing file', { filePath, error });
       throw new Error('Failed to process file');
     } finally {
       await fileHandle.close();
     }
   }
   ```

9. **Error Boundaries (React)**

   ```tsx
   // components/ErrorBoundary.tsx
   import React, { Component, ErrorInfo, ReactNode } from 'react';
   import { logger } from '../utils/logger';

   interface Props {
     children: ReactNode;
     fallback?: ReactNode;
     onError?: (error: Error, errorInfo: ErrorInfo) => void;
   }

   interface State {
     hasError: boolean;
     error?: Error;
   }

   export class ErrorBoundary extends Component<Props, State> {
     constructor(props: Props) {
       super(props);
       this.state = { hasError: false };
     }

     static getDerivedStateFromError(error: Error): State {
       return { hasError: true, error };
     }

     componentDidCatch(error: Error, errorInfo: ErrorInfo): void {
       logger.error('React Error Boundary caught error', {
         error: error.message,
         stack: error.stack,
         componentStack: errorInfo.componentStack,
       });

       this.props.onError?.(error, errorInfo);
     }

     render(): ReactNode {
       if (this.state.hasError) {
         return this.props.fallback || (
           <div className="error-container">
             <h2>Something went wrong</h2>
             <p>We're sorry for the inconvenience. Please try refreshing the page.</p>
             {process.env.NODE_ENV === 'development' && (
               <pre>{this.state.error?.stack}</pre>
             )}
           </div>
         );
       }

       return this.props.children;
     }
   }
   ```

10. **Unhandled Rejection Handler**

    ```typescript
    // utils/process-handlers.ts
    import { logger } from './logger';

    export function setupProcessHandlers(): void {
      // Handle unhandled promise rejections
      process.on('unhandledRejection', (reason: Error, promise: Promise<any>) => {
        logger.error('Unhandled Promise Rejection', {
          reason: reason.message,
          stack: reason.stack,
          promise,
        });

        // Optionally exit the process
        if (!reason.isOperational) {
          process.exit(1);
        }
      });

      // Handle uncaught exceptions
      process.on('uncaughtException', (error: Error) => {
        logger.error('Uncaught Exception', {
          error: error.message,
          stack: error.stack,
        });

        // Always exit on uncaught exception
        process.exit(1);
      });

      // Graceful shutdown
      process.on('SIGTERM', async () => {
        logger.info('SIGTERM received, shutting down gracefully');

        // Close server, database connections, etc.
        await cleanup();

        process.exit(0);
      });
    }
    ```

11. **Validation Error Handling**

    ```typescript
    // middleware/validation.ts
    import { z } from 'zod';
    import { ValidationError } from '../errors';

    export function validate(schema: z.ZodSchema) {
      return (req: Request, res: Response, next: NextFunction) => {
        try {
          schema.parse(req.body);
          next();
        } catch (error) {
          if (error instanceof z.ZodError) {
            const errors: Record<string, string[]> = {};

            error.errors.forEach((err) => {
              const path = err.path.join('.');
              if (!errors[path]) {
                errors[path] = [];
              }
              errors[path].push(err.message);
            });

            next(new ValidationError(errors));
          } else {
            next(error);
          }
        }
      };
    }
    ```

12. **Monitoring and Alerting**

    Integrate with monitoring services:

    ```typescript
    // utils/monitoring.ts
    import * as Sentry from '@sentry/node';

    export function setupMonitoring(): void {
      if (process.env.SENTRY_DSN) {
        Sentry.init({
          dsn: process.env.SENTRY_DSN,
          environment: process.env.NODE_ENV,
          tracesSampleRate: 1.0,
        });
      }
    }

    export function captureException(error: Error, context?: Record<string, any>): void {
      logger.error('Exception captured', { error, context });

      if (process.env.SENTRY_DSN) {
        Sentry.captureException(error, { extra: context });
      }
    }
    ```

13. **Final Deliverables**

    Provide:
    - Custom error classes hierarchy
    - Error handling middleware
    - Structured logging setup
    - Request logging
    - Error boundaries (React)
    - Unhandled rejection handlers
    - Validation error handling
    - Monitoring integration
    - Documentation on error handling patterns

Complete error handling and logging implementation ensuring robust, debuggable applications.
