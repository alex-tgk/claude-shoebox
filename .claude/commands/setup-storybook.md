# Initialize Storybook with TailwindCSS Integration

You are tasked with setting up Storybook in a project with full TailwindCSS integration, addons, and best practices configuration.

## Instructions

1. **Gather Requirements**
   - Ask which package/app to install Storybook in
   - Determine React version and framework (Next.js, Vite, CRA)
   - Check if TailwindCSS is already installed
   - Understand component library structure
   - Ask about required addons and features

2. **Install Storybook**

   **Automatic Setup (Recommended):**
   ```bash
   npx storybook@latest init
   ```

   **Manual Installation:**
   ```bash
   # For Vite + React
   npm install --save-dev @storybook/react-vite storybook

   # For Next.js
   npm install --save-dev @storybook/nextjs storybook
   ```

3. **Install Essential Addons**

   ```bash
   npm install --save-dev \
     @storybook/addon-essentials \
     @storybook/addon-interactions \
     @storybook/addon-links \
     @storybook/addon-a11y \
     @storybook/addon-coverage \
     @storybook/test
   ```

4. **Configure Storybook Main Config**

   Create `.storybook/main.ts`:

   ```typescript
   import type { StorybookConfig } from '@storybook/react-vite';
   import { mergeConfig } from 'vite';
   import path from 'path';

   const config: StorybookConfig = {
     stories: [
       '../src/**/*.mdx',
       '../src/**/*.stories.@(js|jsx|ts|tsx)',
     ],
     addons: [
       '@storybook/addon-essentials',
       '@storybook/addon-interactions',
       '@storybook/addon-links',
       '@storybook/addon-a11y',
       '@storybook/addon-coverage',
     ],
     framework: {
       name: '@storybook/react-vite',
       options: {},
     },
     docs: {
       autodocs: 'tag',
     },
     core: {
       disableTelemetry: true,
     },
     async viteFinal(config) {
       return mergeConfig(config, {
         resolve: {
           alias: {
             '@': path.resolve(__dirname, '../src'),
           },
         },
       });
     },
   };

   export default config;
   ```

   **For Next.js:**
   ```typescript
   import type { StorybookConfig } from '@storybook/nextjs';

   const config: StorybookConfig = {
     stories: [
       '../src/**/*.mdx',
       '../src/**/*.stories.@(js|jsx|ts|tsx)',
     ],
     addons: [
       '@storybook/addon-essentials',
       '@storybook/addon-interactions',
       '@storybook/addon-a11y',
     ],
     framework: {
       name: '@storybook/nextjs',
       options: {},
     },
     staticDirs: ['../public'],
   };

   export default config;
   ```

5. **TailwindCSS Integration**

   **Install TailwindCSS (if not already installed):**
   ```bash
   npm install --save-dev tailwindcss postcss autoprefixer
   npx tailwindcss init -p
   ```

   **Configure Tailwind for Storybook:**

   Update `tailwind.config.js`:
   ```javascript
   /** @type {import('tailwindcss').Config} */
   module.exports = {
     content: [
       './src/**/*.{js,jsx,ts,tsx}',
       './.storybook/**/*.{js,jsx,ts,tsx}', // Add Storybook
     ],
     theme: {
       extend: {
         // Your theme extensions
       },
     },
     plugins: [],
   };
   ```

   **Create Tailwind CSS file (if not exists):**
   ```css
   /* src/styles/globals.css or src/index.css */
   @tailwind base;
   @tailwind components;
   @tailwind utilities;

   /* Optional: Add custom base styles */
   @layer base {
     html {
       @apply font-sans;
     }
   }

   @layer components {
     /* Your component styles */
   }
   ```

6. **Configure Storybook Preview**

   Create `.storybook/preview.ts`:

   ```typescript
   import type { Preview } from '@storybook/react';
   import '../src/styles/globals.css'; // Import Tailwind CSS

   const preview: Preview = {
     parameters: {
       actions: { argTypesRegex: '^on[A-Z].*' },
       controls: {
         matchers: {
           color: /(background|color)$/i,
           date: /Date$/,
         },
       },
       backgrounds: {
         default: 'light',
         values: [
           {
             name: 'light',
             value: '#ffffff',
           },
           {
             name: 'dark',
             value: '#1a202c',
           },
           {
             name: 'gray',
             value: '#f7fafc',
           },
         ],
       },
       viewport: {
         viewports: {
           mobile: {
             name: 'Mobile',
             styles: { width: '375px', height: '667px' },
           },
           tablet: {
             name: 'Tablet',
             styles: { width: '768px', height: '1024px' },
           },
           desktop: {
             name: 'Desktop',
             styles: { width: '1280px', height: '720px' },
           },
         },
       },
     },
     globalTypes: {
       theme: {
         name: 'Theme',
         description: 'Global theme for components',
         defaultValue: 'light',
         toolbar: {
           icon: 'circlehollow',
           items: ['light', 'dark'],
           showName: true,
           dynamicTitle: true,
         },
       },
     },
   };

   export default preview;
   ```

7. **Add Dark Mode Support**

   **Install theme addon:**
   ```bash
   npm install --save-dev storybook-dark-mode
   ```

   **Update main.ts:**
   ```typescript
   addons: [
     // ... other addons
     'storybook-dark-mode',
   ],
   ```

   **Update Tailwind config for dark mode:**
   ```javascript
   module.exports = {
     darkMode: 'class', // or 'media'
     // ... rest of config
   };
   ```

   **Update preview.ts with theme decorator:**
   ```typescript
   import { themes } from '@storybook/theming';

   export const parameters = {
     darkMode: {
       dark: { ...themes.dark },
       light: { ...themes.light },
       darkClass: 'dark',
       lightClass: 'light',
       stylePreview: true,
     },
   };

   export const decorators = [
     (Story, context) => {
       const isDark = context.globals.theme === 'dark';

       return (
         <div className={isDark ? 'dark' : ''}>
           <div className="min-h-screen bg-white dark:bg-gray-900 text-gray-900 dark:text-white p-4">
             <Story />
           </div>
         </div>
       );
     },
   ];
   ```

8. **Create Custom Storybook Theme**

   Create `.storybook/theme.ts`:

   ```typescript
   import { create } from '@storybook/theming/create';

   export default create({
     base: 'light',
     brandTitle: 'Your Component Library',
     brandUrl: 'https://your-site.com',
     brandImage: '/logo.png',
     brandTarget: '_self',

     // UI colors
     colorPrimary: '#3b82f6', // blue-500
     colorSecondary: '#6366f1', // indigo-500

     // UI
     appBg: '#f9fafb',
     appContentBg: '#ffffff',
     appBorderColor: '#e5e7eb',
     appBorderRadius: 8,

     // Typography
     fontBase: '"Inter", sans-serif',
     fontCode: 'monospace',

     // Text colors
     textColor: '#1f2937',
     textInverseColor: '#ffffff',

     // Toolbar default and active colors
     barTextColor: '#6b7280',
     barSelectedColor: '#3b82f6',
     barBg: '#ffffff',

     // Form colors
     inputBg: '#ffffff',
     inputBorder: '#d1d5db',
     inputTextColor: '#1f2937',
     inputBorderRadius: 6,
   });
   ```

   **Apply theme in `.storybook/manager.ts`:**
   ```typescript
   import { addons } from '@storybook/manager-api';
   import theme from './theme';

   addons.setConfig({
     theme,
   });
   ```

9. **Create Global Decorators**

   Create `.storybook/decorators.tsx`:

   ```tsx
   import React from 'react';
   import type { Decorator } from '@storybook/react';

   // Layout decorator for consistent spacing
   export const LayoutDecorator: Decorator = (Story) => (
     <div className="p-8">
       <Story />
     </div>
   );

   // Container decorator for centered content
   export const CenterDecorator: Decorator = (Story) => (
     <div className="flex items-center justify-center min-h-screen">
       <Story />
     </div>
   );

   // Max width decorator
   export const MaxWidthDecorator: Decorator = (Story) => (
     <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
       <Story />
     </div>
   );
   ```

10. **Create Example Component Story**

    Create example story with best practices:

    ```tsx
    // src/components/Button/Button.stories.tsx
    import type { Meta, StoryObj } from '@storybook/react';
    import { fn } from '@storybook/test';
    import { Button } from './Button';

    const meta = {
      title: 'Components/Button',
      component: Button,
      parameters: {
        layout: 'centered',
        docs: {
          description: {
            component: 'A customizable button component with multiple variants and sizes.',
          },
        },
      },
      tags: ['autodocs'],
      argTypes: {
        variant: {
          control: 'select',
          options: ['primary', 'secondary', 'outline', 'ghost'],
          description: 'The visual style variant of the button',
        },
        size: {
          control: 'select',
          options: ['sm', 'md', 'lg'],
          description: 'The size of the button',
        },
        disabled: {
          control: 'boolean',
          description: 'Whether the button is disabled',
        },
      },
      args: {
        onClick: fn(),
      },
    } satisfies Meta<typeof Button>;

    export default meta;
    type Story = StoryObj<typeof meta>;

    export const Primary: Story = {
      args: {
        variant: 'primary',
        children: 'Primary Button',
      },
    };

    export const Secondary: Story = {
      args: {
        variant: 'secondary',
        children: 'Secondary Button',
      },
    };

    export const Outline: Story = {
      args: {
        variant: 'outline',
        children: 'Outline Button',
      },
    };

    export const Sizes: Story = {
      render: () => (
        <div className="flex items-center gap-4">
          <Button size="sm">Small</Button>
          <Button size="md">Medium</Button>
          <Button size="lg">Large</Button>
        </div>
      ),
    };

    export const Disabled: Story = {
      args: {
        disabled: true,
        children: 'Disabled Button',
      },
    };

    export const WithIcon: Story = {
      args: {
        children: (
          <div className="flex items-center gap-2">
            <svg className="w-4 h-4" fill="currentColor" viewBox="0 0 20 20">
              <path d="M10 3a1 1 0 011 1v5h5a1 1 0 110 2h-5v5a1 1 0 11-2 0v-5H4a1 1 0 110-2h5V4a1 1 0 011-1z" />
            </svg>
            <span>Add Item</span>
          </div>
        ),
      },
    };
    ```

11. **Create Documentation Pages**

    Create `.storybook/pages/Introduction.mdx`:

    ```mdx
    import { Meta } from '@storybook/blocks';

    <Meta title="Introduction" />

    # Component Library

    Welcome to the component library documentation.

    ## Overview

    This library provides a collection of reusable React components built with:
    - **React** - UI framework
    - **TypeScript** - Type safety
    - **TailwindCSS** - Utility-first styling
    - **Storybook** - Component documentation

    ## Getting Started

    Install the package:

    ```bash
    npm install @your-org/components
    ```

    Import components:

    ```tsx
    import { Button } from '@your-org/components';

    function App() {
      return <Button>Click me</Button>;
    }
    ```

    ## Design Principles

    - **Accessible** - WCAG 2.1 AA compliant
    - **Composable** - Small, focused components
    - **Themeable** - Customizable with Tailwind
    - **Type-safe** - Full TypeScript support
    ```

12. **Add Package Scripts**

    Update `package.json`:

    ```json
    {
      "scripts": {
        "storybook": "storybook dev -p 6006",
        "build-storybook": "storybook build",
        "storybook:test": "test-storybook",
        "storybook:coverage": "test-storybook --coverage"
      }
    }
    ```

13. **Add Interaction Testing**

    Create interaction test story:

    ```tsx
    import { expect, userEvent, within } from '@storybook/test';

    export const InteractionTest: Story = {
      args: {
        children: 'Click me',
      },
      play: async ({ canvasElement, args }) => {
        const canvas = within(canvasElement);
        const button = canvas.getByRole('button');

        // Test button click
        await userEvent.click(button);
        await expect(args.onClick).toHaveBeenCalled();

        // Test hover state
        await userEvent.hover(button);
        await expect(button).toHaveClass('hover:bg-blue-700');
      },
    };
    ```

14. **Add Accessibility Testing**

    Configure a11y addon in stories:

    ```tsx
    export const AccessibilityTest: Story = {
      args: {
        children: 'Accessible Button',
      },
      parameters: {
        a11y: {
          config: {
            rules: [
              {
                id: 'color-contrast',
                enabled: true,
              },
            ],
          },
        },
      },
    };
    ```

15. **Build and Deploy Configuration**

    Create `.storybook/vite.config.ts` for custom Vite config:

    ```typescript
    import { defineConfig } from 'vite';

    export default defineConfig({
      optimizeDeps: {
        include: ['@storybook/blocks'],
      },
    });
    ```

    **Deploy to Chromatic (optional):**
    ```bash
    npm install --save-dev chromatic
    npx chromatic --project-token=<your-token>
    ```

16. **Create README for Storybook**

    Document:
    - How to run Storybook locally
    - How to create new stories
    - Story naming conventions
    - How to use decorators
    - How to test components
    - Deployment instructions

17. **Final Checklist**

    Ensure:
    - [ ] Storybook runs successfully
    - [ ] TailwindCSS styles load correctly
    - [ ] Dark mode works
    - [ ] All addons are functional
    - [ ] Example stories render properly
    - [ ] Documentation pages display
    - [ ] Interaction tests work
    - [ ] A11y checks run
    - [ ] Build command succeeds

18. **Final Deliverables**

    Provide:
    - Complete Storybook configuration
    - TailwindCSS integration
    - Custom theme
    - Example component stories
    - Documentation pages
    - Testing setup
    - README with instructions
    - Package.json scripts

Complete Storybook setup with full TailwindCSS integration and best practices.
