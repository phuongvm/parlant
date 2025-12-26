# Parlant Project Overview

## Project Purpose
**Parlant** is an **AI Agent Framework** designed to build LLM-powered agents that **reliably follow instructions and behave consistently**. Unlike traditional approaches that rely on complex system prompts and hope for compliance, Parlant **ensures** guideline adherence through a structured framework.

## The Core Problem Parlant Solves
Traditional AI agents face critical issues:
- ❌ Ignore system prompts
- ❌ Hallucinate responses in critical moments
- ❌ Can't handle edge cases consistently
- ❌ Unpredictable behavior in production

## Parlant's Solution
Instead of fighting prompts, Parlant uses **principle-based teaching** with guaranteed compliance:
- ✅ Define rules in natural language
- ✅ **Ensured** rule compliance (not hoped for)
- ✅ Predictable, consistent behavior
- ✅ Production-ready from day one

## Key Features

### 1. **Conversational Journeys**
Define clear customer journeys and how your agent should respond at each step.

### 2. **Behavioral Guidelines** ⭐
Craft agent behavior in natural language; Parlant matches relevant guidelines contextually and ensures they are followed.

### 3. **Tool Integration**
Attach external APIs, data fetchers, or backend services to specific interaction events.

### 4. **Domain Adaptation**
Teach agents domain-specific terminology and craft personalized responses.

### 5. **Canned Responses**
Use response templates to eliminate hallucinations and guarantee style consistency.

### 6. **Explainability**
Understand why and when each guideline was matched and followed.

## Target Use Cases

### Primary Industries
- **Financial Services**: Compliance-first design, built-in risk management
- **Healthcare**: HIPAA-ready agents, patient data protection
- **E-commerce**: Customer service at scale, order processing automation
- **Legal Tech**: Precise legal guidance, document review assistance

### Development Focus
- **Customer-facing agents**: Agents that interact directly with end users
- **Enterprise applications**: Production-grade reliability and compliance
- **Multi-turn conversations**: Complex dialogue management

## Project Type
- **Open Source Framework**: Apache 2.0 license
- **SDK + Server Architecture**: Client SDK + backend server
- **Python-based**: Async-first design with FastAPI server
- **MCP Integration**: FastMCP support for tool integration

## Components

### 1. **Parlant SDK** (`parlant.sdk`)
Python SDK for defining agents, guidelines, tools, and behaviors.

### 2. **Parlant Server** (`parlant-server`)
FastAPI-based backend server that runs agents and manages conversations.

### 3. **React Widget**
Drop-in chat UI component for web applications (separate repo: parlant-chat-react).

### 4. **CLI Tools**
- `parlant`: Client CLI for interacting with agents
- `parlant-server`: Server runner
- `parlant-prepare-migration`: Database migration tool

## Developer Experience

### Quick Start (60 seconds)
```python
import parlant.sdk as p

@p.tool
async def get_weather(context, city: str) -> p.ToolResult:
    return p.ToolResult(f"Sunny, 72°F in {city}")

async def main():
    async with p.Server() as server:
        agent = await server.create_agent(
            name="WeatherBot",
            description="Helpful weather assistant"
        )
        
        await agent.create_guideline(
            condition="User asks about weather",
            action="Get current weather and provide friendly response",
            tools=[get_weather]
        )
        
        # Test playground at http://localhost:8800
```

## Community & Adoption
- **10,000+ developers** using Parlant
- **Active Discord community**
- **Enterprise clients** in financial services, healthcare, legal tech
- **Trending** on GitHub and TrendShift

## Repository Organization
- **src/parlant/**: Main framework code
- **tests/**: Comprehensive test suite (pytest + BDD)
- **docs/**: Documentation and guides
- **examples/**: Example implementations (including healthcare agent)
- **scripts/**: Build, CI, and utility scripts

## Development Philosophy
- **Reliability over flexibility**: Guaranteed behavior > unpredictable creativity
- **Natural language configuration**: Guidelines written in plain English
- **Production-first**: Built for customer-facing applications
- **Explainability**: Full visibility into agent decision-making

## Maintainers
Built by **Emcie** team:
- Yam Marcovitz (yam@emcie.co)
- Dor Zohar (dor@emcie.co)

## Version
Current version: **3.1.0-alpha.1** (active development)

## License
Apache 2.0 - Use anywhere, including commercial projects.