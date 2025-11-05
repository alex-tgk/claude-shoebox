# Generate Code Documentation

You are tasked with generating comprehensive documentation for code including JSDoc/TSDoc comments, inline comments, and README files.

## Instructions

1. **Identify Scope**
   - Ask which file(s) or directory to document
   - Determine documentation type needed:
     - Inline code comments
     - JSDoc/TSDoc/Godoc function documentation
     - README files
     - API documentation
     - Architecture documentation
   - Check existing documentation standards in the project

2. **Code Analysis**
   - Read and understand all code to be documented
   - Identify public APIs and exports
   - Understand function parameters and return values
   - Note edge cases and error conditions
   - Identify complex logic that needs explanation
   - Review dependencies and external integrations

3. **JSDoc/TSDoc Comments (TypeScript/JavaScript)**

   Add documentation for:

   **Functions/Methods:**
   ```typescript
   /**
    * Brief description of what the function does.
    *
    * Detailed explanation if needed, including:
    * - When to use this function
    * - Important behavior notes
    * - Side effects
    *
    * @param paramName - Description of the parameter
    * @param optionalParam - Description (optional)
    * @returns Description of return value
    * @throws {ErrorType} Description of when error is thrown
    *
    * @example
    * ```typescript
    * const result = functionName(arg1, arg2);
    * ```
    */
   ```

   **Classes/Components:**
   ```typescript
   /**
    * Brief description of the class/component.
    *
    * @remarks
    * Additional context, usage notes, or warnings.
    *
    * @example
    * ```tsx
    * <ComponentName prop1="value" />
    * ```
    */
   ```

   **Interfaces/Types:**
   ```typescript
   /**
    * Description of the interface/type.
    *
    * @property propertyName - Description of property
    */
   ```

   **Constants/Enums:**
   ```typescript
   /**
    * Description of what this constant represents.
    * Why this value was chosen.
    */
   ```

4. **Godoc Comments (Go)**

   ```go
   // PackageName provides...
   //
   // Additional package documentation.
   package packagename

   // FunctionName does something specific.
   //
   // It handles these cases:
   //   - Case 1
   //   - Case 2
   //
   // Example usage:
   //   result := FunctionName(arg)
   func FunctionName(arg string) (string, error)
   ```

5. **Inline Comments**

   Add inline comments for:
   - Complex algorithms or logic
   - Non-obvious code behavior
   - Workarounds or hacks (with explanation)
   - Performance optimizations
   - Regex patterns
   - Magic numbers (or replace with constants)
   - Security-sensitive code
   - Business logic decisions

   **Guidelines:**
   - Explain "why", not "what" (code shows what)
   - Keep comments up-to-date with code
   - Avoid obvious comments
   - Use TODO/FIXME/NOTE tags appropriately
   - Keep comments concise

6. **README Files**

   Create or update README.md with:

   **Package/Module README:**
   ```markdown
   # Package/Module Name

   Brief description of what this package does.

   ## Installation

   ```bash
   npm install package-name
   # or
   pnpm add package-name
   ```

   ## Usage

   Basic usage examples with code snippets.

   ```typescript
   import { Something } from 'package-name';

   const result = Something.doThing();
   ```

   ## API Reference

   ### Function/Class Name

   Description and parameters.

   ## Features

   - Feature 1
   - Feature 2

   ## Configuration

   Configuration options if applicable.

   ## Examples

   More detailed examples.

   ## Contributing

   Guidelines for contributors (if open source).

   ## License

   License information.
   ```

   **Project README:**
   - Project overview and purpose
   - Tech stack
   - Getting started guide
   - Prerequisites
   - Installation steps
   - Development workflow
   - Testing instructions
   - Deployment instructions
   - Project structure
   - Contributing guidelines
   - License

7. **API Documentation**

   For REST APIs, document:
   - Endpoint paths
   - HTTP methods
   - Request parameters (query, body, path)
   - Request examples
   - Response format
   - Response status codes
   - Error responses
   - Authentication requirements
   - Rate limiting

   Consider generating:
   - OpenAPI/Swagger specs
   - Postman collections
   - API documentation website

8. **Component Documentation (React)**

   Document:
   - Component purpose
   - Props with types and descriptions
   - Usage examples
   - Accessibility features
   - Styling approach
   - Dependencies
   - Related components

   Enhance Storybook stories:
   - Add descriptions
   - Document controls
   - Add usage examples
   - Include do's and don'ts

9. **Architecture Documentation**

   Create architecture docs for:
   - System overview
   - Component relationships
   - Data flow diagrams
   - Database schema
   - API architecture
   - Deployment architecture
   - Security architecture
   - Integration points

10. **Documentation Best Practices**
    - Keep documentation close to code
    - Update docs when code changes
    - Use clear, concise language
    - Include examples
    - Document edge cases and errors
    - Use consistent terminology
    - Make documentation searchable
    - Add visual diagrams where helpful
    - Version documentation with code
    - Test code examples
    - Consider internationalization

11. **Generate Documentation**
    - Consider using documentation generators:
      - TypeDoc (TypeScript)
      - JSDoc (JavaScript)
      - Godoc (Go)
      - Sphinx (Python)
    - Generate API docs from OpenAPI specs
    - Create documentation website if needed

12. **Review and Validation**
    - Ensure all public APIs are documented
    - Verify examples work correctly
    - Check for typos and grammar
    - Ensure consistency in style
    - Get peer review if possible
    - Test documentation with new users

13. **Final Deliverable**

    Provide summary including:
    - Files documented
    - Types of documentation added
    - Coverage statistics (% of functions documented)
    - README files created/updated
    - Examples of documentation added
    - Recommendations for ongoing documentation

Complete documentation and ensure it's comprehensive, accurate, and helpful.
