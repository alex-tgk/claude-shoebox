# Analyze and Refactor Code

You are tasked with analyzing code and suggesting or implementing refactoring improvements to enhance code quality, maintainability, and performance.

## Instructions

1. **Identify Scope**
   - Ask the user which file(s) or directory to refactor
   - Understand the context and purpose of the code
   - Check if tests exist (run them before and after refactoring)
   - Ask if the user wants suggestions only or implementation

2. **Code Analysis**

   Analyze the code for the following issues:

   **Code Smells:**
   - Duplicated code
   - Long functions/methods (>50 lines)
   - Large classes/files (>300 lines)
   - Long parameter lists (>3-4 parameters)
   - Deep nesting (>3 levels)
   - Magic numbers and strings
   - Inconsistent naming
   - Dead code
   - Commented-out code

   **Design Issues:**
   - Violation of SOLID principles
   - Poor separation of concerns
   - Tight coupling
   - Low cohesion
   - God objects/classes
   - Feature envy
   - Inappropriate intimacy
   - Missing abstractions

   **Maintainability Issues:**
   - Lack of documentation
   - Unclear variable/function names
   - Complex conditionals
   - Missing error handling
   - Inconsistent code style
   - Poor type safety (TypeScript/Go)

3. **Refactoring Strategies**

   **Extract Method/Function:**
   - Break down large functions into smaller, focused ones
   - Each function should do one thing
   - Use meaningful names

   **Extract Variable:**
   - Replace complex expressions with named variables
   - Improve readability
   - Make intent clear

   **Rename:**
   - Use descriptive, meaningful names
   - Follow naming conventions
   - Be consistent across the codebase

   **Remove Duplication:**
   - Extract common code into shared functions
   - Use composition over inheritance
   - Create utility functions or hooks

   **Simplify Conditionals:**
   - Use early returns
   - Replace nested ifs with guard clauses
   - Use ternary operators for simple cases
   - Consider strategy pattern for complex conditions

   **Introduce Parameter Object:**
   - Group related parameters into objects
   - Reduce parameter lists
   - Make function signatures cleaner

   **Replace Magic Numbers:**
   - Define constants with meaningful names
   - Use enums for related constants
   - Add comments explaining the values

   **Move Code:**
   - Relocate code to more appropriate modules
   - Improve file organization
   - Follow feature-based or layer-based structure

4. **TypeScript-Specific Refactoring**
   - Add/improve type definitions
   - Use type guards
   - Leverage union types and discriminated unions
   - Use utility types (Partial, Pick, Omit, etc.)
   - Replace `any` with proper types
   - Use generics where appropriate

5. **React-Specific Refactoring**
   - Extract custom hooks from components
   - Split large components into smaller ones
   - Use composition (children prop, render props)
   - Optimize re-renders (React.memo, useMemo, useCallback)
   - Move business logic out of components
   - Use compound components pattern where appropriate

6. **Performance Improvements**
   - Identify expensive operations
   - Add memoization where beneficial
   - Optimize loops and iterations
   - Reduce unnecessary re-renders (React)
   - Use lazy loading for large components/modules
   - Optimize database queries

7. **Error Handling Improvements**
   - Add try-catch blocks where missing
   - Create custom error types
   - Validate inputs
   - Handle edge cases
   - Add meaningful error messages
   - Implement proper error recovery

8. **Testing Considerations**
   - Run existing tests before refactoring
   - Ensure all tests still pass after refactoring
   - Add tests if coverage decreased
   - Update tests to reflect new structure
   - Add tests for new edge cases discovered

9. **Documentation**
   - Add/update JSDoc or godoc comments
   - Document complex logic
   - Add usage examples
   - Update README if public API changed
   - Add inline comments for non-obvious code

10. **Refactoring Process**
    - Make small, incremental changes
    - Run tests after each change
    - Commit after each successful refactoring step
    - Don't mix refactoring with feature additions
    - Keep functional behavior unchanged
    - Use git to track changes

11. **Report to User**

    Provide a detailed summary including:
    - Issues identified
    - Refactoring changes made
    - Benefits of the changes
    - Before/after code comparisons for key changes
    - Test results (all passing)
    - Recommendations for future improvements
    - Any breaking changes (if unavoidable)

Complete the analysis and refactoring, ensuring all tests pass and code quality improves.
