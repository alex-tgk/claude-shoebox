# Claude Shoebox Monorepo

This is a multi-language monorepo managed by [Nx](https://nx.dev) and [pnpm](https://pnpm.io).

## Structure

```
claude-shoebox/
├── apps/           # Applications (e.g., web apps, APIs, CLIs)
├── packages/       # Shared libraries and packages
├── nx.json         # Nx workspace configuration
└── pnpm-workspace.yaml  # pnpm workspace configuration
```

## Getting Started

### Prerequisites

- Node.js (v18 or later recommended)
- pnpm (v8 or later)

### Installation

```bash
pnpm install
```

## Available Commands

### Build

```bash
# Build all projects
pnpm build

# Build only affected projects
pnpm affected:build
```

### Test

```bash
# Test all projects
pnpm test

# Test only affected projects
pnpm affected:test
```

### Lint

```bash
# Lint all projects
pnpm lint

# Lint only affected projects
pnpm affected:lint
```

### Visualize Dependencies

```bash
# Open the Nx dependency graph
pnpm graph
```

## Adding New Projects

### Adding a Package (Shared Library)

For language-specific packages, you can use Nx generators or create manually:

```bash
# JavaScript/TypeScript package
pnpx nx g @nx/js:library my-lib --directory=packages/my-lib

# Or create manually in packages/my-lib/
```

### Adding an Application

```bash
# JavaScript/TypeScript app
pnpx nx g @nx/node:application my-app --directory=apps/my-app

# Or create manually in apps/my-app/
```

## Multi-Language Support

This monorepo is set up to support multiple languages. Here are some common integrations:

### JavaScript/TypeScript
- Use `@nx/js`, `@nx/node`, `@nx/react`, `@nx/next`, etc.
- Install: `pnpm add -D @nx/js` (or relevant plugin)

### Python
- Use `@nxlv/python` plugin
- Install: `pnpm add -D @nxlv/python`

### Go
- Use `@nx-go/nx-go` plugin
- Install: `pnpm add -D @nx-go/nx-go`

### Rust
- Use `@monodon/rust` plugin
- Install: `pnpm add -D @monodon/rust`

### Java
- Use `@jnxplus/nx-gradle` or `@jnxplus/nx-maven`
- Install: `pnpm add -D @jnxplus/nx-gradle`

## Nx Features

- **Smart rebuilds**: Only rebuild what changed
- **Computation caching**: Cache task results locally and remotely
- **Dependency graph**: Visualize project relationships
- **Affected commands**: Run tasks only on changed projects
- **Parallel execution**: Run tasks in parallel for speed

## Learn More

- [Nx Documentation](https://nx.dev)
- [pnpm Workspaces](https://pnpm.io/workspaces)
- [Nx Plugins](https://nx.dev/plugin-registry)
