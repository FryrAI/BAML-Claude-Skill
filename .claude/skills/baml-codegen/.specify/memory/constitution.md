<!-- Sync Impact Report
Version Change: 1.0.0 → 2.0.0 (Major revision - MCP integration)
Modified Principles:
  - Code Generation First → Live Repository Learning
  - Full Stack BAML → Pattern-Based Generation
  - Pattern Recognition → Autonomous Excellence
  - Self-Debugging → Full Stack Coverage
  - Performance Aware → Self-Updating
Added Sections:
  - Primary Goals
  - Technical Foundation
  - Quality Standards
  - Operational Requirements
Removed Sections:
  - Primary Capabilities (replaced by Technical Foundation)
Templates Requiring Updates:
  ✅ plan-template.md - Updated for MCP integration
  ✅ spec-template.md - Updated for repository patterns
  ✅ tasks-template.md - No changes needed
  ✅ checklist-template.md - No changes needed
  ✅ agent-file-template.md - No changes needed
Follow-up TODOs: None
-->

# BAML Code Generation Skill Constitution v2

## Purpose

Enable Claude Code to autonomously write, debug, and optimize production-ready
BAML applications by leveraging real-time access to official repositories
through MCP servers.

## Core Principles

### I. Live Repository Learning
Use MCP servers to access actual BAML implementations. Every pattern, syntax,
and best practice must be derived from the official BoundaryML repositories.
No outdated knowledge or assumptions - only real, working code from the source.

### II. Pattern-Based Generation
Extract and adapt real patterns from production code. Analyze repository
examples to understand context-appropriate solutions. Match use cases to
existing patterns and adapt them intelligently rather than inventing new
approaches.

### III. Autonomous Excellence
Generate better code than manual development. Every generated solution must
meet or exceed the quality of hand-written code through comprehensive testing,
optimization, and error handling. No human intervention required for production
deployment.

### IV. Full Stack Coverage
From types to deployment, everything included. Generate complete solutions
spanning type definitions, BAML functions, client integrations, test suites,
CI/CD pipelines, and deployment configurations. No component left unimplemented.

### V. Self-Updating
Stay current with latest BAML features via MCP. Continuously query repositories
for new patterns, syntax changes, and best practices. Adapt generation strategies
based on the latest available examples and documentation.

## Primary Goals

- **Generate Production Code**: Every output is deployable, not educational
- **Learn from Source**: Use actual repository code as the source of truth
- **Include Everything**: Types, functions, tests, integrations, deployments
- **Optimize Automatically**: Token reduction, latency, cost optimization built-in
- **Stay Current**: Real-time access to latest syntax and patterns

## Technical Foundation

### MCP Servers (Required)

The following MCP servers MUST be installed and accessible:
- `baml_Docs`: BoundaryML/baml repository for core implementation
- `baml_Examples`: BoundaryML/baml-examples for production patterns

### Core Competencies

- Project scaffolding with proper structure
- Type system design and optimization
- Function engineering with best practices
- Test generation with edge cases
- Integration code for Python/TypeScript/Ruby
- Deployment configurations (Docker, K8s, serverless)

## Success Metrics

All generated code must meet these quantifiable standards:
- **First-Run Success**: >95% - Generated code runs without modification
- **Parsing Success**: >99% - Code compiles with Semantic Analysis Pipeline
- **Token Efficiency**: 55% reduction vs JSON schemas
- **Test Coverage**: 100% auto-generated for all functions
- **Deployment Ready**: Includes monitoring, retry, fallback mechanisms
- **Pattern Accuracy**: Matches repository examples exactly

## Quality Standards

Every generated artifact MUST:
1. Match or exceed repository example quality
2. Include comprehensive error handling
3. Provide complete test coverage
4. Follow BAML best practices from source
5. Be production-deployable without modification

## Non-Goals

This constitution explicitly excludes:
- Teaching or explaining BAML concepts
- Creating documentation or tutorials
- Manual assistance or debugging help
- Operating without MCP servers
- Generating suboptimal or example code

## Operational Requirements

- MCP servers MUST be installed and accessible for optimal operation
- Real-time repository queries for pattern matching
- Dynamic learning from new examples
- Continuous syntax validation against source
- Automatic fallback to cached patterns if MCP unavailable (with user notification)

### Fallback Mode Operation

When MCP servers are unavailable:
1. System MUST notify user of degraded mode operation
2. Generation continues using cached repository patterns (80% functionality retained)
3. Advanced features (real-time pattern updates, latest syntax validation) are disabled
4. User is warned that generated code may not reflect latest BAML features
5. System queues repository updates for when servers return

Fallback mode ensures continuity while maintaining transparency about limitations.

## Governance

The Constitution supersedes all other practices and guidelines. Amendments
require:
1. Clear justification demonstrating improved code generation
2. Impact analysis on MCP server dependencies
3. Validation against repository examples
4. Version increment following semantic versioning

All code generation MUST verify compliance with these principles. Quality
standards are non-negotiable, but fallback mode with user notification is
permitted to ensure developer productivity during MCP server outages.

**Version**: 2.0.0 | **Ratified**: 2025-01-25 | **Last Amended**: 2025-01-25