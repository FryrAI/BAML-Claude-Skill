# Feature Specification: BAML Code Generation Skill

**Feature Branch**: `001-baml-codegen-skill`
**Created**: 2025-01-25
**Status**: Draft
**Input**: User description: "BAML Code Generation Skill that generates production-ready BAML applications by querying official repositories through MCP servers for real-time patterns and syntax"

**Note**: MCP (Model Context Protocol) servers provide programmatic access to the official BoundaryML repositories, enabling real-time pattern extraction and syntax validation.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Generate BAML Code from Requirements (Priority: P1)

A developer needs to create a BAML application for their specific use case. They describe what they want to build (e.g., "I need to extract structured data from invoices") and receive complete, production-ready BAML code that includes type definitions, functions, tests, and integration code.

**Why this priority**: This is the core functionality that delivers immediate value - converting requirements into working BAML code without manual coding.

**Independent Test**: Can be fully tested by providing various requirement descriptions and verifying that complete, compilable BAML code is generated with all necessary components.

**Acceptance Scenarios**:

1. **Given** a developer provides extraction requirements, **When** they request BAML code generation, **Then** they receive complete BAML code with appropriate types, extraction function, tests, and integration templates
2. **Given** a developer provides classification requirements, **When** they request BAML code generation, **Then** they receive optimized classification function with appropriate temperature settings and validation logic
3. **Given** vague or incomplete requirements, **When** the system processes them, **Then** it identifies the most likely pattern and generates appropriate code with reasonable defaults

---

### User Story 2 - Real-Time Pattern Matching from Repositories (Priority: P2)

A developer wants their generated code to match proven production patterns. The system queries official BAML repositories to find similar implementations and adapts them to the specific requirements, ensuring the generated code follows best practices.

**Why this priority**: Ensures generated code quality matches or exceeds manual development by leveraging proven patterns from official sources.

**Independent Test**: Can be tested by verifying that generated code patterns match examples from official repositories and adapt correctly to specific requirements.

**Acceptance Scenarios**:

1. **Given** a request for data extraction, **When** the system generates code, **Then** it matches patterns from official extraction examples in the repositories
2. **Given** a complex multi-step requirement, **When** pattern matching occurs, **Then** the system combines multiple repository patterns intelligently

---

### User Story 3 - Automatic Test and Integration Generation (Priority: P3)

A developer receives not just BAML functions but complete test suites and framework integrations. The system automatically generates comprehensive tests including edge cases and integration code for their chosen framework.

**Why this priority**: Reduces implementation time by providing everything needed for production deployment, not just the core BAML code.

**Independent Test**: Can be tested by verifying that every generated function includes tests with proper coverage and framework-specific integration code.

**Acceptance Scenarios**:

1. **Given** generated BAML functions, **When** test generation completes, **Then** tests cover happy paths, edge cases, and validation scenarios
2. **Given** a target framework preference, **When** integration code generates, **Then** it includes proper async/sync patterns, error handling, and monitoring hooks

---

### User Story 4 - Syntax Validation and Optimization (Priority: P4)

Generated code is automatically validated against the latest BAML syntax rules and optimized for token efficiency. The system ensures all code compiles successfully and performs efficiently.

**Why this priority**: Guarantees that generated code works immediately and costs less to run through automatic optimization.

**Independent Test**: Can be tested by parsing generated code and measuring token usage compared to equivalent manual implementations.

**Acceptance Scenarios**:

1. **Given** generated BAML code, **When** validation runs, **Then** it successfully parses with the BAML compiler
2. **Given** a complex type hierarchy, **When** optimization occurs, **Then** token usage is reduced by at least 55% compared to unoptimized baseline (baseline defined in FR-005: raw API call with verbose JSON schema prompts and no compression techniques)

### Edge Cases

- **MCP servers unavailable**: System falls back to cached patterns (80% functionality retained), warns user of degraded mode, queues updates for when servers return
  - **Retained (80%)**: Core code generation, type synthesis, function generation, test creation, integration code, validation against cached syntax rules, optimization using cached patterns
  - **Degraded (20%)**: Real-time pattern updates from latest repository commits, validation against newest BAML syntax features (uses last cached version), discovery of newly added repository examples, live best practice recommendations
- **Novel requirements with no patterns**: System identifies closest match from cached patterns, generates complete implementation with Conservative Defaults (see Glossary) and inline warnings noting assumptions, logs pattern gap for future repository monitoring
- **Conflicting repository patterns**: System ranks patterns by recency and usage frequency, presents top 3 options to user with trade-off analysis, defaults to most recent
- **Multimodal requirements (image/audio)**: System detects multimodal keywords, includes appropriate image/audio type definitions, generates specialized extraction functions with vision model configurations, validates model compatibility

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST query official BAML repositories to extract current syntax and patterns through specific path queries
- **FR-002**: System MUST generate complete BAML applications including types, functions, tests, integrations, and match user requirements to appropriate repository patterns
- **FR-003**: Users MUST be able to describe requirements in natural language and receive production-ready code
- **FR-004**: System MUST validate all generated code against current BAML grammar and type rules
- **FR-005**: System MUST optimize generated code for token efficiency and performance (55% reduction vs Unoptimized Baseline—see Glossary)
- **FR-006**: System MUST provide comprehensive fallback mechanisms across all components when external repositories are unavailable (80% functionality retained, user notified of degraded mode)
- **FR-007**: System MUST generate framework-specific integration code for at least 6 target platforms (Python, TypeScript, Ruby, Java, Go, C#) where each integration includes:
  - Async/sync execution patterns appropriate to the language
  - Type bindings for function inputs/outputs
  - Error handling with language-idiomatic patterns
  - Client initialization and configuration
  - Example usage code demonstrating function calls
  - Package/dependency management files (requirements.txt, package.json, Gemfile, etc.)
- **FR-008**: System MUST include comprehensive test coverage with all generated functions (happy path, edge cases, performance tests)
- **FR-009**: System MUST stay current with latest BAML features through continuous repository monitoring (daily updates)
- **FR-010**: System MUST track generation performance metrics and costs (<$0.02 per generation)

### Key Entities *(include if feature involves data)*

- **Pattern Library**: Collection of code patterns extracted from official repositories, categorized by use case (extraction, classification, RAG, agents), supporting 1000+ variations
  - **Pattern Variation Definition**: A unique combination of (use_case_type, data_structure_complexity, client_configuration, validation_strategy) extracted from repository examples. For example: "Invoice extraction with nested line items using GPT-4 with retry logic" is one variation, "Invoice extraction with flat structure using Claude without retry" is another.
  - **Measurement Methodology**: Automated repository scanning (task T067a) that:
    1. Traverses all example directories in baml_Examples repository via MCP queries
    2. Parses each .baml file to extract: type structures (flat/nested/recursive), function definitions, client configurations, validation patterns
    3. Categorizes by use_case_type (extraction/classification/RAG/agents)
    4. Measures data_structure_complexity (flat=1 level, nested=2-3 levels, recursive=3+ or self-referential)
    5. Identifies client_configuration (model provider, temperature, max_tokens, retry logic presence)
    6. Detects validation_strategy (none, basic type checking, custom validators, cross-field validation)
    7. Generates unique tuple hash for each distinct (use_case, structure, client, validation) combination
    8. Counts distinct hashes across all examples to reach 1000+ variations target
    9. Validates count stability across multiple scans (variance <5% indicates stable measurement)
- **Syntax Rules**: Current BAML language syntax and grammar rules extracted from parser implementation, updated daily via monitoring
- **Generated Artifact**: Complete package including BAML code, tests, integration templates, and deployment configurations with generation metadata
- **Query Cache**: Session-based storage with 15-minute TTL (optimal for dev sessions), LRU eviction policy, 100MB max size, permanent cache for core syntax

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Generated code compiles successfully on first attempt in >99% of cases (measured over 100 consecutive production generations with ZERO manual edits—code must be used exactly as generated before running `baml-cli validate`)
- **SC-002**: Code generation completes in under 5 seconds for simple functions (<50 lines of BAML code only, single function file), under 30 seconds for complete projects (all artifacts including tests and integration code, >500 total lines)
- **SC-003**: Token usage reduced by 55% or more compared to Unoptimized Baseline (measured as total tokens: prompt + completion per generation request—see Glossary for baseline definition)
- **SC-004**: 100% of generated functions include at least one runnable test (happy path minimum)
- **SC-005**: Generated code matches repository example quality score in 100% of cases (quality metrics defined as: syntax validity = passes `baml-cli validate`, type safety = all types explicitly defined with no `any` types, pattern compliance = structure matches official repository examples for the use case category)
- **SC-006**: Users can go from requirements to deployed application in under 5 minutes (measured from first prompt to running code)
- **SC-007**: System handles 1000+ unique pattern variations without performance degradation (<10% latency increase)
- **SC-008**: Fallback mechanisms activate successfully when repositories unavailable, maintaining 80% functionality (measured by feature availability)
- **SC-009**: Generation cost remains under $0.02 per request (tracked via metrics.md)
- **SC-010**: Skill core remains under 4000 tokens (validated during build)

## Constitution Alignment *(mandatory)*

This feature fully complies with the BAML Code Generation Skill Constitution v2 principles:

| Constitution Principle | Mapped Requirements | Implementation Evidence |
|------------------------|---------------------|-------------------------|
| **I. Live Repository Learning** | FR-001, FR-009, US2 | System queries official BoundaryML repositories via MCP servers for all patterns and syntax (FR-001). Daily repository monitoring ensures continuous learning (FR-009). Pattern matching extracts real production code (US2). |
| **II. Pattern-Based Generation** | FR-002, US2, Edge Cases | Code generation adapts real repository patterns to user requirements (FR-002). Pattern library categorizes 1000+ variations from examples (US2). Novel requirements use closest pattern matches with conservative defaults (Edge Cases). |
| **III. Autonomous Excellence** | FR-005, FR-008, SC-001, SC-005, US4 | Generated code optimized for 55% token reduction (FR-005). 100% test coverage included automatically (FR-008). >99% compilation success without manual edits (SC-001). Quality matches repository examples (SC-005). Comprehensive validation and optimization (US4). |
| **IV. Full Stack Coverage** | FR-002, FR-007, FR-008, US3 | Complete artifacts generated: types, functions, tests, integrations, deployment configs (FR-002). Support for 6 target platforms (FR-007). Automatic test generation with edge cases (FR-008, US3). Framework-specific integration code (US3). |
| **V. Self-Updating** | FR-009, Edge Cases | Daily repository monitoring with validation (FR-009). Real-time pattern updates via MCP queries. Fallback to cached patterns with 80% functionality when servers unavailable (Edge Cases). Continuous adaptation to latest BAML features. |

**Constitution Compliance Status**: ✅ All 5 principles satisfied

**Non-Negotiable Quality Standards Met**:
- First-run success >99% (SC-001)
- Pattern accuracy matches repository examples (SC-005)
- Production-deployable without modification (FR-002, US3)
- Comprehensive error handling and fallback (FR-006, Edge Cases)
- Complete test coverage (FR-008, SC-004)

## Assumptions

- Users have necessary permissions to install and access MCP servers
- Official BAML repositories maintain stable structure and naming conventions
- Generated code targets standard BAML runtime environments
- Network connectivity available for initial pattern library population
- Users provide requirements in English language
- Target deployment environments support generated framework integrations

## Glossary

**Terminology used consistently throughout this specification:**

- **Repository Example**: Actual working code extracted from official BoundaryML repositories (baml_Docs, baml_Examples)
- **Pattern Template**: Synthesized abstraction derived from multiple repository examples, representing a general solution structure
- **Pattern Variation**: A unique combination of (use_case_type, data_structure_complexity, client_configuration, validation_strategy)
- **Use Case Category**: High-level classification of BAML applications (extraction, classification, RAG, agents)
- **MCP Server**: Model Context Protocol server providing programmatic access to BoundaryML repositories
- **Fallback Mode**: Degraded operation using cached patterns when MCP servers are unavailable (80% functionality)
- **Generated Artifact**: Complete package including BAML code, tests, integration code, and deployment configurations
- **Unoptimized Baseline**: The reference implementation used for measuring optimization improvements, defined as a raw API call with verbose JSON schema prompts, explicit field descriptions, no type reuse, no prompt compression techniques, and no caching strategies. All optimization metrics (FR-005, SC-003) measure token reduction against this baseline. Example: A baseline invoice extraction would use inline JSON schema with full field descriptions repeated for each property, versus optimized BAML using compact type definitions and implicit validation.
- **Conservative Defaults**: Fallback configuration values used when requirements are novel or ambiguous: temperature=0.1 (deterministic), max_tokens=500 (safety limit), simple types only (string/int/float/bool), single-pass generation (no retries), basic validation (type checking only), standard client configuration (no custom parameters)