---
agent: agent
description: Create an implementation plan with estimation and workable tasks
---

# Implementation Planning

Create a **concise** implementation plan with **clear, actionable tasks**.

## Guidelines

- **Concise**: Keep descriptions short and actionable
- **Clear Requirements**: Each task must have verifiable completion criteria
- **Workable**: Tasks should be small enough to complete in one session

## Pre-requisites

This prompt expects an existing user story at `.copilot/{feature-name}/requirements.md`.
If no user story exists, use `userstory.prompt.md` first.

## Process

1. **Read Requirements**
   - Load `.copilot/{feature-name}/requirements.md`
   - Understand acceptance criteria and scope
   - Note all requirements that must be satisfied

2. **Analyze Codebase**
   - Identify files to modify/create
   - Understand existing patterns and conventions
   - Review test structure and naming
   - Review documentation structure

3. **Define Implementation Strategy**
   - Choose approach based on existing architecture
   - Identify risks and mitigations
   - Plan for testability

4. **Break Down into Workable Tasks**
   - Each task should take ≤2 hours
   - Tasks should be independently verifiable
   - Include testing and documentation tasks

5. **Estimate Effort**
   - T-shirt sizing: S (≤1h), M (1-2h), L (2-4h), XL (>4h)
   - XL tasks should be broken down further

6. **Request Feedback**
   - Present plan summary
   - Ask for approval or adjustments

## Output: `.copilot/{feature-name}/plan.md`

```markdown
# Implementation Plan: {Feature Name}

> **User Story**: See [requirements.md](requirements.md)

## Strategy
{1-2 sentences on the implementation approach}

## Estimation Summary
| Size | Count | Total Hours |
|------|-------|-------------|
| S    | {n}   | {n}h        |
| M    | {n}   | {n*1.5}h    |
| L    | {n}   | {n*3}h      |
| **Total** | {N} | {X}h   |

## Tasks

### Phase 1: {Phase Name}

- [ ] **Task 1.1**: {Title} `[S]`
  - Files: `path/to/file.kt`
  - Done when: {verifiable criterion}

- [ ] **Task 1.2**: {Title} `[M]`
  - Files: `path/to/file.kt`, `path/to/other.kt`
  - Done when: {verifiable criterion}

### Phase 2: Testing

- [ ] **Task 2.1**: Unit tests for {component} `[M]`
  - Files: `path/to/ComponentTest.kt`
  - Done when: Tests pass, coverage adequate

- [ ] **Task 2.2**: Integration tests `[L]` (if applicable)
  - Files: `path/to/IntegrationTest.kt`
  - Done when: End-to-end flow verified

### Phase 3: Documentation

- [ ] **Task 3.1**: Update user docs `[S]`
  - Files: `doc/reference/feature.rst`
  - Done when: Usage documented with examples

- [ ] **Task 3.2**: Update developer docs `[S]` (if needed)
  - Files: `doc/developer/feature.md`
  - Done when: Architecture changes documented

## Checklist

### Before Starting
- [ ] Requirements reviewed and understood
- [ ] Codebase patterns identified
- [ ] No blocking questions

### Before Completion
- [ ] All tasks completed
- [ ] All acceptance criteria from `requirements.md` met
- [ ] All tests pass
- [ ] Documentation updated
- [ ] User approval received

## Verification

{Determine commands based on project type during planning}

| Step | Command | Expected Result |
|------|---------|-----------------|
| Run tests | {project-specific command} | All tests pass |
| Build | {project-specific command} | Build succeeds |
| {Additional step} | {command} | {expected} |

## Risks

| Risk | Mitigation |
|------|------------|
| {Risk description} | {How to handle} |
```

## Task Sizing Guide

| Size | Time | Complexity |
|------|------|------------|
| S | ≤1h | Single file, straightforward change |
| M | 1-2h | Few files, some logic |
| L | 2-4h | Multiple files, moderate complexity |
| XL | >4h | **Break down further** |

## Before Finishing

**MUST** ask for feedback using `vscode_askQuestions`:
- Is the strategy appropriate?
- Are estimates reasonable?
- Are tasks sufficiently granular?
