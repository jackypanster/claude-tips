# Development Guidelines

## Philosophy

### Core Beliefs

- **Incremental progress over big bangs** - Small changes that compile and pass tests
- **Learning from existing code** - Study and plan before implementing
- **Pragmatic over dogmatic** - Adapt to project reality
- **Clear intent over clever code** - Be boring and obvious

### Simplicity Means

- Single responsibility per function/class
- Avoid premature abstractions
- No clever tricks - choose the boring solution
- If you need to explain it, it's too complex

## Process

### 1. Planning & Staging

Break complex work into 3-5 stages. Document in `IMPLEMENTATION_PLAN.md`:

```markdown
## Stage N: [Name]

**Goal**: [Specific deliverable]
**Success Criteria**: [Testable outcomes]
**Tests**: [Specific test cases]
**Status**: [Not Started|In Progress|Complete]
**Time Estimate**: [Rough estimate]
**Dependencies**: [What this stage depends on]
```

- Update status as you progress
- Remove file when all stages are done
- **Review plan with team** if it affects shared components

### 2. Implementation Flow

1. **Understand** - Study existing patterns in codebase
2. **Plan** - Sketch the approach, identify edge cases
3. **Test** - Write test first (red)
4. **Implement** - Minimal code to pass (green)
5. **Refactor** - Clean up with tests passing
6. **Review** - Self-review before commit
7. **Commit** - With clear message linking to plan

### 3. When Stuck (After 3 Attempts)

**CRITICAL**: Maximum 3 attempts per issue, then STOP.

1. **Document what failed**:
   - What you tried
   - Specific error messages
   - Why you think it failed
   - **Time spent on each attempt**

2. **Research alternatives**:
   - Find 2-3 similar implementations
   - Note different approaches used
   - **Check project documentation/wiki**

3. **Question fundamentals**:
   - Is this the right abstraction level?
   - Can this be split into smaller problems?
   - Is there a simpler approach entirely?
   - **Is this even necessary?**

4. **Seek help**:
   - Ask team member familiar with the area
   - Create detailed issue with research
   - **Don't struggle alone beyond 3 attempts**

## Technical Standards

### Architecture Principles

- **Composition over inheritance** - Use dependency injection
- **Interfaces over singletons** - Enable testing and flexibility
- **Explicit over implicit** - Clear data flow and dependencies
- **Test-driven when possible** - Never disable tests, fix them
- **Configuration over hardcoding** - Use environment variables/config files

### Code Quality

- **Every commit must**:
  - Compile successfully
  - Pass all existing tests
  - Include tests for new functionality
  - Follow project formatting/linting
  - **Not break existing functionality**

- **Before committing**:
  - Run formatters/linters
  - Self-review changes
  - Ensure commit message explains "why"
  - **Check git diff for unintended changes**

### Error Handling

- Fail fast with descriptive messages
- Include context for debugging
- Handle errors at appropriate level
- Never silently swallow exceptions
- **Log errors with sufficient detail for debugging**

### Security Considerations

- **Never commit**:
  - API keys, passwords, tokens
  - Personal information
  - Development secrets to production config
- **Always**:
  - Validate user inputs
  - Use parameterized queries
  - Follow least privilege principle

## Decision Framework

When multiple valid approaches exist, choose based on:

1. **Testability** - Can I easily test this?
2. **Readability** - Will someone understand this in 6 months?
3. **Consistency** - Does this match project patterns?
4. **Simplicity** - Is this the simplest solution that works?
5. **Reversibility** - How hard to change later?
6. **Performance** - Does this meet performance requirements?
7. **Security** - Are there any security implications?

## Project Integration

### Learning the Codebase

- Find 3 similar features/components
- Identify common patterns and conventions
- Use same libraries/utilities when possible
- Follow existing test patterns
- **Read project README and contributing guidelines**
- **Understand the deployment process**

### Tooling

- Use project's existing build system
- Use project's test framework
- Use project's formatter/linter settings
- Don't introduce new tools without strong justification
- **Keep dependencies up to date (security)**

### Communication

- **Update team on significant changes**
- **Document breaking changes clearly**
- **Use clear, descriptive commit messages**
- **Link commits to issues/tickets when applicable**

## Quality Gates

### Definition of Done

- [ ] Tests written and passing
- [ ] Code follows project conventions
- [ ] No linter/formatter warnings
- [ ] Commit messages are clear
- [ ] Implementation matches plan
- [ ] No TODOs without issue numbers
- [ ] **Performance benchmarks met (if applicable)**
- [ ] **Documentation updated (if public API changed)**
- [ ] **Security review completed (if handling sensitive data)**

### Test Guidelines

- Test behavior, not implementation
- One assertion per test when possible
- Clear test names describing scenario
- Use existing test utilities/helpers
- Tests should be deterministic
- **Test edge cases and error conditions**
- **Maintain reasonable test coverage**

### Performance Guidelines

- **Profile before optimizing**
- **Set performance budgets for critical paths**
- **Monitor memory usage in long-running processes**
- **Use appropriate data structures for the use case**

## Emergency Procedures

### Production Issues

1. **Immediate response**:
   - Assess impact and severity
   - Implement quick fix or rollback
   - Communicate status to stakeholders

2. **Follow-up**:
   - Root cause analysis
   - Implement proper fix
   - Update monitoring/alerting
   - Document lessons learned

### Recovery from Mistakes

- **Git mistakes**: Use `git reflog` to recover
- **Database mistakes**: Use backups, never run destructive queries in production
- **Deployment mistakes**: Have rollback plan ready

## Important Reminders

**NEVER**:
- Use `--no-verify` to bypass commit hooks
- Disable tests instead of fixing them
- Commit code that doesn't compile
- Make assumptions - verify with existing code
- **Push directly to main/master without review**
- **Commit sensitive information**

**ALWAYS**:
- Commit working code incrementally
- Update plan documentation as you go
- Learn from existing implementations
- Stop after 3 failed attempts and reassess
- **Run tests locally before pushing**
- **Review your own code before requesting review**
- **Keep commits atomic and focused**

## Context-Specific Notes

*This section should be customized per project:*

- **Tech stack**: [Framework, language, database]
- **Key patterns**: [Specific patterns used in this project]
- **Common gotchas**: [Project-specific issues to watch for]
- **Deployment process**: [How to deploy safely]
- **Team contacts**: [Who to ask for different areas]
