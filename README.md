# Specification-Driven Development Demo

## What is Specification-Driven Development?

Specification-Driven Development (SDD) is a software development approach where specifications become executable artifacts that directly generate working implementations. Instead of specifications merely guiding developers, they serve as the foundation for AI-assisted development, ensuring that what you build matches what you intended from the start.

## What is GitHub Speckit?

GitHub Speckit is an open-source toolkit that brings structure and intent to AI-assisted software development. It provides a systematic workflow through slash commands that help you define project principles, specify requirements, create technical plans, generate tasks, and implement features—all while maintaining consistency across your development process.

## Speckit Commands

### `/speckit.constitution`
**Prompt: Required**

Creates your project's governing principles and development guidelines.

**What it does:**
- Establishes non-negotiable principles that will govern all subsequent development decisions
- Creates a constitutional framework that enforces constraints during planning and implementation

**Files created:**
- `.specify/memory/constitution.md` - Contains your project's governing principles, coding standards, architectural constraints, and quality requirements

**How it's used:**
- Referenced by `/speckit.plan` to ensure architectural decisions comply with your principles
- Enforces "Phase -1 Pre-Implementation Gates" that validate simplicity and anti-abstraction rules
- Acts as a constraint system for the AI throughout the entire workflow

Examples:
- `/speckit.constitution Create principles focused on code quality and testing standards`
- `/speckit.constitution Define guidelines emphasizing user experience consistency and performance`
- `/speckit.constitution Establish rules for accessibility, security, and maintainability`

### `/speckit.specify`
**Prompt: Required**

Defines what you want to build (requirements and user stories). Focus on the *what* and *why*, not implementation details.

**What it does:**
- Transforms a feature description into a complete, structured specification
- Automatically creates a semantic branch name from your description (e.g., "003-chat-system")
- Generates feature numbering (automatically incremented: 001, 002, 003)

**Files and folders created:**
- `specs/[branch-name]/` - Feature directory for this specification
- `specs/[branch-name]/spec.md` - Contains user stories, acceptance criteria, clarification markers for ambiguous requirements, and completeness checklists

**How it's used:**
- Serves as the authoritative source of requirements for the feature
- Fed into `/speckit.plan` to generate technical implementation plans
- Used by `/speckit.analyze` to validate that tasks cover all requirements
- Provides the "what" and "why" that guides all subsequent development

Examples:
- `/speckit.specify Build a photo organizer that helps users create and manage albums`
- `/speckit.specify Create a task management system with priority levels and due dates`
- `/speckit.specify Design a dashboard showing real-time analytics for user engagement`

### `/speckit.clarify`
**Prompt: Optional**

Helps refine and clarify underspecified areas before planning.

**What it does:**
- Reviews the existing `spec.md` for ambiguous or underspecified requirements
- Asks clarifying questions to fill gaps in the specification
- Updates the specification with additional details

**Files modified:**
- `specs/[branch-name]/spec.md` - Updates the specification with clarified requirements

**How it's used:**
- Run after `/speckit.specify` but before `/speckit.plan` to ensure completeness
- Reduces ambiguity that could lead to incorrect implementation decisions
- Optional step—skip if your specification is already detailed enough

Examples:
- `/speckit.clarify`
- `/speckit.clarify What are the expected user roles and permissions?`

### `/speckit.plan`
**Prompt: Required**

Translates intent into a technical approach, recording architectural choices, data flow, and dependencies.

**What it does:**
- Generates a comprehensive implementation plan from the specification
- Validates against constitutional principles before proceeding
- Documents technology selections with rationale
- Breaks down the implementation into phases

**Files and folders created:**
- `specs/[branch-name]/plan.md` - High-level implementation strategy, phase gates, technology selections, and complexity tracking
- `specs/[branch-name]/research.md` - Technical context (library compatibility, performance benchmarks, security implications)
- `specs/[branch-name]/data-model.md` - Entity schemas, relationships, database-agnostic data structure definitions
- `specs/[branch-name]/contracts/` - Directory containing API endpoint contracts, message formats, service boundaries
- `specs/[branch-name]/quickstart.md` - Key test scenarios, critical user workflows, acceptance validation checkpoints

**How it's used:**
- Bridges the gap between business requirements (`spec.md`) and executable tasks
- Enforces constitutional principles through "Phase -1 Pre-Implementation Gates"
- Provides architectural context for `/speckit.tasks` to generate actionable work items
- Documents decisions for future reference and team alignment

Examples:
- `/speckit.plan Use Vite with vanilla HTML, CSS, and JavaScript—minimal libraries`
- `/speckit.plan Build with React, TypeScript, and Tailwind CSS using a component-based architecture`
- `/speckit.plan Implement using Node.js backend with Express and PostgreSQL database`

### `/speckit.tasks`
**Prompt: Optional**

Breaks the plan into smaller, actionable tasks for implementation.

**What it does:**
- Derives executable task lists from implementation plans and design documents
- Analyzes `plan.md`, `data-model.md`, `contracts/`, and `research.md` to generate specific tasks
- Identifies tasks that can be parallelized for concurrent execution
- Creates sequential dependencies for tasks that must be done in order

**Files created:**
- `specs/[branch-name]/tasks.md` - Actionable task breakdown with parallelization markers `[P]` for independent tasks, safe parallel groupings, and sequential dependencies

**How it's used:**
- Final specification artifact fed directly to `/speckit.implement` or human developers
- Each task is self-contained with enough context for independent execution
- Parallelization markers enable concurrent work by multiple agents or developers
- Provides a checklist to track implementation progress

Examples:
- `/speckit.tasks`
- `/speckit.tasks Focus on frontend components first`

### `/speckit.analyze`
**Prompt: Optional**

Checks for consistency, ensuring tasks align with the plan and original specification.

**What it does:**
- Performs cross-artifact consistency analysis across all specification documents
- Validates that tasks in `tasks.md` cover all requirements from `spec.md`
- Checks that the plan aligns with constitutional principles
- Identifies gaps, conflicts, or missing coverage

**Files analyzed:**
- `spec.md` - Original requirements
- `plan.md` - Technical approach
- `tasks.md` - Implementation tasks
- `constitution.md` - Governing principles

**How it's used:**
- Run after `/speckit.tasks` to validate completeness before implementation
- Catches missing requirements, contradictions, or deviations from principles
- Provides a quality gate to prevent incomplete or inconsistent implementations
- Optional but recommended for complex features

Examples:
- `/speckit.analyze`
- `/speckit.analyze Check coverage of authentication requirements`

### `/speckit.implement`
**Prompt: Optional**

Executes all tasks and builds your feature according to the plan.

**What it does:**
- Reads all tasks from `tasks.md` and executes them sequentially or in parallel
- Creates actual code files, components, APIs, tests, and documentation
- Follows the technical approach outlined in `plan.md`
- Respects constitutional principles throughout implementation

**Files created:**
- Actual source code files in your project (e.g., `src/`, `components/`, `api/`, etc.)
- Test files
- Configuration files
- Documentation
- Any other artifacts specified in the tasks

**How it's used:**
- Final step that transforms specifications into working code
- Executes tasks marked with `[P]` in parallel when possible
- Creates a complete, tested implementation based on all previous specification work
- Results in a feature branch ready for testing and code review

Examples:
- `/speckit.implement`
- `/speckit.implement Start with the highest priority tasks`

---

## Complete Workflow Example

Here's how all commands work together to build a real-time chat feature:

```
1. /speckit.constitution Create principles for real-time features
   → Creates: .specify/memory/constitution.md

2. /speckit.specify Real-time chat with message history and user presence
   → Creates: specs/003-chat-system/spec.md
   → Auto-generates branch: 003-chat-system

3. /speckit.plan WebSocket messaging, PostgreSQL history, Redis presence
   → Creates: specs/003-chat-system/plan.md
             specs/003-chat-system/research.md
             specs/003-chat-system/data-model.md
             specs/003-chat-system/contracts/
             specs/003-chat-system/quickstart.md

4. /speckit.tasks
   → Creates: specs/003-chat-system/tasks.md

5. /speckit.analyze
   → Validates consistency across all specification files

6. /speckit.implement
   → Creates: src/chat/ChatComponent.tsx
             src/api/websocket.ts
             src/models/Message.ts
             tests/chat.test.ts
             ... (all actual code files)
```

**Time to complete:** ~15 minutes from idea to implementation

---

Learn more at [github.com/github/spec-kit](https://github.com/github/spec-kit)
