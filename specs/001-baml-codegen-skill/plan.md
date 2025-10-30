# Implementation Plan: BAML Code Generation Skill

**Branch**: `001-baml-codegen-skill` | **Date**: 2025-01-25 | **Spec**: [spec.md](spec.md)
**Input**: Feature specification from `/specs/001-baml-codegen-skill/spec.md`

**Note**: This plan implements a Claude Code skill that generates production-ready BAML code by leveraging MCP servers for real-time repository access.

## Summary

Build a BAML Code Generation Skill that autonomously generates production-ready BAML applications by querying official BoundaryML repositories through MCP servers. The skill will extract patterns, validate syntax, and synthesize complete solutions including types, functions, tests, and integrations - ensuring generated code matches or exceeds manual development quality.

## Technical Context

**Language/Version**: Python 3.11 (skill implementation), TypeScript/Python/Ruby (generated integrations)
**BAML Version**: Latest from baml_Docs repository (dynamically fetched)
**MCP Servers**: baml_Docs (REQUIRED), baml_Examples (REQUIRED)
**Primary Dependencies**: MCP interface libraries, BAML parser (from repository)
**Storage**: Local pattern cache, session-based query cache
**Testing**: pytest for skill tests, BAML test framework for generated code
**Target Platform**: Claude Code runtime environment
**Project Type**: single - Claude Code skill package
**Performance Goals**: <5s simple function (<50 lines BAML code only, single function file), <30s full project (all artifacts including tests and integration code, >500 total lines), 55% token reduction vs Unoptimized Baseline
**Constraints**: <$0.02/generation tracked via metrics, <4000 tokens for skill core (validated), MCP servers required
**Scale/Scope**: 1000+ pattern variations, 100+ daily users, all BAML use cases

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

- [x] **Live Repository Learning**: Are patterns derived from actual BAML repository examples?
  - Yes, all patterns extracted from baml_Docs and baml_Examples via MCP
- [x] **Pattern-Based Generation**: Does solution adapt real production patterns?
  - Yes, synthesis based on repository patterns matched to requirements
- [x] **Autonomous Excellence**: Will generated code exceed manual development quality?
  - Yes, automatic optimization, comprehensive tests, best practices enforced
- [x] **Full Stack Coverage**: Are all components included (types to deployment)?
  - Yes, generates types, functions, tests, integrations, deployment configs
- [x] **Self-Updating**: Can solution adapt to latest BAML features via MCP?
  - Yes, real-time repository queries ensure current syntax and patterns

## Project Structure

### Documentation (this feature)

```text
specs/001-baml-codegen-skill/
   plan.md              # This file (implementation plan)
   research.md          # Phase 0: MCP patterns and skill architecture research
   data-model.md        # Phase 1: Pattern library and cache structures
   quickstart.md        # Phase 1: Skill usage guide
   contracts/           # Phase 1: MCP query interfaces
      mcp-queries.yaml # MCP server query patterns
      generation.yaml  # Code generation API
   tasks.md             # Phase 2: Implementation tasks
```

### Source Code (repository root)

```text
baml-claude-skill/
   SKILL.md             # Main skill definition (~4000 tokens)
   lib/
      mcp_interface.md # MCP server query interface
      pattern_matcher.md # Pattern recognition engine
      pattern_library.md # Pattern library data structure
      code_generator.md # Code synthesis pipeline
      validator.md     # Quality validation framework
      cache_manager.md # Cache management for query results
      pattern_extractor.md # Pattern extraction from repositories
      pattern_adapter.md # Pattern adaptation engine
      requirement_parser.md # Natural language requirement parser
      test_generator.md # Test generation system
      integration_builder.md # Framework integration generator
      deployment_builder.md # Deployment config generator
      optimizer.md     # Code optimization engine
      metrics.md       # Performance and cost metrics
      output_formatter.md # Output formatting utilities
      utils.md         # Error handling and logging
      fallback_patterns.md # Offline fallback patterns
      repository_monitor.md # Continuous repository monitoring
   templates/
      extraction/      # Invoice, resume, receipt patterns
      classification/  # Intent, sentiment, category patterns
      rag/            # Citation, search patterns
      agents/         # Planning, execution patterns
      integrations/    # Framework-specific integration templates
   cache/
      patterns.json   # Cached repository patterns
      syntax.json     # Cached syntax rules
      query_cache.json # Session-based query cache with TTL
   metadata.yaml       # Skill configuration
   TROUBLESHOOTING.md # Error codes and troubleshooting guide

tests/
   unit/              # Skill component tests
   integration/       # MCP integration tests
   generation/        # Generated code validation tests
   performance/       # Performance benchmark tests
```

**Structure Decision**: Single project structure chosen as this is a Claude Code skill package that generates code rather than a deployed application. The skill itself lives in markdown files with supporting templates and caches.

## Complexity Tracking

> No constitution violations - all principles satisfied through MCP-based architecture

## Phase 0: Research & Discovery

### MCP Repository Mapping

**Task**: Document repository structures and key paths

```yaml
baml_docs_paths:
  parser: engine/language/lib/baml-core/src/parser/
  grammar: engine/language/lib/baml-core/src/grammar.pest
  types: engine/language/lib/baml-types/src/
  validation: engine/language/lib/baml-core/src/validate/
  directives: engine/language/lib/baml-core/src/directives/
  clients: engine/language/lib/baml-lib/src/clients/
  tests: engine/language/tests/

baml_examples_paths:
  extraction:
    - extract-receipt/
    - extract-resume/
    - extract-invoice/
  classification:
    - classify-intent/
    - classify-sentiment/
  rag:
    - rag-citations/
    - rag-search/
  agents:
    - agent-planning/
    - multi-agent/
  integrations:
    - python-fastapi-starter/
    - nextjs-starter/
    - ruby-rails/
```

### Pattern Extraction Strategy

**Task**: Define how to extract and categorize patterns

1. Query all example directories via MCP
2. Parse BAML files to extract:
   - Type definitions
   - Function signatures
   - Client configurations
   - Test patterns
3. Categorize by use case (extraction, classification, RAG, agents)
4. Store in structured pattern library

### Skill Architecture Research

**Task**: Design optimal skill loading strategy

```yaml
skill_layers:
  detection: # ~200 tokens
    - Trigger keywords (BAML, LLM, structured)
    - MCP server availability check
    - Activation decision

  core: # ~3800 tokens (validated against limit)
    - MCP query patterns
    - Pattern matching algorithms
    - Code synthesis rules
    - Optimization strategies
    - Quality validators

  dynamic: # MCP-loaded on demand
    - Repository patterns
    - Syntax rules
    - Test templates
    - Integration examples
```

## Phase 1: Design & Architecture

### Data Model

**Note**: Pattern Library entity is defined in [spec.md](spec.md#key-entities) with measurement criteria for 1000+ variations. The structure below provides implementation details.

**Pattern Library Structure**:

```yaml
PatternLibrary:
  patterns:
    extraction:
      triggers: [extract, parse, structure]
      examples: # From MCP queries
        - name: invoice_extraction
          source: baml_Examples/extract-invoice
          types: [Invoice, LineItem]
          functions: [ExtractInvoice]
          tests: [test_extraction.py]
      templates: # Synthesized patterns
        - base_extraction_template
        - multimodal_extraction_template
      optimizations:
        token_reduction: strategies
        prompt_engineering: techniques

    classification:
      # Similar structure

    rag:
      # Similar structure

    agents:
      # Similar structure

SyntaxRules:
  types:
    primitives: [string, int, float, bool, null]
    collections: [array, map]
    complex: [class, enum, union]
  directives:
    function: [@function, @client, @test]
    type: [@description, @alias]
  validation:
    parser_rules: # From grammar.pest
    type_checking: # From validator

QueryCache:
  session:
    queries: Map<query_hash, result>
    ttl: 900 # 15 minutes - optimal for development sessions
    eviction_policy: LRU # Least Recently Used
    max_size: 100MB
    scope: MCP query results, pattern searches, temporary data
  permanent:
    core_syntax: # Never expires, no TTL
    type_definitions: # Never expires, no TTL
    repository_patterns: # Never expires, no TTL
    refresh_check: daily # Via repository_monitor.md - checks for updates without expiring cache
    update_strategy: Validates cached data against repository, updates only if changes detected
```

### API Contracts

**MCP Query Interface**:

```yaml
# contracts/mcp-queries.yaml
mcp_queries:
  get_pattern:
    server: baml_Examples
    query: "**/{pattern_type}/**/*.baml"
    returns: Array<BamlFile>

  get_syntax:
    server: baml_Docs
    query: "engine/language/lib/baml-core/src/parser/"
    returns: SyntaxRules

  validate_code:
    server: baml_Docs
    query: "engine/language/lib/baml-core/src/validate/"
    input: generated_code
    returns: ValidationResult

  get_specific_example:
    server: baml_Examples
    queries:
      - "extract-receipt/"
      - "extract-resume/"
      - "extract-invoice/"
      - "classify-intent/"
      - "classify-sentiment/"
      - "rag-citations/"
      - "rag-search/"
      - "agent-planning/"
      - "multi-agent/"
    returns: ExampleCode
```

**Code Generation API**:

```yaml
# contracts/generation.yaml
generation_api:
  generate:
    input:
      requirements: string
      target_language?: python|typescript|ruby|java|golang|csharp
      optimization_level?: standard|aggressive
      include_multimodal?: boolean # For image/audio support
      include_production_features?: boolean # Monitoring, retry, fallback (default: true)
    output:
      baml_code: string
      tests: Array<TestFile>
      integration: IntegrationCode
      deployment: DeploymentConfig
      production_features:
        monitoring_hooks: MonitoringCode # Telemetry, logging, error tracking
        retry_logic: RetryConfig # Exponential backoff, max retries
        fallback_patterns: FallbackCode # Graceful degradation strategies
      metadata:
        pattern_used: string
        token_count: number
        optimization_savings: percentage
        generation_cost: float # In USD
        generation_time_ms: number
        compilation_success: boolean
```

### Component Interfaces

**MCP Interface**:
```python
class MCPInterface:
    async def query_examples(pattern: str) -> List[Example]
    async def get_syntax(feature: str) -> SyntaxRules
    async def validate(code: str) -> ValidationResult
    async def query_specific_path(path: str) -> str
    async def check_server_availability() -> bool
```

**Pattern Matcher**:
```python
class PatternMatcher:
    def identify_pattern(requirements: str) -> PatternType
    def find_similar(pattern: PatternType) -> List[Example]
    def rank_matches(examples: List[Example]) -> List[RankedMatch]
    def validate_pattern_variations(count: int) -> bool # For 1000+ variations
```

**Code Generator**:
```python
class CodeGenerator:
    async def generate(requirements: str) -> GeneratedCode
    def synthesize(examples: List[Example], requirements: str) -> str
    def optimize(code: str) -> OptimizedCode
    def track_generation_metrics(code: str) -> GenerationMetrics
```

**Quality Validator**:
```python
class QualityValidator:
    def validate_syntax(code: str) -> bool
    def validate_types(code: str) -> bool
    def check_completeness(code: str) -> CompletionStatus
    def measure_quality(code: str) -> QualityMetrics
    def validate_token_count() -> bool # Ensure <4000 tokens
```

**Repository Monitor**:
```python
class RepositoryMonitor:
    async def check_updates() -> UpdateStatus
    def schedule_monitoring() -> None  # Implements cron-style daily scheduler at 00:00 UTC
    def update_pattern_cache() -> None
    def track_feature_changes() -> List[Change]
    def validate_before_update(new_patterns: List[Pattern]) -> bool  # Validate patterns compile before cache update
    def rollback_on_failure() -> None  # Restore previous cache version if validation fails

    # Update triggers:
    # - Scheduled: Daily at 00:00 UTC via internal cron
    # - Manual: User can trigger via /baml-skill update command
    # - Future: Webhook from BoundaryML repositories (not in v1)
```

### Quickstart Guide

```markdown
# BAML Code Generation Skill - Quick Start

## Prerequisites
1. Install MCP servers:
   ```bash
   claude mcp add "baml_Docs" --scope user -- npx -y mcp-remote https://gitmcp.io/BoundaryML/baml
   claude mcp add "baml_Examples" -- npx -y mcp-remote https://gitmcp.io/BoundaryML/baml-examples
   ```

## Basic Usage
```
User: "Generate BAML code to extract invoice data"
Skill: [Generates complete BAML with Invoice type, ExtractInvoice function, tests, and integration]
```

## Advanced Features
- Pattern matching from repositories
- Automatic optimization (55% token reduction vs Unoptimized Baseline)
- Test generation
- Framework integrations (Python, TypeScript, Ruby, Java, Go, C#)
- Multimodal support (image/audio)
- Performance tracking (<$0.02/generation)
- Repository monitoring for updates

## Examples
1. Extraction: "Create BAML to parse receipts"
2. Classification: "Build sentiment classifier"
3. RAG: "Generate citation-aware search"
4. Agents: "Create planning agent"
5. Multimodal: "Extract data from images"

## Performance Targets
- Simple functions (<50 lines): <5 seconds
- Complete projects: <30 seconds
- Compilation success rate: >95%
- Deployment time: <5 minutes
```

## Phase 2: Implementation Planning

The implementation phase will be handled by the `/speckit.tasks` command, which will generate:
- Detailed task breakdown
- Dependency management
- Parallel execution opportunities
- Testing strategy
- Deployment process

Key implementation areas:
1. MCP server integration with specific path queries
2. Pattern recognition engine with 1000+ variation support
3. Code synthesis pipeline
4. Test generation system
5. Quality validation framework
6. Caching and optimization with LRU eviction
7. Performance and cost tracking
8. Repository monitoring for continuous updates
9. Multimodal support handling
10. Extended framework support (6+ languages)

---

**Next Steps**:
1. Execute Phase 0 research to map repositories
2. Run Phase 1 design to create data models and contracts
3. Use `/speckit.tasks` to generate implementation tasks
4. Begin development with MCP server setup