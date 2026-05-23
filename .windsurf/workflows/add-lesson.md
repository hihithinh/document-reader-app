---
description: Add a lesson learned to tasks/lessons.md after making a mistake
---

# Add Lesson Workflow

This workflow adds a new lesson to `tasks/lessons.md` after AI makes a mistake or receives correction from user.

## When to Use

Use this workflow when:
- User corrects AI's mistake
- AI realizes it made an error
- User points out a better approach
- AI wants to document a learning

## Steps

### 1. Identify the Mistake

What went wrong?
- What did AI do incorrectly?
- What was the user's correction?
- What should have been done instead?

### 2. Analyze Root Cause

Why did it happen?
- Missing knowledge?
- Wrong assumption?
- Didn't follow existing rules?
- Misunderstood requirements?

### 3. Extract the Lesson

What to do differently next time?
- Specific action to take
- Rule to follow
- Check to perform
- Tool to use

### 4. Formulate the Rule

General principle to prevent recurrence:
- If X situation, then Y action
- Always check Z before doing W
- Never assume A, always verify B

### 5. Add to lessons.md

Add entry in this format:

```markdown
## YYYY-MM-DD: Brief description
**Mistake:** What went wrong
**Root Cause:** Why it happened
**Lesson:** What to do differently
**Rule:** Principle to follow
```

### 6. Update Related Rules (if needed)

If the lesson reveals a gap in critical-rules.md or workflow-principles.md:
- Consider adding to critical-rules.md if it's a MUST-follow rule
- Consider adding to workflow-principles.md if it's a best practice
- Or keep in lessons.md if it's context-specific

## Example

**User correction:** "You forgot to add i18n translation for the error message"

**Lesson entry:**
```markdown
## 2026-05-07: Missing i18n for error message
**Mistake:** Added hardcoded error message "Invalid input" instead of using t()
**Root Cause:** Focused on logic, forgot to check critical-rules.md for i18n requirement
**Lesson:** ALWAYS check critical-rules.md before writing any user-facing text
**Rule:** Already in critical-rules.md - need to review rules before starting each task
```

## Notes

- Add lessons immediately after correction
- Be specific about what went wrong
- Focus on actionable lessons
- Review lessons.md at start of similar tasks
- Update critical-rules.md if pattern repeats 3+ times
