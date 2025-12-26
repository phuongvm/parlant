# Parlant Code Style & Conventions

## General Principles

### Type Safety First
- **Strict mypy mode**: All code must pass strict type checking
- **Type hints required**: All functions, methods, and variables
- **Pydantic models**: For data validation and serialization

### Async-First Design
- **asyncio**: Primary concurrency model
- **async/await**: Use throughout codebase
- **Context managers**: For resource management

### Production-Grade Quality
- **Reliability**: Code must be predictable and consistent
- **Testability**: All code should be unit testable
- **Observability**: Structured logging and telemetry

## Python Version & Compatibility
- **Target**: Python 3.12
- **Support**: Python 3.10 - 3.13
- **Features**: Use modern Python features (3.10+ syntax)

## Code Formatting (Ruff)

### Configuration File
**ruff.toml** at project root

### Line Length
- **Maximum**: 100 characters
- **Same as Black**: Industry standard

### Indentation
- **4 spaces**: No tabs
- **Consistent**: Throughout all Python files

### Quotes
- **Double quotes** for strings: `"hello"`
- **Exception**: Use single quotes when it avoids escaping

### Import Ordering
- Standard library imports first
- Third-party imports second
- Local application imports last
- **Alphabetically sorted** within each group

### Enabled Lint Rules
```toml
select = [
    "E4",      # Import errors
    "E7",      # Statement errors
    "E9",      # Runtime errors
    "F",       # Pyflakes
    "W293",    # Blank line with whitespace
    "PLR1722", # Use sys.exit()
    "PTH204",  # Use pathlib
    "PLW2901", # Outer loop variable overwrite
]
```

### Ignored Rules
- **E203**: Whitespace before ':' (conflicts with Black)

### Comments
- **Inline comments**: Use sparingly, prefer self-documenting code
- **Block comments**: For complex logic explanation
- **Docstrings**: Required for all public functions/classes

## Type Checking (mypy)

### Configuration File
**mypy.ini** at project root

### Strict Mode
```ini
[mypy]
strict = True
warn_unused_ignores = False
disable_error_code = type-abstract
```

### Settings
- **namespace_packages = True**: Support namespace packages
- **explicit_package_bases = True**: Explicit package structure
- **mypy_path = src**: Source root for type checking
- **files = src, tests**: Check both source and tests
- **exclude = scripts**: Don't check utility scripts
- **plugins = pydantic.mypy**: Pydantic type support

### Type Hints Requirements
All functions and methods must have:
1. **Parameter types**: Every parameter annotated
2. **Return type**: Explicit return type annotation
3. **No Any**: Avoid `Any` unless absolutely necessary

Example:
```python
async def create_agent(
    self,
    name: str,
    description: str | None = None
) -> Agent:
    ...
```

## Testing (pytest)

### Configuration File
**pytest.ini** at project root

### Testing Framework
- **pytest**: Primary test framework
- **pytest-asyncio**: For async tests (asyncio_mode = auto)
- **pytest-bdd**: For behavior-driven tests
- **pytest-cov**: Coverage reporting
- **pytest-xdist**: Parallel test execution

### Test Organization
```
tests/
├── unit/           # Unit tests
├── integration/    # Integration tests
├── bdd/            # BDD feature tests
└── fixtures/       # Shared fixtures
```

### Test File Naming
- **test_*.py**: Test files start with `test_`
- **test_<module_name>.py**: Match source module names
- **Descriptive**: Clear test purpose in filename

### Test Function Naming
```python
def test_agent_creation_succeeds():
    """Test that agent creation works correctly."""
    ...

async def test_async_guideline_matching():
    """Test async guideline matching behavior."""
    ...
```

### Fixtures
- **conftest.py**: Shared fixtures
- **Scope**: Use appropriate fixture scope (function, module, session)
- **Async fixtures**: For async test setup

### Test Coverage
- **High coverage**: Aim for >80%
- **Critical paths**: 100% coverage for core functionality
- **pytest-cov**: Integrated coverage reporting

## Naming Conventions

### Variables & Functions
- **snake_case**: For variables and functions
- **Descriptive**: Clear, meaningful names
- **No abbreviations**: Unless widely understood (e.g., `id`, `url`)

```python
agent_name = "WeatherBot"
user_message = "Hello"

async def create_guideline(condition: str, action: str) -> Guideline:
    ...
```

### Classes
- **PascalCase**: For class names
- **Noun-based**: Represent entities or concepts

```python
class Agent:
    ...

class GuidelineMatchingEngine:
    ...
```

### Constants
- **UPPER_SNAKE_CASE**: For module-level constants
- **Immutable**: Constants should not be modified

```python
DEFAULT_TIMEOUT = 30
MAX_RETRIES = 3
API_VERSION = "v1"
```

### Private Members
- **Single underscore prefix**: For internal use
- **Double underscore**: For name mangling (rare)

```python
class Agent:
    def __init__(self):
        self._internal_state = {}
        
    def _internal_method(self):
        ...
```

## Docstrings

### Style
- **Google style** or **NumPy style**: Consistent throughout
- **Required**: For all public functions, classes, methods
- **Optional**: For private members (but encouraged)

### Example
```python
async def create_agent(
    name: str,
    description: str | None = None
) -> Agent:
    """Create a new agent instance.
    
    Args:
        name: The agent's display name
        description: Optional agent description
    
    Returns:
        Agent: The newly created agent instance
    
    Raises:
        ValueError: If name is empty or invalid
    """
    ...
```

## Error Handling

### Exception Types
- **Specific exceptions**: Catch specific exception types
- **Never bare except**: Always specify exception type
- **Re-raise when appropriate**: Don't swallow errors

```python
# Good
try:
    result = await process_data()
except ValueError as e:
    logger.error("Invalid data", exc_info=e)
    raise

# Bad
try:
    result = await process_data()
except:  # Don't do this!
    pass
```

### Custom Exceptions
- **Inherit from appropriate base**: ValueError, TypeError, etc.
- **Meaningful names**: ClearException purpose
- **Include context**: Helpful error messages

## Logging

### Structured Logging
- **structlog**: Primary logging library
- **Key-value pairs**: Structured log data
- **Levels**: DEBUG, INFO, WARNING, ERROR

```python
logger.info(
    "agent_created",
    agent_id=agent.id,
    agent_name=agent.name
)
```

### Log Levels
- **DEBUG**: Detailed diagnostic information
- **INFO**: General informational messages
- **WARNING**: Warning messages (recoverable issues)
- **ERROR**: Error messages (failures)

## Async Patterns

### Context Managers
```python
async with Server() as server:
    agent = await server.create_agent(...)
```

### Resource Cleanup
- **Always use context managers**: For resources
- **try/finally**: When context managers not available
- **aiofiles**: For async file operations

### Concurrent Operations
- **asyncio.gather**: For parallel operations
- **asyncio.create_task**: For background tasks
- **Proper cancellation**: Handle task cancellation

## Import Organization

### Order
1. Standard library imports
2. Related third-party imports
3. Local application/library imports

### Example
```python
# Standard library
import asyncio
from typing import Any, Optional

# Third-party
from fastapi import FastAPI
from pydantic import BaseModel

# Local
from parlant.core.agents import Agent
from parlant.sdk import tool
```

## File Organization

### Module Structure
```
src/parlant/
├── __init__.py      # Package initialization
├── sdk.py           # Public SDK interface
├── core/            # Core business logic
├── adapters/        # External integrations
├── api/             # REST API definitions
└── bin/             # CLI entry points
```

### File Size
- **Reasonable size**: Aim for <500 lines per file
- **Single responsibility**: One main concept per file
- **Split when needed**: Create submodules for complexity

## Git Commit Conventions

### DCO Sign-Off Required
All commits must be signed off:
```bash
git commit -s -m "Your commit message"
```

Or use git hooks (`.githooks/`):
```bash
git config core.hookspath .githooks
```

### Commit Messages
- **Clear and descriptive**: What and why
- **Present tense**: "Add feature" not "Added feature"
- **Reference issues**: When applicable

## Code Review Standards

### Before Submitting PR
- [ ] All tests pass
- [ ] Type checking passes (mypy)
- [ ] Linting passes (ruff)
- [ ] Code coverage maintained/improved
- [ ] Documentation updated
- [ ] CHANGELOG.md updated (if applicable)

### PR Description
- Clear description of changes
- Links to related issues
- Test coverage notes
- Breaking changes highlighted