# PR Example: Custom Chatbot Workflows

> **Purpose**: Example PR format for tasks from the Chatbot Workflows feature
> **Related**: [PRD](./prd-chatbot-workflows.md) | [SPEC](./spec-chatbot-workflows.md)

---

## Understanding Task IDs (T1, T2, etc.)

The technical spec includes a **Task Breakdown** section that decomposes the feature into discrete, implementable units. Each task has:

- **ID**: `T1`, `T2`, etc. - unique identifier for referencing in PRs and tickets
- **Description**: What the task accomplishes
- **Dependencies**: Which tasks must complete first
- **Priority**: P0 (MVP required) or P1 (important but deferrable)

See the [Task Breakdown table](./spec-chatbot-workflows.md#task-breakdown) and [dependency graph](./spec-chatbot-workflows.md#task-dependency-graph) in the spec for the full list.

**Example tasks referenced in this document:**

| ID | Task | Layer |
|----|------|-------|
| T2 | Workflow repository (CRUD operations) | Data |
| T3 | Workflow validation (graph structure) | Data |
| T8 | Workflow Matcher (trigger evaluation) | Execution |
| T14 | Chatbot integration (hook into pipeline) | Execution |
| T17 | UI: Workflow list page | UI |

---

## Example PR: T2 + T3 - Workflow Repository & Validation

### Title

```
feat(workflows): add workflow repository with graph validation
```

### Description

```markdown
## Summary

- Add `WorkflowRepository` class with CRUD operations for workflow storage
- Implement workflow graph validation (acyclic check, node reachability, trigger config validation)
- Add unit tests for repository and validation logic

This implements tasks T2 and T3 from the chatbot workflows spec, providing the data access layer that the API endpoints will use.

## Test plan

- [ ] Unit tests pass: `npm test -- --grep "WorkflowRepository"`
- [ ] Validation rejects cyclic graphs
- [ ] Validation rejects unreachable nodes
- [ ] Validation rejects invalid trigger configs
- [ ] Can create, read, update, and soft-delete workflows

🤖 Generated with [Claude Code](https://claude.com/claude-code)
```

---

## Example PR: T8 - Workflow Matcher

### Title

```
feat(workflows): implement workflow matcher for trigger evaluation
```

### Description

```markdown
## Summary

- Add `WorkflowMatcher` service that evaluates active workflows against incoming messages
- Support trigger types: `intent_match`, `keyword_contains`, `conversation_start`
- Integrate with Redis cache for fast lookup of active workflows
- Return highest-priority matching workflow (higher priority number wins, then most recently published)

Implements T8 from the chatbot workflows spec. This is the core component that determines which workflow should execute for a given conversation event.

## Test plan

- [ ] Matcher returns null when no workflows match
- [ ] Matcher returns correct workflow for intent triggers
- [ ] Matcher returns correct workflow for keyword triggers
- [ ] Priority ordering works correctly (higher priority wins)
- [ ] Falls back to most recently published when priorities are equal
- [ ] Performance: matching completes in < 10ms with 100 active workflows

🤖 Generated with [Claude Code](https://claude.com/claude-code)
```

---

## Example PR: T17 - UI Workflow List Page

### Title

```
feat(ui): add workflow list page with search and filtering
```

### Description

```markdown
## Summary

- Add `/workflows` page showing all workflows for current tenant
- Implement search by workflow name
- Add status filter dropdown (All, Draft, Active, Archived)
- Display workflow cards with name, trigger type, status, and last updated
- Add "New Workflow" button linking to editor

Implements T17 from the chatbot workflows spec. This is the entry point for conversation designers to manage their workflows.

## Test plan

- [ ] Page loads and displays workflows from API
- [ ] Search filters workflows by name (debounced)
- [ ] Status filter works correctly
- [ ] Empty state shown when no workflows exist
- [ ] Loading state shown while fetching
- [ ] Error state shown on API failure
- [ ] "New Workflow" button navigates to `/workflows/new`
- [ ] Responsive layout works on tablet and desktop

## Screenshots

| Desktop | Tablet |
|---------|--------|
| [screenshot] | [screenshot] |

🤖 Generated with [Claude Code](https://claude.com/claude-code)
```

---

## Example PR: T14 - Chatbot Integration

### Title

```
feat(chatbot): integrate workflow executor into message pipeline
```

### Description

```markdown
## Summary

- Hook `WorkflowExecutor` into the chatbot message handling pipeline
- On each incoming message, check for matching workflows before default handling
- Execute matched workflow and return responses to user
- Fall back to default chatbot behavior when no workflow matches or execution fails
- Add feature flag `ENABLE_WORKFLOW_EXECUTION` for gradual rollout

Implements T14 from the chatbot workflows spec. This connects the workflow system to the existing chatbot, enabling workflows to handle conversations.

## Test plan

- [ ] Messages trigger workflow matching when feature flag enabled
- [ ] Matched workflow executes and returns responses
- [ ] Default behavior used when no workflow matches
- [ ] Default behavior used when workflow execution fails (graceful degradation)
- [ ] Feature flag disables workflow execution entirely
- [ ] Execution logged for debugging
- [ ] P95 latency increase < 50ms

## Rollout plan

1. Deploy with feature flag disabled
2. Enable for internal tenant (dogfooding)
3. Enable for 5% of tenants, monitor latency
4. Gradual rollout to 100%

🤖 Generated with [Claude Code](https://claude.com/claude-code)
```

---

## PR Conventions

### Commit Message Format

```
<type>(<scope>): <short description>

<body - what and why>

Co-Authored-By: Claude Opus 4.5 <noreply@anthropic.com>
```

**Types**: `feat`, `fix`, `refactor`, `test`, `docs`, `chore`

**Scopes for this feature**: `workflows`, `chatbot`, `ui`, `api`

### Branch Naming

```
feat/workflows-t2-repository
feat/workflows-t8-matcher
feat/workflows-t17-list-page
fix/workflows-cache-invalidation
```

### PR Size Guidelines

| Size | Lines Changed | Review Time |
|------|---------------|-------------|
| Small | < 200 | Quick review |
| Medium | 200-500 | Standard review |
| Large | 500+ | Consider splitting |

Tasks from the spec are already scoped to be reasonable PR sizes (most are 100-300 lines).

### Linking to Spec Tasks

Always reference the task ID from the spec in your PR:

- "Implements T8 from the chatbot workflows spec"
- "Part of T20 (node config panels) - this PR adds the Message node config"

### Review Checklist

- [ ] Tests added/updated
- [ ] No console.logs or debug code
- [ ] Error handling in place
- [ ] Security considerations addressed (see spec)
- [ ] Performance targets met (see spec)
- [ ] Documentation updated if needed
