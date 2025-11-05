# Autonomous Agents

This directory contains 8 specialized agent configurations for autonomous task execution in Claude Code.

## 📊 Overview

- **Total Agents**: 8
- **Tool Access**: Varies by agent (Read, Write, Edit, Bash, Grep, Glob, WebSearch)
- **File Size**: 3.9KB - 12KB per agent
- **Purpose**: Autonomous helpers for specific development tasks

## 🤖 Available Agents

### 1. **Full Stack Builder** (3.9KB)
**File**: `full-stack-builder.md`

**Role**: End-to-end feature development specialist

**Tool Access**: Read, Write, Edit, Bash, Grep, Glob, WebSearch (full access)

**Primary Responsibilities**:
- Build complete features from requirements
- Handle frontend, backend, database, and tests
- Create deployment configurations
- Ensure production readiness

**Best For**:
- "Build a user authentication feature with email/password and OAuth"
- "Create a real-time chat system with WebSocket support"
- "Develop a payment integration with Stripe"

**Communication Style**: Progress updates at each phase, clear next steps

---

### 2. **Bug Hunter** (4.4KB)
**File**: `bug-hunter.md`

**Role**: Systematic bug detection and resolution specialist

**Tool Access**: Read, Grep, Edit, Bash

**Primary Responsibilities**:
- Reproduce and diagnose bugs methodically
- Identify root causes using debugging tools
- Fix bugs with minimal changes
- Add regression tests to prevent recurrence

**Best For**:
- "Fix the login crash when password contains special characters"
- "Debug memory leak in the data processing service"
- "Resolve intermittent test failures in CI pipeline"

**Communication Style**: Methodical investigation with hypotheses and findings

---

### 3. **Docs Writer** (5.4KB)
**File**: `docs-writer.md`

**Role**: Comprehensive technical documentation specialist

**Tool Access**: Read, Write, Glob, Grep, Edit

**Primary Responsibilities**:
- Create API documentation from code
- Write user guides and tutorials
- Generate comprehensive README files
- Add inline code documentation (JSDoc/TSDoc/Godoc)

**Best For**:
- "Document all API endpoints in the payment service"
- "Create a user guide for the admin dashboard"
- "Write comprehensive README for this open-source library"

**Communication Style**: Clear, structured, with examples and diagrams

---

### 4. **Test Automator** (6.6KB)
**File**: `test-automator.md`

**Role**: Test suite development and coverage improvement specialist

**Tool Access**: Read, Write, Edit, Bash, Grep, Glob

**Primary Responsibilities**:
- Write unit tests for business logic
- Create integration tests for APIs and databases
- Develop e2e tests for user workflows
- Improve code coverage to target percentage

**Best For**:
- "Write unit tests for the authentication module"
- "Create e2e tests for the checkout flow"
- "Increase test coverage from 40% to 80%"

**Communication Style**: Coverage metrics, test case summaries, CI integration status

---

### 5. **Performance Optimizer** (6.8KB)
**File**: `performance-optimizer.md`

**Role**: Code performance analysis and optimization specialist

**Tool Access**: Read, Edit, Bash, Grep, Glob

**Primary Responsibilities**:
- Profile code to identify bottlenecks
- Optimize slow database queries
- Improve frontend rendering performance
- Implement caching strategies

**Best For**:
- "Optimize the slow dashboard load time (currently 8s)"
- "Reduce API response time from 2s to <200ms"
- "Fix React component re-rendering issues"

**Communication Style**: Metrics-driven with before/after comparisons

---

### 6. **Security Hardener** (8.8KB)
**File**: `security-hardener.md`

**Role**: Security audit and vulnerability remediation specialist

**Tool Access**: Read, Grep, Edit, Bash, Glob

**Primary Responsibilities**:
- Scan for security vulnerabilities (OWASP Top 10)
- Fix authentication and authorization issues
- Implement secrets management
- Add security headers and HTTPS

**Best For**:
- "Audit the codebase for security vulnerabilities"
- "Fix SQL injection vulnerabilities in the API"
- "Implement proper authentication and authorization"

**Communication Style**: Severity-rated findings with remediation steps

---

### 7. **Refactor Expert** (10KB)
**File**: `refactor-expert.md`

**Role**: Code quality and maintainability improvement specialist

**Tool Access**: Read, Edit, Glob, Grep, Bash

**Primary Responsibilities**:
- Eliminate code smells and anti-patterns
- Apply SOLID principles
- Reduce cyclomatic complexity
- Extract reusable components/functions

**Best For**:
- "Refactor this 500-line function into manageable pieces"
- "Remove code duplication across the codebase"
- "Improve code structure following SOLID principles"

**Communication Style**: Code quality metrics, refactoring recommendations

---

### 8. **Deployment Specialist** (12KB)
**File**: `deployment-specialist.md`

**Role**: Infrastructure, deployment, and DevOps automation specialist

**Tool Access**: Read, Write, Edit, Bash, Glob

**Primary Responsibilities**:
- Set up CI/CD pipelines (GitHub Actions, Jenkins)
- Create Docker and Kubernetes configurations
- Implement infrastructure as code (Terraform)
- Configure monitoring and logging

**Best For**:
- "Set up CI/CD pipeline for automated deployments"
- "Deploy the application to AWS with Kubernetes"
- "Create infrastructure as code using Terraform"

**Communication Style**: Infrastructure diagrams, deployment status, runbooks

---

## 🎯 Agent Structure

Each agent configuration includes:

### 1. Agent Name & Role
Clear identity and primary function

### 2. Primary Responsibilities
5-8 core tasks the agent handles

### 3. Tool Access
Specific tools the agent can use:
- **Read**: Read files and code
- **Write**: Create new files
- **Edit**: Modify existing files
- **Bash**: Execute shell commands
- **Grep**: Search code patterns
- **Glob**: Find files by pattern
- **WebSearch**: Search the web (limited agents)

### 4. Operating Principles
Core philosophy and approach (8-12 principles)

### 5. Tech Stack Expertise
Technologies, frameworks, and tools the agent knows

### 6. Workflow
Step-by-step process (10 steps) the agent follows

### 7. Communication Style
How the agent reports progress and findings

### 8. Example Invocations
Real-world usage scenarios (5-10 examples)

### 9. Success Criteria
What defines task completion for the agent

## 💡 How to Use Agents

### Invocation Patterns

Agents work best with clear, specific requests:

```bash
# Good: Specific and actionable
"Bug Hunter, investigate why the login fails when using OAuth providers"

# Good: Clear scope and goals
"Test Automator, create unit tests for the payment processing module with 80% coverage"

# Less ideal: Too vague
"Fix the bugs"
```

### Best Practices

1. **Be specific** - Provide context and expected outcomes
2. **One agent at a time** - Focus on one specialized task
3. **Provide constraints** - Mention time, scope, or technical limits
4. **Share context** - Point to relevant files, docs, or tickets
5. **Review outputs** - Agents are autonomous but benefit from human oversight

### Agent Selection Guide

**Choose based on your task**:

| Task Type | Agent | Example |
|-----------|-------|---------|
| New feature | Full Stack Builder | "Build user dashboard with charts" |
| Bug fix | Bug Hunter | "Debug API timeout issues" |
| Documentation | Docs Writer | "Document all API endpoints" |
| Testing | Test Automator | "Add tests for auth module" |
| Slow performance | Performance Optimizer | "Speed up database queries" |
| Security issue | Security Hardener | "Fix XSS vulnerabilities" |
| Code quality | Refactor Expert | "Refactor payment logic" |
| Deployment | Deployment Specialist | "Set up Kubernetes deployment" |

## 🔄 Agent Workflows

### Example: Building a New Feature

```
1. Full Stack Builder - Initial implementation
   ↓
2. Test Automator - Add test coverage
   ↓
3. Security Hardener - Security review
   ↓
4. Docs Writer - Create documentation
   ↓
5. Deployment Specialist - Deploy to production
```

### Example: Fixing Performance Issues

```
1. Performance Optimizer - Profile and optimize
   ↓
2. Test Automator - Add performance tests
   ↓
3. Docs Writer - Document optimizations
```

### Example: Code Quality Improvement

```
1. Security Hardener - Security audit
   ↓
2. Refactor Expert - Code cleanup
   ↓
3. Test Automator - Increase coverage
   ↓
4. Code Reviewer - Final review (skill)
```

## 🛠️ Tool Access Matrix

| Agent | Read | Write | Edit | Bash | Grep | Glob | WebSearch |
|-------|------|-------|------|------|------|------|-----------|
| Full Stack Builder | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Bug Hunter | ✅ | ❌ | ✅ | ✅ | ✅ | ❌ | ❌ |
| Docs Writer | ✅ | ✅ | ✅ | ❌ | ✅ | ✅ | ❌ |
| Test Automator | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ |
| Performance Optimizer | ✅ | ❌ | ✅ | ✅ | ✅ | ✅ | ❌ |
| Security Hardener | ✅ | ❌ | ✅ | ✅ | ✅ | ✅ | ❌ |
| Refactor Expert | ✅ | ❌ | ✅ | ✅ | ✅ | ✅ | ❌ |
| Deployment Specialist | ✅ | ✅ | ✅ | ✅ | ❌ | ✅ | ❌ |

## 📚 Related Resources

- **Skills**: See `.claude/skills/` for specialized domain expertise
- **Slash Commands**: See `.claude/commands/` for quick, reusable prompts
- **PRDs**: See `docs/prds/` for complete business project templates
- **Prompts**: See `docs/prompts/` for AI-assisted development templates

## 🎓 Creating Custom Agents

Want to create your own agent? Follow this template:

```markdown
# {Agent Name}

## Role
[One-sentence description]

## Primary Responsibilities
- [Responsibility 1]
- [Responsibility 2]
...

## Tool Access
- Read, Write, Edit, Bash, Grep, Glob, WebSearch

## Operating Principles
1. [Principle 1]
2. [Principle 2]
...

## Tech Stack Expertise
[Technologies the agent knows]

## Workflow
1. [Step 1]
2. [Step 2]
...

## Communication Style
[How the agent communicates]

## Example Invocations
- "[Example 1]"
- "[Example 2]"
...

## Success Criteria
- [Criterion 1]
- [Criterion 2]
...
```

Save as `.claude/agents/{agent-name}.md`

---

**Total Agents**: 8
**Specializations**: Full-stack, debugging, testing, performance, security, refactoring, docs, deployment
**Last Updated**: 2025-11-05
