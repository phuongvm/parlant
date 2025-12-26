# Suggested Commands for Parlant Project

## System Information (Windows PowerShell)

### Directory Navigation
```powershell
# List directory contents
Get-ChildItem
ls
dir

# Change directory
cd <path>
Set-Location <path>

# Get current directory
Get-Location
pwd

# Create directory
New-Item -ItemType Directory -Path <path>
mkdir <path>
```

### File Operations
```powershell
# Read file content
Get-Content <file>
cat <file>

# Search in files
Select-String -Pattern "<text>" -Path <file>
grep "<text>" <file>

# Find files
Get-ChildItem -Recurse -Filter "*.py"
```

## Poetry Commands (Package Management)

### Installation & Setup
```powershell
# Install Poetry (if not installed)
pip install poetry

# Install project dependencies
poetry install

# Install with extras (e.g., for specific LLM provider)
poetry install --extras "anthropic"
poetry install --extras "gemini vertex"
poetry install --extras "chroma"

# Install all extras
poetry install --all-extras

# Install development dependencies only
poetry install --only dev
```

### Dependency Management
```powershell
# Add a new dependency
poetry add <package-name>

# Add a development dependency
poetry add --group dev <package-name>

# Add optional dependency (extra)
poetry add --optional <package-name>

# Update dependencies
poetry update

# Update specific package
poetry update <package-name>

# Show installed packages
poetry show

# Show dependency tree
poetry show --tree
```

### Virtual Environment
```powershell
# Activate virtual environment
poetry shell

# Run command in virtual environment
poetry run <command>

# Show virtual environment info
poetry env info

# Remove virtual environment
poetry env remove python
```

## Testing Commands

### Run Tests
```powershell
# Run all tests
poetry run pytest

# Run tests with coverage
poetry run pytest --cov=src --cov-report=html

# Run tests in parallel
poetry run pytest -n auto

# Run specific test file
poetry run pytest tests/test_agents.py

# Run specific test function
poetry run pytest tests/test_agents.py::test_agent_creation

# Run tests matching pattern
poetry run pytest -k "agent"

# Run tests with verbose output
poetry run pytest -v

# Run tests with output (don't capture stdout)
poetry run pytest -s

# Run BDD tests
poetry run pytest tests/ --bdd-features-base-dir=tests/

# Generate HTML test report
poetry run pytest --html=report.html --self-contained-html

# Run tests with TAP output
poetry run pytest --tap-stream
```

### Test Coverage
```powershell
# Generate coverage report
poetry run pytest --cov=src

# Coverage with HTML report
poetry run pytest --cov=src --cov-report=html

# Coverage with terminal report
poetry run pytest --cov=src --cov-report=term

# Coverage with missing lines
poetry run pytest --cov=src --cov-report=term-missing
```

## Type Checking (mypy)

```powershell
# Run type checking on entire project
poetry run mypy src tests

# Type check specific file
poetry run mypy src/parlant/core/agents.py

# Type check with strict mode (already enabled in mypy.ini)
poetry run mypy --strict src

# Show error codes
poetry run mypy --show-error-codes src

# Generate HTML report
poetry run mypy --html-report mypy-report src
```

## Linting & Formatting (Ruff)

### Linting
```powershell
# Check all files
poetry run ruff check .

# Check specific directory
poetry run ruff check src

# Check with auto-fix
poetry run ruff check --fix .

# Show all violations (not just first per line)
poetry run ruff check --show-fixes .

# Check specific file
poetry run ruff check src/parlant/sdk.py
```

### Formatting
```powershell
# Format all files
poetry run ruff format .

# Format specific directory
poetry run ruff format src

# Check formatting (without applying)
poetry run ruff format --check .

# Format specific file
poetry run ruff format src/parlant/sdk.py
```

## Running Parlant

### Start Server
```powershell
# Run Parlant server (default port 8800)
poetry run parlant-server

# Run with custom port
poetry run parlant-server --port 8080

# Run with specific host
poetry run parlant-server --host 0.0.0.0

# Run with environment variables
$env:OPENAI_API_KEY="sk-..."
poetry run parlant-server
```

### Client CLI
```powershell
# Run Parlant CLI
poetry run parlant --help

# Interact with agent
poetry run parlant agent <agent-id>

# List agents
poetry run parlant list-agents
```

### Migration Tools
```powershell
# Prepare database migration
poetry run parlant-prepare-migration
```

## Development Commands

### Initialize Repository
```powershell
# Run initialization script
poetry run python scripts/initialize_repo.py
```

### Linting Scripts
```powershell
# Run lint script
poetry run python scripts/lint.py
```

### Version Management
```powershell
# Check version
poetry run python scripts/version.py
```

### Publishing
```powershell
# Publish package (maintainers only)
poetry run python scripts/publish.py
```

## Quality Assurance (Full Suite)

### Run All QA Checks
```powershell
# Complete quality check
poetry run pytest --cov=src && poetry run mypy src tests && poetry run ruff check .

# Or step by step:
poetry run pytest --cov=src         # Tests
poetry run mypy src tests            # Type checking
poetry run ruff check --fix .        # Linting
poetry run ruff format .             # Formatting
```

## Git Commands

### Basic Operations
```powershell
# Status
git status

# Pull latest changes
git pull

# Add changes (don't forget DCO sign-off!)
git add .

# Commit with DCO sign-off (REQUIRED)
git commit -s -m "Your message"

# Push
git push

# Branch operations
git branch                    # List branches
git checkout -b <branch>      # Create and switch
git checkout <branch>         # Switch branch
```

### Git Hooks Setup
```powershell
# Configure git to use project hooks (includes DCO sign-off)
git config core.hookspath .githooks

# Verify hook setup
git config --get core.hookspath
```

## Python REPL

### Interactive Development
```powershell
# Start IPython shell with project context
poetry run ipython

# Run Python script
poetry run python script.py

# Run module as script
poetry run python -m parlant.sdk
```

## Docker (Dev Container)

### Build & Run
```powershell
# If using Dev Container (.devcontainer/)
# Open in VS Code with Dev Containers extension
code --folder-uri vscode-remote://dev-container+<path>
```

## Environment Variables

### Required Variables
```powershell
# OpenAI API Key (primary)
$env:OPENAI_API_KEY="sk-..."

# Optional: Other LLM providers
$env:ANTHROPIC_API_KEY="sk-ant-..."
$env:GOOGLE_API_KEY="..."
$env:GEMINI_API_KEY="..."

# Optional: Database connections
$env:MONGODB_URI="mongodb://localhost:27017"

# Optional: Observability
$env:OTEL_EXPORTER_OTLP_ENDPOINT="http://localhost:4317"
```

### Load from .env File
```powershell
# Create .env file in project root
# Poetry will automatically load it
```

## Build & Distribution

### Build Package
```powershell
# Build distribution packages
poetry build

# Output: dist/parlant-3.1.0a1-py3-none-any.whl
#         dist/parlant-3.1.0a1.tar.gz
```

### Install Local Package
```powershell
# Install from built wheel
pip install dist/parlant-3.1.0a1-py3-none-any.whl

# Install in editable mode
pip install -e .
```

## Documentation

### View Documentation
```powershell
# Open online documentation
start https://parlant.io/docs

# Open examples
start https://parlant.io/docs/quickstart/examples
```

## Troubleshooting

### Clear Caches
```powershell
# Remove Python cache files
Get-ChildItem -Recurse -Filter "*.pyc" | Remove-Item
Get-ChildItem -Recurse -Filter "__pycache__" | Remove-Item -Recurse

# Clear pytest cache
Remove-Item -Recurse -Force .pytest_cache

# Clear mypy cache
Remove-Item -Recurse -Force .mypy_cache

# Clear ruff cache
Remove-Item -Recurse -Force .ruff_cache
```

### Reinstall Dependencies
```powershell
# Remove lock file and reinstall
Remove-Item poetry.lock
poetry install
```

### Reset Virtual Environment
```powershell
# Remove and recreate virtual environment
poetry env remove python
poetry install
```

## Performance & Profiling

### Profile Tests
```powershell
# Run tests with timing
poetry run pytest --durations=10

# Profile specific test
poetry run pytest --profile tests/test_slow.py
```

## CI/CD Scripts

### Run CI Scripts Locally
```powershell
# CI linting check
poetry run python scripts/ci/lint.py

# CI test suite
poetry run python scripts/ci/test.py
```

## Quick Reference

### Daily Development Workflow
```powershell
# 1. Pull latest changes
git pull

# 2. Install/update dependencies
poetry install

# 3. Make changes...

# 4. Run QA before committing
poetry run pytest --cov=src
poetry run mypy src tests
poetry run ruff check --fix .

# 5. Commit with DCO
git add .
git commit -s -m "feat: add new feature"

# 6. Push
git push
```

### First-Time Setup
```powershell
# 1. Clone repository
git clone https://github.com/emcie-co/parlant.git
cd parlant

# 2. Install Poetry
pip install poetry

# 3. Install dependencies
poetry install

# 4. Set up git hooks
git config core.hookspath .githooks

# 5. Set environment variables
$env:OPENAI_API_KEY="sk-..."

# 6. Run tests to verify
poetry run pytest

# 7. Start development server
poetry run parlant-server
```