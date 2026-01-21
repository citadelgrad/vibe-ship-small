## Summary

<!-- Brief description of what this PR does (2-3 sentences max) -->

## Type of Change

- [ ] Bug fix (non-breaking change that fixes an issue)
- [ ] New feature (non-breaking change that adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to change)
- [ ] Refactor (code change that neither fixes a bug nor adds a feature)
- [ ] Documentation update
- [ ] Configuration change

## Spec Reference

<!-- Link to the technical spec for feature work. Required for feature branches. -->

**Spec**: `/docs/specs/[feature-name].md`
**Task**: Completes task [T#] from the spec

## Changes Made

<!-- Bullet list of specific changes -->

-
-
-

## Architecture Changes

<!-- If this PR changes system architecture, include updated C4 diagram -->

<details>
<summary>C4 Diagram (click to expand)</summary>

```mermaid
C4Container
    title [Diagram Title]

    %% Add your diagram here
```

</details>

## Screenshots/Recordings

<!-- For UI changes, add before/after screenshots or recordings -->

| Before | After |
|--------|-------|
| [image] | [image] |

## Testing

### Automated Tests
- [ ] Unit tests added/updated
- [ ] Integration tests added/updated
- [ ] All existing tests pass

### Manual Testing
<!-- Steps to manually verify this change -->

1.
2.
3.

## Checklist

### Size & Scope
- [ ] PR is ≤ 400 lines (excluding generated files, tests, and snapshots)
- [ ] PR addresses a single concern (not mixing features/refactors/fixes)
- [ ] If > 400 lines, tech lead has approved with justification: [link to approval]

### Quality
- [ ] Self-review completed
- [ ] No console.logs, debuggers, or commented-out code
- [ ] Error handling is appropriate
- [ ] No new security vulnerabilities introduced

### Documentation
- [ ] Code comments added for non-obvious logic
- [ ] README updated (if applicable)
- [ ] API documentation updated (if applicable)

### Database
- [ ] Migration is backward compatible
- [ ] Rollback migration tested
- [ ] No N+1 queries introduced

## Deployment Notes

<!-- Any special instructions for deployment -->

- [ ] Feature flag required: `flag_name`
- [ ] Environment variables added: [list]
- [ ] Database migration required
- [ ] Cache invalidation needed

## Related Issues

<!-- Link to Jira tickets, GitHub issues, or related PRs -->

- Closes [JIRA-XXX]
- Related to #[PR number]
