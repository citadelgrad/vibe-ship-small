# PRD: Custom Chatbot Workflows

> **Status**: Draft
> **Author**: [PM Name]
> **Last Updated**: 2026-01-21

---

## Problem Statement

### The Pain Point
Users need to customize how the chatbot responds to different scenarios, but currently all conversation logic is hardcoded. This forces engineering involvement for every business logic change, creating a bottleneck and slowing time-to-market for new conversation patterns.

### Root Cause Analysis (5 Whys)
1. Why can't users customize chatbot behavior? → Conversation logic is in code
2. Why is it in code? → No visual workflow system exists
3. Why wasn't one built? → Initial MVP prioritized speed over flexibility
4. Why does this matter now? → Customer requests require frequent logic changes
5. **Root cause** → Lack of user-configurable workflow system creates engineering dependency for business logic changes

---

## User Stories

### Primary User Story
> As a **conversation designer**, I want to **create and modify chatbot workflows visually**, so that I can **launch new conversation patterns without engineering support**.

### Additional User Stories
- As a conversation designer, I want to **test workflows before publishing**, so that I can validate behavior without affecting production users
- As a conversation designer, I want to **see which workflows are active**, so that I can understand current chatbot behavior
- As a conversation designer, I want to **duplicate existing workflows**, so that I can create variations without starting from scratch
- As an admin, I want to **control who can publish workflows**, so that I can prevent unauthorized changes to production

---

## Success Metrics

### Leading Indicators (Measurable Immediately)
| Metric | Current | Target | How to Measure |
|--------|---------|--------|----------------|
| Time to create new workflow | N/A (requires eng) | < 30 minutes | Track workflow creation timestamps |
| Workflows created per week | 0 | 5+ | Count in database |
| Engineering tickets for conv logic | ~10/sprint | < 2/sprint | Jira ticket audit |

### Lagging Indicators (Business Outcomes Over Time)
| Metric | Baseline | Target | Timeframe |
|--------|----------|--------|-----------|
| Time-to-market for new conv patterns | 2 weeks | 2 days | 3 months |
| Conversation designer satisfaction | TBD | > 4/5 | Survey at 1 month |

---

## Requirements

### Functional Requirements

**Workflow Creation**
1. Users shall create workflows using a visual node-based editor
2. Users shall define trigger conditions (e.g., intent match, keyword, time-based)
3. Users shall add action nodes (e.g., send message, collect input, call API, branch)
4. Users shall connect nodes to define conversation flow
5. Users shall save workflows as drafts without publishing

**Workflow Management**
6. Users shall view a list of all workflows with status (draft/active/archived)
7. Users shall duplicate existing workflows
8. Users shall archive workflows (soft delete)
9. Users shall search/filter workflows by name, status, trigger type

**Workflow Execution**
10. The system shall evaluate active workflows when conversations occur
11. The system shall execute the highest-priority matching workflow
12. The system shall log workflow execution for debugging

**Testing & Publishing**
13. Users shall test workflows in a sandbox environment
14. Users shall publish workflows to make them active
15. Users shall rollback to previous workflow versions

### Non-Functional Requirements

| Category | Requirement |
|----------|-------------|
| Performance | Workflow evaluation < 50ms at P95 (must not slow chatbot response) |
| Scalability | Support 500+ active workflows per tenant |
| Security | Role-based access: Editor (create/edit), Publisher (publish), Admin (all) |
| Reliability | Workflow execution must not crash chatbot on malformed workflow |
| Audit | All publish/unpublish actions logged with user and timestamp |

---

## Scope

### In Scope (MVP)
- Visual workflow editor (nodes: Message, Input, Condition, API Call)
- Workflow CRUD (create, read, update, archive)
- Basic trigger types: Intent match, Keyword contains
- Draft/Published states
- Workflow execution engine integrated with chatbot
- Basic test mode (simulate conversation)

### Out of Scope (Future Phases)
- **Version history / diff view** - Track later based on usage
- **Workflow analytics** - Separate initiative after MVP
- **Scheduled workflows** - Time-based triggers deferred
- **A/B testing workflows** - Requires experimentation platform
- **Import/export workflows** - Nice-to-have, not MVP
- **Collaborative editing** - Single editor at a time for MVP
- **Custom node types** - Predefined nodes only for MVP

---

## Dependencies

### External Dependencies
| Dependency | Owner | Status | Risk if Delayed |
|------------|-------|--------|-----------------|
| Intent recognition service | ML Team | Ready | Cannot implement intent triggers |

### Technical Dependencies
- Existing chatbot message handling pipeline (will integrate with)
- User authentication/authorization system (will use existing)

---

## Open Questions

> To discuss during grooming:

1. [ ] What's the priority order when multiple workflows match? (First match? Weighted? User-defined priority?)
2. [ ] Should we support "workflow chaining" (one workflow triggers another)?
3. [ ] How do we handle workflows that become invalid (e.g., reference deleted intent)?
4. [ ] Do we need workflow-level feature flags for gradual rollout?

---

## Appendix

### Competitive Analysis
| Product | Approach | Strengths | Weaknesses |
|---------|----------|-----------|------------|
| Dialogflow CX | Visual flow builder | Mature, well-documented | Complex, Google lock-in |
| Botpress | Node-based editor | Open source, flexible | Steep learning curve |
| Voiceflow | Drag-and-drop canvas | Designer-friendly | Limited API integration |

### Rough Wireframe Concept
```
┌─────────────────────────────────────────────────────────┐
│ Workflows                              [+ New Workflow] │
├─────────────────────────────────────────────────────────┤
│ Search... [________]  Filter: [All ▼]                   │
├─────────────────────────────────────────────────────────┤
│ ┌─────────────────────────────────────────────────────┐ │
│ │ Welcome Flow                    [Active] [Edit]     │ │
│ │ Trigger: Conversation Start                         │ │
│ └─────────────────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────────────────┐ │
│ │ FAQ Handler                     [Draft]  [Edit]     │ │
│ │ Trigger: Intent = "ask_faq"                         │ │
│ └─────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────┘
```
