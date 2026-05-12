---
mode: agent
description: Create a user story with requirements and acceptance criteria
---

# User Story Creation

Create a **concise** user story with **clear requirements**.

## Guidelines

- **Concise**: Avoid unnecessary words; be direct
- **Clear Requirements**: Each requirement must be testable and unambiguous
- **No Implementation Details**: Focus on WHAT, not HOW

## Process

1. **Understand the Feature**
   - Ask clarifying questions if the request is ambiguous
   - Identify target users and their goals

2. **Explore the Codebase**
   - Search for related code, patterns, and conventions
   - Understand existing architecture
   - Identify integration points

3. **Ask for Clarification** (if needed)
   - Use `vscode_askQuestions` tool before proceeding
   - Ask when: user story is vague, multiple approaches exist, edge cases unclear

4. **Create User Story Document**
   - Create directory: `.copilot/{feature-name}/`
   - Write `requirements.md`
   - Update `.copilot/README.md` with new feature

5. **Request Feedback**
   - Present summary to user
   - Ask for approval or changes

## Output: `.copilot/{feature-name}/requirements.md`

```markdown
# Feature: {Feature Name}

## Overview
{One-sentence description}

## Pre-requisites
- {Dependency or precondition, if any}

## User Story
As a {user type}
I want {goal/desire}
So that {benefit/value}

## Requirements

### Functional
- **MUST**: {Critical requirement}
- **SHOULD**: {Important but not blocking}
- **MAY**: {Nice-to-have}

### Testing (MANDATORY)
- Unit tests for new/modified code
- Integration tests (if cross-component)
- All existing tests pass

### Documentation (MANDATORY)
- Developer docs (if architecture changes)
- User docs (if usage changes)
- API docs (if public API changes)

## Clarifications

| Question | Answer/Assumption |
|----------|-------------------|
| {Question} | {Answer or assumption made} |

## Tasks
1. {High-level task}
   - {Subtask}
2. {High-level task}

## Scope

### In Scope
- {What IS included}

### Out of Scope
- {What is NOT included}

## Acceptance Criteria
- [ ] Given {context}, When {action}, Then {result}
- [ ] Given {context}, When {action}, Then {result}

## Dependencies
- {Other features or systems this depends on}
```

## Feature Naming

Use kebab-case derived from the main requirement:
- "Add user login" → `user-login`
- "Support multiple API specs" → `multi-api-specs`

## Before Finishing

**MUST** ask for feedback using `vscode_askQuestions`:
- Are requirements complete?
- Are acceptance criteria sufficient?
- Any missing clarifications?

## Remember

- **Quality over speed**: It's better to ask questions than make wrong assumptions
- **Incremental delivery**: Break large features into small, deliverable tasks
- **Test-first thinking**: Consider testability when planning tasks; tests are NOT optional
- **Documentation is code**: Docs are part of the deliverable, not an afterthought
- **Verification**: Always include a verification step to run tests before marking complete
- **Update User Story Table**: Always add new features to `.copilot/README.md` table with links to requirements.md and plan.md
