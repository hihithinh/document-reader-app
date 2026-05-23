---
trigger: always_on
---

# Critical Rules (Always-on)

These rules MUST be followed for EVERY code change without exception.

## Function Verification (NEVER VIOLATE)

**CRITICAL RULE**: MUST verify that a function/method exists before using it.

Steps to follow:
1. Before using ANY function, use `grep_search` to check if it exists
2. Check the exact function signature and parameters
3. Never assume a function exists based on naming patterns
4. If function doesn't exist, find correct alternative or create it

**Examples:**
```python
# ❌ Wrong - assuming function exists
parser.parse_php_code(...)

# ✅ Correct - grep first, then use exact function
# grep_search for "parse_php_code"
# Found: parser.parse() - use this instead
parser.parse(...)
```

## Python Environment (NEVER VIOLATE)

**CRITICAL RULE**: Always activate virtual environment before running Python commands.

```bash
# Always activate venv before running Python commands
source venv/bin/activate

# Or use full command
source venv/bin/activate && python script.py
```

## Type Check (NEVER VIOLATE)

**CRITICAL RULE**: Type check MUST pass before commit (for Python).

- Run `mypy` before every commit for Python code
- Fix ALL type errors (no exceptions, even pre-existing ones)
- Never commit code with type errors
- Never push code with type errors

```bash
# Always run before commit
source venv/bin/activate && mypy src/
```

## Code Style (NEVER VIOLATE)

**CRITICAL RULE**: Follow PEP 8 for Python and PSR-12 for PHP.

**Python:**
- Use `black` for formatting
- Use `flake8` for linting
- Maximum line length: 88 characters (black default)

```bash
# Format Python code
source venv/bin/activate && black src/
# Lint Python code
source venv/bin/activate && flake8 src/
```

**PHP:**
- Follow PSR-12 coding standard
- Use 4 spaces for indentation
- Use camelCase for methods, PascalCase for classes

## Git Workflow (NEVER VIOLATE)

**CRITICAL RULE**: Use simple git workflow for research project.

- For research experiments: Create descriptive branch names
- For documentation/refactoring: Push directly to `main` or `develop`
- Always write descriptive commit messages

**Example:**
```bash
# Research experiment - create descriptive branch
git checkout -b experiment/php-ast-parser-v2
# make changes
git add .
git commit -m "experiment: implement PHP AST parser version 2"
git push origin experiment/php-ast-parser-v2

# Documentation - push directly to main
git checkout main
git pull origin main
# make changes
git add .
git commit -m "docs: update literature review with new papers"
git push origin main
```

## Task Scope (NEVER VIOLATE)

**CRITICAL RULE**: Chỉ làm những gì user yêu cầu. Không tự ý làm thêm, không đề xuất, không implement feature chưa được yêu cầu.

- ❌ KHÔNG BAO GIỜ tự ý làm việc mà không được yêu cầu
- ❌ KHÔNG BAO GIỜ commit, push, hoặc thay đổi mà không có sự chấp thuận rõ ràng
- ❌ KHÔNG BAO GIỜ tạo file, branch, hoặc workflows mà không được yêu cầu
- ❌ KHÔNG BAO GIỜ assume user muốn làm gì - phải hỏi trước
- ✅ Chỉ làm đúng những gì user yêu cầu
- ✅ Nếu không chắc, hãy hỏi để làm rõ
- ✅ Giữ nguyên scope của task, không làm "helpful extras"

**Khi push trực tiếp đến main/develop:**
- ✅ Refactoring không thay đổi functionality
- ✅ Cập nhật file cấu hình
- ✅ Cập nhật documentation
- ✅ Cập nhật dependencies
- ✅ Cải thiện tooling (workflows, skills, rules)
- ✅ Fix formatting/linting

**Khi tạo branch:**
- ✅ Thử nghiệm nghiên cứu mới
- ✅ Feature lớn cần nhiều bước
- ✅ Thay đổi có thể break code hiện tại
