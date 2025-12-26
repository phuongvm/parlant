# Task Completion Checklist for Parlant

## Before Starting Any Task

### 1. Environment Setup
- [ ] **Virtual environment activated**: `poetry shell` or use `poetry run`
- [ ] **Dependencies updated**: `poetry install` (if needed)
- [ ] **Environment variables set**: Required API keys (OPENAI_API_KEY, etc.)
- [ ] **Latest code pulled**: `git pull`

### 2. Branch Management
- [ ] **Create feature branch**: `git checkout -b feature/task-name`
- [ ] **Branch naming**: Use descriptive names (e.g., `feature/add-guideline-api`, `fix/agent-crash`)

## During Development

### 1. Code Quality Standards
- [ ] **Type hints**: All functions have proper type annotations
- [ ] **Docstrings**: Public functions and classes documented
- [ ] **Error handling**: Specific exceptions, no bare `except:`
- [ ] **Async patterns**: Proper use of async/await, context managers
- [ ] **Logging**: Structured logging with appropriate levels

### 2. Testing Requirements
- [ ] **Unit tests written**: For new functionality
- [ ] **Async tests**: Use `pytest-asyncio` for async code
- [ ] **Edge cases covered**: Test boundary conditions
- [ ] **Existing tests pass**: No broken tests
- [ ] **Test coverage maintained**: Aim for >80%

### 3. Code Style Compliance
- [ ] **Ruff formatting**: Code follows ruff.toml configuration
- [ ] **Line length**: Maximum 100 characters
- [ ] **Import order**: Standard lib → third-party → local
- [ ] **Naming conventions**: snake_case, PascalCase, UPPER_SNAKE_CASE

## Before Committing

### The Holy Trinity (MUST ALL PASS) ✅

#### 1. Tests Pass
```powershell
poetry run pytest --cov=src
```
- [ ] **All tests pass**: No failures or errors
- [ ] **Coverage maintained**: No significant drop in coverage
- [ ] **New tests added**: For new functionality

#### 2. Type Checking Passes
```powershell
poetry run mypy src tests
```
- [ ] **No type errors**: Strict mode compliance
- [ ] **Type hints complete**: All new functions typed
- [ ] **No `Any` abuse**: Use specific types

#### 3. Linting Passes
```powershell
poetry run ruff check --fix .
```
- [ ] **No lint errors**: After auto-fix
- [ ] **Code formatted**: `poetry run ruff format .`
- [ ] **Style consistent**: Follows project conventions

### Additional Checks
- [ ] **No debug code**: Remove print statements, debugger calls
- [ ] **No commented code**: Remove or properly document
- [ ] **No secrets**: No API keys, passwords in code
- [ ] **Dependencies updated**: If new packages added

## Documentation Updates

### Code Documentation
- [ ] **Docstrings updated**: For modified functions/classes
- [ ] **Comments reviewed**: Clear and necessary
- [ ] **Type hints accurate**: Reflect actual types

### Project Documentation
- [ ] **README.md**: Update if user-facing changes
- [ ] **CHANGELOG.md**: Document changes (if applicable)
- [ ] **Examples**: Update if SDK changes
- [ ] **API docs**: Update if API changes

## Git Commit Standards

### DCO Sign-Off (REQUIRED)
- [ ] **Git hooks configured**: `git config core.hookspath .githooks`
  OR
- [ ] **Manual sign-off**: Use `-s` flag: `git commit -s -m "message"`

### Commit Message Quality
- [ ] **Clear and descriptive**: What and why
- [ ] **Present tense**: "Add feature" not "Added feature"
- [ ] **Reference issues**: If applicable (e.g., "Fixes #123")
- [ ] **Breaking changes**: Clearly marked if any

### Commit Message Format
```
<type>: <description>

[optional body]

[optional footer]

Signed-off-by: Your Name <your.email@example.com>
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

## Before Creating Pull Request

### Code Review Preparation
- [ ] **Self-review code**: Read through all changes
- [ ] **Remove debug code**: Clean up temporary code
- [ ] **Squash commits**: If multiple WIP commits
- [ ] **Rebase on develop**: `git rebase origin/develop`

### PR Description
- [ ] **Clear title**: Summarize the change
- [ ] **Detailed description**: What, why, how
- [ ] **Link issues**: Reference related issues
- [ ] **Test coverage**: Explain testing approach
- [ ] **Breaking changes**: Highlight if any
- [ ] **Screenshots**: If UI changes

### Quality Checks
```powershell
# Run full QA suite
poetry run pytest --cov=src && `
poetry run mypy src tests && `
poetry run ruff check .
```
- [ ] **All checks pass**: Tests, types, linting
- [ ] **No warnings**: Address all warnings
- [ ] **Coverage report**: Verify coverage

## After PR Approval

### Pre-Merge Checks
- [ ] **Conflicts resolved**: Rebase/merge conflicts fixed
- [ ] **CI passes**: All GitHub Actions green
- [ ] **Reviews addressed**: All comments resolved
- [ ] **Final QA**: Run tests one more time

### Post-Merge
- [ ] **Delete feature branch**: Clean up local and remote
- [ ] **Pull latest**: Update local develop branch
- [ ] **Monitor**: Watch for any issues in production/staging

## Special Workflows

### Adding New LLM Provider

- [ ] **Add optional dependency**: In `pyproject.toml` under `[tool.poetry.dependencies]`
- [ ] **Create extra**: In `[tool.poetry.extras]`
- [ ] **Implement adapter**: In `src/parlant/adapters/`
- [ ] **Add tests**: Provider-specific tests
- [ ] **Update documentation**: README and provider docs
- [ ] **Test installation**: `poetry install --extras "provider-name"`

### Adding New API Endpoint

- [ ] **Define route**: In `src/parlant/api/`
- [ ] **Add validation**: Pydantic models
- [ ] **Implement logic**: In `src/parlant/core/`
- [ ] **Add tests**: Unit and integration tests
- [ ] **Update OpenAPI spec**: If using code generation
- [ ] **Test manually**: With parlant-server running

### Modifying Guidelines System

- [ ] **Update matching engine**: Core logic in `src/parlant/core/`
- [ ] **Add tests**: Extensive guideline matching tests
- [ ] **Test explainability**: Ensure debug output works
- [ ] **Performance test**: Check impact on matching speed
- [ ] **Update examples**: Show new guideline features

### Database Schema Changes

- [ ] **Create migration**: Using `parlant-prepare-migration`
- [ ] **Test migration**: Up and down
- [ ] **Update models**: Pydantic models and types
- [ ] **Backward compatibility**: Consider existing data
- [ ] **Document migration**: In CHANGELOG

## Python-Specific Checklists

### Async Code Review
- [ ] **Proper await usage**: All async calls awaited
- [ ] **Context managers**: Resources properly managed
- [ ] **Exception handling**: Async exceptions caught
- [ ] **Task cleanup**: Background tasks cancelled properly
- [ ] **No blocking calls**: No sync I/O in async functions

### Type Safety Review
- [ ] **No `Any` unless necessary**: Use specific types
- [ ] **Generic types**: Use `TypeVar` appropriately
- [ ] **Union types**: Use `|` syntax (Python 3.10+)
- [ ] **Optional types**: Explicit `| None` where applicable
- [ ] **Return types**: Never omit return type annotation

### Performance Considerations
- [ ] **Avoid N+1 queries**: Batch database operations
- [ ] **Cache when appropriate**: Use caching utilities
- [ ] **Lazy loading**: Don't load unnecessary data
- [ ] **Resource limits**: Set appropriate timeouts
- [ ] **Memory usage**: Profile for memory leaks

## Red Flags (STOP if these occur)

🚫 **DO NOT COMMIT if:**
- Tests are failing
- Type checking has errors
- Linting shows critical issues
- Secrets are in the code
- No DCO sign-off
- Breaking changes without discussion
- Coverage drops significantly

🚫 **DO NOT MERGE if:**
- CI is failing
- No code review approval
- Merge conflicts unresolved
- Documentation not updated
- CHANGELOG not updated (for significant changes)

## Quality Standards Summary

### Mandatory (Every Commit)
1. ✅ **Tests pass**: `poetry run pytest --cov=src`
2. ✅ **Types check**: `poetry run mypy src tests`
3. ✅ **Linting clean**: `poetry run ruff check .`
4. ✅ **DCO signed**: Commit must be signed off

### Recommended (Before PR)
- Documentation updated
- Examples updated (if SDK changes)
- Performance tested (if relevant)
- Security reviewed (if applicable)

### Nice to Have
- Additional test cases
- Code comments for complex logic
- Performance benchmarks
- Integration test scenarios

## Automated Enforcement

### Git Hooks (.githooks/)
- **pre-commit**: Runs linting and type checking
- **commit-msg**: Adds DCO sign-off automatically

### CI/CD (GitHub Actions)
- **Test suite**: Runs on all PRs
- **Type checking**: mypy validation
- **Linting**: ruff validation
- **Coverage**: Reports coverage changes
- **Build**: Ensures package builds correctly

## When Task is Complete

### Final Verification
- [ ] **Objective met**: Task requirements fulfilled
- [ ] **All tests pass**: No regressions
- [ ] **Documentation current**: Changes documented
- [ ] **No technical debt**: Code is clean and maintainable

### Handoff
- [ ] **PR merged**: Code integrated into develop
- [ ] **Issue closed**: Related issues updated
- [ ] **Team notified**: If significant changes
- [ ] **Demo ready**: Can demonstrate changes to stakeholders

## Quick Command Reference

```powershell
# Pre-commit checklist (run this before every commit)
poetry run pytest --cov=src && `
poetry run mypy src tests && `
poetry run ruff check --fix . && `
poetry run ruff format .

# If all green, commit with DCO
git add .
git commit -s -m "feat: your feature description"
```