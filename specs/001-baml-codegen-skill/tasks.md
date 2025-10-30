---

description: "Task list for BAML Code Generation Skill implementation"
---

# Tasks: BAML Code Generation Skill

**Input**: Design documents from `/specs/001-baml-codegen-skill/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, contracts/

**Tests**: Tests are included as requested for validating the skill functionality

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3, US4)
- Include exact file paths in descriptions

## Path Conventions

- **Single project**: `baml-claude-skill/` at repository root
- **Tests**: `tests/` at repository root
- **Documentation**: `specs/001-baml-codegen-skill/`

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Project initialization and skill structure

- [X] T001 Create skill directory structure at baml-claude-skill/
- [X] T002 [P] Initialize SKILL.md with core structure (4000 token budget)
- [X] T003 [P] Create metadata.yaml with skill configuration
- [X] T004 [P] Set up cache directory structure at baml-claude-skill/cache/
- [X] T005 [P] Create lib directory for skill modules at baml-claude-skill/lib/
- [X] T006 [P] Initialize templates directory structure at baml-claude-skill/templates/
- [X] T006a Validate MCP server availability (baml_Docs, baml_Examples) and provide clear error if missing

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Core MCP integration that MUST be complete before ANY user story can be implemented

**⚠️ CRITICAL**: No user story work can begin until this phase is complete

- [X] T007 Implement MCP interface base class in baml-claude-skill/lib/mcp_interface.md
- [X] T008 Create MCP query patterns for baml_Docs server in baml-claude-skill/lib/mcp_interface.md
- [X] T009 Implement MCP connection validation and fallback logic in baml-claude-skill/lib/mcp_interface.md
- [X] T010 [P] Create pattern library data structure in baml-claude-skill/lib/pattern_library.md
- [X] T011 [P] Implement cache manager for query results in baml-claude-skill/lib/cache_manager.md
- [X] T012 Set up error handling and logging framework in baml-claude-skill/lib/utils.md

**Checkpoint**: Foundation ready - user story implementation can now begin in parallel

---

## Phase 3: User Story 1 - Generate BAML Code from Requirements (Priority: P1) 🎯 MVP

**Goal**: Convert natural language requirements into complete, production-ready BAML code

**Independent Test**: Provide various requirements and verify complete BAML generation

### Tests for User Story 1 ⚠️

> **NOTE: Write these tests FIRST, ensure they FAIL before implementation**

- [ ] T013 [P] [US1] Create test for extraction requirement parsing in tests/unit/test_requirement_parser.py
- [ ] T014 [P] [US1] Create test for classification requirement parsing in tests/unit/test_requirement_parser.py
- [ ] T015 [P] [US1] Create integration test for end-to-end generation in tests/integration/test_generation_pipeline.py
- [ ] T015a [P] [US1] Create test for multimodal requirement detection in tests/unit/test_multimodal_detection.py

### Implementation for User Story 1

- [ ] T016 [US1] Implement requirement parser in baml-claude-skill/lib/requirement_parser.md
- [ ] T016a [P] [US1] Extend requirement parser with multimodal keyword detection (image, audio, vision, OCR) in baml-claude-skill/lib/requirement_parser.md#multimodal
- [ ] T016b [P] [US1] Implement vision model configuration generator in baml-claude-skill/lib/code_generator.md#vision_models
- [ ] T016c [P] [US1] Create multimodal type generator (image, audio types) in baml-claude-skill/lib/code_generator.md#multimodal_types
- [ ] T017 [US1] Create pattern matcher for requirement analysis in baml-claude-skill/lib/pattern_matcher.md
- [ ] T018 [P] [US1] Implement code synthesis engine in baml-claude-skill/lib/code_generator.md
- [ ] T019 [P] [US1] Create type generator for BAML types in baml-claude-skill/lib/code_generator.md#types
- [ ] T020 [P] [US1] Create function generator for BAML functions in baml-claude-skill/lib/code_generator.md#functions
- [ ] T021 [US1] Implement template selection logic in baml-claude-skill/lib/pattern_matcher.md#templates
- [ ] T022 [US1] Create output formatter for generated code in baml-claude-skill/lib/output_formatter.md
- [ ] T023 [US1] Add generation metadata tracking in baml-claude-skill/lib/code_generator.md#metadata

**Checkpoint**: At this point, User Story 1 should be fully functional and testable independently

---

## Phase 4: User Story 2 - Real-Time Pattern Matching from Repositories (Priority: P2)

**Goal**: Query and adapt patterns from official BAML repositories

**Independent Test**: Verify patterns match official repository examples

### Tests for User Story 2 ⚠️

- [ ] T024 [P] [US2] Create test for MCP repository queries in tests/integration/test_mcp_queries.py
- [ ] T025 [P] [US2] Create test for pattern extraction from examples in tests/unit/test_pattern_extraction.py
- [ ] T026 [P] [US2] Create test for pattern adaptation logic in tests/unit/test_pattern_adaptation.py

### Implementation for User Story 2

- [ ] T027 [US2] Implement repository query builder for baml_Docs in baml-claude-skill/lib/mcp_interface.md#query_builder
- [ ] T028 [P] [US2] Create pattern extractor for extraction examples in baml-claude-skill/lib/pattern_extractor.md#extraction
- [ ] T029 [P] [US2] Create pattern extractor for classification examples in baml-claude-skill/lib/pattern_extractor.md#classification
- [ ] T030 [P] [US2] Create pattern extractor for RAG examples in baml-claude-skill/lib/pattern_extractor.md#rag
- [ ] T031 [P] [US2] Create pattern extractor for agent examples in baml-claude-skill/lib/pattern_extractor.md#agents
- [ ] T032 [US2] Implement pattern similarity scoring in baml-claude-skill/lib/pattern_matcher.md#similarity
- [ ] T033 [US2] Create pattern adaptation engine in baml-claude-skill/lib/pattern_adapter.md
- [ ] T034 [US2] Implement repository structure mapper in baml-claude-skill/lib/mcp_interface.md#structure_map
- [ ] T034a [P] [US2] Query specific extraction example paths (extract-receipt/, extract-resume/, extract-invoice/) via MCP
- [ ] T034b [P] [US2] Query specific classification example paths (classify-intent/, classify-sentiment/) via MCP
- [ ] T034c [P] [US2] Query specific RAG example paths (rag-citations/, rag-search/) via MCP
- [ ] T034d [P] [US2] Query specific agent example paths (agent-planning/, multi-agent/) via MCP

**Checkpoint**: At this point, User Stories 1 AND 2 should both work independently

---

## Phase 5: User Story 3 - Automatic Test and Integration Generation (Priority: P3)

**Goal**: Generate comprehensive test suites and framework integrations

**Independent Test**: Verify every function has tests and integration code

### Tests for User Story 3 ⚠️

- [ ] T035 [P] [US3] Create test for test generation coverage in tests/unit/test_test_generator.py
- [ ] T036 [P] [US3] Create test for Python integration generation in tests/unit/test_integration_python.py
- [ ] T037 [P] [US3] Create test for TypeScript integration generation in tests/unit/test_integration_typescript.py
- [ ] T037a [P] [US3] Create test for Ruby integration generation in tests/unit/test_integration_ruby.py
- [ ] T037b [P] [US3] Create test for Java integration generation in tests/unit/test_integration_java.py
- [ ] T037c [P] [US3] Create test for Go integration generation in tests/unit/test_integration_go.py
- [ ] T037d [P] [US3] Create test for C# integration generation in tests/unit/test_integration_csharp.py

### Implementation for User Story 3

- [ ] T038 [US3] Implement test generator base class in baml-claude-skill/lib/test_generator.md
- [ ] T039 [P] [US3] Create happy path test generator in baml-claude-skill/lib/test_generator.md#happy_path
- [ ] T040 [P] [US3] Create edge case test generator in baml-claude-skill/lib/test_generator.md#edge_cases
- [ ] T041 [P] [US3] Create performance test generator in baml-claude-skill/lib/test_generator.md#performance
- [ ] T042 [P] [US3] Implement Python integration generator in baml-claude-skill/lib/integration_builder.md#python
- [ ] T043 [P] [US3] Implement TypeScript integration generator in baml-claude-skill/lib/integration_builder.md#typescript
- [ ] T044 [P] [US3] Implement Ruby integration generator in baml-claude-skill/lib/integration_builder.md#ruby
- [ ] T044a [P] [US3] Implement Java integration generator in baml-claude-skill/lib/integration_builder.md#java
- [ ] T044b [P] [US3] Implement Go integration generator in baml-claude-skill/lib/integration_builder.md#go
- [ ] T044c [P] [US3] Implement C# integration generator in baml-claude-skill/lib/integration_builder.md#csharp
- [ ] T045 [US3] Create framework-specific templates in baml-claude-skill/templates/integrations/
- [ ] T046 [US3] Implement deployment config generator in baml-claude-skill/lib/deployment_builder.md
- [ ] T046a [P] [US3] Generate monitoring hooks (telemetry, logging, error tracking) in baml-claude-skill/lib/integration_builder.md#monitoring
- [ ] T046b [P] [US3] Generate retry logic patterns (exponential backoff, max retries) in baml-claude-skill/lib/integration_builder.md#retry
- [ ] T046c [P] [US3] Generate fallback patterns for graceful degradation in baml-claude-skill/lib/integration_builder.md#fallback

**Checkpoint**: All user stories (1, 2, 3) should now be independently functional

---

## Phase 6: User Story 4 - Syntax Validation and Optimization (Priority: P4)

**Goal**: Validate and optimize generated code for correctness and efficiency

**Independent Test**: Verify code validates and achieves >50% token reduction

### Tests for User Story 4 ⚠️

- [ ] T047 [P] [US4] Create test for syntax validation in tests/unit/test_syntax_validator.py
- [ ] T048 [P] [US4] Create test for token optimization in tests/unit/test_optimizer.py
- [ ] T049 [P] [US4] Create test for performance metrics in tests/integration/test_performance.py

### Implementation for User Story 4

- [ ] T050 [US4] Implement syntax validator using MCP queries in baml-claude-skill/lib/validator.md#syntax
- [ ] T051 [P] [US4] Create type validator for BAML types in baml-claude-skill/lib/validator.md#types
- [ ] T052 [P] [US4] Create semantic validator for logic correctness in baml-claude-skill/lib/validator.md#semantic
- [ ] T053 [US4] Implement token optimizer for prompt compression in baml-claude-skill/lib/optimizer.md#tokens
- [ ] T054 [P] [US4] Create type simplification optimizer in baml-claude-skill/lib/optimizer.md#types
- [ ] T055 [P] [US4] Create caching strategy optimizer in baml-claude-skill/lib/optimizer.md#caching
- [ ] T056 [US4] Implement performance metrics collector in baml-claude-skill/lib/metrics.md
- [ ] T057 [US4] Create optimization report generator in baml-claude-skill/lib/optimizer.md#reporting
- [ ] T057a [US4] Add generation cost tracking (<$0.02 per generation) in baml-claude-skill/lib/metrics.md#cost_tracking
- [ ] T057b [US4] Add generation time tracking for simple vs complex functions in baml-claude-skill/lib/metrics.md#performance
- [ ] T057c [US4] Validate SKILL.md token count remains under 4000 tokens in tests/unit/test_skill_validation.py
- [ ] T057d [US4] Add compilation success rate tracking (>95% target) in baml-claude-skill/lib/metrics.md#success_rate

**Checkpoint**: All four user stories should now be complete and independently testable

---

## Phase 7: Polish & Cross-Cutting Concerns

**Purpose**: Improvements that affect multiple user stories

- [ ] T058 [P] Create comprehensive examples in baml-claude-skill/templates/extraction/
- [ ] T059 [P] Create comprehensive examples in baml-claude-skill/templates/classification/
- [ ] T060 [P] Create comprehensive examples in baml-claude-skill/templates/rag/
- [ ] T061 [P] Create comprehensive examples in baml-claude-skill/templates/agents/
- [ ] T062 Update SKILL.md with complete implementation (~3800 tokens)
- [ ] T063 [P] Optimize cache strategies for performance in baml-claude-skill/lib/cache_manager.md
- [ ] T063a [P] Validate cache TTL behavior (15-min session cache, LRU eviction, daily permanent cache refresh) in tests/unit/test_cache_manager.py
- [ ] T064 [P] Add telemetry and usage tracking in baml-claude-skill/lib/metrics.md
- [ ] T065 Create comprehensive fallback patterns for MCP unavailability in baml-claude-skill/lib/fallback_patterns.md
- [ ] T065a [P] Add fallback handling in pattern matcher (baml-claude-skill/lib/pattern_matcher.md#fallback)
- [ ] T065b [P] Add fallback handling in code generator (baml-claude-skill/lib/code_generator.md#fallback)
- [ ] T065c [P] Add fallback handling in validator (baml-claude-skill/lib/validator.md#fallback)
- [ ] T065d Validate 80% functionality retention during fallback mode in tests/integration/test_fallback.py
- [ ] T065e [P] Implement MCP reconnection logic with exponential backoff in baml-claude-skill/lib/mcp_interface.md#reconnection
- [ ] T065f [P] Add fallback handling in test generator (baml-claude-skill/lib/test_generator.md#fallback)
- [ ] T065g [P] Add fallback handling in integration builder (baml-claude-skill/lib/integration_builder.md#fallback)
- [ ] T065h [P] Add fallback handling in deployment builder (baml-claude-skill/lib/deployment_builder.md#fallback)
- [ ] T065i [P] Add fallback handling in optimizer (baml-claude-skill/lib/optimizer.md#fallback)
- [ ] T065j [P] Add fallback handling in pattern extractor (baml-claude-skill/lib/pattern_extractor.md#fallback)
- [ ] T065k [P] Add fallback handling in repository monitor (baml-claude-skill/lib/repository_monitor.md#fallback)
- [ ] T066 [P] Run end-to-end validation tests in tests/integration/
- [ ] T067 [P] Performance benchmark all generation scenarios in tests/performance/
- [ ] T067a Test system with 1000+ pattern variations in tests/performance/test_pattern_variations.py
- [ ] T067b Validate <10% latency increase with 1000+ patterns in tests/performance/test_latency.py
- [ ] T067c Create end-to-end deployment timing test (requirements to deployed app <5 min) in tests/integration/test_deployment_timing.py
- [ ] T068 Update quickstart.md with final usage examples
- [ ] T069 Document error codes and troubleshooting in baml-claude-skill/TROUBLESHOOTING.md
- [ ] T070 Implement continuous repository monitoring in baml-claude-skill/lib/repository_monitor.md
- [ ] T070a Add daily update scheduler (cron-style at 00:00 UTC) in baml-claude-skill/lib/repository_monitor.md#scheduler
- [ ] T070b Create feature change tracking in baml-claude-skill/lib/repository_monitor.md#changes
- [ ] T070c Update pattern cache on repository changes in baml-claude-skill/lib/repository_monitor.md#cache_update
- [ ] T070d Implement validation before cache update in baml-claude-skill/lib/repository_monitor.md#validation
- [ ] T070e Create rollback mechanism for failed updates in baml-claude-skill/lib/repository_monitor.md#rollback
- [ ] T070f Add manual update trigger command in baml-claude-skill/lib/repository_monitor.md#manual_trigger
- [ ] T070g [P] Implement network error handling and retry logic for repository monitoring in baml-claude-skill/lib/repository_monitor.md#error_handling
- [ ] T071 Package skill for deployment

**Checkpoint**: All user stories validated, optimization complete, documentation updated, skill ready for production deployment

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately
- **Foundational (Phase 2)**: Depends on Setup completion - BLOCKS all user stories
- **User Stories (Phase 3+)**: All depend on Foundational phase completion
  - User stories can then proceed in parallel (if staffed)
  - Or sequentially in priority order (P1 → P2 → P3 → P4)
- **Polish (Phase 7)**: Depends on all desired user stories being complete

### User Story Dependencies

- **User Story 1 (P1)**: Can start after Foundational (Phase 2) - No dependencies on other stories
- **User Story 2 (P2)**: Can start after Foundational (Phase 2) - Enhances US1 but independently testable
- **User Story 3 (P3)**: Can start after Foundational (Phase 2) - Builds on US1 output but independently testable
- **User Story 4 (P4)**: Can start after Foundational (Phase 2) - Validates any generated code independently

### Within Each User Story

- Tests MUST be written and FAIL before implementation
- Core implementation before optimizations
- Story complete before moving to next priority

### Parallel Opportunities

- All Setup tasks marked [P] can run in parallel
- All Foundational tasks marked [P] can run in parallel after T007-T009 complete
- Once Foundational phase completes, all user stories can start in parallel
- All tests for a user story marked [P] can run in parallel
- All template/example creation tasks marked [P] can run in parallel

---

## Parallel Example: User Story 1

```bash
# Launch all tests for User Story 1 together:
Task: "Create test for extraction requirement parsing in tests/unit/test_requirement_parser.py"
Task: "Create test for classification requirement parsing in tests/unit/test_requirement_parser.py"
Task: "Create integration test for end-to-end generation in tests/integration/test_generation_pipeline.py"

# After requirement parser (T016) and pattern matcher (T017) complete, launch generators in parallel:
Task: "Implement code synthesis engine in baml-claude-skill/lib/code_generator.md"
Task: "Create type generator for BAML types in baml-claude-skill/lib/code_generator.md#types"
Task: "Create function generator for BAML functions in baml-claude-skill/lib/code_generator.md#functions"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup
2. Complete Phase 2: Foundational (CRITICAL - blocks all stories)
3. Complete Phase 3: User Story 1
4. **STOP and VALIDATE**: Test User Story 1 independently
5. Deploy/demo if ready

### Incremental Delivery

1. Complete Setup + Foundational → Foundation ready
2. Add User Story 1 → Test independently → Deploy/Demo (MVP!)
3. Add User Story 2 → Test independently → Deploy/Demo
4. Add User Story 3 → Test independently → Deploy/Demo
5. Add User Story 4 → Test independently → Deploy/Demo
6. Each story adds value without breaking previous stories

### Parallel Team Strategy

With multiple developers:

1. Team completes Setup + Foundational together
2. Once Foundational is done:
   - Developer A: User Story 1 (T013-T023)
   - Developer B: User Story 2 (T024-T034)
   - Developer C: User Story 3 (T035-T046)
   - Developer D: User Story 4 (T047-T057)
3. Stories complete and integrate independently

---

## Notes

- [P] tasks = different files, no dependencies
- [Story] label maps task to specific user story for traceability
- Each user story should be independently completable and testable
- Verify tests fail before implementing
- Commit after each task or logical group
- Stop at any checkpoint to validate story independently
- Total tasks: 119 (7 setup + 6 foundational + 15 US1 + 19 US2 + 18 US3 + 15 US4 + 39 polish)
- Task ID format: T### with letter suffixes (a, b, c) for parallel sub-tasks added during refinement