---
name: system-check-flow
description: Guide for checking entire system (Python Parser → PHP Code → Data Structures) before making changes
---

# System Check Flow

This skill guides you through checking the entire system before making changes for research code.

## When to Use

Use this skill when:
- Changing data structures or validation rules
- Adding new parsing patterns
- Modifying AST node types
- Updating PHP code analysis logic
- Any change that touches multiple layers

## The Problem

**Failure to check entire system results in:**
- Parser accepts PHP code but AST node doesn't match
- AST node defined but PHP code doesn't parse correctly
- Data inconsistency between parsing and analysis
- Runtime errors that could have been prevented

## The Solution: Check All Three Layers

### 1. Python Parser Check

**What to look for:**
- Parser functions that process PHP code
- AST node definitions
- Type annotations for AST nodes
- Parsing logic and validation

**Tools to use:**
```bash
# Find all occurrences in parser
grep_search -r "parse_php" src/

# Check AST node definitions
grep_search -r "class.*Node" src/

# Find in parsing logic
grep_search -r "def.*parse" src/
```

**Example - PHP Function Parsing:**
```python
# src/stage1_ast/php_parser.py
def parse_function(node: ast.FunctionDef) -> FunctionNode:
    # ← Parser logic
    if not node.name:
        raise ValueError("Function name required")
    return FunctionNode(name=node.name)
```

### 2. PHP Code Check

**What to look for:**
- PHP code samples being parsed
- Test cases for parsing
- Expected AST structure
- PHP syntax patterns

**Tools to use:**
```bash
# Find PHP test files
find dataset/ -name "*.php"

# Check parsing examples
grep_search -r "function.*{" dataset/
```

**Example - PHP Function Code:**
```php
// dataset/bagisto/app/Services/OrderService.php
public function createOrder($data) {
    // ← PHP code to parse
    return $order;
}
```

### 3. Data Structure Check

**What to look for:**
- AST node class definitions
- Data model classes
- Type hints and annotations
- Serialization/deserialization logic

**Tools to use:**
```bash
# Find data models
grep_search -r "dataclass" src/
grep_search -r "class.*Model" src/

# Check type definitions
grep_search -r "from typing import" src/
```

**Example - AST Node Definition:**
```python
# src/stage1_ast/ast_nodes.py
@dataclass
class FunctionNode:
    name: str
    parameters: List[ParameterNode]
    body: List[StatementNode]
```

## The Full Flow

### Step 1: Identify the Change

Example: "Add support for PHP 8.0 named parameters in function calls"

**Change:** Parse and represent named parameters in AST

### Step 2: Search ALL Occurrences in Python Parser

```bash
grep_search -r "parse_function" src/
grep_search -r "FunctionNode" src/
```

**Found:**
- `src/stage1_ast/php_parser.py` - Function parsing logic
- `src/stage1_ast/ast_nodes.py` - FunctionNode definition

**Action needed:**
- Add named parameter parsing to parser
- Update FunctionNode to include named parameters

### Step 3: Search ALL Occurrences in PHP Code

```bash
find dataset/ -name "*.php" -exec grep -l "function" {} \;
```

**Found:**
- Various PHP files with function calls
- Need test cases with named parameters

**Action needed:**
- Add PHP test cases with named parameters
- Verify parser handles them correctly

### Step 4: Search ALL Occurrences in Data Structures

```bash
grep_search -r "class.*Node" src/
grep_search -r "dataclass" src/
```

**Found:**
- AST node definitions in `ast_nodes.py`
- ParameterNode class

**Action needed:**
- Add `is_named` field to ParameterNode
- Update type hints

### Step 5: Update ALL Layers Consistently

**Python Parser:**
```python
def parse_function_call(node: ast.Call) -> FunctionCallNode:
    # ← Add named parameter parsing
    named_args = [arg for arg in node.keywords]
    return FunctionCallNode(
        name=node.func.id,
        named_parameters=named_args
    )
```

**Data Structure:**
```python
@dataclass
class ParameterNode:
    name: str
    is_named: bool = False  # ← Added field
```

**PHP Test Case:**
```php
// dataset/test_named_params.php
function greet($name, $age) {
    return "Hello $name, age $age";
}

greet(name: "John", age: 30);  // ← Named parameters
```

### Step 6: Test the Entire Flow

1. **Parser test:**
   - Run parser on test PHP file
   - Verify AST includes named parameters
   - Check type annotations

2. **Data structure test:**
   - Verify ParameterNode has is_named field
   - Check serialization works

3. **Integration test:**
   - Parse full PHP file
   - Verify complete AST structure
   - Run mypy type check

## Checklist

Before making ANY change that touches data:

- [ ] Identified the change being made
- [ ] Searched ALL occurrences in Python parser
- [ ] Searched ALL occurrences in PHP code
- [ ] Searched ALL occurrences in data structures
- [ ] Updated ALL layers consistently
- [ ] Added test cases if needed
- [ ] Tested entire flow from parser → data structure
- [ ] Type check passes (mypy)
- [ ] Code style passes (black)

## Common Mistakes

### ❌ Only updating parser
```python
# Parser handles named parameters
def parse_function_call(node):
    named_args = node.keywords

# But data structure doesn't support it
@dataclass
class ParameterNode:
    name: str
    # Missing is_named field!
```

### ❌ Only updating data structure
```python
# Data structure has is_named
@dataclass
class ParameterNode:
    is_named: bool

# But parser doesn't set it
def parse_function_call(node):
    # Missing named parameter logic
    return ParameterNode(name="arg")
```

### ❌ Forgetting type hints
```python
# Added new field but no type hint
@dataclass
class ParameterNode:
    is_named  # ← Missing type annotation

# mypy will fail!
```

## Summary

**Always follow this flow:**
1. Identify the change being made
2. Search for ALL occurrences in Python parser
3. Search for ALL occurrences in PHP code
4. Search for ALL occurrences in data structures
5. Update ALL layers consistently
6. Add test cases if needed
7. Test the entire flow from parser → data structure
8. Verify type check passes (mypy)

**Remember:** A change is not complete until ALL layers are updated and tested.
