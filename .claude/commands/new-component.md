# Generate New React Component

You are tasked with generating a new React component with TypeScript, Storybook story, and comprehensive tests.

## Instructions

1. **Gather Requirements**
   - Ask the user for the component name (in PascalCase, e.g., "Button", "UserProfile")
   - Ask where to create the component (which package/app in the monorepo)
   - Understand the component's purpose and key props/functionality
   - Confirm if the component should use TailwindCSS for styling

2. **Component Structure**
   Create the following files:
   - `{ComponentName}.tsx` - Main component file
   - `{ComponentName}.stories.tsx` - Storybook story
   - `{ComponentName}.test.tsx` - Test file (using Vitest/Jest and React Testing Library)
   - `index.ts` - Barrel export file

3. **Component File ({ComponentName}.tsx)**
   - Use TypeScript with proper type definitions
   - Define a Props interface with JSDoc comments
   - Use React.FC or typed function component
   - Include proper prop validation
   - Use TailwindCSS for styling with semantic class names
   - Add display name for debugging
   - Export both named and default exports
   - Include accessibility attributes (aria-labels, roles, etc.)

4. **Storybook Story ({ComponentName}.stories.tsx)**
   - Use Component Story Format (CSF3)
   - Include meta configuration with title and component
   - Create at least 3 stories:
     - Default/Primary
     - All Props variant
     - Edge cases (empty state, loading, error, disabled, etc.)
   - Add args and argTypes for interactive controls
   - Include documentation in the story

5. **Test File ({ComponentName}.test.tsx)**
   - Use Vitest or Jest with React Testing Library
   - Test rendering with default props
   - Test all prop variations
   - Test user interactions (clicks, inputs, etc.)
   - Test accessibility (screen reader support)
   - Test edge cases and error states
   - Aim for >90% code coverage

6. **Index File (index.ts)**
   - Export the component and its types
   - Include re-exports for easy importing

7. **Best Practices**
   - Follow atomic design principles if applicable
   - Keep components small and focused (single responsibility)
   - Make components reusable and composable
   - Use semantic HTML elements
   - Ensure keyboard navigation works
   - Follow WCAG 2.1 accessibility guidelines
   - Add helpful JSDoc comments
   - Use meaningful variable and prop names

8. **After Creation**
   - Verify all files compile without errors
   - Run the test suite and ensure all tests pass
   - Check that Storybook renders the component correctly
   - Provide usage examples to the user

## Example Structure

```
components/
└── {ComponentName}/
    ├── {ComponentName}.tsx
    ├── {ComponentName}.stories.tsx
    ├── {ComponentName}.test.tsx
    └── index.ts
```

Complete all steps and confirm successful creation with the user.
