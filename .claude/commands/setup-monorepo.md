# Add New Package/App to Nx Monorepo

You are tasked with adding a new package or application to an existing Nx monorepo, following best practices and ensuring proper integration.

## Instructions

1. **Gather Requirements**
   - Ask what type to create (app, library, package)
   - Determine the name and purpose
   - Understand tech stack (React, Node.js, Go, etc.)
   - Ask about dependencies on other packages
   - Determine if it should be publishable
   - Understand build and test requirements

2. **Analyze Existing Monorepo**
   - Review workspace structure
   - Check nx.json configuration
   - Review package.json workspace settings
   - Identify naming conventions
   - Check existing project patterns
   - Review tsconfig.json setup

3. **Create New Application**

   **React Application with Vite:**
   ```bash
   npx nx generate @nx/react:app my-app \
     --bundler=vite \
     --style=css \
     --routing=true \
     --unitTestRunner=vitest \
     --e2eTestRunner=playwright
   ```

   **Next.js Application:**
   ```bash
   npx nx generate @nx/next:app my-next-app \
     --style=css \
     --appDir=true
   ```

   **Node.js Application (Express):**
   ```bash
   npx nx generate @nx/node:app my-api \
     --framework=express \
     --docker=true
   ```

4. **Create New Library**

   **React Component Library:**
   ```bash
   npx nx generate @nx/react:library ui-components \
     --directory=packages/ui-components \
     --publishable \
     --importPath=@myorg/ui-components \
     --bundler=vite \
     --unitTestRunner=vitest \
     --component=true
   ```

   **TypeScript Utility Library:**
   ```bash
   npx nx generate @nx/js:library utils \
     --directory=packages/utils \
     --publishable \
     --importPath=@myorg/utils \
     --bundler=tsc \
     --unitTestRunner=vitest
   ```

   **Shared Types Library:**
   ```bash
   npx nx generate @nx/js:library types \
     --directory=packages/types \
     --publishable \
     --importPath=@myorg/types \
     --bundler=tsc
   ```

5. **Project Structure**

   Ensure consistent structure:

   **Application Structure:**
   ```
   apps/my-app/
   ├── src/
   │   ├── app/
   │   │   ├── components/
   │   │   ├── pages/
   │   │   ├── hooks/
   │   │   ├── utils/
   │   │   └── App.tsx
   │   ├── assets/
   │   ├── styles/
   │   ├── main.tsx
   │   └── vite-env.d.ts
   ├── public/
   ├── index.html
   ├── vite.config.ts
   ├── tsconfig.json
   ├── tsconfig.app.json
   ├── project.json
   └── README.md
   ```

   **Library Structure:**
   ```
   packages/ui-components/
   ├── src/
   │   ├── components/
   │   │   ├── Button/
   │   │   │   ├── Button.tsx
   │   │   │   ├── Button.test.tsx
   │   │   │   ├── Button.stories.tsx
   │   │   │   └── index.ts
   │   │   └── index.ts
   │   ├── hooks/
   │   ├── utils/
   │   └── index.ts
   ├── tsconfig.json
   ├── tsconfig.lib.json
   ├── vite.config.ts
   ├── project.json
   ├── package.json
   └── README.md
   ```

6. **Configure project.json**

   ```json
   {
     "name": "ui-components",
     "$schema": "../../node_modules/nx/schemas/project-schema.json",
     "sourceRoot": "packages/ui-components/src",
     "projectType": "library",
     "tags": ["type:ui", "scope:shared"],
     "targets": {
       "build": {
         "executor": "@nx/vite:build",
         "outputs": ["{options.outputPath}"],
         "options": {
           "outputPath": "dist/packages/ui-components",
           "main": "packages/ui-components/src/index.ts",
           "tsConfig": "packages/ui-components/tsconfig.lib.json",
           "assets": ["packages/ui-components/*.md"]
         }
       },
       "test": {
         "executor": "@nx/vite:test",
         "outputs": ["{workspaceRoot}/coverage/packages/ui-components"],
         "options": {
           "passWithNoTests": true,
           "reportsDirectory": "../../coverage/packages/ui-components"
         }
       },
       "lint": {
         "executor": "@nx/eslint:lint",
         "outputs": ["{options.outputFile}"],
         "options": {
           "lintFilePatterns": ["packages/ui-components/**/*.{ts,tsx,js,jsx}"]
         }
       },
       "storybook": {
         "executor": "@nx/storybook:storybook",
         "options": {
           "port": 6006,
           "configDir": "packages/ui-components/.storybook"
         }
       },
       "build-storybook": {
         "executor": "@nx/storybook:build",
         "outputs": ["{options.outputDir}"],
         "options": {
           "outputDir": "dist/storybook/ui-components",
           "configDir": "packages/ui-components/.storybook"
         }
       }
     }
   }
   ```

7. **Configure TypeScript**

   **tsconfig.json (base):**
   ```json
   {
     "extends": "../../tsconfig.base.json",
     "compilerOptions": {
       "jsx": "react-jsx",
       "allowJs": false,
       "esModuleInterop": false,
       "allowSyntheticDefaultImports": true,
       "forceConsistentCasingInFileNames": true,
       "strict": true,
       "noImplicitOverride": true,
       "noPropertyAccessFromIndexSignature": true,
       "noImplicitReturns": true,
       "noFallthroughCasesInSwitch": true
     },
     "files": [],
     "include": [],
     "references": [
       {
         "path": "./tsconfig.lib.json"
       },
       {
         "path": "./tsconfig.spec.json"
       }
     ]
   }
   ```

   **tsconfig.lib.json:**
   ```json
   {
     "extends": "./tsconfig.json",
     "compilerOptions": {
       "outDir": "../../dist/out-tsc",
       "types": ["node"]
     },
     "include": ["src/**/*.ts", "src/**/*.tsx"],
     "exclude": [
       "src/**/*.spec.ts",
       "src/**/*.spec.tsx",
       "src/**/*.test.ts",
       "src/**/*.test.tsx",
       "src/**/*.stories.ts",
       "src/**/*.stories.tsx"
     ]
   }
   ```

8. **Update Workspace Configuration**

   **Update tsconfig.base.json paths:**
   ```json
   {
     "compilerOptions": {
       "paths": {
         "@myorg/ui-components": ["packages/ui-components/src/index.ts"],
         "@myorg/utils": ["packages/utils/src/index.ts"],
         "@myorg/types": ["packages/types/src/index.ts"]
       }
     }
   }
   ```

9. **Configure Package.json (for publishable packages)**

   ```json
   {
     "name": "@myorg/ui-components",
     "version": "0.1.0",
     "type": "module",
     "main": "./dist/index.cjs",
     "module": "./dist/index.js",
     "types": "./dist/index.d.ts",
     "exports": {
       ".": {
         "import": "./dist/index.js",
         "require": "./dist/index.cjs",
         "types": "./dist/index.d.ts"
       }
     },
     "files": [
       "dist",
       "README.md"
     ],
     "publishConfig": {
       "access": "public"
     },
     "peerDependencies": {
       "react": "^18.0.0",
       "react-dom": "^18.0.0"
     },
     "devDependencies": {
       "react": "^18.2.0",
       "react-dom": "^18.2.0"
     }
   }
   ```

10. **Add Dependencies**

    **Install package dependencies:**
    ```bash
    # Add dependency to specific project
    pnpm add axios --filter @myorg/ui-components

    # Add dev dependency
    pnpm add -D vitest --filter @myorg/ui-components

    # Add workspace dependency
    pnpm add @myorg/utils --filter @myorg/ui-components --workspace
    ```

11. **Configure Dependency Constraints**

    **Update nx.json with tags:**
    ```json
    {
      "tasksRunnerOptions": {
        "default": {
          "runner": "nx/tasks-runners/default",
          "options": {
            "cacheableOperations": ["build", "lint", "test"]
          }
        }
      },
      "targetDefaults": {
        "build": {
          "dependsOn": ["^build"]
        }
      },
      "namedInputs": {
        "default": ["{projectRoot}/**/*", "sharedGlobals"],
        "sharedGlobals": [],
        "production": [
          "default",
          "!{projectRoot}/**/?(*.)+(spec|test).[jt]s?(x)?(.snap)",
          "!{projectRoot}/tsconfig.spec.json",
          "!{projectRoot}/.eslintrc.json",
          "!{projectRoot}/**/*.stories.@(js|jsx|ts|tsx|mdx)"
        ]
      }
    }
    ```

    **Update .eslintrc.json with boundary rules:**
    ```json
    {
      "overrides": [
        {
          "files": ["*.ts", "*.tsx"],
          "rules": {
            "@nx/enforce-module-boundaries": [
              "error",
              {
                "allow": [],
                "depConstraints": [
                  {
                    "sourceTag": "scope:shared",
                    "onlyDependOnLibsWithTags": ["scope:shared"]
                  },
                  {
                    "sourceTag": "type:app",
                    "onlyDependOnLibsWithTags": [
                      "type:feature",
                      "type:ui",
                      "type:util"
                    ]
                  },
                  {
                    "sourceTag": "type:feature",
                    "onlyDependOnLibsWithTags": ["type:ui", "type:util"]
                  },
                  {
                    "sourceTag": "type:ui",
                    "onlyDependOnLibsWithTags": ["type:util"]
                  }
                ]
              }
            ]
          }
        }
      ]
    }
    ```

12. **Create README**

    ```markdown
    # @myorg/ui-components

    Shared UI component library for MyOrg applications.

    ## Installation

    ```bash
    pnpm add @myorg/ui-components
    ```

    ## Usage

    ```tsx
    import { Button } from '@myorg/ui-components';

    function App() {
      return <Button variant="primary">Click me</Button>;
    }
    ```

    ## Development

    ```bash
    # Run tests
    pnpm nx test ui-components

    # Run Storybook
    pnpm nx storybook ui-components

    # Build
    pnpm nx build ui-components

    # Lint
    pnpm nx lint ui-components
    ```

    ## Components

    - Button
    - Input
    - Card
    - Modal

    See Storybook for full documentation.
    ```

13. **Add to CI/CD**

    **Update GitHub Actions:**
    ```yaml
    # Only build affected projects
    - name: Build affected
      run: pnpm nx affected:build --base=origin/main

    - name: Test affected
      run: pnpm nx affected:test --base=origin/main

    - name: Lint affected
      run: pnpm nx affected:lint --base=origin/main
    ```

14. **Generate and Visualize Dependency Graph**

    ```bash
    # Visualize project graph
    pnpm nx graph

    # Show affected projects
    pnpm nx affected:graph

    # Check circular dependencies
    pnpm nx graph --focus=@myorg/ui-components
    ```

15. **Run Common Commands**

    ```bash
    # Build the package
    pnpm nx build ui-components

    # Test the package
    pnpm nx test ui-components

    # Lint the package
    pnpm nx lint ui-components

    # Build all affected projects
    pnpm nx affected:build

    # Run command for all projects
    pnpm nx run-many --target=build --all

    # Run command for specific projects
    pnpm nx run-many --target=test --projects=ui-components,utils
    ```

16. **Verify Integration**

    - Import from new package in existing app
    - Run build to ensure no errors
    - Check TypeScript path resolution
    - Verify tests run correctly
    - Check dependency graph
    - Ensure no circular dependencies

17. **Final Checklist**

    Ensure:
    - [ ] Project created with proper structure
    - [ ] project.json configured correctly
    - [ ] TypeScript configured and compiling
    - [ ] Package.json set up (if publishable)
    - [ ] Paths added to tsconfig.base.json
    - [ ] Tags configured for dependency constraints
    - [ ] Tests run successfully
    - [ ] Build completes without errors
    - [ ] README documentation created
    - [ ] Can import from other packages
    - [ ] No circular dependencies
    - [ ] CI/CD updated if needed

18. **Final Deliverables**

    Provide:
    - Complete package/app structure
    - Configuration files
    - Example component or code
    - Tests
    - README documentation
    - Integration instructions
    - Commands for common tasks
    - Dependency graph screenshot

Complete the monorepo package setup ensuring proper integration and following Nx best practices.
