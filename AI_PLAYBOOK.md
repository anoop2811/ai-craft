# The AI Playbook

*Tactical guidance for teams who craft with AI. This document operationalizes the AI Constitution.*

---

## How to Use This Playbook

This is not a rulebook—it's a field guide. Each chapter provides:
- **The Philosophy** — Why this tool/practice matters
- **The Practice** — How to use it effectively
- **The Patterns** — Specific scenarios with examples
- **The Anti-Patterns** — What to avoid and why

Reference the Constitution articles each chapter implements. When in doubt, the Constitution governs.

---

# Part I: Grounding AI in Your Codebase

---

## Chapter 1: CLAUDE.md — The Soul of Your Codebase

*Implements: Constitution Article V (Craft Standards), Article I (Hierarchy of Understanding)*

### The Philosophy

A codebase is not just code. It's decisions. It's philosophy. It's the accumulated wisdom of everyone who touched it. CLAUDE.md is how you transfer that wisdom to AI.

Think of CLAUDE.md as onboarding documentation—but for an AI that will forget everything between sessions. Every session starts fresh. CLAUDE.md is the institutional memory that persists.

> "Read the codebase like you're studying a masterpiece. Understand the patterns, the philosophy, the *soul* of this code."

### The Practice

CLAUDE.md lives at the root of your repository (or in directories where context differs). It should answer:

1. **What is this?** — The elevator pitch an AI needs to understand the domain
2. **What matters here?** — The non-negotiable principles and patterns
3. **What are the conventions?** — Naming, structure, style that AI must follow
4. **What are the landmines?** — Areas of complexity, legacy decisions, known issues
5. **What is the workflow?** — How changes flow from idea to production

### The Template

```markdown
# CLAUDE.md

## Project Overview
[2-3 sentences: What is this project? Who uses it? What problem does it solve?]

## Architecture Philosophy
[The WHY behind structural decisions. Not documentation—wisdom.]

Example:
- We use hexagonal architecture because we swap infrastructure frequently
- Domain logic never imports from infrastructure; adapters bridge the gap
- Every external dependency is behind an interface we control

## Code Conventions

### Naming
- Services: `{Domain}Service` (e.g., `PaymentService`)
- Repositories: `{Entity}Repository` (e.g., `UserRepository`)
- Use cases: `{Verb}{Noun}UseCase` (e.g., `ProcessRefundUseCase`)

### Patterns We Use
- Result types over exceptions for expected failures
- Repository pattern for all data access
- Factory functions over constructors for complex objects

### Patterns We Avoid
- No inheritance for code reuse (composition only)
- No magic strings (constants or enums)
- No business logic in controllers

## Testing Philosophy
[How we think about tests—not just how to run them]

Example:
- Outside-in TDD: Start with acceptance test, work inward
- Test behavior, not implementation
- One assertion per test where possible
- Test names describe the behavior: `should_reject_payment_when_insufficient_funds`

## Directory Structure
```
src/
├── domain/          # Pure business logic, no dependencies
├── application/     # Use cases, orchestration
├── infrastructure/  # External concerns (DB, APIs, etc.)
└── presentation/    # Controllers, views, CLI
```

## Current Focus
[What the team is actively working on—gives AI context for priorities]

## Known Complexity
[Areas where AI should tread carefully]

Example:
- `legacy/billing/` — Old system, migration in progress, don't extend
- `PaymentProcessor` — Complex state machine, read thoroughly before touching
- Date handling — All dates are UTC internally, converted at boundaries

## Commands
```bash
npm test              # Run all tests
npm run test:watch    # TDD mode
npm run lint          # Must pass before commit
npm run build         # Verify before pushing
```

## Review Checklist
Before suggesting code is complete, verify:
- [ ] Tests pass
- [ ] No new lint warnings
- [ ] Follows naming conventions above
- [ ] No business logic leaked into infrastructure
- [ ] Changes traced to acceptance criteria
```

### Practical Scenarios

**Scenario 1: New Team Member Joins**

A new developer joins. Before their first pairing session, they should read CLAUDE.md. It's the same context the AI needs—which means maintaining CLAUDE.md benefits both AI and humans.

**Scenario 2: AI Suggests Wrong Pattern**

AI suggests using inheritance for a new feature. CLAUDE.md explicitly says "No inheritance for code reuse." The navigator catches this, references CLAUDE.md, and redirects AI toward composition.

**Scenario 3: Working in Legacy Code**

AI is asked to modify `legacy/billing/`. CLAUDE.md warns this is a migration target. The pair decides to check with the team before extending it, avoiding work that would be thrown away.

### Anti-Patterns

| Anti-Pattern | Why It Fails |
|--------------|--------------|
| Empty CLAUDE.md | AI has no context, makes wrong assumptions |
| CLAUDE.md as API docs | AI needs philosophy, not just facts |
| Stale CLAUDE.md | Worse than none—AI follows outdated patterns |
| 50-page CLAUDE.md | AI context has limits; keep it focused |
| No "Known Complexity" section | AI will confidently break fragile things |

### Maintenance Ritual

CLAUDE.md is reviewed every sprint retrospective:
- Does it still reflect how we work?
- Did AI make mistakes that better context would prevent?
- What did new team members wish they'd known sooner?

---

## Chapter 2: AGENTS.md — A README for AI Agents

*Implements: Constitution Article I (Hierarchy of Understanding), Article V (Craft Standards)*

### The Philosophy

AGENTS.md is a README for AI agents—a dedicated, predictable place to provide context and instructions that help AI coding agents work on your project. Just as README.md helps humans understand a project, AGENTS.md helps AI agents understand how to contribute effectively.

> "Read the codebase like you're studying a masterpiece. Understand the patterns, the philosophy, the *soul* of this code."

AGENTS.md is now a standard stewarded by the Agentic AI Foundation under the Linux Foundation, supported across 60,000+ open-source projects and multiple AI agents including Claude, OpenAI Codex, Google Jules, Cursor, and others.

### The Practice

**Location**: Place AGENTS.md at your repository root. For monorepos or packages with different conventions, nested AGENTS.md files in subdirectories take precedence for those areas.

**Format**: Standard Markdown. No required fields—use whatever headings make sense for your project. The agent parses the text you provide.

**Relationship to CLAUDE.md**:

These serve different purposes and different audiences:

| Aspect | CLAUDE.md | AGENTS.md |
|--------|-----------|-----------|
| **Purpose** | Transfer the *soul* of the codebase | Provide *instructions* for contributing |
| **Question it answers** | "Why do we do things this way?" | "How do I do things here?" |
| **Audience** | Any AI (Claude, Copilot, future tools) | AI agents actively working on code |
| **Content type** | Philosophy, principles, rationale | Commands, checklists, conventions |
| **Changes when** | Architecture or principles change | Tooling or process changes |
| **Tone** | Wisdom and guidance | Instructions and rules |

**The Litmus Test**:
- "Why do we use hexagonal architecture?" → CLAUDE.md (philosophy)
- "How do I run the tests?" → AGENTS.md (instruction)
- "What patterns do we avoid and why?" → CLAUDE.md (principle + rationale)
- "What's the PR title format?" → AGENTS.md (convention)

**Why Two Files?**
- CLAUDE.md is for *understanding*—it helps AI reason about the codebase
- AGENTS.md is for *action*—it helps AI execute correctly
- Some overlap is natural and acceptable (better documented twice than not at all)
- Different AI tools may prioritize one over the other

### The Template

```markdown
# AGENTS.md

## Project Overview
[Brief description: what this project does, who uses it, key technologies]

## Development Environment

### Setup
```bash
# Clone and install
git clone [repo]
npm install  # or pip install -r requirements.txt, etc.

# Required environment variables
cp .env.example .env
# Fill in: DATABASE_URL, API_KEY
```

### Running Locally
```bash
npm run dev      # Start development server
npm run db:seed  # Seed test data
```

## Build and Test Commands

### Essential Commands
```bash
npm test           # Run all tests (MUST pass before commits)
npm run test:watch # TDD mode
npm run lint       # Linting (auto-fixed on commit)
npm run typecheck  # TypeScript checks
npm run build      # Production build
```

### Testing Philosophy
- We practice outside-in TDD (see Constitution Article II)
- Test files: colocated as `*.test.ts`
- Use factories over fixtures: `/test/factories/`
- Mock external services, not internal modules

## Code Style Guidelines

### Naming Conventions
- Components: PascalCase (`UserProfile.tsx`)
- Utilities: camelCase (`formatDate.ts`)
- Constants: SCREAMING_SNAKE_CASE
- Test files: `[name].test.ts`

### Patterns We Follow
- Functional components only (no classes)
- Result types over exceptions
- Composition over inheritance
- Explicit over implicit

### Patterns to Avoid
- No `any` types without justification
- No barrel exports (index.ts re-exports)
- No business logic in components
- No direct DOM manipulation in React

## PR and Commit Guidelines

### Commit Messages
Format: `type(scope): description`
Types: feat, fix, refactor, test, docs, chore

Examples:
- `feat(auth): add password reset flow`
- `fix(orders): handle null shipping address`
- `refactor(api): extract validation middleware`

### PR Requirements
- [ ] Tests pass
- [ ] No new lint warnings
- [ ] Follows conventions in this file
- [ ] Traced to acceptance criteria
- [ ] Both pair members can explain the code

### PR Title Format
`[TICKET-123] Brief description of change`

## Architecture Notes

### Directory Structure
```
src/
├── domain/       # Business logic (no framework deps)
├── application/  # Use cases, orchestration
├── infrastructure/  # DB, APIs, external services
└── presentation/    # UI, controllers
```

### Key Abstractions
- All external I/O behind interfaces
- Repository pattern for data access
- Use cases are single-purpose

## Security Considerations

### Sensitive Areas
- `/src/auth/` - Authentication logic, review carefully
- `/src/payments/` - PCI compliance required
- `.env` files - Never commit, never log

### Security Checklist
- [ ] No secrets in code
- [ ] Input validation at boundaries
- [ ] SQL queries parameterized
- [ ] Auth checks on all protected routes

## Current Focus

### Active Work
- Migrating to React 18
- Adding OpenTelemetry tracing
- Performance optimization for dashboard

### Known Issues
- Legacy billing code in `/src/legacy/` - don't extend
- Flaky test in `checkout.test.ts` - skip if blocking

## Getting Help

### Team Conventions
See CLAUDE.md for architectural philosophy and patterns.

### When Stuck
- Check existing similar code first
- Ask in #engineering Slack
- Escalate ambiguity rather than assume
```

### Hierarchical Resolution

For monorepos or complex projects:

```
/AGENTS.md                    # Root-level defaults
/packages/api/AGENTS.md       # API-specific overrides
/packages/frontend/AGENTS.md  # Frontend-specific overrides
```

The closest AGENTS.md to the edited file wins. Explicit user prompts override everything.

### Practical Scenarios

**Scenario 1: New Agent, New Codebase**

```
AI agent starts working on your project:

1. Reads AGENTS.md at repo root
2. Understands: TypeScript, React, outside-in TDD
3. Sees: "npm test must pass before commits"
4. Notes: "No business logic in components"
5. Checks: security considerations for auth changes

AI now has context to contribute appropriately.
```

**Scenario 2: Monorepo Navigation**

```
Project structure:
/AGENTS.md                     # "Use pnpm, not npm"
/packages/api/AGENTS.md        # "Python 3.11, pytest"
/packages/frontend/AGENTS.md   # "React 18, Vitest"

AI editing /packages/api/src/handler.py:
→ Uses /packages/api/AGENTS.md
→ Knows to use pytest, not Jest
→ Follows Python conventions, not TypeScript
```

**Scenario 3: AGENTS.md + Constitution Integration**

```
AGENTS.md says: "Run tests before committing"
Constitution says: "Humans write first failing test"

AI behavior:
1. Waits for human to write first test
2. Helps with implementation
3. Runs tests via MCP before suggesting commit
4. Both constraints are honored
```

### Living Documentation

Treat AGENTS.md as living documentation:
- Update when conventions change
- Add gotchas as they're discovered
- Remove outdated information
- Review quarterly with CLAUDE.md

### Anti-Patterns

| Anti-Pattern | Why It Fails |
|--------------|--------------|
| Empty AGENTS.md | Agent has no context, makes wrong assumptions |
| Stale instructions | Agent follows outdated patterns |
| Conflicting AGENTS.md files | Agent gets confused, inconsistent behavior |
| Too much detail | Agent context limits; keep it focused |
| No testing instructions | Agent doesn't know how to verify work |
| Missing security section | Agent may miss security considerations |

---

## Chapter 3: A2A Protocol — Agent-to-Agent Communication

*Implements: Constitution Article VI (Boundaries), Article I (Hierarchy of Understanding)*

### The Philosophy

A2A (Agent-to-Agent) is an open protocol that enables AI agents built on different frameworks to communicate and collaborate. While MCP connects an agent to tools, A2A connects agents to each other.

> "Multiple Claude instances aren't redundancy—they're collaboration between different perspectives."

A2A enables specialized agents to work together on complex problems without exposing their internal implementation. Think of it as an API contract between autonomous AI systems.

### When to Use A2A

| Scenario | Use A2A? | Why |
|----------|----------|-----|
| Single AI helping with coding | No | Direct interaction sufficient |
| Specialized agents within your system | Maybe | Consider if agents need independence |
| Integrating external AI services | Yes | Standard protocol for interop |
| Multi-vendor AI ecosystem | Yes | Vendor-neutral communication |
| Agents that must protect internal logic | Yes | A2A preserves opacity |

### A2A vs MCP: The Distinction

```
┌─────────────────────────────────────────────────────────┐
│                     YOUR SYSTEM                         │
│                                                         │
│  ┌─────────────┐         ┌─────────────┐               │
│  │   Agent A   │◄──A2A──►│   Agent B   │               │
│  │  (Claude)   │         │  (External) │               │
│  └──────┬──────┘         └─────────────┘               │
│         │                                               │
│        MCP                                              │
│         │                                               │
│  ┌──────▼──────┐                                       │
│  │   Tools     │                                       │
│  │ (filesystem,│                                       │
│  │  database,  │                                       │
│  │  browser)   │                                       │
│  └─────────────┘                                       │
└─────────────────────────────────────────────────────────┘

MCP = Agent ↔ Tools (extend what one agent can do)
A2A = Agent ↔ Agent (enable agents to collaborate)
```

**MCP answers**: "What tools can this agent use?"
**A2A answers**: "How do agents talk to each other?"

### The A2A Protocol

**Transport**: JSON-RPC 2.0 over HTTP(S)

**Interaction Modes**:
- Synchronous request/response
- Server-sent events (streaming)
- Asynchronous push notifications (webhooks)

**Data Formats**: Text, files, structured JSON

### Core Concepts

#### 1. Agent Cards (Discovery)

Every A2A agent publishes an Agent Card describing its capabilities:

```json
{
  "name": "CodeReviewAgent",
  "description": "Reviews code for quality, security, and conventions",
  "url": "https://review.example.com",
  "version": "1.0.0",
  "skills": [
    {
      "name": "review_pull_request",
      "description": "Review a PR for issues",
      "inputSchema": {
        "type": "object",
        "properties": {
          "repo": { "type": "string" },
          "pr_number": { "type": "integer" }
        },
        "required": ["repo", "pr_number"]
      }
    },
    {
      "name": "check_security",
      "description": "Scan code for security vulnerabilities",
      "inputSchema": { ... }
    }
  ],
  "authentication": {
    "type": "bearer",
    "instructions": "Obtain token from admin portal"
  }
}
```

Location: `https://agent.example.com/.well-known/agent.json`

#### 2. Tasks (Lifecycle)

A2A interactions are organized as Tasks with defined lifecycle:

```
┌──────────┐     ┌──────────┐     ┌──────────┐
│ Created  │────►│ Running  │────►│ Completed│
└──────────┘     └────┬─────┘     └──────────┘
                      │
                      ▼
                ┌──────────┐
                │  Failed  │
                └──────────┘
```

Tasks can be:
- Short-lived (single request/response)
- Long-running (polling or webhook for completion)
- Streaming (progressive results)

#### 3. Skills (Capabilities)

Skills are the methods an agent exposes for others to invoke:

```python
# Defining a skill
@skill(
    name="analyze_code",
    description="Analyze code quality and suggest improvements"
)
async def analyze_code(code: str, language: str) -> AnalysisResult:
    # Agent's internal logic (opaque to caller)
    ...
```

### The Practice: Implementing A2A

#### Setting Up an A2A Server (Python)

```python
# Install: pip install a2a-sdk

from a2a import A2AServer, skill, AgentCard

# Define your agent's capabilities
card = AgentCard(
    name="ArchitectAgent",
    description="Designs system architecture from requirements",
    skills=[
        {
            "name": "design_component",
            "description": "Design a system component",
            "inputSchema": {...}
        }
    ]
)

server = A2AServer(card)

@server.skill("design_component")
async def design_component(requirements: dict) -> dict:
    # Your architecture logic here
    return {
        "components": [...],
        "interfaces": [...],
        "recommendations": [...]
    }

# Run the server
server.run(port=8080)
```

#### Calling an A2A Agent (Client)

```python
from a2a import A2AClient

# Discover agent capabilities
client = A2AClient("https://review-agent.example.com")
card = await client.get_agent_card()

print(f"Agent: {card.name}")
print(f"Skills: {[s.name for s in card.skills]}")

# Invoke a skill
result = await client.invoke(
    skill="review_pull_request",
    input={
        "repo": "myorg/myrepo",
        "pr_number": 123
    }
)

print(result.output)
```

### Practical Scenarios

**Scenario 1: Specialized Agent Pipeline**

Your development workflow uses multiple specialized agents:

```
┌────────────────┐
│ Requirements   │
│ (from PM)      │
└───────┬────────┘
        │
        ▼
┌────────────────┐     A2A      ┌────────────────┐
│ Architect      │─────────────►│ Security       │
│ Agent          │              │ Review Agent   │
└───────┬────────┘              └───────┬────────┘
        │                               │
        │ A2A                           │ A2A
        ▼                               ▼
┌────────────────┐              ┌────────────────┐
│ Implementation │              │ Test Generation│
│ Agent          │              │ Agent          │
└───────┬────────┘              └────────────────┘
        │
        ▼
   Human Review
   (Constitution
    checkpoint)
```

AGENTS.md for this setup:
```markdown
## Agent Pipeline

### Flow
1. ArchitectAgent receives requirements → produces design
2. SecurityReviewAgent reviews design → produces security assessment
3. ImplementationAgent implements design → produces code
4. TestGenerationAgent suggests test cases → human writes first test

### A2A Endpoints
- Architect: https://architect.internal/.well-known/agent.json
- Security: https://security.internal/.well-known/agent.json
- Implementation: https://impl.internal/.well-known/agent.json
- Tests: https://tests.internal/.well-known/agent.json

### Human Checkpoints (per Constitution)
- [ ] Requirements approval
- [ ] Design approval
- [ ] Security sign-off
- [ ] First test written by human
- [ ] Final review before merge
```

**Scenario 2: External Agent Integration**

Integrating with a partner's AI service:

```markdown
## External Agent: PartnerPaymentAgent

**Discovery**: https://partner.example.com/.well-known/agent.json

**Authentication**:
- Type: mTLS
- Certificates: Rotated quarterly
- Contact: partner-integrations@example.com

**Skills We Use**:
- `process_payment` - Submit payment for processing
- `get_payment_status` - Check payment status
- `refund_payment` - Initiate refund

**Our Responsibilities**:
- Validate payment data before sending
- Handle async responses via webhook
- Retry with exponential backoff (max 3 attempts)
- Log all A2A interactions for audit

**Their SLA**:
- Response within 30 seconds
- 99.9% availability
- Webhook delivery within 5 minutes

**Human Checkpoint**:
Payments > $10,000 require human approval before A2A call

**Error Handling**:
```python
if response.status == "failed":
    if response.error.retryable:
        schedule_retry(exponential_backoff)
    else:
        escalate_to_human(response.error)
```
```

**Scenario 3: Multi-Vendor Agent Ecosystem**

Your organization uses agents from multiple vendors:

```markdown
## Agent Ecosystem

### Internal Agents (we control)
| Agent | Purpose | A2A Endpoint |
|-------|---------|--------------|
| CodeGen | Generate implementation | https://codegen.internal/... |
| DocGen | Generate documentation | https://docgen.internal/... |

### External Agents (vendor-provided)
| Vendor | Agent | Purpose | A2A Endpoint |
|--------|-------|---------|--------------|
| Vendor A | SecurityScan | SAST/DAST scanning | https://vendor-a.com/... |
| Vendor B | Compliance | Regulatory checks | https://vendor-b.com/... |

### Integration Pattern
All external A2A calls go through our gateway:
1. Gateway validates request against Constitution
2. Gateway logs interaction for audit
3. Gateway enforces rate limits
4. Gateway handles auth token rotation

### Fallback Policy
If external agent unavailable:
1. Queue request for retry
2. Notify team after 3 failures
3. Allow human override to proceed without check
```

### A2A Security Principles

```markdown
## A2A Security Policy

### Authentication
- Internal agents: mTLS with internal CA
- External agents: OAuth 2.0 or API keys
- Token rotation: Every 90 days minimum

### Authorization
- Principle of least privilege
- Each agent only accesses skills it needs
- Human approval for sensitive operations

### Data Protection
- No PII in A2A payloads without encryption
- Audit log all inter-agent communication
- Data classification labels on all payloads

### Opacity Preservation
A2A is designed to keep agent internals private:
- Don't expose internal reasoning
- Don't share training data
- Don't reveal proprietary algorithms

### Failure Modes
- Network failure → Retry with backoff
- Auth failure → Alert, don't retry
- Skill failure → Log, escalate to human
- Timeout → Cancel task, notify human
```

### Claude-Flow: Multi-Agent Orchestration for Claude

[Claude-Flow](https://github.com/ruvnet/claude-flow) is an open-source orchestration platform that coordinates multiple Claude agents in collaborative workflows. While A2A is a protocol for agent communication, Claude-Flow is a ready-to-use system for deploying multi-agent swarms.

#### When to Use Claude-Flow

| Scenario | Use Claude-Flow? |
|----------|-----------------|
| Simple single-agent coding tasks | No — direct Claude interaction sufficient |
| Complex multi-step features | Yes — coordinate specialized agents |
| Research + implementation in parallel | Yes — researcher and developer agents |
| Large refactoring projects | Yes — analysis, planning, implementation agents |
| Tasks requiring persistent memory | Yes — built-in memory across sessions |

#### Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│                    Claude-Flow System                        │
│                                                              │
│  ┌─────────────┐                                            │
│  │   Queen     │ ← Coordinator: assigns tasks, manages flow │
│  │ Coordinator │                                            │
│  └──────┬──────┘                                            │
│         │                                                    │
│    ┌────┴────┬─────────┬─────────┬─────────┐               │
│    ▼         ▼         ▼         ▼         ▼               │
│ ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐              │
│ │Archi-│ │Devel-│ │Test  │ │Review│ │Resea-│              │
│ │tect  │ │oper  │ │Agent │ │Agent │ │rcher │              │
│ └──────┘ └──────┘ └──────┘ └──────┘ └──────┘              │
│                                                              │
│  ┌─────────────────────────────────────────────────────┐    │
│  │              Memory Layer (AgentDB)                  │    │
│  │  • Persistent across sessions                       │    │
│  │  • Semantic vector search                           │    │
│  │  • Pattern learning                                 │    │
│  └─────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────┘
```

#### Two Operating Modes

**Swarm Mode** — Quick, single-task execution
```bash
# Natural language task execution
npx claude-flow swarm "Build REST API with JWT authentication" --claude

# Characteristics:
# - Instant setup
# - Task-scoped memory
# - Best for focused tasks
```

**Hive-Mind Mode** — Complex, multi-feature projects
```bash
# Initialize persistent session
npx claude-flow init my-project

# Start hive-mind for a feature
npx claude-flow hive-mind "User authentication system"

# Continue later with context preserved
npx claude-flow resume my-project

# Characteristics:
# - Persistent memory across sessions
# - Interactive configuration
# - Best for large features or projects
```

#### Key Capabilities

**1. Specialized Agents**
Claude-Flow includes 64+ specialized agents across domains:
- Development agents (architect, implementer, debugger)
- Research agents (analyst, documentation reader)
- Quality agents (tester, reviewer, security scanner)
- Deployment agents (CI/CD, release management)

**2. Persistent Memory**
```
Session 1: "Analyze the payment module"
  → Memory stores: module structure, patterns found, concerns

Session 2: "Refactor payment validation"
  → Memory recalls: previous analysis, knows context
  → No need to re-explain the codebase
```

**3. Skill System**
25 Claude Skills activate automatically through natural language:
```
You say: "Review this PR for security issues"
Activates: GitHub Integration + Security Analysis skills

You say: "Set up pre-commit hooks for formatting"
Activates: Automation + Hook Configuration skills
```

**4. MCP Integration**
100+ MCP tools available:
- Swarm initialization and agent spawning
- Memory storage and retrieval
- GitHub repository analysis
- Performance benchmarking

#### Using Claude-Flow with the Constitution

Claude-Flow is powerful, but must respect Constitution principles:

**Human Checkpoints Still Required**
```markdown
## Claude-Flow Workflow with Constitution

1. Human provides requirements (Article III)
2. Researcher Agent gathers context
3. Architect Agent proposes design
4. ⚠️ HUMAN CHECKPOINT: Approve design
5. Human writes first failing test (Article II)
6. Developer Agent implements
7. Test Agent suggests additional tests
8. Review Agent checks against CLAUDE.md
9. ⚠️ HUMAN CHECKPOINT: Final review
10. Human approves merge
```

**Configure Human Checkpoints**
```yaml
# claude-flow.config.yaml
checkpoints:
  design_approval: required
  first_test: human_only  # Never delegate
  security_changes: required
  api_changes: required
  final_review: required

agents:
  developer:
    boundaries:
      - never_skip_failing_tests
      - follow_claude_md_conventions
      - escalate_ambiguity
```

#### Practical Scenario: Feature Development

```
Task: "Add user export functionality for GDPR compliance"

Phase 1: Research (Researcher Agent)
─────────────────────────────────────
Researcher: "Analyzing codebase for user data locations..."
Researcher: "Found: UserRepository, OrderRepository, PreferencesStore"
Researcher: "GDPR requirements: right to access, right to erasure"
→ Memory: stores findings for later phases

Phase 2: Design (Architect Agent)
─────────────────────────────────────
Architect: "Proposing ExportService with streaming CSV..."
Architect: "Following hexagonal architecture per CLAUDE.md..."

⚠️ HUMAN CHECKPOINT
Pair reviews design, approves with modifications

Phase 3: Implementation (Developer Agent)
─────────────────────────────────────
Human: Writes first failing test
Developer: "Implementing ExportService..."
Developer: "Following Result type pattern per CLAUDE.md..."

Phase 4: Review (Review Agent)
─────────────────────────────────────
Reviewer: "Checking against conventions..."
Reviewer: "✓ Naming follows patterns"
Reviewer: "✓ No business logic in infrastructure"
Reviewer: "⚠ Suggest: add explicit error messages"

⚠️ HUMAN CHECKPOINT
Pair reviews, approves, merges
```

#### Getting Started

```bash
# Install Claude-Flow
npm install -g claude-flow@alpha

# Initialize in your project
npx claude-flow init --force

# Start with a task
npx claude-flow swarm "describe your task" --claude
```

#### Claude-Flow Boundaries

To align with our Constitution, set these boundaries:

```markdown
## Claude-Flow Boundaries (add to AGENTS.md)

### Never Delegate
- Writing acceptance criteria
- Writing first failing test
- Final merge approval
- Security-sensitive decisions

### Agent Boundaries
- Agents follow CLAUDE.md conventions
- Agents escalate ambiguity to humans
- Agents don't modify without test coverage
- Agents log all significant decisions

### Memory Hygiene Protocol

*Implements Constitution Article VIII.2 (Agent Memory Is Not Team Knowledge)*

Agent memory is powerful but creates risk. Knowledge that lives only in the agent system is invisible debt.

#### Weekly Memory Sync

Every week, the team should:
1. Review what's stored in agent memory (patterns, context, learned behaviors)
2. Verify at least 2 team members understand each significant stored pattern
3. Transfer valuable learnings to CLAUDE.md, AGENTS.md, or code comments
4. Delete memory that only one person (or no one) understands

#### Memory Lifecycle

| Memory Type | Retention | Action at End |
|-------------|-----------|---------------|
| Feature-specific context | Until feature ships | Delete or transfer to docs |
| Codebase patterns | Quarterly review | Confirm still accurate or delete |
| Session context | End of session | Auto-expires |
| Long-term learnings | 6 months max | Transfer to docs and renew, or delete |

#### The Redundancy Test

Ask quarterly: *If agent memory were deleted tomorrow, could the team continue working?*

- If **yes**: Memory is a useful accelerant, not a dependency. ✓
- If **no**: Knowledge has concentrated in the system. Fix immediately.

#### Memory Is Not Documentation

Anything worth keeping in agent memory should also exist in:
- CLAUDE.md (if it's philosophy or patterns)
- AGENTS.md (if it's instructions or process)
- Code comments (if it's implementation context)
- README or docs (if it's user-facing)

Agent memory supplements documentation. It never replaces it.
```

### Anti-Patterns

| Anti-Pattern | Why It Fails |
|--------------|--------------|
| Exposing internal state via A2A | Violates opacity principle |
| No authentication between agents | Security vulnerability |
| Synchronous calls for long operations | Timeouts, poor UX |
| No human checkpoints in pipeline | Violates Constitution |
| Hardcoded agent URLs | Breaks when agents move |
| No retry/fallback strategy | Single point of failure |
| Trusting external agent output blindly | Must validate |
| Letting Claude-Flow write first tests | Violates TDD Compact |
| Skipping design review for speed | Creates rework, misalignment |
| Not syncing human knowledge with agent memory | Knowledge silos in the system |

---

## Chapter 4: MCP Servers — Extending AI Capabilities

*Implements: Constitution Article VI (Boundaries), Article V (Craft Standards)*

### The Philosophy

Model Context Protocol (MCP) servers give AI access to tools, data sources, and capabilities beyond text generation. Think of them as controlled extensions of what AI can perceive and do.

> "Use bash tools, MCP servers, and custom commands like a virtuoso uses their instruments."

The key word is *controlled*. Every MCP server is a capability grant. You're deciding what AI can access and what it cannot. This is a security and workflow design decision.

### The Practice

MCP servers should:
1. **Do one thing well** — Single responsibility, clear purpose
2. **Have explicit permissions** — Read-only vs. read-write, scoped access
3. **Log their actions** — Auditability for debugging and compliance
4. **Fail gracefully** — Clear error messages, no silent failures
5. **Respect boundaries** — Never bypass Constitution principles

### MCP Server Inventory

Maintain a registry of available MCP servers:

```markdown
## MCP Server Registry

### filesystem
**Purpose**: Read project files, understand codebase structure
**Permissions**: Read-only to project directory
**Use When**: AI needs to understand existing code, find patterns
**Never Use For**: Writing files directly (use explicit write tools)

### git
**Purpose**: Read git history, understand change evolution
**Permissions**: Read-only
**Use When**: Understanding why code exists, finding when bugs were introduced
**Never Use For**: Making commits (human checkpoint required)

### database (dev-only)
**Purpose**: Query development database for understanding schema/data
**Permissions**: Read-only, dev environment only
**Use When**: Understanding data structures, debugging data issues
**Never Use For**: Production access (blocked), data modification
**⚠ Warning**: Never expose in production MCP configuration

### browser
**Purpose**: View rendered application, verify visual changes
**Permissions**: Navigate, screenshot
**Use When**: Verifying frontend changes, debugging UI issues
**Never Use For**: Automated testing (use proper test framework)

### terminal
**Purpose**: Run predefined commands (build, test, lint)
**Permissions**: Allowlisted commands only
**Use When**: Verifying changes work, running TDD cycle
**Never Use For**: Arbitrary command execution
**Allowlist**:
  - npm test
  - npm run build
  - npm run lint
  - npm run typecheck
```

### Practical Scenarios

**Scenario 1: Understanding Unfamiliar Code**

Navigator asks AI: "How does the payment retry logic work?"

```
AI uses: filesystem MCP → reads PaymentService
AI uses: git MCP → finds commit that introduced retry logic
AI uses: git MCP → reads commit message explaining the "why"

AI response: "Payment retry was added in commit abc123 after the
Stripe outage in March. It uses exponential backoff with jitter,
max 3 retries. The original discussion is in PR #456."
```

The navigator now has context no documentation provided.

**Scenario 2: TDD Cycle with MCP**

Driver writes failing test. AI assists with implementation.

```
1. Driver writes test → test fails
2. AI uses: terminal MCP → confirms test fails (red)
3. AI suggests implementation
4. Driver types implementation
5. AI uses: terminal MCP → confirms test passes (green)
6. Pair discusses refactoring
7. AI suggests refactor
8. AI uses: terminal MCP → confirms tests still pass
9. AI uses: terminal MCP → runs lint, confirms no warnings
```

The TDD cycle is AI-assisted but human-driven.

**Scenario 3: Debugging with Database Context**

Bug report: "User sees wrong subscription status"

```
AI uses: database MCP → queries user subscription state
AI uses: filesystem MCP → reads SubscriptionService logic
AI uses: git MCP → finds recent changes to subscription code

AI identifies: "The migration in commit xyz added a status column
but didn't backfill existing records. Users created before March 1
have NULL status, which the UI renders as 'inactive'."
```

Human decides: write migration to backfill, add NOT NULL constraint.

**Scenario 4: Visual Verification**

Story requires UI change: "Add export button to dashboard"

```
1. Implementation complete
2. AI uses: browser MCP → navigates to dashboard
3. AI uses: browser MCP → takes screenshot
4. AI compares to design mock
5. AI notes: "Button is present but spacing differs from mock.
   Design shows 16px margin-top, implementation has 8px."
```

Pair fixes spacing before marking complete.

### MCP Security Principles

```markdown
## MCP Security Policy

### Environment Segregation
- Development MCP config: Full tool access
- CI/CD MCP config: Read-only, no database
- Production: No MCP access (AI doesn't touch production directly)

### Credential Management
- MCP servers never receive production credentials
- API keys scoped to minimum required permissions
- Rotate keys quarterly, immediately on team changes

### Audit Logging
- All MCP tool invocations logged with timestamp, parameters, result
- Logs retained for [compliance period]
- Anomaly alerts for unusual patterns (bulk reads, off-hours access)

### Allowlisting Philosophy
Default deny. Each tool capability explicitly granted:
- ✓ Read source files in /src
- ✓ Run npm test
- ✗ Read .env files (blocked)
- ✗ Run arbitrary shell commands (blocked)
- ✗ Access /secrets directory (blocked)
```

### Anti-Patterns

| Anti-Pattern | Why It Fails |
|--------------|--------------|
| Production database MCP | Security nightmare, violates least privilege |
| Write access without human checkpoint | AI can break things faster than you can recover |
| No command allowlist | AI runs `rm -rf` "to clean up" |
| MCP config in repository | Credentials leak |
| Same MCP config for all environments | Violates segregation |

---

# Part II: Workflow Integration

---

## Chapter 5: The AI-Assisted TDD Cycle

*Implements: Constitution Article II (TDD Compact), Article VII (Rituals)*

### The Philosophy

TDD is not bureaucracy. It's a design discipline. AI accelerates the *implementation* part of the cycle but must never shortcut the *thinking* part.

> "Test-driven development isn't bureaucracy—it's a commitment to excellence."

The cycle: **Red → Green → Refactor**

- **Red**: Human writes failing test (the thinking)
- **Green**: AI may assist implementation (the building)
- **Refactor**: Human leads, AI suggests (the crafting)

### The Practice

#### Phase 1: Red (Human Territory)

The navigator and driver discuss the acceptance criterion. Together they:
1. Identify the behavior to test
2. Name the test (the name IS the specification)
3. Write the assertion first (what should be true?)
4. Write the setup (what state is needed?)
5. Run the test—confirm it fails for the right reason

**AI's Role**: Silent. Watching. Learning context.

#### Phase 2: Green (AI-Assisted)

The test is red. Now AI may participate:

```
Driver: "We have a failing test for 'should reject payment when
        insufficient funds'. What's the simplest implementation?"

AI: [Reviews the test, understands the interface]
    "The simplest implementation that passes:

    if (account.balance < amount) {
      return Result.failure(InsufficientFunds);
    }

    This checks the specific case. Want me to consider edge cases?"

Navigator: "What about exactly equal balance?"

AI: "The test says 'insufficient'—so equal should pass.
    The current implementation handles this (< not <=).
    Should I suggest a test for the boundary case?"

Driver: "Yes, but I'll write it."
```

**Key behaviors**:
- AI implements to the test, not beyond
- AI asks about ambiguity rather than assuming
- Human writes additional tests

#### Phase 3: Refactor (Human-Led)

Tests are green. Now we improve the design without changing behavior.

```
Navigator: "I see three places checking account.balance.
           Is there an abstraction here?"

AI: "I see the pattern. Options:
    1. Method on Account: account.hasSufficientFunds(amount)
    2. Value object: Money with comparison operators
    3. Leave as-is (it's only three places)

    Option 1 follows your naming convention (verb+noun methods
    on entities). Option 2 is more powerful but might be
    over-engineering for three uses. What feels right?"

Navigator: "Option 1. It reads well in the conditionals."

Driver: [Implements the refactor]

AI: [Runs tests via MCP] "All tests pass. The refactor is safe."
```

**Key behaviors**:
- AI presents options, not decisions
- AI references CLAUDE.md conventions
- AI verifies safety with tests

### Practical Scenarios

**Scenario 1: Outside-In TDD for a New Feature**

Story: "User can view their order history"

```
Layer 1: Acceptance Test (Outer)
─────────────────────────────────
Human writes:
  it('shows order history for authenticated user', async () => {
    const user = await createUser();
    await createOrder(user, { items: ['Widget'], total: 100 });
    await createOrder(user, { items: ['Gadget'], total: 200 });

    const response = await request(app)
      .get('/orders')
      .set('Authorization', `Bearer ${user.token}`);

    expect(response.status).toBe(200);
    expect(response.body.orders).toHaveLength(2);
    expect(response.body.orders[0].total).toBe(200); // Most recent first
  });

Test fails: 404 (route doesn't exist)

Layer 2: Controller Test
─────────────────────────
Human writes:
  it('returns orders from service', async () => {
    const mockOrders = [{ id: 1, total: 100 }];
    orderService.getOrdersForUser.mockResolvedValue(mockOrders);

    const result = await controller.getOrders(userId);

    expect(result).toEqual({ orders: mockOrders });
  });

Test fails: controller.getOrders is not a function

AI assists:
  "Based on your controller convention (thin controllers,
  delegate to services), here's the implementation:

  async getOrders(userId: string) {
    const orders = await this.orderService.getOrdersForUser(userId);
    return { orders };
  }"

Test passes. Move inward.

Layer 3: Service Test
─────────────────────
Human writes:
  it('returns orders sorted by date descending', async () => {
    const old = await createOrder({ createdAt: yesterday });
    const recent = await createOrder({ createdAt: today });

    const result = await service.getOrdersForUser(userId);

    expect(result[0].id).toBe(recent.id);
    expect(result[1].id).toBe(old.id);
  });

Test fails: service method doesn't exist

AI assists with implementation.

Tests pass. Acceptance test now passes.
```

**Scenario 2: AI Tries to Skip the Test**

```
Driver: "We need to add email validation to registration."

AI: "I can add email validation. Here's a regex that handles
    most cases, plus a check for disposable email domains..."

Navigator: "Stop. We haven't written a test. What behavior
           are we specifying?"

Driver: "Right. The acceptance criterion says 'reject invalid
        emails with helpful message'. Let me write that test first."

[Writes test: should_reject_registration_with_invalid_email]
[Writes test: should_show_helpful_message_for_invalid_email]

Navigator: "Now we know what 'invalid' and 'helpful' mean
           in our context. AI, what's the simplest implementation?"
```

**Scenario 3: Refactoring with AI Assistance**

```
Navigator: "This PaymentProcessor has grown to 400 lines.
           It's doing too much."

AI: [Analyzes the class]
    "I see these distinct responsibilities:
    1. Payment validation (lines 45-120)
    2. Fraud checking (lines 121-200)
    3. Gateway communication (lines 201-350)
    4. Receipt generation (lines 351-400)

    Following your hexagonal architecture:
    - Validation → domain service
    - Fraud checking → domain service (or external via port)
    - Gateway → infrastructure adapter
    - Receipt → infrastructure adapter

    Shall I propose the extracted interfaces first?"

Navigator: "Yes, but let's do one at a time. Start with
           gateway extraction since that's the clearest boundary."

[Pair extracts PaymentGateway interface]
[All tests still pass]
[Repeat for each responsibility]
```

### Anti-Patterns

| Anti-Pattern | Why It Fails |
|--------------|--------------|
| AI writes the first test | Test doesn't encode human understanding |
| "Make the tests pass" without review | AI may implement nonsense that technically passes |
| Skipping refactor phase | Technical debt accumulates faster with AI speed |
| Testing implementation details | Refactoring becomes impossible |
| AI runs tests without human seeing results | Human loses feedback loop |

---

## Chapter 6: Prompt Patterns That Honor the Constitution

*Implements: All Constitution Articles*

### The Philosophy

How you talk to AI determines what you get back. Prompts are not commands—they're conversations that establish context, constraints, and expectations.

> "Before you write a single line, sketch the architecture in your mind. Create a plan so clear, so well-reasoned, that anyone could understand it."

The same applies to prompts. A clear prompt produces clear output. A vague prompt produces confident nonsense.

### The Patterns

#### Pattern 1: The Context-First Prompt

**Structure**:
```
[Context about the codebase/situation]
[What you're trying to achieve]
[Constraints from Constitution/CLAUDE.md]
[Specific question or request]
```

**Example**:
```
We're implementing the order export feature (story #234).
The acceptance criteria require CSV export with streaming for large datasets.

Our CLAUDE.md says:
- Infrastructure code goes in /src/infrastructure
- Use Result types over exceptions
- All external I/O behind interfaces

The failing test is:
  should_stream_orders_to_csv_without_loading_all_into_memory

What's the simplest implementation that passes this test
while following our patterns?
```

**Why it works**: AI has context, constraints, and a specific target. It can't wander.

#### Pattern 2: The Options Prompt

When you need to make a decision, ask AI to present options—not make the choice.

**Example**:
```
We need to add caching to the ProductCatalog queries.
Response time is currently 800ms; target is <200ms.

Options to consider:
- In-memory cache (simple but doesn't survive restarts)
- Redis (distributed but adds infrastructure)
- HTTP caching headers (client-side, reduces server load)

For each option, tell me:
1. Implementation complexity in our codebase
2. How it affects our test strategy
3. Operational considerations

Don't recommend one. Present the tradeoffs so we can decide.
```

**Why it works**: AI provides analysis; humans provide judgment.

#### Pattern 3: The Constraint-First Prompt

When AI keeps suggesting approaches you don't want:

**Example**:
```
CONSTRAINTS (non-negotiable):
- No new dependencies
- No changes to public API
- Must work with existing database schema
- Solution must be understood by the team in <10 minutes

Within these constraints, how would you implement rate limiting
for the /api/search endpoint?
```

**Why it works**: Constraints are stated upfront, not discovered after three wrong suggestions.

#### Pattern 4: The Review Request

After implementation, ask AI to review against standards:

**Example**:
```
I've implemented the export feature. Before I ask for human review,
check this against:

1. Our CLAUDE.md conventions (attached)
2. The acceptance criteria (listed below)
3. The Constitution's craft standards:
   - Simplest solution that works?
   - Names that reveal intent?
   - Edge cases handled with grace?

Be critical. What would a senior engineer catch in review?
```

**Why it works**: AI becomes a pre-filter, catching obvious issues before human review.

#### Pattern 5: The Teaching Prompt

When using AI to learn (Constitution Article VI.2 encourages this):

**Example**:
```
I'm unfamiliar with how our event sourcing implementation works.

Don't write code for me. Instead:
1. Explain the pattern as implemented in /src/domain/events
2. Walk me through an example: how does UserRegistered event flow through the system?
3. Quiz me: what would happen if I needed to add a new event type?

I need to understand this to pair on it tomorrow.
```

**Why it works**: AI teaches; human learns. Knowledge transfers to the human, not just the codebase.

#### Pattern 6: The Ultrathink Prompt

For complex problems that need deep consideration:

**Example**:
```
**ultrathink**

We're hitting a wall. The checkout flow has 47 edge cases,
12 payment methods, and 3 different tax calculation systems.
Every change breaks something else.

Don't give me quick fixes. Think deeply:
- What is the *real* structure of this problem?
- What would the ideal architecture look like if we started fresh?
- How would we migrate from current to ideal incrementally?

Take your time. I'd rather have one profound insight
than ten superficial suggestions.
```

**Why it works**: Signals that speed is not the goal; depth is.

### Anti-Patterns

| Anti-Pattern | Why It Fails |
|--------------|--------------|
| "Write me a function that..." | No context, no constraints, probably wrong |
| "Fix this bug" [pastes error] | AI guesses at cause without understanding system |
| "Make it better" | Better how? AI will add complexity |
| "Just do it" | Skips the thinking that prevents mistakes |
| Copy-pasting AI output without reading | Violates Constitution Article I |

### The Prompt Checklist

Before sending a significant prompt, verify:

- [ ] **Context provided**: Does AI know what codebase/feature/story?
- [ ] **Constraints stated**: Does AI know what's off-limits?
- [ ] **Target specified**: Does AI know what success looks like?
- [ ] **Constitution honored**: Am I asking AI to do something reserved for humans?
- [ ] **Learning preserved**: Will I understand the output, or just use it?

---

## Chapter 7: Spec-Driven Development with AI

*Implements: Constitution Foundation (Spec-Driven Development), Article III (Story Protocol)*

### The Philosophy

Specs are contracts that enable parallel work, catch integration bugs early, and give AI the constraints it needs to generate conformant code.

> "A well-written spec gives AI the constraints it needs to generate conformant code."

The sequence matters:
1. **Acceptance criteria** define what the user needs
2. **Spec** defines the contract between components
3. **Tests** verify the contract is honored
4. **Implementation** fulfills the contract

AI is dangerous at step 1 (user understanding is human work), useful at steps 2-4.

### The Practice

#### Spec Types and When to Use Them

| Spec Type | Use For | Format |
|-----------|---------|--------|
| API Specification | REST/HTTP interfaces | OpenAPI 3.x |
| Event Specification | Async messaging | AsyncAPI |
| Type Interface | Internal boundaries | TypeScript interfaces / Protocol Buffers |
| Behavioral Contract | Complex state machines | State charts / Decision tables |

#### Workflow: API Feature with OpenAPI

**Step 1: Human writes acceptance criteria**
```markdown
Story: User retrieves their profile

Acceptance Criteria:
- Authenticated user can GET their profile
- Response includes: name, email, memberSince
- 401 if not authenticated
- 404 if user deleted
```

**Step 2: Human drafts spec (AI may assist with syntax)**
```yaml
# openapi.yaml
paths:
  /users/me:
    get:
      summary: Get current user profile
      security:
        - bearerAuth: []
      responses:
        '200':
          description: User profile
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/UserProfile'
        '401':
          description: Not authenticated
        '404':
          description: User not found

components:
  schemas:
    UserProfile:
      type: object
      required: [name, email, memberSince]
      properties:
        name:
          type: string
          example: "Jane Developer"
        email:
          type: string
          format: email
        memberSince:
          type: string
          format: date
```

**Step 3: Generate contract tests**
```
Human: "Given this OpenAPI spec, what test cases do we need
        to verify the contract?"

AI: "Contract tests needed:
     1. 200: Returns UserProfile matching schema
     2. 200: All required fields present
     3. 401: Missing auth header → 401
     4. 401: Invalid token → 401
     5. 404: Deleted user → 404
     6. Response Content-Type is application/json

     Shall I generate the test skeletons for your framework?"
```

**Step 4: Human writes first contract test**
```typescript
describe('GET /users/me contract', () => {
  it('returns UserProfile matching schema when authenticated', async () => {
    const user = await createAuthenticatedUser();

    const response = await request(app)
      .get('/users/me')
      .set('Authorization', `Bearer ${user.token}`);

    expect(response.status).toBe(200);
    expect(response.body).toMatchSchema(UserProfileSchema);
  });
});
```

**Step 5: AI assists implementation against spec**
```
Human: "Implement the /users/me endpoint to pass this test
        and conform to the OpenAPI spec."

AI: [Reads spec, understands contract]
    "Implementation following your controller conventions:

    // src/presentation/UserController.ts
    async getMe(req: AuthenticatedRequest): Promise<UserProfile> {
      const user = await this.userService.findById(req.userId);
      if (!user) {
        throw new NotFoundError('User not found');
      }
      return {
        name: user.name,
        email: user.email,
        memberSince: user.createdAt.toISOString().split('T')[0]
      };
    }

    This returns exactly the schema fields. The date format
    matches OpenAPI's 'date' format (YYYY-MM-DD)."
```

### Practical Scenarios

**Scenario 1: Frontend-Backend Parallel Development**

```
Day 1 Morning:
- Team agrees on acceptance criteria for "User Dashboard"
- Human drafts OpenAPI spec for /api/dashboard endpoint
- Spec committed to repository

Day 1 Afternoon:
- Backend pair: Implements endpoint against spec
- Frontend pair: Builds UI using mock server generated from spec
- Both pairs use AI assistance, both constrained by same spec

Day 2:
- Integration test runs against real backend
- Contract violations caught immediately (spec is source of truth)
- Fixes are targeted: "Response missing 'lastLogin' field per spec"
```

**Scenario 2: AI Suggests Spec Violation**

```
AI: "I can add a 'preferences' field to the response—it would
     be useful for the UI to have theme settings."

Navigator: "That's not in the spec. If we need preferences,
           we update the spec first, then implement."

Driver: "Good catch. Let's check if the story requires it."

[Reviews acceptance criteria—preferences not mentioned]

Navigator: "Not in scope. We can propose it for a future story,
           but this implementation follows the current spec."
```

**Scenario 3: Async Event Contract with AsyncAPI**

```yaml
# asyncapi.yaml
channels:
  orders/created:
    publish:
      message:
        $ref: '#/components/messages/OrderCreated'

components:
  messages:
    OrderCreated:
      payload:
        type: object
        required: [orderId, userId, total, createdAt]
        properties:
          orderId:
            type: string
            format: uuid
          userId:
            type: string
          total:
            type: number
            minimum: 0
          createdAt:
            type: string
            format: date-time
```

AI assistance:
```
Human: "Generate a test that verifies our OrderCreated events
        conform to the AsyncAPI spec."

AI: "Contract test for event schema:

    it('publishes OrderCreated event matching AsyncAPI spec', async () => {
      const order = await createOrder({ total: 100 });

      const event = await captureEvent('orders/created');

      expect(event.orderId).toMatch(uuidRegex);
      expect(event.userId).toBeDefined();
      expect(event.total).toBeGreaterThanOrEqual(0);
      expect(event.createdAt).toMatch(iso8601Regex);

      // Full schema validation
      expect(event).toMatchAsyncAPISchema('OrderCreated');
    });

    Want me to add tests for edge cases like zero-total orders?"
```

### SpecKit: Tooling for Spec-Driven Development

[GitHub SpecKit](https://github.com/github/spec-kit) is an open-source toolkit that formalizes spec-driven development for AI-assisted workflows. It provides structure for the specification → planning → implementation cycle.

#### The SpecKit Philosophy

SpecKit embodies the principle: *Make your technical decisions explicit, reviewable, and evolvable.*

Rather than exhaustive waterfall documents, SpecKit creates living documents that capture the "why" behind architectural choices. This surfaces assumptions early and prevents miscommunication between team members and AI agents.

#### The Three-Step Workflow

```
┌────────────────────────────────────────────────────────────┐
│  /specify                                                  │
│  "What are we building and why?"                          │
│  • Requirements and motivations                           │
│  • User needs and acceptance criteria                     │
│  • NO technical decisions yet                             │
└────────────────────┬───────────────────────────────────────┘
                     │
                     ▼
┌────────────────────────────────────────────────────────────┐
│  /plan                                                     │
│  "How will we build it?"                                  │
│  • Technical implementation approach                      │
│  • Frameworks, libraries, infrastructure                  │
│  • Architecture decisions with rationale                  │
└────────────────────┬───────────────────────────────────────┘
                     │
                     ▼
┌────────────────────────────────────────────────────────────┐
│  /tasks                                                    │
│  "What are the implementation chunks?"                    │
│  • Phased, manageable work items                         │
│  • Context preserved across tasks                        │
│  • AI can implement sequentially                         │
└────────────────────────────────────────────────────────────┘
```

#### SpecKit Artifacts

**1. Constitution Document**
```markdown
# Project Constitution

## Non-Negotiables
- All APIs must be OpenAPI-specified before implementation
- No direct database access from presentation layer
- Security review required for auth changes

## Organizational Conventions
- We use TypeScript for all backend services
- Error handling via Result types, not exceptions
- Tests colocated with source files
```

**2. Spec Template**
```markdown
# Feature: User Profile Export

## Motivation
Users need to export their data for GDPR compliance and personal records.

## User Experience
1. User navigates to Settings → Privacy
2. User clicks "Export My Data"
3. System generates CSV within 30 seconds
4. User downloads file

## Acceptance Criteria
- [ ] Authenticated users can export
- [ ] Export includes: profile, orders, preferences
- [ ] Large exports stream (don't OOM)
- [ ] Audit log records export requests

## Out of Scope
- Scheduled/recurring exports
- Format selection (CSV only for v1)
```

**3. Technical Plan**
```markdown
# Technical Plan: User Profile Export

## Approach
Streaming CSV generation with chunked database reads.

## Components
- ExportService (application layer) - orchestrates export
- CsvStreamWriter (infrastructure) - writes CSV chunks
- ExportController (presentation) - handles HTTP

## Data Flow
```
Request → Auth Check → ExportService
                           ↓
                    ChunkedUserQuery (1000 records/chunk)
                           ↓
                    CsvStreamWriter → Response Stream
```

## Dependencies
- fast-csv library for streaming CSV
- Existing UserRepository (read-only access)

## Open Questions
- [ ] Should we encrypt the download? (Ask security team)
- [ ] Rate limiting policy? (Ask product)
```

**4. Tasks Breakdown**
```markdown
# Tasks: User Profile Export

## Phase 1: Core Implementation
- [ ] Task 1.1: Create ExportService interface and tests
- [ ] Task 1.2: Implement ChunkedUserQuery
- [ ] Task 1.3: Implement CsvStreamWriter

## Phase 2: Integration
- [ ] Task 2.1: Create ExportController
- [ ] Task 2.2: Wire up streaming response
- [ ] Task 2.3: Add audit logging

## Phase 3: Polish
- [ ] Task 3.1: Error handling and edge cases
- [ ] Task 3.2: Performance testing with large datasets
- [ ] Task 3.3: Documentation
```

#### Using SpecKit with the Constitution

SpecKit's workflow maps directly to our Constitution:

| SpecKit Step | Constitution Article |
|--------------|---------------------|
| /specify | Article III (Story Protocol) - Human writes requirements |
| /plan | Article I (Understanding) - Understand before implementing |
| /tasks | Article II (TDD) - Human writes first test per task |
| Constitution doc | CLAUDE.md - Project philosophy and conventions |

**Integration example**:
```
1. PM creates spec using /specify
2. Pair reviews spec, ensures acceptance criteria are testable
3. Pair runs /plan to document technical approach
4. Human reviews plan, approves architecture
5. Pair runs /tasks to break down work
6. For each task:
   a. Human writes first failing test (Constitution Article II)
   b. AI assists implementation
   c. Pair reviews together
```

#### Getting Started with SpecKit

```bash
# Install SpecKit CLI
uvx --from git+https://github.com/github/spec-kit.git specify init my-project

# Project structure created:
my-project/
├── specs/
│   └── template.md
├── plans/
│   └── template.md
├── tasks/
│   └── template.md
└── constitution.md
```

SpecKit is agent-agnostic—it works with Claude, GitHub Copilot, Cursor, and other AI coding assistants.

### Anti-Patterns

| Anti-Pattern | Why It Fails |
|--------------|--------------|
| Implementation before spec | Contract is implicit, discovered through bugs |
| Spec as documentation (written after) | Drift between spec and reality |
| AI generates spec from code | Spec should constrain code, not describe it |
| Ignoring spec validation in CI | Violations ship to production |
| Different specs per environment | Integration becomes environment-dependent |
| Skipping /plan and going straight to /tasks | Technical decisions made ad-hoc, inconsistently |
| AI writes the spec | Loses human understanding of requirements |

---

# Part III: The Craft

---

## Chapter 8: Iteration and Refinement

*Implements: Constitution Article V (Craft Standards), Article VII (Rituals)*

### The Philosophy

> "The first version is never good enough. Take screenshots. Run tests. Compare results. Refine until it's not just working, but *insanely great*."

AI makes first drafts cheap. This is dangerous—it tempts us to ship first drafts. The discipline is to treat AI output as raw material, not finished product.

### The Practice

#### The Refinement Loop

```
1. AI generates first draft
2. Human reviews against craft standards
3. Human identifies improvements
4. AI assists with refinement
5. Repeat until craft standards met
6. Human confirms: "This is ready for review"
```

#### Craft Standards Checklist

Before considering code complete, verify:

**Clarity**
- [ ] Could a new team member understand this in 5 minutes?
- [ ] Are there any "clever" tricks that should be simplified?
- [ ] Do names reveal intent without needing comments?

**Simplicity**
- [ ] Is there any code that could be removed?
- [ ] Are there abstractions that serve only one use case?
- [ ] Could this be expressed more directly?

**Consistency**
- [ ] Does this follow CLAUDE.md patterns?
- [ ] Would this look natural next to existing code?
- [ ] Are similar things done similarly?

**Robustness**
- [ ] Are edge cases handled gracefully?
- [ ] Are error messages helpful to the user?
- [ ] Is the failure mode obvious, not silent?

### Practical Scenarios

**Scenario 1: Refining AI-Generated Code**

```
AI generates:
  function processOrder(order) {
    if (order && order.items && order.items.length > 0) {
      const total = order.items.reduce((sum, item) => {
        return sum + (item.price * item.quantity);
      }, 0);
      if (order.discount) {
        return total * (1 - order.discount);
      }
      return total;
    }
    return 0;
  }

Navigator: "This works but violates our craft standards.
           Let's refine."

Iteration 1 - Clarity:
  "The nested conditionals are hard to follow.
   What if we use early returns?"

AI refines:
  function calculateOrderTotal(order: Order): number {
    if (!order?.items?.length) {
      return 0;
    }

    const subtotal = order.items.reduce(
      (sum, item) => sum + item.price * item.quantity,
      0
    );

    return applyDiscount(subtotal, order.discount);
  }

Iteration 2 - Naming:
  "What does 'applyDiscount' do with undefined discount?"

AI refines:
  function applyDiscount(amount: number, discountRate?: number): number {
    if (!discountRate) return amount;
    return amount * (1 - discountRate);
  }

Navigator: "Now it reads like documentation. Ship it."
```

**Scenario 2: The "Good Enough" Trap**

```
Driver: "The tests pass. Let's move on."

Navigator: "Wait. This function is 45 lines. Our convention
           is functions under 20 lines. Can we break it up?"

Driver: "But it works..."

Navigator: "Working is table stakes. We committed to craft.
           AI, can you identify natural seams in this function?"

AI: "I see three distinct responsibilities:
     1. Input validation (lines 1-12)
     2. Business logic (lines 13-35)
     3. Response formatting (lines 36-45)

     Each could be a focused function. Want me to propose
     the extraction?"

[Pair refactors into three clear functions]
[Tests still pass]
[Code now matches team standards]
```

**Scenario 3: Visual Refinement**

```
Story: "Update button styling to match new design system"

Implementation complete. AI uses browser MCP to compare:

AI: "Screenshot comparison:
     ✓ Button color matches design (#0066CC)
     ✓ Border radius matches (8px)
     ✗ Font weight differs (design: 600, impl: 400)
     ✗ Padding differs (design: 12px 24px, impl: 8px 16px)

     The button is functionally correct but visually off.
     Shall I suggest the CSS adjustments?"

Driver: "Yes, and let's add a visual regression test
        so this doesn't drift again."
```

### Anti-Patterns

| Anti-Pattern | Why It Fails |
|--------------|--------------|
| "Tests pass, ship it" | Working is minimum bar, not the goal |
| No iteration on AI output | First drafts become permanent |
| Refining alone (without pair) | Loses the second perspective |
| Refining forever | Diminishing returns; know when to stop |
| Ignoring "code smell" intuition | Your instinct is pattern recognition; trust it |

---

## Chapter 9: Simplification

*Implements: Constitution Article V.1 (Simplicity Over Speed)*

### The Philosophy

> "Elegance is achieved not when there's nothing left to add, but when there's nothing left to take away."

AI generates code quickly. This is precisely why simplification matters more than ever—complexity is now cheap to produce, which makes it easier to accumulate.

The discipline: After AI generates, ask "What can we remove?"

### The Practice

#### The Simplification Questions

1. **Is this abstraction earning its keep?**
   - Does it have more than one caller?
   - Does it hide meaningful complexity?
   - Would inline code be clearer?

2. **Is this parameter necessary?**
   - Is it always the same value?
   - Could it be derived from other parameters?
   - Does the function need this flexibility?

3. **Is this branch reachable?**
   - Can this condition ever be true?
   - Is this defensive code defending against impossible states?
   - Are we handling errors that can't happen?

4. **Is this the simplest expression?**
   - Could a library do this better?
   - Could we use built-in language features?
   - Is there a more direct path to the result?

### Practical Scenarios

**Scenario 1: Removing Premature Abstraction**

```
AI generates:
  interface OrderProcessor {
    process(order: Order): Promise<Result>;
  }

  class StandardOrderProcessor implements OrderProcessor {
    async process(order: Order): Promise<Result> {
      // ... 20 lines of logic
    }
  }

  // Usage (only one place in codebase):
  const processor: OrderProcessor = new StandardOrderProcessor();
  return processor.process(order);

Navigator: "We have an interface with one implementation
           and one caller. This is premature abstraction."

AI: "You're right. Simplified:

    async function processOrder(order: Order): Promise<Result> {
      // ... same 20 lines
    }

    // Usage:
    return processOrder(order);

    We can extract an interface later if we actually need
    multiple implementations."

Driver: "Much cleaner. The abstraction was speculative."
```

**Scenario 2: Removing Defensive Code**

```
AI generates:
  function getUser(id: string): User | null {
    if (!id) return null;
    if (typeof id !== 'string') return null;
    if (id.length === 0) return null;
    if (id.length > 100) return null;

    return this.repository.findById(id);
  }

Navigator: "Where is this called from?"

AI: "Only from authenticated routes where id comes from
     the JWT token, which is already validated."

Navigator: "So these checks are defending against impossible
           states. The type system guarantees id is a string.
           The auth middleware guarantees it's valid."

Simplified:
  function getUser(id: string): User | null {
    return this.repository.findById(id);
  }

Driver: "We trust our boundaries. Internal code doesn't
        need to re-validate."
```

**Scenario 3: Simplifying Control Flow**

```
AI generates:
  function calculateShipping(order: Order): number {
    let shipping = 0;
    if (order.total > 100) {
      shipping = 0; // Free shipping
    } else if (order.total > 50) {
      shipping = 5;
    } else if (order.total > 25) {
      shipping = 8;
    } else {
      shipping = 12;
    }
    if (order.isPriority) {
      shipping = shipping + 10;
    }
    if (order.destination === 'international') {
      shipping = shipping * 2;
    }
    return shipping;
  }

Navigator: "This reads like assembly. Can we express
           the business rules more directly?"

AI: "The rules are:
     1. Base shipping by tier
     2. Priority adds flat fee
     3. International doubles it

    Simplified:
    function calculateShipping(order: Order): number {
      const base = getBaseShipping(order.total);
      const withPriority = order.isPriority ? base + 10 : base;
      return order.destination === 'international'
        ? withPriority * 2
        : withPriority;
    }

    function getBaseShipping(total: number): number {
      if (total > 100) return 0;
      if (total > 50) return 5;
      if (total > 25) return 8;
      return 12;
    }

    Each function does one thing. Rules are visible."
```

### The Simplification Ritual

After any significant AI-assisted implementation:

```
1. Navigator asks: "What can we remove?"
2. Pair identifies candidates:
   - Unused parameters
   - Single-use abstractions
   - Defensive checks for impossible states
   - Redundant comments (code should speak)
3. For each candidate, ask: "What breaks if we remove this?"
4. If nothing breaks: remove it
5. Run tests to confirm
```

### Anti-Patterns

| Anti-Pattern | Why It Fails |
|--------------|--------------|
| "Leave it, it might be useful" | YAGNI—complexity has carrying cost |
| Abstracting with one use case | Premature; wait for second case |
| Defending against callers | Trust your system boundaries |
| Comments that repeat code | Duplication that drifts |
| Keeping code "for reference" | That's what git history is for |

---

# Part IV: Team Dynamics

---

## Chapter 10: Pairing with AI Present

*Implements: Constitution Article I (Hierarchy of Understanding), Article IV (Knowledge Preservation)*

### The Philosophy

The pair is two humans. AI is a tool, not a third pair member. The dynamics of pairing—the knowledge transfer, the second perspective, the sustainable pace—must be preserved even when AI accelerates implementation.

### The Practice

#### The Roles Remain

**Navigator's Job** (unchanged):
- Think ahead
- Catch errors
- Hold the acceptance criteria
- Question assumptions
- AI is another information source, like documentation

**Driver's Job** (unchanged):
- Control the keyboard
- Focus on syntax and immediate implementation
- Vocalize decisions
- AI suggestions are processed through the driver, not around them

#### AI Interaction Protocol

```
1. Navigator decides if/when to consult AI
2. Navigator frames the question
3. AI responds
4. Navigator and Driver discuss the response
5. Driver implements (typing, not pasting)
6. Both understand before moving on
```

**The key**: AI talks to the pair, not to individuals. Both must understand.

### Practical Scenarios

**Scenario 1: Navigator Uses AI for Context**

```
Navigator: "I'm not sure how the event system works.
           Let me check."

[Navigator asks AI about the event system]

AI: [Explains the pattern, cites relevant files]

Navigator: "Got it. So we need to publish an event here,
           and the SubscriptionService will pick it up."

Driver: "Makes sense. What's the event schema?"

Navigator: "AI showed me—it's in /src/domain/events.
           The pattern is EventName with a payload type.
           Let me pull up that file so we can see the convention."

[Both look at existing events]

Driver: "I see the pattern. I'll write the new event."
```

**Scenario 2: Driver Resists Paste Temptation**

```
AI suggests a 15-line implementation.

Driver: "That looks right, but I'm going to type it out.
        Explain as I go?"

Navigator: "Sure. Start with the interface..."

[Driver types, Navigator explains]

Driver: "Wait, what's this Result.mapError doing?"

Navigator: "It transforms the error type. Let's look at
           how we use it elsewhere..."

[Pair learns a pattern they would have missed by pasting]
```

**Scenario 3: Pair Rejects AI Suggestion**

```
AI: "I suggest using dependency injection here to
     make the service testable."

Navigator: "We already have a factory pattern for this.
           DI would be inconsistent with our approach."

Driver: "And it would require changes to the container
        setup. Not worth it for one service."

Navigator: "Agreed. AI, given our factory pattern in
           CLAUDE.md, how would you approach this instead?"

AI: [Provides solution consistent with team patterns]

Navigator: "Better. That matches our conventions."
```

**Scenario 4: Preventing Knowledge Silos**

```
End of pairing session:

Navigator: "Before we switch, can you explain back to me
           how this new service works?"

Driver: "Sure. It receives OrderPlaced events, validates
        the inventory, and either confirms or rejects..."

[Driver explains; Navigator confirms understanding]

Navigator: "Good. And I can explain the event sourcing
           decision we made?"

[Navigator explains; Driver confirms]

Both understand. Knowledge didn't silo in either person
or in the AI conversation.
```

### The Pair Rotation Schedule

AI does not change rotation frequency. If anything, increase it:

```
Traditional: Rotate pairs every 2-3 days
With AI: Consider rotating every 1-2 days

Why: AI acceleration means more code per session.
     More code = more knowledge to distribute.
     Faster rotation = wider knowledge distribution.
```

### Anti-Patterns

| Anti-Pattern | Why It Fails |
|--------------|--------------|
| Driver pastes AI output while navigator checks email | No second perspective, no knowledge transfer |
| "AI said so" as justification | AI isn't a team member; humans decide |
| One person "owns" the AI conversation | Knowledge silos in the AI operator |
| Skipping explanation because "AI was clear" | The pair must understand, not just AI |
| Longer sessions because "AI makes us faster" | Cognitive load accumulates; pace matters |

---

## Chapter 11: When Things Go Wrong

*Implements: Constitution Article IV.3 (The Debugging Principle), Article VI.3 (The Veto Power)*

### The Philosophy

AI will make mistakes. AI will suggest bugs. AI will confidently assert incorrect things. This is not a failure of AI—it's expected behavior. The system is designed to catch these failures through:
- Tests (catch behavioral errors)
- Pair review (catch logical errors)
- Constitution principles (catch process errors)

### The Practice

#### The Failure Modes

**1. AI suggests code that doesn't compile**
Response: Normal. Fix and continue.

**2. AI suggests code that fails tests**
Response: Normal. The test caught it. Refine.

**3. AI suggests code that passes tests but is wrong**
Response: Test gap. Write more tests. Review understanding.

**4. AI suggests architecture that violates CLAUDE.md**
Response: Redirect with constraints. Reference CLAUDE.md explicitly.

**5. AI generates code nobody on the pair understands**
Response: Stop. Do not use code you cannot debug. Simplify or research.

**6. AI confidently asserts something false**
Response: Verify against source. AI is an assistant, not an authority.

#### The Veto in Practice

```
Navigator: "I don't like this approach."

Driver: "It passes the tests."

Navigator: "I know, but I have a bad feeling about it.
           Something about the state management feels fragile."

Driver: "Can you articulate it?"

Navigator: "Not yet. But per the Constitution, I'm vetoing.
           Let's implement it without AI so I can think through it."

[Pair implements manually]

Navigator: "Now I see it. The AI's version had a race condition
           between the state update and the event publish.
           Our version handles it in a transaction."

Driver: "Good catch. The test didn't cover that timing."
```

The veto requires no justification, but often surfaces important intuitions.

### Practical Scenarios

**Scenario 1: AI Bug in Production**

```
Incident: Orders occasionally showing wrong totals

Investigation:
[AI-assisted debugging]

AI: "Looking at the OrderCalculator, I see the implementation
    I suggested last week. The reduce function initializes
    at 0 but doesn't handle floating point precision."

Postmortem questions:
1. Why didn't tests catch this? → Tests used integers, not decimals
2. Why didn't review catch this? → We didn't question the AI output
3. What's the fix? → Use decimal library or cents-as-integers

Action items:
- Add test with decimal values
- Fix calculation to use integer cents
- Add "money handling" section to CLAUDE.md
- Review other AI-generated financial calculations
```

**Scenario 2: AI Confidently Wrong**

```
Navigator: "What's the time complexity of this algorithm?"

AI: "This is O(n) because we iterate through the list once."

Navigator: "Wait—there's a nested loop on line 15."

AI: "You're right, I missed that. With the nested loop,
    it's O(n²). I apologize for the error."

Driver: "Good thing we checked. For our data size,
        O(n²) might be a problem."

Lesson: Verify AI assertions. Confidence ≠ correctness.
```

**Scenario 3: The Debugging Principle Enforced**

```
AI generates complex regex for validation.

Navigator: "Can you explain how this regex works?"

Driver: "Not really. It has lookaheads and I'm not
        sure what the capture groups are for."

Navigator: "Then we can't ship it. Constitution Article IV.3:
           'If AI generated code you cannot debug, you do not ship it.'"

Options:
1. Learn the regex (AI teaches, we understand)
2. Simplify to something we understand
3. Use a validation library

Pair chooses option 2: simpler regex + explicit checks.
```

### The Incident Retrospective Template

When AI-related issues occur, add these questions to your retrospective:

```markdown
## AI-Specific Retro Questions

1. **Where did the AI suggestion enter the codebase?**
   - Which pairing session?
   - Was it reviewed by both pair members?

2. **What Constitution principle was violated?**
   - Did we skip understanding? (Article I)
   - Did we skip tests? (Article II)
   - Did we violate CLAUDE.md? (Article V)

3. **What would have caught this earlier?**
   - Better test coverage?
   - Stricter adherence to ritual?
   - More skepticism of AI output?

4. **How do we prevent recurrence?**
   - Update CLAUDE.md with new guidance?
   - Add to team conventions?
   - Create specific test patterns?
```

### Anti-Patterns

| Anti-Pattern | Why It Fails |
|--------------|--------------|
| Blaming AI for bugs | AI isn't responsible; humans who shipped it are |
| Removing AI after an incident | Throwing away a tool; fix the process instead |
| Not documenting AI-related learnings | Same mistakes repeat |
| Defending AI output in review | "AI wrote it" is not a justification |
| Over-correcting with excessive review | Slows everything; fix the specific gap |

---

# Part V: Reference

---

## Quick Reference Card

### Constitution Articles Summary

| Article | Core Principle | Key Rule |
|---------|----------------|----------|
| I | Hierarchy of Understanding | Humans understand before AI generates; understanding over acceptance |
| II | TDD Compact | Humans write first failing test |
| III | Contract Protocol | Stories → Specs → Tests → Code; AI reads contracts, humans write them |
| IV | Knowledge Preservation | No silent generation; rotation continues |
| V | Craft Standards | Simplicity; codebase voice; beauty; iterate relentlessly; respect history |
| VI | Boundaries | AI may explore/propose but not decide; humans onboard humans |
| VII | Rituals | Pre-implementation pause (incl. git history); post-review; weekly reflection |
| VIII | Multi-Agent Compact | Human checkpoints non-negotiable; agent memory ≠ team knowledge |
| IX | Solo Developer Protocol | Additional discipline when pairing isn't possible |
| X | Amendments | Quarterly review; team consensus; core protections (I-IV, VIII-IX) |

### MCP Server Quick Reference

| Server | Use For | Never Use For |
|--------|---------|---------------|
| filesystem | Reading code, understanding patterns | Writing files directly |
| git | Understanding history, blame, PR context | Making commits |
| database | Understanding schema, debugging data | Production access, writes |
| browser | Visual verification, UI debugging | Automated testing |
| terminal | Running tests, builds, lint | Arbitrary commands |

### Prompt Pattern Quick Reference

| Pattern | When to Use | Key Element |
|---------|-------------|-------------|
| Context-First | Any significant request | State codebase context first |
| Options | Decision needed | "Present tradeoffs, don't recommend" |
| Constraint-First | AI keeps suggesting wrong approach | List non-negotiables upfront |
| Review Request | Before human review | Reference CLAUDE.md explicitly |
| Teaching | Learning new concept | "Don't write code; explain" |
| Ultrathink | Complex/stuck problem | "Think deeply; no quick fixes" |

### TDD Phase Responsibilities

| Phase | Human Does | AI May Do |
|-------|------------|-----------|
| Red | Write failing test | Watch, learn context |
| Green | Type implementation | Suggest implementation |
| Refactor | Decide what to improve | Suggest refactorings |

### Daily Checklist

```
Before starting:
□ CLAUDE.md is current
□ Pair assigned and present
□ User story and acceptance criteria understood

During implementation:
□ Tests written before implementation
□ Both pair members understand all code
□ AI suggestions discussed, not just accepted

Before completing:
□ All acceptance criteria have tests
□ Code reviewed against CLAUDE.md
□ Both pair members can explain the implementation
```

---

## Appendix A: CLAUDE.md Examples by Domain

### Web API Project

```markdown
# CLAUDE.md - OrderService API

## Overview
REST API for order management. Node.js + Express + PostgreSQL.
Part of larger e-commerce platform.

## Architecture
- Hexagonal architecture (ports and adapters)
- Domain logic in /src/domain (no framework dependencies)
- Express-specific code in /src/infrastructure/http
- Database access via repositories in /src/infrastructure/db

## Conventions
- Controllers: thin, delegate to use cases
- Use cases: one public method, named after the use case
- Repositories: return domain objects, not database rows
- Error handling: Result<T, E> types, not exceptions

## Testing
- Unit tests: /src/**/*.test.ts (colocated)
- Integration tests: /test/integration/*.test.ts
- Use test factories, not fixtures

## Current Work
- Migrating from callback-based to async/await
- Adding OpenTelemetry tracing

## Landmines
- /src/legacy/billing - do not extend, migration planned
- OrderStatus enum - complex state machine, read carefully
```

### React Frontend Project

```markdown
# CLAUDE.md - Dashboard UI

## Overview
React 18 + TypeScript dashboard for analytics platform.
Consumes REST API defined in /api/openapi.yaml.

## Architecture
- Feature-based folder structure (/src/features/*)
- Shared components in /src/components
- API layer generated from OpenAPI spec
- State: React Query for server state, Zustand for UI state

## Conventions
- Components: function components only, no classes
- Styling: Tailwind CSS, no inline styles object
- Testing: React Testing Library, test behavior not implementation
- Naming: PascalCase components, camelCase hooks

## Design System
- Use components from /src/components/ui
- Colors defined in tailwind.config.js
- Don't add new colors without design approval

## Current Work
- Accessibility audit in progress
- Dark mode implementation

## Landmines
- /src/features/legacy-charts - uses deprecated library, don't extend
- Custom hooks in /src/hooks/useAnalytics - complex caching logic
```

### Python ML Pipeline

```markdown
# CLAUDE.md - Model Training Pipeline

## Overview
ML pipeline for recommendation system. Python 3.11 + PyTorch.

## Architecture
- /src/data - data loading and preprocessing
- /src/models - model definitions
- /src/training - training loops and evaluation
- /src/serving - model serving and inference

## Conventions
- Type hints on all public functions
- Docstrings in Google style
- Config via Pydantic models, not dicts
- Logging via structlog, not print

## Testing
- pytest with fixtures in /tests/conftest.py
- ML tests use small synthetic datasets
- Integration tests require GPU, run separately

## Current Work
- Migrating to PyTorch 2.0 compile
- Adding experiment tracking with MLflow

## Landmines
- /src/models/legacy_recommender.py - deprecated, don't use
- Data loading assumes specific S3 bucket structure
```

---

## Appendix B: Team Adoption Guide

### Week 1: Foundation

**Day 1-2: Constitution Workshop**
- Read AI Constitution as a team
- Discuss each article
- Identify questions and concerns
- Initial amendments if needed

**Day 3-4: CLAUDE.md Creation**
- Each team writes CLAUDE.md for their codebase
- Review each other's CLAUDE.md files
- Iterate based on feedback

**Day 5: Ritual Practice**
- Practice Pre-Implementation Pause with a sample story
- Practice Post-Implementation Review
- Identify friction points

### Week 2: Pilot

**Pilot one feature with full Constitution compliance**
- Select a medium-complexity story
- Apply all rituals and practices
- Document what works and what doesn't
- Daily check-ins

### Week 3: Iteration

**Retrospective and adjustment**
- What rituals felt valuable?
- What felt like overhead?
- What gaps did we discover?
- Amend Constitution or Playbook based on learnings

### Week 4+: Steady State

**Ongoing practices**
- Weekly reflections (Constitution Article VII.3)
- Quarterly Constitution review
- Continuous CLAUDE.md updates
- Playbook chapter additions as needed

---

## Appendix C: Metrics and Signals

### Healthy Signals

| Signal | Indicates |
|--------|-----------|
| AI suggestions frequently refined | Team is iterating, not accepting first draft |
| Pair rotation continues at same pace | Knowledge distribution is working |
| CLAUDE.md updated regularly | Team is learning and documenting |
| Vetoes happen occasionally | Team is exercising judgment |
| Tests still written first | TDD discipline maintained |

### Warning Signals

| Signal | May Indicate |
|--------|--------------|
| AI code shipped without modification | Insufficient scrutiny |
| Knowledge concentrated in "AI expert" | Pair dynamics breaking down |
| CLAUDE.md stale | Team not maintaining context |
| No vetoes ever | Over-trust in AI |
| Tests written after implementation | TDD discipline slipping |
| Bugs traced to AI suggestions | Review process gaps |

### What to Measure

```
Track quarterly:
- % of stories where first test was human-written
- Pair rotation frequency (before/after AI adoption)
- Time from story start to first failing test
- Bugs attributed to AI-generated code
- CLAUDE.md update frequency

Don't track:
- "AI usage rate" (encourages gaming)
- "Time saved by AI" (encourages speed over craft)
- "Lines of code from AI" (meaningless metric)
```

---

## The Closing

This Playbook is a living document. As tools evolve, as your team learns, as the field matures—update it. The Constitution provides the principles; this Playbook provides the practices. Both should grow with your team.

> "The people who are crazy enough to think they can change the world are the ones who do."

Use these tools wisely. Build things that matter. Leave the codebase—and your team—better than you found them.

---

*AI Playbook v1.0*
*Companion to the AI Constitution*
*Review quarterly alongside Constitution*