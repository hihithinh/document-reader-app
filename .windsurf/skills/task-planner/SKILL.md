# Task Planner Skill

## When to Use

Use this skill when:
- User asks to create a task checklist
- User wants to break down a complex task into implementation steps
- User needs to plan the implementation order for subtasks
- User wants to track progress across multiple related tasks

## Prerequisites

- Task description or requirements must be provided
- No external dependencies required

## Steps

### 1. Understand the Task

Read the task description and identify:
- Main objective/goal
- Key requirements
- Constraints or limitations
- Expected outcome

### 2. Break Down into Subtasks

Divide the main task into smaller, actionable subtasks:
- Group related tasks together
- Identify dependencies between tasks
- Determine logical implementation order

### 3. Create Checklist File

Create a checklist file in `.windsurf/tasks/<TASK-NAME>/checklist.md` with the following structure:

```markdown
# <TASK-NAME>: <Task Title>

## Overview
<Summary of the overall task>

## Subtasks

### <SUBTASK-1>: <Subtask Title>
**Status:** Pending | In Progress | Completed
**Priority:** High | Medium | Low

**Requirements:**
- <Requirement 1>
- <Requirement 2>

**Implementation Steps:**
- [ ] <Step 1>
  - <Sub-step 1.1>
  - <Sub-step 1.2>
- [ ] <Step 2>
  - <Sub-step 2.1>

**Files to Modify:**
- `<file-path-1>`
- `<file-path-2>`

---

### <SUBTASK-2>: <Subtask Title>
**Status:** Pending | In Progress | Completed
**Priority:** High | Medium | Low

**Requirements:**
- <Requirement 1>

**Implementation Steps:**
- [ ] <Step 1>
- [ ] <Step 2>

**Files to Modify:**
- `<file-path-1>`

---

## Implementation Order

1. **<SUBTASK-1>** - <Reason for this order>
2. **<SUBTASK-2>** - <Reason for this order>

## Testing Checklist

### <SUBTASK-1>
- [ ] <Test case 1>
- [ ] <Test case 2>

### <SUBTASK-2>
- [ ] <Test case 1>

## Notes

- <Important note 1>
- <Important note 2>
```

### 4. Break Down Requirements into Steps

For each requirement, break it down into:
- Python parser changes (parsing logic, AST nodes)
- PHP code changes (test cases, samples)
- Data structure changes (models, type hints)
- Documentation changes (README, literature review)

### 5. Identify Files to Modify

For each step, identify the specific files that need to be modified:
- Python: Parser modules, AST node definitions, test files
- PHP: Test cases, sample code in dataset/
- Documentation: Implementation docs, literature review

### 6. Determine Implementation Order

Based on dependencies:
- Foundation features first (data structures, AST nodes)
- Parser logic second (parsing implementation)
- Test cases third (PHP samples)
- Documentation last

### 7. Add Testing Checklist

For each subtask, add test cases:
- Happy path scenarios
- Edge cases
- Error scenarios
- Type checking (mypy)

### 8. Add Notes

Include important notes:
- Existing AST nodes or patterns
- Known dependencies or constraints
- Potential risks or considerations

## Example

**Task:** Implement PHP Class Parsing

**Checklist Structure:**
```markdown
# php-class-parsing: PHP Class Parsing Implementation

## Overview
Implement parsing for PHP classes including properties, methods, and inheritance.

## Subtasks

### class-ast-nodes: Class AST Node Definitions
**Status:** Pending
**Priority:** High

**Requirements:**
- Define ClassNode dataclass
- Define PropertyNode dataclass
- Define MethodNode dataclass
- Add type hints

**Implementation Steps:**
- [ ] Python: Create ClassNode in ast_nodes.py
  - Add name, properties, methods, parent_class fields
  - Add type hints for all fields
- [ ] Python: Create PropertyNode in ast_nodes.py
  - Add name, visibility, default_value fields
- [ ] Python: Create MethodNode in ast_nodes.py
  - Add name, parameters, body, visibility fields

**Files to Modify:**
- src/stage1_ast/ast_nodes.py

---

### class-parser: Class Parsing Logic
**Status:** Pending
**Priority:** High

**Requirements:**
- Parse class declarations
- Parse class properties
- Parse class methods
- Handle inheritance

**Implementation Steps:**
- [ ] Python: Add parse_class function to php_parser.py
  - Extract class name
  - Parse properties
  - Parse methods
  - Handle extends keyword
- [ ] Python: Add parse_property function
- [ ] Python: Add parse_method function

**Files to Modify:**
- src/stage1_ast/php_parser.py

---

### class-test-cases: PHP Class Test Cases
**Status:** Pending
**Priority:** Medium

**Requirements:**
- Add PHP class samples
- Test inheritance
- Test visibility modifiers

**Implementation Steps:**
- [ ] PHP: Create test_class.php in dataset/
  - Add simple class
  - Add class with properties
  - Add class with methods
  - Add class with inheritance
- [ ] Python: Add test cases in test_parser.py

**Files to Modify:**
- dataset/test_class.php
- tests/test_parser.py

---

## Implementation Order

1. **class-ast-nodes** - Data structures needed first
2. **class-parser** - Parser logic depends on AST nodes
3. **class-test-cases** - Test cases depend on parser

## Testing Checklist

### class-ast-nodes
- [ ] mypy type check passes
- [ ] All fields have type hints
- [ ] Dataclass validation works

### class-parser
- [ ] Parses simple class correctly
- [ ] Parses class with properties
- [ ] Parses class with methods
- [ ] Handles inheritance
- [ ] mypy type check passes

### class-test-cases
- [ ] Parser handles all test cases
- [ ] AST structure is correct
- [ ] No parsing errors

## Notes

- Follow existing AST node patterns
- Use dataclass for all node types
- Type hints are mandatory (mypy check)
- Test with real PHP code from Bagisto dataset
```

## Output

Present the checklist file path to the user:
```
Created checklist: .windsurf/tasks/<TASK-NAME>/checklist.md
```

## Notes

- Use markdown format for the checklist
- Include Python, PHP, and documentation steps
- Add type hints for all Python code
- Include file paths for all modifications
- Add testing checklist for each subtask
- Keep the structure generic and reusable
