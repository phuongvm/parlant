# Parlant Technology Stack

## Programming Language
- **Python**: 3.10 - 3.13 (restricted for PyTorch/Triton compatibility)
- **Target Version**: Python 3.12 (for type checking and linting)

## Package Management
- **Poetry**: Primary dependency manager
- **Poetry Lock**: Strict version locking for reproducibility

## Core Framework Dependencies

### Web Framework & Server
- **FastAPI** (^0.120.0): Web framework for REST API
- **Uvicorn** (^0.38.0): ASGI server
- **Starlette** (^0.49.0): Web toolkit (updated for security)

### LLM Integration
- **OpenAI** (^2.8.0): Primary LLM provider SDK
- **FastMCP** (2.13.0): Model Context Protocol integration
- **MCP** (^1.16.0): Model Context Protocol core
- **Tiktoken** (^0.12): Token counting for OpenAI models
- **Tokenizers** (^0.21): Hugging Face tokenizers

### Optional LLM Provider Support
Via `poetry extras`:
- **Anthropic** (`anthropic` extra): Claude models
- **Google Gemini** (`gemini` extra): Google's Gemini models
- **Google Vertex AI** (`vertex` extra): Enterprise Google AI
- **AWS Bedrock** (`aws` extra): Amazon's LLM service
- **Ollama** (`ollama` extra): Local LLM hosting
- **Cerebras** (`cerebras` extra): Cerebras Cloud SDK
- **Together AI** (`together` extra): Together.ai platform
- **LiteLLM** (`litellm` extra): Multi-provider abstraction
- **Mistral** (`mistral` extra): Mistral AI models
- **DeepSeek** (`deepseek` extra): DeepSeek models
- **Zhipu** (`zhipu` extra): Zhipu AI (China)

### AI/ML Libraries
- **PyTorch** (^2.8.0, optional): Deep learning framework
- **Transformers** (^4.53.0, optional): Hugging Face transformers
- **Nano-VectorDB** (^0.0.4.3): Lightweight vector database

### Vector Database Options
Via `poetry extras`:
- **ChromaDB** (`chroma` extra): Vector database
- **Qdrant** (`qdrant` extra): Alternative vector DB

### Data Storage
- **MongoDB** (`mongo` extra, ^4.11.1): NoSQL database option
- **Snowflake** (`snowflake` extra, ^3.12.0): Data warehouse connector

### Async & Concurrency
- **aiofiles** (^24.1.0): Async file I/O
- **aiorwlock** (^1.5.0): Async read-write locks
- **contextvars** (^2.4): Context variables for async
- **httpx** (^0.28.1): Async HTTP client

### Data Processing & Validation
- **Pydantic**: Data validation (via FastAPI)
- **jsonschema** (^4.23.0): JSON schema validation
- **jsonfinder** (^0.4.2): JSON extraction utilities

### Scheduling & Rate Limiting
- **croniter** (^5.0.1): Cron expression parsing
- **limits** (^5.5.0): Rate limiting

### API & OpenAPI
- **aiopenapi3** (0.8.1): Async OpenAPI client
- **openapi3-parser** (1.1.21): OpenAPI spec parser

### Templating & Configuration
- **Jinja2** (^3.1.6): Template engine
- **python-dotenv** (^1.0.1): Environment variable management
- **TOML** (^0.10.2): TOML configuration parser

### Authentication & Security
- **Authlib** (^1.6.5): OAuth and authentication
- **AWS SDK (Boto3)** (^1.35.70): AWS service integration
- **Azure Identity** (`azure` extra, ^1.20.0): Azure authentication

### Observability & Logging
- **structlog** (^24.4.0): Structured logging
- **coloredlogs** (^15.0.1): Colored console logging
- **colorama** (^0.4.6): Cross-platform colored output
- **OpenTelemetry** suite (^1.37.0):
  - opentelemetry-api
  - opentelemetry-sdk
  - opentelemetry-instrumentation
  - opentelemetry-exporter-otlp

### Utilities
- **Click** (^8.1.7): CLI framework
- **Rich** (^14.0.0): Rich terminal output
- **Tabulate** (^0.9.0): Table formatting
- **cachetools** (^6.0.0): Caching utilities
- **more-itertools** (>=10.3.0): Iterator utilities
- **networkx** (^3.3): Graph algorithms
- **nanoid** (^2.0.0): Unique ID generation
- **semver** (^3.0.2): Semantic versioning
- **python-dateutil** (^2.8.2): Date/time utilities
- **requests** (^2.32.5): HTTP client (sync)
- **websocket-client** (^1.5.3): WebSocket client
- **lagom** (^2.6.0): Dependency injection

### Client SDK
- **parlant-client**: Official Python client (from GitHub, tag: develop.1763631946)

## Development Tools

### Testing
- **pytest** (^8.0.0): Test framework
- **pytest-asyncio** (^0.23.5): Async test support
- **pytest-bdd** (^7.1.2): Behavior-driven development
- **pytest-cov** (^5.0.0): Coverage reporting
- **pytest-tap** (^3.4): TAP output format
- **pytest-xdist** (^3.6.1): Parallel test execution
- **pytest-timing**: Custom timing plugin (from GitHub)

### Type Checking
- **mypy** (^1.18.1): Static type checker
- **Strict mode enabled**: Full type safety enforcement
- **Pydantic plugin**: Enhanced Pydantic model checking

### Linting & Formatting
- **Ruff** (^0.9.1): Fast Python linter and formatter
- Replaces: flake8, black, isort, pyupgrade, etc.
- Configuration: ruff.toml

### Code Quality
- **pep8-naming** (^0.13.3): PEP 8 naming conventions

### Development Experience
- **ipython** (^8.26.0): Enhanced Python shell
- **python-dotenv** (^1.0.1): Environment management

### Type Stubs
- **types-aiofiles** (^24.1.0.20240626)
- **types-cachetools** (^6.0.0.20250525)
- **types-croniter** (^4.0.0.20241030)
- **types-jsonschema** (^4.22.0.20240610)
- **types-python-dateutil** (^2.8.19.20240106)
- **types-requests** (^2.32.0.20240712)

## Build System
- **Poetry Core**: Build backend
- **PEP 517/518 compliant**: Modern Python packaging

## Entry Points (Console Scripts)
1. **parlant**: Client CLI (`parlant.bin.client:main`)
2. **parlant-server**: Server runner (`parlant.bin.server:main`)
3. **parlant-prepare-migration**: Migration tool (`parlant.bin.prepare_migration:main`)

## Platform Support
- **Cross-platform**: Windows, Linux, macOS
- **Windows-specific**: This instance runs on Windows
- **Async-first**: Built on asyncio

## External Integrations
- **Discord**: Community platform integration
- **GitHub**: Source control and CI/CD
- **Docker**: Containerization support (via .devcontainer)

## Version Control
- **Git**: Version control
- **Git Hooks**: Pre-commit hooks in `.githooks`
- **DCO**: Developer Certificate of Origin for commits

## CI/CD
- **GitHub Actions**: Automated testing and deployment
- **Scripts**: CI scripts in `scripts/ci/`

## Documentation
- **Fern**: API documentation generator (scripts/fern/)
- **Markdown**: Project documentation

## System Requirements
- **Python**: 3.10 or higher (up to 3.13)
- **OS**: Windows, Linux, or macOS
- **Memory**: Varies by LLM provider and model size
- **Storage**: Depends on vector database choice