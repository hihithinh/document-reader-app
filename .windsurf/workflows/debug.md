---
description: Debug workflow using trial-and-error approach
---

# Debug Workflow

This workflow provides a systematic approach to debugging issues using trial-and-error methodology.

## Prerequisites
- Understand the issue description
- Identify affected files/components
- Have access to the codebase

## Steps

### 1. Understand the Problem
- Read the issue description carefully
- Identify expected behavior vs actual behavior
- Note any error messages or logs provided

### 2. Compare with Working Components
- Find similar components/features that work correctly
- Compare code differences between working and broken components
- Look for patterns in the working code that might be missing in the broken code

### 3. Debug Layer by Layer with Logging
Add print statements at each layer to trace data flow:

**Layer 1: Input to functions**
- Log parameters when functions are called
- Verify input data is correct

**Layer 2: State updates**
- Log state values before and after changes
- Check if state updates are applied correctly

**Layer 3: Data processing**
- Log intermediate results
- Verify transformations are correct

**Layer 4: Output/return values**
- Log return values
- Verify final output matches expectations

### 4. Categorize the Issue
Based on logging results, categorize the problem:

**All data incorrect**
- Likely parsing logic or data structure issue
- Check parser implementation, AST node definitions

**Some data correct, some incorrect**
- Specific logic issue (parsing rule, transformation)
- Focus on the logic affecting the incorrect data

**Type A data incorrect, Type B correct**
- Logic specific to Type A
- Check type-specific handlers/transformations

### 5. Avoid Common Pitfalls
- **Type hints missing**: Add type hints to catch errors early with mypy
- **Dataclass fields mismatched**: Verify all fields match between definition and usage
- **Parser returns None**: Check if parser handles all PHP syntax variations
- **AST node not initialized**: Verify all required fields are set
- **List vs single value**: Check if function expects list but receives single value

### 6. Trial-and-Error Approach
When stuck:
1. Make one small change
2. Test
3. If it works, commit and continue
4. If it doesn't work, revert and try a different approach
5. Don't make multiple changes at once

### 7. Communication with User
- If 15 minutes without progress → Ask user for direction
- If user requests revert → Revert all changes immediately
- Explain your approach before making large changes
- Get approval before implementing complex solutions

### 8. Document the Root Cause
When the issue is fixed:
- Document the actual root cause
- Note what didn't work and why
- Save the working solution for future reference

## Example: PHP Function Parsing Bug

### Problem
Parser fails to parse PHP functions with default parameter values.

### Comparison
Simple functions without defaults parse correctly, functions with defaults don't.

### Logging Results
- parse_function: receives function node with defaults
- ParameterNode creation: default_value field is None
- Expected: default_value should contain the default expression

### Root Cause
Parser didn't extract default values from AST node. Only extracted parameter name and type.

### Solution
Added logic to extract default values from ast.Constant or ast.Name nodes in parse_parameter function.

## Notes

- Always run mypy after changes
- Remove debug logging before final commit
- Use type checking to catch errors early
- Test with real PHP code from dataset
