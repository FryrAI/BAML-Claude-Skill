# Implementation Plan: [FEATURE]

**Branch**: `[###-feature-name]` | **Date**: [DATE] | **Spec**: [link]
**Input**: Feature specification from `/specs/[###-feature-name]/spec.md`

**Note**: This template is filled in by the `/speckit.plan` command. See `.specify/templates/commands/plan.md` for the execution workflow.

## Summary

[Extract from feature spec: primary requirement + technical approach from research]

## Technical Context

<!--
  ACTION REQUIRED: Replace the content in this section with the technical details
  for the project. The structure here is presented in advisory capacity to guide
  the iteration process.
-->

**Language/Version**: [e.g., Python 3.11, TypeScript 5.0, Ruby 3.2 or NEEDS CLARIFICATION]
**BAML Version**: [e.g., baml-py 0.62.0, @boundaryml/baml 0.62.0 or NEEDS CLARIFICATION]
**MCP Servers**: baml_Docs (REQUIRED), baml_Examples (REQUIRED)
**Primary Dependencies**: [e.g., FastAPI, Express, Rails or NEEDS CLARIFICATION]
**Storage**: [if applicable, e.g., PostgreSQL, Redis, S3 or N/A]
**Testing**: [e.g., pytest, jest, rspec or NEEDS CLARIFICATION]
**Target Platform**: [e.g., Linux server, Docker, Serverless or NEEDS CLARIFICATION]
**Project Type**: [single/web/mobile - determines source structure]
**Performance Goals**: [domain-specific, e.g., <100ms latency, 55% token reduction or NEEDS CLARIFICATION]
**Constraints**: [domain-specific, e.g., <$0.01/request, <1000 tokens/prompt or NEEDS CLARIFICATION]
**Scale/Scope**: [domain-specific, e.g., 10k requests/day, 50 BAML functions or NEEDS CLARIFICATION]

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

- [ ] **Live Repository Learning**: Are patterns derived from actual BAML repository examples?
- [ ] **Pattern-Based Generation**: Does solution adapt real production patterns?
- [ ] **Autonomous Excellence**: Will generated code exceed manual development quality?
- [ ] **Full Stack Coverage**: Are all components included (types to deployment)?
- [ ] **Self-Updating**: Can solution adapt to latest BAML features via MCP?

## Project Structure

### Documentation (this feature)

```text
specs/[###-feature]/
├── plan.md              # This file (/speckit.plan command output)
├── research.md          # Phase 0 output (/speckit.plan command)
├── data-model.md        # Phase 1 output (/speckit.plan command)
├── quickstart.md        # Phase 1 output (/speckit.plan command)
├── contracts/           # Phase 1 output (/speckit.plan command)
└── tasks.md             # Phase 2 output (/speckit.tasks command - NOT created by /speckit.plan)
```

### Source Code (repository root)
<!--
  ACTION REQUIRED: Replace the placeholder tree below with the concrete layout
  for this feature. Delete unused options and expand the chosen structure with
  real paths (e.g., apps/admin, packages/something). The delivered plan must
  not include Option labels.
-->

```text
# [REMOVE IF UNUSED] Option 1: Single project (DEFAULT)
src/
├── models/
├── services/
├── cli/
└── lib/

tests/
├── contract/
├── integration/
└── unit/

# [REMOVE IF UNUSED] Option 2: Web application (when "frontend" + "backend" detected)
backend/
├── src/
│   ├── models/
│   ├── services/
│   └── api/
└── tests/

frontend/
├── src/
│   ├── components/
│   ├── pages/
│   └── services/
└── tests/

# [REMOVE IF UNUSED] Option 3: Mobile + API (when "iOS/Android" detected)
api/
└── [same as backend above]

ios/ or android/
└── [platform-specific structure: feature modules, UI flows, platform tests]
```

**Structure Decision**: [Document the selected structure and reference the real
directories captured above]

## Complexity Tracking

> **Fill ONLY if Constitution Check has violations that must be justified**

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| [e.g., 4th project] | [current need] | [why 3 projects insufficient] |
| [e.g., Repository pattern] | [specific problem] | [why direct DB access insufficient] |
