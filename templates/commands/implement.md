---
description: Execute tasks from tasks.md. For novels - write chapters following scene plans with automatic tracking. For software - implement code following TDD and technical plan.
scripts:
  sh: scripts/bash/check-prerequisites.sh --json --require-tasks --include-tasks
  ps: scripts/powershell/check-prerequisites.ps1 -Json -RequireTasks -IncludeTasks
---

The user input can be provided directly by the agent or as a command argument - you **MUST** consider it before proceeding with the prompt (if not empty).

User input:

$ARGUMENTS

1. Run `{SCRIPT}` from repo root and parse FEATURE_DIR and AVAILABLE_DOCS list. All paths must be absolute.

2. Load and analyze the implementation context:
   - **REQUIRED**: Read tasks.md for the complete task list and execution plan
   - **REQUIRED**: Read plan.md for context (narrative/technical approach and structure)
   - **Detect project type** from tasks.md content:
     * **Novel writing**: Chapter writing tasks, scene breakdown references, tracking updates
     * **Software**: Setup/test/implementation tasks, contract references, TDD workflow

3. Parse tasks.md structure and extract:
   - **Task phases**: Setup → Chapter Writing / Tests → Core / Implementation → Quality / Polish
   - **Task dependencies**: Sequential vs parallel execution rules
   - **Task details**: ID, description, file paths, parallel markers [P]
   - **Execution flow**: Order and dependency requirements

4. **For Novel Writing Projects** - Execute writing workflow:

   **Phase 1: Setup**
   - Create chapter directory structure (chapters/)
   - Initialize character tracking files (/characters/[name].md)
   - Initialize foreshadowing tracker (/foreshadowing/tracker.md)
   - Initialize timeline (/timeline/master.md)

   **Phase 2: Chapter Writing (Scene-by-Scene)**
   - Load scene-breakdown.md for scene details
   - For each chapter:
     * Write Scene 1 following scene plan (location, characters, purpose, emotional arc, key events)
     * Write Scene 2
     * Write Scene 3 (etc.)
     * Integrate scenes into cohesive chapter flow
     * Add scene transitions
   - **Writing guidelines** from plan.md Narrative Context:
     * Maintain POV consistency (1st/3rd person, limited/omniscient)
     * Follow tense (past/present)
     * Match tone target
     * Include sensory details for immersion
   - **Scene checklist** for each written scene:
     * Clear time and location established
     * POV character perspective maintained
     * Emotional arc progresses (start → conflict → end)
     * At least one of: plot advancement, character development, information reveal
     * Foreshadowing planted/hinted/paid off as planned in scene breakdown
   
   **Phase 3: Quality Tracking (After Each Chapter)**
   - Update /foreshadowing/tracker.md:
     * Log new foreshadowing with IDs (F001, F002, etc.)
     * Mark hinted foreshadowing
     * Mark resolved foreshadowing
     * Verify payoff timeline (<50 chapters from setup)
   - Update /timeline/master.md:
     * Add chapter events with in-story dates/times
     * Record character locations
     * Note duration of events
     * Verify no chronological contradictions
   - Update /characters/[name].md for each character:
     * Physical state changes
     * Emotional state evolution
     * Knowledge gained
     * Relationship changes
     * Goals/motivations updates
     * Arc progress percentage

   **Phase 4: Arc-Level Quality Audits (Every 10 Chapters)**
   - Foreshadowing audit: All planted items logged and payoffs scheduled?
   - Timeline consistency: No chronological contradictions?
   - Character arc verification: Growth aligns with planned trajectory?
   - World consistency: No rule violations vs /world-building/rules.md?
   - Pacing analysis: Balance of high/low tension chapters?

   **Phase 5: Revision & Polish**
   - Review early chapters for consistency with later reveals
   - Cross-chapter continuity (character descriptions, world details match)
   - Prose quality pass (rhythm, voice, clarity)
   - Final foreshadowing verification (all tracked items resolved or explained)

5. **For Software Projects** - Execute implementation workflow:

   **Phase 1: Setup**
   - Initialize project structure
   - Install dependencies
   - Configure linting and formatting

   **Phase 2: Tests First (TDD) - MUST COMPLETE BEFORE IMPLEMENTATION**
   - Write contract tests for all API endpoints
   - Write integration tests for user scenarios
   - Verify all tests FAIL (red phase)
   - Get user approval before proceeding to implementation

   **Phase 3: Core Implementation**
   - Implement models/entities
   - Implement services and business logic
   - Implement CLI commands
   - Implement API endpoints
   - Make tests PASS (green phase)

   **Phase 4: Integration**
   - Database connections
   - Middleware (auth, logging, error handling)
   - External service integrations

   **Phase 5: Polish**
   - Unit tests for edge cases
   - Performance optimization
   - Documentation updates
   - Code cleanup and refactoring

6. Progress tracking and error handling:
   - Report progress after each completed task
   - Halt execution if any non-parallel task fails
   - For parallel tasks [P], continue with successful tasks, report failed ones
   - Provide clear error messages with context for debugging
   - **IMPORTANT** For completed tasks, mark them as [X] in the tasks.md file

7. Completion validation:
   - **For novels**:
     * All chapters written according to scene breakdowns?
     * All foreshadowing logged and tracked?
     * Timeline complete and contradiction-free?
     * Character arcs progress documented?
     * Arc-level audits passed?
   - **For software**:
     * All required tasks completed?
     * Features match specification?
     * Tests pass and coverage meets requirements?
     * Implementation follows technical plan?
   
8. Report final status with summary of completed work.

**Behavior rules**:
- **For novels**: 
  * Never skip quality tracking tasks - they prevent continuity errors
  * Maintain consistency with constitution world rules
  * Reference scene-breakdown.md for every scene's purpose and structure
  * Update tracking files immediately after each chapter
- **For software**:
  * Never skip test-first workflow
  * Follow constitution principles (Library-First, CLI Interface, etc.)
  * Validate against contracts before implementation

Note: This command assumes a complete task breakdown exists in tasks.md. If tasks are incomplete or missing, suggest running `/tasks` first to regenerate the task list.
