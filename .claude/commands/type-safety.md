# Add and Improve TypeScript Type Safety

You are tasked with adding or improving TypeScript types across the codebase to enhance type safety, catch bugs early, and improve developer experience.

## Instructions

1. **Analyze Current State**
   - Ask which file(s) or directory to improve
   - Check TypeScript configuration (tsconfig.json)
   - Identify uses of `any`, `unknown`, or missing types
   - Review existing type definitions
   - Check for type errors in the codebase
   - Assess current strict mode settings

2. **TypeScript Configuration Review**

   Review and recommend tsconfig.json settings:
   ```json
   {
     "compilerOptions": {
       "strict": true,              // Enable all strict type checking
       "noImplicitAny": true,       // Error on implied any
       "strictNullChecks": true,    // Strict null checking
       "strictFunctionTypes": true, // Strict function type checking
       "noImplicitThis": true,      // Error on implicit this
       "noImplicitReturns": true,   // Error on implicit returns
       "noFallthroughCasesInSwitch": true,
       "noUnusedLocals": true,      // Error on unused variables
       "noUnusedParameters": true,  // Error on unused parameters
       "exactOptionalPropertyTypes": true,
       "noUncheckedIndexedAccess": true
     }
   }
   ```

3. **Eliminate `any` Types**

   **Identify all `any` usage:**
   - Search for `: any`
   - Search for `as any`
   - Check function parameters
   - Check return types

   **Replace with specific types:**
   ```typescript
   // Bad
   function process(data: any): any {
     return data.value;
   }

   // Good
   interface DataInput {
     value: string;
   }
   function process(data: DataInput): string {
     return data.value;
   }
   ```

   **Use `unknown` for truly unknown types:**
   ```typescript
   // When you don't know the type
   function parseJSON(input: string): unknown {
     return JSON.parse(input);
   }

   // Then use type guards
   const result = parseJSON(data);
   if (isUser(result)) {
     console.log(result.name);
   }
   ```

4. **Create Type Definitions**

   **Interfaces for object shapes:**
   ```typescript
   interface User {
     id: string;
     name: string;
     email: string;
     role: 'admin' | 'user';
     createdAt: Date;
   }
   ```

   **Type aliases for unions/intersections:**
   ```typescript
   type Status = 'pending' | 'success' | 'error';
   type Result = SuccessResult | ErrorResult;
   ```

   **Discriminated unions:**
   ```typescript
   type ApiResponse =
     | { status: 'success'; data: Data }
     | { status: 'error'; error: string };
   ```

5. **Generic Types**

   Add generics for reusable, type-safe code:

   ```typescript
   // Generic functions
   function identity<T>(value: T): T {
     return value;
   }

   // Generic interfaces
   interface Repository<T> {
     findById(id: string): Promise<T | null>;
     save(entity: T): Promise<T>;
     delete(id: string): Promise<void>;
   }

   // Generic constraints
   function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
     return obj[key];
   }
   ```

6. **Utility Types**

   Use TypeScript utility types effectively:

   ```typescript
   // Partial - make all properties optional
   type PartialUser = Partial<User>;

   // Pick - select specific properties
   type UserPreview = Pick<User, 'id' | 'name'>;

   // Omit - exclude specific properties
   type UserWithoutPassword = Omit<User, 'password'>;

   // Required - make all properties required
   type RequiredConfig = Required<Config>;

   // Record - create object type
   type UserMap = Record<string, User>;

   // ReturnType - extract return type
   type FunctionReturn = ReturnType<typeof myFunction>;

   // Parameters - extract parameter types
   type FunctionParams = Parameters<typeof myFunction>;
   ```

7. **Type Guards**

   Create type guards for runtime type checking:

   ```typescript
   function isUser(value: unknown): value is User {
     return (
       typeof value === 'object' &&
       value !== null &&
       'id' in value &&
       'name' in value &&
       'email' in value
     );
   }

   function assertIsUser(value: unknown): asserts value is User {
     if (!isUser(value)) {
       throw new Error('Not a valid User');
     }
   }
   ```

8. **Strict Null Checking**

   Handle null/undefined explicitly:

   ```typescript
   // Use optional chaining
   const userName = user?.name;

   // Use nullish coalescing
   const displayName = userName ?? 'Anonymous';

   // Use non-null assertion (sparingly!)
   const name = user!.name;

   // Better: type narrowing
   if (user) {
     console.log(user.name);
   }
   ```

9. **Function Types**

   Properly type functions:

   ```typescript
   // Function type
   type Handler = (event: Event) => void;

   // Function with multiple signatures (overloads)
   function format(value: string): string;
   function format(value: number): string;
   function format(value: string | number): string {
     return String(value);
   }

   // Async functions
   async function fetchUser(id: string): Promise<User> {
     // implementation
   }

   // Callbacks
   function processData(
     data: Data,
     callback: (result: Result) => void
   ): void {
     // implementation
   }
   ```

10. **React Component Types**

    Properly type React components:

    ```typescript
    // Function component with props
    interface ButtonProps {
      label: string;
      onClick: () => void;
      disabled?: boolean;
      children?: React.ReactNode;
    }

    const Button: React.FC<ButtonProps> = ({ label, onClick, disabled }) => {
      return <button onClick={onClick} disabled={disabled}>{label}</button>;
    };

    // Or without React.FC
    function Button({ label, onClick, disabled }: ButtonProps) {
      return <button onClick={onClick} disabled={disabled}>{label}</button>;
    }

    // Hooks
    const [count, setCount] = useState<number>(0);
    const [user, setUser] = useState<User | null>(null);

    // Refs
    const inputRef = useRef<HTMLInputElement>(null);

    // Context
    const UserContext = createContext<User | null>(null);

    // Event handlers
    const handleClick = (event: React.MouseEvent<HTMLButtonElement>) => {
      // implementation
    };
    ```

11. **API Response Types**

    Type external API responses:

    ```typescript
    // Define API response types
    interface ApiResponse<T> {
      data: T;
      status: number;
      message: string;
    }

    // Use with fetch
    async function fetchUsers(): Promise<User[]> {
      const response = await fetch('/api/users');
      const data: ApiResponse<User[]> = await response.json();
      return data.data;
    }

    // Use Zod or similar for runtime validation
    import { z } from 'zod';

    const UserSchema = z.object({
      id: z.string(),
      name: z.string(),
      email: z.string().email(),
    });

    type User = z.infer<typeof UserSchema>;
    ```

12. **Module Augmentation**

    Extend third-party types when needed:

    ```typescript
    declare module 'express-serve-static-core' {
      interface Request {
        user?: User;
      }
    }
    ```

13. **Type-Only Imports**

    Use type-only imports for better tree-shaking:

    ```typescript
    import type { User, Post } from './types';
    ```

14. **Const Assertions**

    Use const assertions for literal types:

    ```typescript
    const colors = ['red', 'blue', 'green'] as const;
    type Color = typeof colors[number]; // 'red' | 'blue' | 'green'

    const config = {
      apiUrl: 'https://api.example.com',
      timeout: 5000,
    } as const;
    ```

15. **Index Signatures**

    Properly type dynamic properties:

    ```typescript
    interface StringMap {
      [key: string]: string;
    }

    // Better with Record
    type StringMap = Record<string, string>;
    ```

16. **Testing and Validation**
    - Run TypeScript compiler: `tsc --noEmit`
    - Check for type errors
    - Ensure no implicit any
    - Run tests to ensure types work correctly
    - Test type narrowing works as expected

17. **Documentation**
    - Add JSDoc comments with type info
    - Document generic type parameters
    - Explain complex types
    - Provide usage examples

18. **Final Report**

    Provide comprehensive report including:
    - Files updated with improved types
    - Number of `any` types eliminated
    - New type definitions created
    - Type errors fixed
    - Remaining type issues (if any)
    - Recommendations for stricter settings
    - Before/after TypeScript error count
    - Benefits of improved type safety

Complete the type safety improvements and ensure the codebase has strong, maintainable types.
