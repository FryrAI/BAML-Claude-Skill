# BAML Code Generation Skill - Quick Start Guide

**Version**: 1.0.0
**Last Updated**: 2025-01-25

## Overview

The BAML Code Generation Skill enables Claude Code to automatically generate production-ready BAML applications by learning from official BoundaryML repositories. Simply describe what you want to build, and receive complete BAML code with types, functions, tests, and integrations.

## Prerequisites

### 1. Install MCP Servers (Required)

The skill requires two MCP servers to access BAML repositories:

```bash
# Install baml_Docs MCP server (core BAML implementation)
claude mcp add "baml_Docs" --scope user -- npx -y mcp-remote https://gitmcp.io/BoundaryML/baml

# Install baml_Examples MCP server (production patterns) - if available
claude mcp add "baml_Examples" -- npx -y mcp-remote https://gitmcp.io/BoundaryML/baml-examples
```

### 2. Verify Installation

Check that MCP servers are accessible:
```
User: "Check MCP server status for BAML"
Claude: [Verifies both servers are responding]
```

## Basic Usage

### Simple Generation

```
User: "Generate BAML code to extract invoice data"

Claude: [Generates complete BAML including:
  - Invoice and LineItem types
  - ExtractInvoice function
  - Test suite
  - Python/TypeScript integration]
```

### With Framework Integration

```
User: "Create BAML sentiment classifier with FastAPI integration"

Claude: [Generates:
  - Sentiment enum and Result class
  - ClassifySentiment function
  - FastAPI endpoints
  - Async Python client
  - Docker configuration]
```

## Common Use Cases

### 1. Data Extraction

Extract structured data from unstructured text:

```
User: "Build BAML to extract resume information including experience and skills"

Response includes:
- Resume, Experience, Skill types
- ExtractResume function with step-by-step reasoning
- Comprehensive test coverage
- Integration templates
```

### 2. Classification

Categorize inputs with confidence scores:

```
User: "Generate intent classifier for customer support with confidence levels"

Response includes:
- Intent enum with categories
- ClassifyIntent function
- Confidence scoring
- Reasoning capture
```

### 3. RAG (Retrieval-Augmented Generation)

Build citation-aware search systems:

```
User: "Create RAG system with source citations"

Response includes:
- Citation and Document types
- SearchWithCitations function
- Source tracking
- Confidence metrics
```

### 4. Agents

Design planning and execution agents:

```
User: "Build planning agent for task automation"

Response includes:
- Task and Plan types
- PlanExecution function
- State management
- Error handling
```

## Advanced Features

### Optimization Levels

```
User: "Generate extraction function with aggressive optimization"

Claude: [Applies:
  - Token reduction strategies
  - Prompt compression
  - Type simplification
  - Caching patterns]
```

### Multimodal Support

```
User: "Create BAML function to analyze images and extract text"

Claude: [Generates:
  - Image-aware types
  - Multimodal function
  - Base64 handling
  - Vision model configuration]
```

### Custom Framework Integration

```
User: "Generate BAML with Next.js and TypeScript integration"

Claude: [Provides:
  - Type-safe TypeScript client
  - Next.js API routes
  - Streaming support
  - Error boundaries]
```

## Quick Commands

### Pattern Exploration
```
"Show me BAML extraction patterns"
"What classification examples are available?"
"List RAG implementation patterns"
```

### Code Generation
```
"Generate BAML for [use case]"
"Create [pattern type] function with tests"
"Build complete BAML project for [domain]"
```

### Optimization
```
"Optimize this BAML code for tokens"
"Reduce latency for this function"
"Improve cost efficiency"
```

### Validation
```
"Validate this BAML syntax"
"Check if this code will compile"
"Test this function definition"
```

## Output Structure

Every generation includes:

```
generated_code/
├── baml_src/
│   ├── types.baml       # Type definitions
│   ├── functions.baml   # BAML functions
│   └── clients.baml     # Client configurations
├── tests/
│   ├── test_*.py        # Test suites
│   └── fixtures/        # Test data
├── integration/
│   ├── python/          # Python integration
│   ├── typescript/      # TypeScript integration
│   └── ruby/           # Ruby integration
└── deployment/
    ├── Dockerfile       # Container configuration
    ├── docker-compose.yml
    └── .env.example    # Environment variables
```

## Best Practices

### 1. Be Specific
```
Good: "Extract invoice line items with description, quantity, and price"
Better: "Extract invoice line items including description, quantity, unit price, and tax rate, handling multiple currencies"
```

### 2. Specify Integration Needs
```
Good: "Generate BAML with Python integration"
Better: "Generate BAML with async Python FastAPI integration and Redis caching"
```

### 3. Request Optimization
```
"Generate optimized BAML for high-volume extraction (10k+ requests/day)"
```

### 4. Include Edge Cases
```
"Create classifier that handles empty input and malformed data"
```

## Performance Expectations

| Operation | Time | Success Rate |
|-----------|------|--------------|
| Simple Function | <5s | >95% |
| Complex System | <20s | >95% |
| Full Project | <30s | >90% |

| Metric | Target |
|--------|--------|
| First-run Compilation | >95% |
| Token Reduction | >50% |
| Test Coverage | 100% |

## Troubleshooting

### MCP Server Issues
```
Error: "MCP server unavailable"
Solution: Verify installation with commands above
Fallback: Skill uses cached patterns when offline
```

### Generation Failures
```
Error: "Pattern not found"
Solution: Provide more specific requirements
Alternative: Try different pattern category
```

### Validation Errors
```
Error: "Generated code validation failed"
Solution: Report issue with generation ID
Workaround: Request regeneration with constraints
```

## Examples Repository

Access full examples:
```
User: "Show complete extraction example"
User: "Demonstrate classification patterns"
User: "Provide RAG implementation"
```

## Getting Help

- **Documentation**: "Explain BAML [feature]"
- **Patterns**: "Show available patterns for [use case]"
- **Optimization**: "How to optimize for [metric]"
- **Integration**: "Setup [framework] integration"

## Version Updates

The skill automatically stays current by:
- Querying latest repository versions
- Updating syntax rules dynamically
- Learning new patterns from examples
- Adapting to BAML language changes

No manual updates required - MCP servers provide real-time access to latest BAML features.

---

**Quick Start Checklist**:
- [ ] MCP servers installed
- [ ] Connection verified
- [ ] First generation successful
- [ ] Tests passing
- [ ] Integration working

Ready to generate production BAML code in seconds!