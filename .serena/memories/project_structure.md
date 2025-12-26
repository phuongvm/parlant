# Parlant Project Structure

## Root Directory Layout

```
parlant/
├── .devcontainer/          # Dev container configuration (VS Code)
├── .githooks/              # Git hooks (includes DCO sign-off)
├── .github/                # GitHub Actions workflows and templates
├── .serena/                # Serena MCP metadata (auto-generated)
├── docs/                   # Documentation and assets
├── examples/               # Example implementations
├── scripts/                # Build, CI, and utility scripts
├── src/                    # Source code (main package)
├── tests/                  # Test suite
├── .gitignore              # Git ignore patterns
├── CHANGELOG.md            # Version history
├── CLAUDE.md               # Claude AI integration notes
├── CONTRIBUTING.md         # Contribution guidelines
├── DCO.md                  # Developer Certificate of Origin
├── LICENSE                 # Apache 2.0 license
├── llms.txt                # LLM integration documentation
├── mypy.ini                # Type checking configuration
├── poetry.lock             # Locked dependencies
├── pyproject.toml          # Project metadata and dependencies
├── pytest.ini              # Test configuration
├── pytest_stochastics.json # Stochastic test configuration
├── README.md               # Project overview and quick start
└── ruff.toml               # Linting and formatting configuration
```

## Source Code Structure (`src/parlant/`)

```
src/parlant/
├── __init__.py             # Package initialization
├── sdk.py                  # Public SDK interface (primary entry point)
├── py.typed                # PEP 561 type marker
│
├── adapters/               # External system integrations
│   ├── __init__.py
│   ├── anthropic/          # Anthropic Claude integration
│   ├── azure/              # Azure services integration
│   ├── aws/                # AWS Bedrock integration
│   ├── cerebras/           # Cerebras Cloud integration
│   ├── chroma/             # ChromaDB vector database
│   ├── deepseek/           # DeepSeek integration
│   ├── gemini/             # Google Gemini integration
│   ├── litellm/            # LiteLLM multi-provider
│   ├── mistral/            # Mistral AI integration
│   ├── mongo/              # MongoDB integration
│   ├── ollama/             # Ollama local LLM
│   ├── openai/             # OpenAI integration (primary)
│   ├── qdrant/             # Qdrant vector database
│   ├── snowflake/          # Snowflake connector
│   ├── together/           # Together AI integration
│   ├── vertex/             # Google Vertex AI
│   └── zhipu/              # Zhipu AI integration
│
├── api/                    # REST API definitions
│   ├── __init__.py
│   ├── routes/             # API route handlers
│   ├── models/             # API request/response models
│   └── middleware/         # API middleware (auth, logging, etc.)
│
├── bin/                    # CLI entry points
│   ├── __init__.py
│   ├── client.py           # parlant CLI (main)
│   ├── server.py           # parlant-server CLI (main)
│   └── prepare_migration.py # parlant-prepare-migration CLI (main)
│
└── core/                   # Core business logic
    ├── __init__.py
    ├── agents/             # Agent management
    ├── guidelines/         # Guideline system and matching engine
    ├── journeys/           # Conversation journey management
    ├── tools/              # Tool integration system
    ├── context/            # Context management
    ├── responses/          # Canned response system
    ├── glossary/           # Domain terminology
    ├── sessions/           # Session management
    ├── persistence/        # Data persistence layer
    ├── services/           # Business services
    └── models/             # Core domain models
```

## Test Structure (`tests/`)

```
tests/
├── __init__.py
├── conftest.py             # Shared pytest fixtures
│
├── unit/                   # Unit tests
│   ├── test_agents.py
│   ├── test_guidelines.py
│   ├── test_tools.py
│   └── ...
│
├── integration/            # Integration tests
│   ├── test_api.py
│   ├── test_llm_providers.py
│   └── ...
│
├── bdd/                    # Behavior-driven tests
│   ├── features/           # Gherkin feature files
│   ├── step_defs/          # Step definitions
│   └── ...
│
└── fixtures/               # Test data and fixtures
    ├── agents.json
    ├── guidelines.json
    └── ...
```

## Documentation Structure (`docs/`)

```
docs/
├── LogoTransparentDark.png   # Project logo (dark theme)
├── LogoTransparentLight.png  # Project logo (light theme)
├── demo.gif                  # Demo animation
├── architecture/             # Architecture documentation
├── api/                      # API reference
├── concepts/                 # Concept guides
│   ├── agents.md
│   ├── guidelines.md
│   ├── journeys.md
│   └── tools.md
├── quickstart/               # Getting started guides
│   ├── installation.md
│   └── examples.md
└── advanced/                 # Advanced topics
    ├── explainability.md
    └── customization.md
```

## Examples Structure (`examples/`)

```
examples/
├── quickstart/               # Quick start examples
│   ├── weather_bot.py
│   └── customer_service.py
│
├── healthcare/               # Healthcare agent example
│   ├── main.py
│   ├── guidelines.py
│   └── tools.py
│
├── financial/                # Financial services example
│   └── ...
│
└── e-commerce/               # E-commerce example
    └── ...
```

## Scripts Structure (`scripts/`)

```
scripts/
├── __init__.py
├── utils.py                  # Shared utilities
│
├── ci/                       # CI/CD scripts
│   ├── lint.py
│   ├── test.py
│   └── build.py
│
├── fern/                     # Fern documentation generator
│   └── ...
│
├── generate_client_sdk.py   # SDK generation
├── initialize_repo.py        # Repository initialization
├── install_packages.py       # Package installation helper
├── lint.py                   # Linting script
├── publish.py                # Publishing script
└── version.py                # Version management
```

## Configuration Files

### Python Configuration
- **`pyproject.toml`**: Project metadata, dependencies, Poetry configuration, tool settings
- **`poetry.lock`**: Locked dependency versions
- **`mypy.ini`**: Type checking configuration (strict mode)
- **`pytest.ini`**: Test runner configuration
- **`ruff.toml`**: Linting and formatting rules

### Git Configuration
- **`.gitignore`**: Files to exclude from version control
- **`.githooks/`**: Custom git hooks (DCO sign-off)
- **`DCO.md`**: Developer Certificate of Origin

### GitHub Configuration
- **`.github/workflows/`**: GitHub Actions CI/CD pipelines
- **`.github/ISSUE_TEMPLATE/`**: Issue templates
- **`.github/PULL_REQUEST_TEMPLATE.md`**: PR template

### Development Environment
- **`.devcontainer/`**: VS Code dev container configuration
- **`llms.txt`**: LLM integration documentation

## Key Files by Purpose

### User-Facing Documentation
- **README.md**: Project overview, quick start, features
- **CHANGELOG.md**: Version history and changes
- **CONTRIBUTING.md**: How to contribute
- **LICENSE**: Apache 2.0 license text

### Entry Points
- **`src/parlant/sdk.py`**: Main SDK interface (import as `parlant.sdk`)
- **`src/parlant/bin/client.py`**: `parlant` CLI command
- **`src/parlant/bin/server.py`**: `parlant-server` CLI command

### Core Implementation
- **`src/parlant/core/agents/`**: Agent creation and management
- **`src/parlant/core/guidelines/`**: Guideline matching engine
- **`src/parlant/core/tools/`**: Tool integration system

### Adapter Pattern
- **`src/parlant/adapters/openai/`**: OpenAI integration (primary LLM)
- **`src/parlant/adapters/anthropic/`**: Claude integration
- **`src/parlant/adapters/chroma/`**: Vector database integration

## File Naming Conventions

### Python Files
- **`snake_case.py`**: Module names
- **`test_*.py`**: Test files
- **`conftest.py`**: Pytest configuration
- **`__init__.py`**: Package initialization

### Documentation Files
- **`UPPERCASE.md`**: Root-level docs (README, CHANGELOG, CONTRIBUTING)
- **`lowercase.md`**: Nested docs (concepts, guides)

### Configuration Files
- **`.ini`**: INI format (mypy, pytest)
- **`.toml`**: TOML format (pyproject, ruff)
- **`.json`**: JSON format (test data, stochastics)

## Import Patterns

### Public API (Users)
```python
import parlant.sdk as p

# Use SDK through 'p' namespace
agent = await p.Server().create_agent(...)
```

### Internal Modules (Developers)
```python
from parlant.core.agents import Agent
from parlant.core.guidelines import GuidelineMatchingEngine
from parlant.adapters.openai import OpenAIAdapter
```

## Build Artifacts (Gitignored)

### Python Cache
- **`__pycache__/`**: Bytecode cache
- **`*.pyc`**: Compiled Python files
- **`.mypy_cache/`**: mypy cache
- **`.pytest_cache/`**: pytest cache
- **`.ruff_cache/`**: ruff cache

### Development
- **`.venv/`**: Virtual environment
- **`venv/`**: Alternative venv name
- **`.env`**: Environment variables (secrets)

### Build Output
- **`dist/`**: Build distributions
- **`build/`**: Build artifacts
- **`*.egg-info/`**: Package metadata

### IDE
- **`.vscode/`**: VS Code settings
- **`.idea/`**: PyCharm settings

### Reports
- **`htmlcov/`**: Coverage HTML reports
- **`mypy-report/`**: mypy HTML reports
- **`report.html`**: Test HTML report

## Navigation Guidelines

### Finding Core Logic
1. Start at **`src/parlant/sdk.py`** for public API
2. Look in **`src/parlant/core/`** for business logic
3. Check **`src/parlant/adapters/`** for integrations

### Finding Tests
1. **`tests/unit/`** for unit tests
2. **`tests/integration/`** for integration tests
3. **`tests/bdd/`** for BDD tests
4. Match test file to source file: `src/parlant/core/agents.py` → `tests/unit/test_agents.py`

### Finding Configuration
1. **Root level** for tool configs (ruff.toml, mypy.ini)
2. **`pyproject.toml`** for project metadata and Poetry settings
3. **`.env`** for secrets (create from example if needed)

### Finding Documentation
1. **README.md** for overview
2. **`docs/concepts/`** for feature guides
3. **`docs/quickstart/`** for getting started
4. **`examples/`** for working code

### Finding Scripts
1. **`scripts/`** for build and utility scripts
2. **`scripts/ci/`** for CI/CD automation
3. **Entry points** in `pyproject.toml` [tool.poetry.scripts]

## Common Patterns

### Module Organization
- Each directory has `__init__.py`
- Public API exported in `__init__.py`
- Private modules prefixed with `_`

### Test Organization
- Tests mirror source structure
- One test file per source file (generally)
- Fixtures in `conftest.py`

### Configuration Hierarchy
1. **pyproject.toml**: Project-level config
2. **Tool-specific configs**: mypy.ini, ruff.toml, pytest.ini
3. **Environment variables**: Runtime configuration

### Data Flow
```
User Code
    ↓
SDK (parlant.sdk)
    ↓
Core Logic (parlant.core)
    ↓
Adapters (parlant.adapters)
    ↓
External Systems (LLMs, DBs, etc.)
```