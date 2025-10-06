---
description: Generate executable task list. For novels - break down scenes into writing tasks with quality checks. For software - create implementation tasks from technical plan.
scripts:
  sh: scripts/bash/check-prerequisites.sh --json --paths-only
  ps: scripts/powershell/check-prerequisites.ps1 -Json -PathsOnly
---

The user input to you can be provided directly by the agent or as a command argument - you **MUST** consider it before proceeding with the prompt (if not empty).

User input:

$ARGUMENTS

Given any user guidance, do this:

1. Run `{SCRIPT}` from repo root and parse JSON for FEATURE_DIR, FEATURE_SPEC, IMPL_PLAN. All paths must be absolute.
   - If plan.md is missing, instruct user to run `/plan` first.

2. Load and analyze planning documents:
   - **REQUIRED**: Read plan.md to understand the scope and structure
   - **Detect project type** from plan.md content:
     * **Novel writing**: Narrative Context, scene-breakdown.md, character-states.md, continuity-check.md
     * **Software**: Technical Context, data-model.md, contracts/, research.md

3. **For Novel Writing Projects**:
   - Load `/templates/tasks-template.md` as base structure
   - Parse scene-breakdown.md:
     * Extract all chapters and scenes
     * Note scene purposes (plot/character/info/foreshadowing)
     * Identify emotional arcs and key events
   - Parse character-states.md:
     * Extract character development tracking requirements
   - Parse continuity-check.md:
     * Extract foreshadowing tracking tasks
     * Extract timeline update requirements
   
   Generate writing tasks by category:
   - **Setup**: Chapter directory structure, tracking file initialization (characters/, foreshadowing/, timeline/)
   - **Chapter Writing**: Scene drafts (one task per scene)
   - **Integration**: Scene-to-scene transitions, chapter flow
   - **Quality Tracking**: Foreshadowing updates, timeline updates, character state updates
   - **Arc Reviews**: Every 10 chapters - consistency audits
   - **Revision**: Chapter-level polish after first draft

   Apply task rules for novels:
   - Scenes in different chapters = mark [P] for parallel writing
   - Scenes in same chapter = sequential (Scene 1 → Scene 2 → Scene 3)
   - Quality tracking tasks = after each chapter completion
   - Arc-level audits = every 10 chapters
   - Each writing task must reference:
     * Exact file path (chapters/###-title.md)
     * Scene number and purpose
     * Foreshadowing to plant/hint/payoff
     * Character states to track

4. **For Software Projects**:
   - Load `/templates/tasks-template.md` as base structure
   - Parse data-model.md → entity creation tasks
   - Parse contracts/ → contract test tasks
   - Parse plan.md → implementation tasks
   
   Generate implementation tasks by category:
   - **Setup**: Project init, dependencies, linting
   - **Tests First (TDD)**: Contract tests, integration tests (MUST come before implementation)
   - **Core Implementation**: Models, services, CLI, endpoints
   - **Integration**: DB, middleware, logging
   - **Polish**: Unit tests, performance, docs

   Apply task rules for software:
   - Different files = mark [P] for parallel execution
   - Same file = sequential
   - Tests before implementation (TDD)
   - Each task must reference exact file path

5. Number tasks sequentially (T001, T002, ...).

6. Generate dependency graph showing task execution order.

7. Create parallel execution examples showing which tasks can run simultaneously.

8. Validate task completeness:
   - **For novels**:
     * All scenes have writing tasks?
     * All chapters have integration and tracking tasks?
     * Arc-level audits scheduled appropriately?
     * Foreshadowing/timeline/character updates included?
   - **For software**:
     * All contracts have tests?
     * All entities have models?
     * All endpoints implemented?
     * Tests come before implementation?

9. Write tasks.md to FEATURE_DIR with complete task breakdown.

10. Report completion:
    - Total task count
    - Task categories breakdown
    - Estimated parallel execution opportunities
    - Path to tasks.md
    - Suggested next command: `/implement`

**Critical task generation rules**:

For novels:
- **Granularity**: One task per scene (not per chapter)
- **Tracking**: Separate tasks for foreshadowing/timeline/character updates after each chapter
- **Quality gates**: Audit tasks every 10 chapters
- **Parallelization**: Different chapters can be written in parallel
- **File paths**: All tasks specify exact chapter file and line range

For software:
- **Granularity**: One task per component/file
- **TDD**: Test tasks always before implementation tasks
- **Parallelization**: Independent files/modules marked [P]
- **File paths**: All tasks specify exact source/test file paths

**Validation gates**:
- No task overwrites content another [P] task is creating
- Parallel tasks are truly independent
- Dependencies are explicit and correct
- Each task has clear completion criteria
