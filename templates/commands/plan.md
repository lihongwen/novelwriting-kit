---
description: Execute the planning workflow. For novels - create detailed chapter/scene breakdown. For software - generate implementation plan with design artifacts.
scripts:
  sh: scripts/bash/setup-plan.sh --json
  ps: scripts/powershell/setup-plan.ps1 -Json
---

The user input to you can be provided directly by the agent or as a command argument - you **MUST** consider it before proceeding with the prompt (if not empty).

User input:

$ARGUMENTS

Given the planning details provided as an argument, do this:

1. Run `{SCRIPT}` from the repo root and parse JSON for FEATURE_SPEC, IMPL_PLAN, SPECS_DIR, BRANCH. All future file paths must be absolute.
   - BEFORE proceeding, inspect FEATURE_SPEC for a `## Clarifications` section with at least one `Session` subheading. If missing or clearly ambiguous areas remain (vague adjectives, unresolved critical choices), PAUSE and instruct the user to run `/clarify` first to reduce rework. Only continue if: (a) Clarifications exist OR (b) an explicit user override is provided (e.g., "proceed without clarification"). Do not attempt to fabricate clarifications yourself.

2. Read and analyze the specification to understand:
   - **Detect project type** from spec content:
     * **Novel writing**: Story Beats, Character Arcs, Foreshadowing Map, Timeline
     * **Software**: Functional Requirements, User Stories, API contracts
   - Extract requirements, goals, constraints, and success criteria

3. Read the constitution at `/memory/constitution.md` to understand governing principles.

4. Execute the appropriate planning template based on project type:

   **For Novel Writing Projects**:
   - Load `/templates/plan-template.md` (already copied to IMPL_PLAN path)
   - Set Input path to FEATURE_SPEC
   - Run the Execution Flow steps 1-9 for **Chapter Planning**:
     * Fill Narrative Context (POV, voice, chapter structure, pacing)
     * Run Constitution Check (World Consistency, Character Integrity, Foreshadowing, Timeline, Pacing gates)
     * Phase 0: Research historical/technical details for accuracy
     * Phase 1: Generate scene-breakdown.md (detailed scene-by-scene plan with emotional arcs, foreshadowing markers)
     * Phase 1: Generate character-states.md (track character development chapter-by-chapter)
     * Phase 1: Generate continuity-check.md (timeline verification, foreshadowing status tracking)
     * Phase 2: Describe writing task generation approach (DO NOT create tasks.md)
   - Incorporate user-provided details from arguments into Narrative Context: {ARGS}
   - **Critical for novels**: Ensure every scene has:
     * Clear purpose (plot/character/info/foreshadowing)
     * Emotional arc (start → conflict → end)
     * Foreshadowing tracking (plant/hint/payoff)
     * Continuity verification (timeline, character knowledge, world state)

   **For Software Projects**:
   - Load `/templates/plan-template.md`
   - Set Input path to FEATURE_SPEC
   - Run the Execution Flow steps 1-9 for **Implementation Planning**:
     * Fill Technical Context (language, dependencies, storage, testing)
     * Run Constitution Check (Library-First, CLI Interface, Test-First, etc.)
     * Phase 0: Generate research.md (technology decisions, best practices)
     * Phase 1: Generate contracts/ (API specifications)
     * Phase 1: Generate data-model.md (entities, relationships)
     * Phase 1: Generate quickstart.md (validation scenarios)
     * Phase 2: Describe task generation approach (DO NOT create tasks.md)
   - Incorporate user-provided details from arguments into Technical Context: {ARGS}

5. Verify execution completed:
   - Check Progress Tracking shows all phases complete
   - Ensure all required artifacts were generated in $SPECS_DIR:
     * **Novels**: research.md, scene-breakdown.md, character-states.md, continuity-check.md
     * **Software**: research.md, data-model.md, contracts/, quickstart.md
   - Confirm no ERROR states in execution

6. Report results with branch name, file paths, and generated artifacts.

Use absolute paths with the repository root for all file operations to avoid path issues.

**Important reminders**:
- The template is self-contained and executable
- Follow error handling and gate checks as specified
- Update Progress Tracking as you complete each phase
- **For novels**: Scene breakdown is the most critical artifact - every scene must have purpose and tracking
- **For software**: Contracts and data model drive implementation
- Phase 2 (tasks.md generation) is handled by the `/tasks` command, NOT `/plan`
