# Hands-On Exercise: Building a Feedback Widget with GitHub Speckit

## Overview

This is a hands-on exercise designed to help you practice the complete Specification-Driven Development workflow using GitHub Speckit. You'll build a simple feedback collection widget from scratch by following each step of the Speckit workflowfrom establishing project principles to implementing the final solution.

By the end of this exercise, you'll have:
- Created a constitutional framework for your project
- Specified requirements for a feedback widget
- Generated a technical implementation plan
- Created actionable tasks
- Implemented a working feature

This exercise is based on the content in [README.md](README.md). Follow each step below in order.

---

## Pre-Requirements

Before starting this exercise, ensure you have the following installed:

### 1. Install Node.js and Next.js

Create a new Next.js project (if starting from scratch):
```bash
npx create-next-app@latest feedback-widget-demo
cd feedback-widget-demo
```

### 2. Enable GitHub Spec Kit for Your Project

Use the following command to enable GitHub Speckit for your project:

```bash
uvx --from git+https://github.com/github/spec-kit.git specify init --here
```

This will initialize Spec Kit in your current project directory and make the `/speckit.*` commands available.

### 3. Verify Installation

Restart VS Code to see the installation take effect. After restarting, ensure Spec Kit is properly initialized by checking if the `/speckit.*` commands are available in your Claude Code interface.

---

## Step 1: Create Your Constitution

Run the following command to establish your project's governing principles:

```
/speckit.constitution create the constitution to use the existing project to build a simple and fast software. no testing is needed unless explicitly asked for. Include jsdocs, documentation for all functions and components.
```

**What this creates:**
- `.specify/memory/constitution.md` - Your project's governing principles

**Expected outcome:** A constitutional document that emphasizes simplicity, speed, documentation standards (jsdocs), and clarifies that testing is optional unless requested.

---

## Step 2: Specify Your Feature

Run the following command to create a detailed specification for the feedback widget:

```
/speckit.specify Build a feedback collection widget for marketing campaigns.

Users should be able to:
- Submit feedback with a 1-5 star rating and text comment (max 500 chars)
- View all submitted feedback in a clean table
- Delete individual feedback entries

Keep it minimal and functional - this is for internal campaign testing, not public-facing. Use a simple in-memory data store for now (no database setup needed for this demo).
```

**What this creates:**
- `specs/[branch-name]/` - Feature directory (branch name will be auto-generated, e.g., "001-feedback-widget")
- `specs/[branch-name]/spec.md` - Complete specification with user stories and acceptance criteria

**Expected outcome:** A structured specification document outlining all requirements for the feedback widget, including the star rating system, comment functionality, table view, and delete capability.

---

## Step 3: Clarify Requirements (Optional)

If you need to clarify any ambiguous requirements, run:

```
/speckit.clarify
```

**What this does:**
- Reviews your `spec.md` for any unclear or missing details
- Asks clarifying questions
- Updates the specification with additional information

**Expected outcome:** A refined specification with any ambiguities resolved. You can skip this step if the specification is already clear enough.

---

## Step 4: Create Technical Plan

Run the following command to generate a technical implementation plan:

```
/speckit.plan Build within the existing Next.js project structure. Use React components with TypeScript, style with Tailwind CSS for rapid development. Implement in-memory storage using React state management. Keep the component architecture simple and focused, with proper jsdocs for all functions and components.
```

**What this creates:**
- `specs/[branch-name]/plan.md` - High-level implementation strategy
- `specs/[branch-name]/research.md` - Technical research and decisions
- `specs/[branch-name]/data-model.md` - Data structure definitions
- `specs/[branch-name]/contracts/` - API/interface contracts
- `specs/[branch-name]/quickstart.md` - Test scenarios

**Expected outcome:** A comprehensive technical plan that defines:
- How to integrate the widget into the existing Next.js app structure
- React component architecture for the feedback widget
- Tailwind CSS utility classes for styling
- In-memory state management approach (useState/useReducer)
- Data model for feedback entries (rating, comment, timestamp, id)
- TypeScript interfaces and types

---

## Step 5: Generate Tasks

Run the following command to break down the plan into actionable tasks:

```
/speckit.tasks
```

**What this creates:**
- `specs/[branch-name]/tasks.md` - Detailed task list with parallelization markers

**Expected outcome:** A task list that might include:
- Create TypeScript interfaces for feedback data model
- Implement star rating React component
- Create feedback form component with validation
- Build feedback table/list component
- Implement delete functionality with state management
- Style components with Tailwind CSS utility classes
- Write jsdocs for all functions and components

Tasks marked with `[P]` can be done in parallel.

---

## Step 6: Analyze Consistency (Optional)

Run the following command to validate your specifications:

```
/speckit.analyze
```

**What this does:**
- Validates that all tasks cover the requirements from `spec.md`
- Checks alignment with constitutional principles
- Identifies any gaps or conflicts

**Expected outcome:** A report confirming that your tasks cover all requirements and comply with your constitution (simplicity, documentation, no mandatory testing).

---

## Step 7: Implement the Feature

Run the following command to build the actual code:

```
/speckit.implement
```

**What this creates:**
- React component files (TypeScript/TSX)
- Documentation (jsdocs)
- Any configuration files needed

**Expected outcome:** A working feedback widget.

---

## Verification

After completing the implementation, verify that your feedback widget:

1. Displays a clean form with star rating (1-5) and text input (max 500 chars)
2. Submits feedback and adds it to the React state (in-memory store)
3. Displays all feedback entries in a styled list/table using Tailwind CSS
4. Allows deleting individual entries with proper state updates
5. Has TypeScript types defined for all data structures
6. Has jsdocs on all functions and components
7. Follows the simple, minimal approach defined in your constitution
8. Integrates properly into the Next.js project structure

---

## Expected Time

This complete workflow typically takes **~15-20 minutes** from constitution to working implementation.

---

## Next Steps

After completing this exercise, try:
- Adding additional features (e.g., edit feedback, filter by rating)
- Creating a new constitution with different principles (e.g., requiring tests)
- Building a different feature using the same workflow
- Comparing the speed and consistency of Speckit vs. traditional development

---

For more information about each command, see the [README.md](README.md).
