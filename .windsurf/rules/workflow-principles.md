---
trigger: always_on
---

# Workflow Principles (Always-on)

These principles guide how you work on tasks. Follow them to maintain quality and efficiency.

## 1. Plan Mode Default

**Enter plan mode for ANY non-trivial task (3+ steps or architectural decisions)**

- Use `todo_list` tool to create and track plan
- Write detailed specs upfront to reduce ambiguity
- Break down into concrete, actionable steps
- If something goes sideways, STOP and re-plan immediately - don't keep pushing

**Example:**
```
Task: Implement PHP AST parser for Laravel framework
Plan:
- [ ] Research existing PHP parsers
- [ ] Design parser architecture
- [ ] Implement basic AST parsing
- [ ] Add Laravel-specific patterns
- [ ] Test with sample Laravel code
- [ ] Type check with mypy
- [ ] Document usage
```

## 2. Research Strategy

**Use code exploration tools liberally to understand context**

- Use `grep_search` to find all occurrences of a symbol
- Read related files to understand full context
- Never make assumptions - verify everything

**Pattern:**
1. Search for existing implementations
2. Read related code
3. Understand patterns
4. Follow existing patterns

## 3. Self-Improvement Loop

**After ANY correction from user: learn from it**

- Update `tasks/lessons.md` with the mistake and lesson
- Write rules to prevent same mistake
- Review lessons at start of similar tasks
- Ruthlessly iterate until mistake rate drops

**Example entry in lessons.md:**
```markdown
## 2026-05-23: Assumed PHP function exists
**Mistake:** Used `parse_php_code()` without checking if it exists
**Root Cause:** Didn't grep_search for function before using
**Lesson:** ALWAYS verify function exists before using it
**Rule:** Use grep_search to check function signature first
```

## 4. Verification Before Done

**Never mark a task complete without proving it works**

- Run type check: `source venv/bin/activate && mypy src/`
- Test the change (manual or automated)
- Check logs for errors
- Ask yourself: "Would this pass academic review?"
- Demonstrate correctness to user

**Checklist:**
- [ ] Type check passes (mypy for Python)
- [ ] Code style passes (black for Python, PSR-12 for PHP)
- [ ] Manual test successful
- [ ] Follows existing patterns
- [ ] No regressions introduced

## 5. Demand Elegance (Balanced)

**For non-trivial changes: pause and ask "is there a more elegant way?"**

- If a fix feels hacky: implement the elegant solution
- Consider: "Knowing everything I know now, what's the best approach?"
- Challenge your own work before presenting it
- **BUT**: Skip this for simple, obvious fixes - don't over-engineer

**When to apply:**
- ✅ Architectural changes
- ✅ New research algorithms
- ✅ Complex bug fixes
- ❌ Simple typo fixes
- ❌ Obvious one-line changes

## 6. Autonomous Execution

**When given a task: just do it. Don't ask for hand-holding**

- Bug report? Fix it. Point at logs/errors, then resolve
- Type error? Fix it, don't ask what to do
- Zero context switching required from user

**Pattern:**
1. Understand the problem
2. Research the solution
3. Implement the fix
4. Verify it works
5. Report completion

**Exceptions (when to ask):**
- Ambiguous requirements
- Multiple valid approaches (architectural decision)
- Missing information that user must provide
- Breaking changes that need approval
