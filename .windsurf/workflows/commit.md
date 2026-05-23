---
description: Commit changes with descriptive messages for research project
---

# Commit Workflow

This workflow commits changes with descriptive messages for the research project.

## When to Use

Use this workflow when:
- You have completed a task and want to commit changes
- You need to commit documentation updates
- You want to commit refactoring or code improvements

## Prerequisites

- Changes should be tested and working
- Type check should pass (mypy for Python)
- Code style should pass (black for Python, PSR-12 for PHP)

## Step 1: Type Check Before Commit

Before committing, run type check as per `critical-rules.md`:

```bash
source venv/bin/activate && mypy src/
```

Fix ALL type errors before committing. See `critical-rules.md` for type check requirements.

## Step 2: Code Style Check

Check code style:

```bash
# Python
source venv/bin/activate && black src/
source venv/bin/activate && flake8 src/

# PHP (manual check for PSR-12)
# Ensure 4 spaces indentation, camelCase methods, PascalCase classes
```

## Step 3: Stage Changed Files

Stage only the files you modified/added:

```bash
git add <file-path-1>
git add <file-path-2>
git add <file-path-3>
```

Replace `<file-path>` with the actual paths of the files you changed.

## Step 4: Commit with Descriptive Message

Commit changes with the following format:

**Format:**
```
<type>: <brief description in one line>
```

**Commit types:**
- `feat`: New feature or functionality
- `fix`: Bug fix
- `refactor`: Code refactoring without changing functionality
- `docs`: Documentation changes
- `chore`: Maintenance tasks, config changes
- `test`: Adding or updating tests
- `experiment`: Research experiment or trial implementation

**Examples:**
- `feat: add PHP class parsing support`
- `fix: handle default parameter values in function parsing`
- `refactor: simplify AST node structure`
- `docs: update literature review with new papers`
- `chore: update mypy configuration`
- `test: add test cases for PHP 8.0 named parameters`
- `experiment: try alternative approach for parsing Laravel routes`

**For research experiments:**
Use descriptive branch names and commit messages:
```bash
git checkout -b experiment/php-ast-parser-v2
git commit -m "experiment: implement PHP AST parser version 2"
```

**For documentation/refactoring:**
Push directly to main/develop:
```bash
git checkout main
git commit -m "docs: update README with setup instructions"
```

## Step 5: Push Changes

After committing, push to remote:

```bash
# For feature/experiment branch
git push origin <branch-name>

# For main/develop
git push origin main
# or
git push origin develop
```

**IMPORTANT**: Ask user before pushing. Let user review commit message first.

## Commit Strategy

When making multiple related changes, split them into logical commits:

**Example: Updating .windsurf configuration for research project**

1. **Commit: Update rules** - Update critical-rules.md and workflow-principles.md
2. **Commit: Update skills** - Update system-check-flow and task-planner
3. **Commit: Remove irrelevant skills** - Remove React/Node.js/Plane skills
4. **Commit: Remove irrelevant workflows** - Remove Plane/PR/commit workflows
5. **Commit: Update remaining workflows** - Update debug and review
6. **Commit: Add commit workflow** - Add commit workflow back

**Guidelines for splitting commits:**
- Group related changes together
- Separate deletions from additions
- Separate documentation from code
- Each commit should be self-contained and testable
- Avoid mixing different types of changes in one commit

## Notes

- Write descriptive commit messages that explain WHAT and WHY
- Keep commit messages in English for consistency
- Use present tense ("add" not "added")
- For research experiments, use `experiment:` prefix
- For documentation, use `docs:` prefix
- Never commit code with type errors
- Never commit code with style violations
- Split large changes into multiple logical commits
