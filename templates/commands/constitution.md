---
description: Create or update the writing constitution (world-building rules, character principles, narrative guidelines for novels) or project constitution (coding principles for software), ensuring all dependent templates stay in sync.
---

The user input to you can be provided directly by the agent or as a command argument - you **MUST** consider it before proceeding with the prompt (if not empty).

User input:

$ARGUMENTS

You are updating the constitution at `/memory/constitution.md`. 

**Context Detection**: First, determine the project type from user input:
- **Novel Writing**: Keywords like world-building, characters, foreshadowing, chapters, plot, protagonist, magic system, narrative, story, arc
- **Software Development**: Keywords like code, features, APIs, tests, deployment, architecture, database, frontend, backend

The constitution template contains placeholder tokens in square brackets (e.g. `[PROJECT_NAME]` or `[NOVEL_TITLE]`, `[PRINCIPLE_1_NAME]`). Your job is to (a) detect project type, (b) collect/derive concrete values based on project type, (c) fill the template precisely, and (d) propagate any amendments across dependent artifacts.

Follow this execution flow:

1. Load the existing constitution template at `/memory/constitution.md`.
   - Identify every placeholder token of the form `[ALL_CAPS_IDENTIFIER]`.
   **IMPORTANT**: The user might require less or more principles than the ones used in the template. If a number is specified, respect that - follow the general template. You will update the doc accordingly.

2. **Detect project type** and collect/derive values for placeholders:
   
   **For Novel Writing Projects**:
   - `[NOVEL_TITLE]` → Novel title from user or repo context
   - Principles focus on:
     * World Consistency (magic systems, physical laws, cultural rules)
     * Character Arc Integrity (gradual development, personality consistency)
     * Foreshadowing Management (tracking, payoff timing, Chekhov's Gun)
     * Timeline Accuracy (chronological coherence, POV sync)
     * Pacing & Rhythm (tension balance, chapter hooks)
   - Required documentation: /world-building/, /characters/, /foreshadowing/tracker.md, /timeline/master.md
   - Quality gates: Chapter-level, Arc-level (10-20 chapters), Milestone (50+ chapters)
   
   **For Software Projects**:
   - `[PROJECT_NAME]` → Project name from user or repo
   - Principles focus on:
     * Library-First (modular design)
     * CLI Interface (observability)
     * Test-First (TDD mandatory)
     * Integration Testing (contract-first)
     * Simplicity (YAGNI, minimal abstraction)
   - Required documentation: contracts/, data-model.md, implementation-details/
   - Quality gates: Phase gates (pre-implementation), test coverage

   - If user input supplies a value, use it.
   - Otherwise infer from existing repo context (README, docs, prior constitution versions if embedded).
   - For governance dates: `RATIFICATION_DATE` is the original adoption date (if unknown ask or mark TODO), `LAST_AMENDED_DATE` is today if changes are made, otherwise keep previous.
   - `CONSTITUTION_VERSION` must increment according to semantic versioning:
     * MAJOR: Backward incompatible governance/principle removals or redefinitions.
     * MINOR: New principle/section added or materially expanded guidance.
     * PATCH: Clarifications, wording, typo fixes, non-semantic refinements.

3. Draft the updated constitution content:
   - Replace every placeholder with concrete text (no bracketed tokens left except intentionally retained template slots explicitly justified).
   - Preserve heading hierarchy and remove comments once replaced unless they still add clarifying guidance.
   - **For novel constitutions**: Each Principle section should:
     * Succinct name line with Chinese/English
     * Paragraph or bullet list capturing non‑negotiable rules
     * Quality gates specific to writing (chapter/arc/milestone reviews)
     * Tracking requirements (what files to maintain)
   - **For software constitutions**: Each Principle section should:
     * Succinct name line
     * Non-negotiable rules (MUST/SHOULD)
     * Explicit rationale if not obvious
   - Ensure Governance section lists amendment procedure, versioning policy, and compliance review expectations.

4. Consistency propagation checklist:
   - Read `/templates/plan-template.md` and ensure any "Constitution Check" or rules align with updated principles.
   - Read `/templates/spec-template.md` for scope/requirements alignment—update if constitution adds/removes mandatory sections or constraints.
   - Read `/templates/tasks-template.md` and ensure task categorization reflects new or removed principle-driven task types.
   - Read each command file in `/templates/commands/*.md` to verify no outdated references remain.
   - Read runtime guidance docs (README.md, NOVEL-WRITING-GUIDE.md if novel, docs/quickstart.md).

5. Produce a Sync Impact Report (prepend as an HTML comment at top of the constitution file after update):
   - Version change: old → new
   - List of modified principles (old title → new title if renamed)
   - Added sections
   - Removed sections
   - Templates requiring updates (✅ updated / ⚠ pending) with file paths
   - Follow-up TODOs if any placeholders intentionally deferred.

6. Validation before final output:
   - No remaining unexplained bracket tokens.
   - Version line matches report.
   - Dates ISO format YYYY-MM-DD.
   - **For novels**: World rules, foreshadowing tracking, timeline management, character arcs are present
   - **For software**: Test-first, library-first, observability principles are present
   - Principles are declarative, testable, and free of vague language ("should" → replace with MUST/SHOULD rationale where appropriate).

7. Write the completed constitution back to `/memory/constitution.md` (overwrite).

8. Output a final summary to the user with:
   - New version and bump rationale.
   - Project type detected (Novel Writing / Software Development).
   - Any files flagged for manual follow-up.
   - Suggested commit message (e.g., `docs: amend constitution to vX.Y.Z (novel writing principles + foreshadowing tracking)` or `docs: amend constitution to vX.Y.Z (principle additions + governance update)`).

Formatting & Style Requirements:
- Use Markdown headings exactly as in the template (do not demote/promote levels).
- Wrap long rationale lines to keep readability (<100 chars ideally).
- Keep a single blank line between sections.
- Avoid trailing whitespace.

If the user supplies partial updates (e.g., only one principle revision), still perform validation and version decision steps.

If critical info missing (e.g., ratification date truly unknown), insert `TODO(<FIELD_NAME>): explanation` and include in the Sync Impact Report under deferred items.

Do not create a new template; always operate on the existing `/memory/constitution.md` file.
