# 🎯 Claude Shoebox

> The ultimate AI-powered development arsenal: 30 business ideas, 30 slash commands, 10 skills, 8 agents, and 150+ prompts.

[![PRDs](https://img.shields.io/badge/PRDs-30-blue)](docs/prds/)
[![Commands](https://img.shields.io/badge/Commands-30-green)](.claude/commands/)
[![Skills](https://img.shields.io/badge/Skills-10-purple)](.claude/skills/)
[![Agents](https://img.shields.io/badge/Agents-8-orange)](.claude/agents/)
[![Prompts](https://img.shields.io/badge/Prompts-150+-red)](docs/prompts/)

---

## 🚀 Quick Links

- 📋 [**30 AI Business Ideas**](docs/prds/README.md) - Complete PRDs for one-person businesses
- ⚡ [**30 Slash Commands**](.claude/commands/README.md) - Instant development automation
- 🎓 [**10 Specialized Skills**](.claude/skills/README.md) - Deep technical expertise
- 🤖 [**8 Autonomous Agents**](.claude/agents/README.md) - Task automation helpers
- 📚 [**150+ Prompt Templates**](docs/prompts/README.md) - AI-assisted development
- 📖 [**Complete Guide**](MASTER-README.md) - Full documentation

---

## 💎 What's Inside

| Resource | Count | Description |
|----------|-------|-------------|
| 📋 Business Ideas | 30 | AI-powered business PRDs (6-12 weeks to build, <$500 investment) |
| ⚡ Slash Commands | 30 | Dev + business automation (15 each) |
| 🎓 Skills | 10 | Specialized domain expertise |
| 🤖 Agents | 8 | Autonomous task helpers |
| 📚 Prompts | 150+ | Copy-paste templates across 8 categories |

**Total**: 87+ files, 15,000+ lines of production-ready content

---

## 🎯 Use Cases

### 👤 Solo Entrepreneurs
Build an AI business in 6-12 weeks with <$500 investment

### 👨‍💻 Developers
10x your coding speed with commands, skills, and prompts

### 👥 Product Teams
Standardize workflows with shared commands and templates

### 🏢 Agencies
Reference PRDs as service offerings and use tools for client work

---

## 📂 Monorepo Structure

This is a multi-language monorepo managed by [Nx](https://nx.dev) and [pnpm](https://pnpm.io).

```
claude-shoebox/
├── .claude/
│   ├── commands/          # 30 custom slash commands
│   ├── skills/            # 10 specialized skills
│   └── agents/            # 8 autonomous agents
├── docs/
│   ├── prds/              # 30 AI business ideas
│   └── prompts/           # 150+ prompt templates
├── apps/                  # Monorepo applications
├── packages/              # Shared libraries
├── nx.json                # Nx workspace config
├── pnpm-workspace.yaml    # pnpm workspace config
├── README.md              # This file
└── MASTER-README.md       # Complete documentation
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
