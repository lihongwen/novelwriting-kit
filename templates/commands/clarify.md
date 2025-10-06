---
description: Identify underspecified areas in the current story arc outline (for novels) or feature spec (for software) by asking up to 5 highly targeted clarification questions and encoding answers back into the spec.
scripts:
   sh: scripts/bash/check-prerequisites.sh --json --paths-only
   ps: scripts/powershell/check-prerequisites.ps1 -Json -PathsOnly
---

The user input to you can be provided directly by the agent or as a command argument - you **MUST** consider it before proceeding with the prompt (if not empty).

User input:

$ARGUMENTS

Goal: Detect and reduce ambiguity or missing decision points in the active specification and record the clarifications directly in the spec file.

Note: This clarification workflow is expected to run (and be completed) BEFORE invoking `/plan`. If the user explicitly states they are skipping clarification (e.g., exploratory spike), you may proceed, but must warn that downstream rework risk increases.

Execution steps:

1. Run `{SCRIPT}` from repo root **once** (combined `--json --paths-only` mode / `-Json -PathsOnly`). Parse minimal JSON payload fields:
   - `FEATURE_DIR`
   - `FEATURE_SPEC`
   - (Optionally capture `IMPL_PLAN`, `TASKS` for future chained flows.)
   - If JSON parsing fails, abort and instruct user to re-run `/specify` or verify feature branch environment.

2. Load the current spec file. **Detect project type** from content:
   - **Novel writing indicators**: Story Beats, Character Arcs, Foreshadowing Map, chapters, plot points
   - **Software indicators**: Functional Requirements, API contracts, user stories, technical constraints

3. Perform structured ambiguity & coverage scan based on project type:

   **For Novel Writing Projects**, scan these categories:
   
   Plot Structure & Story Beats:
   - Clear inciting incident and stakes
   - Escalation pattern defined
   - Climax and resolution approach
   - Subplot integration
   
   Character Development:
   - Protagonist motivation and goals
   - Character arc type (growth/fall/flat)
   - Key turning points for character change
   - Supporting character roles
   - Relationship dynamics
   
   Foreshadowing & Setup:
   - Planted elements clearly identified
   - Payoff timing planned
   - Chekhov's Gun compliance (no unused setups)
   - Mystery/revelation structure
   
   World-Building & Setting:
   - World rules and constraints
   - Magic/tech system mechanics (if applicable)
   - Geographic/cultural context
   - Historical background relevance
   
   Timeline & Chronology:
   - In-story time span
   - Event sequence clarity
   - Multiple POV timeline sync (if applicable)
   - Flashback/flash-forward anchors
   
   Conflict & Stakes:
   - External conflicts defined
   - Internal conflicts articulated
   - Stakes escalation pattern
   - Antagonist motivation (if applicable)
   
   Theme & Meaning:
   - Central theme identification
   - Thematic resolution approach
   - Symbolic elements
   
   Narrative Style:
   - POV consistency (1st/3rd person, limited/omniscient)
   - Tense consistency
   - Tone target
   
   Pacing & Structure:
   - High/low tension balance
   - Scene vs. summary ratio
   - Chapter count and length targets
   
   Edge Cases & Complications:
   - Character death or major loss
   - Betrayal or alliance shifts
   - Moral dilemmas
   - Time pressure elements

   **For Software Projects**, scan these categories:
   
   Functional Scope & Behavior:
   - Core user goals & success criteria
   - Explicit out-of-scope declarations
   - User roles / personas differentiation
   
   Domain & Data Model:
   - Entities, attributes, relationships
   - Identity & uniqueness rules
   - Lifecycle/state transitions
   - Data volume / scale assumptions
   
   [Additional software-specific categories as in original...]

   For each category with Partial or Missing status, add a candidate question opportunity unless clarification would not materially change implementation/writing strategy.

4. Generate (internally) a prioritized queue of candidate clarification questions (maximum 5). Do NOT output them all at once. Apply these constraints:
    - Maximum of 5 total questions across the whole session.
    - Each question must be answerable with EITHER:
       * A short multiple‑choice selection (2–5 distinct, mutually exclusive options), OR
       * A one-word / short‑phrase answer (explicitly constrain: "Answer in <=5 words").
   - **For novels**: Prioritize character motivations, plot logic gaps, foreshadowing targets, timeline conflicts, world rule inconsistencies
   - **For software**: Prioritize architecture impacts, data modeling, test design, UX behavior, compliance
   - Ensure category coverage balance
   - Favor clarifications that reduce downstream rework risk

5. Sequential questioning loop (interactive):
    - Present EXACTLY ONE question at a time.
    - For multiple‑choice questions render options as a Markdown table:

       | Option | Description |
       |--------|-------------|
       | A | <Option A description> |
       | B | <Option B description> |
       | C | <Option C description> |
       | Short | Provide a different short answer (<=5 words) |

    - For short‑answer style (no meaningful discrete options), output a single line after the question: `Format: Short answer (<=5 words)`.
    - After the user answers:
       * Validate the answer maps to one option or fits the <=5 word constraint.
       * If ambiguous, ask for a quick disambiguation (count still belongs to same question; do not advance).
       * Once satisfactory, record it in working memory (do not yet write to disk) and move to the next queued question.
    - Stop asking further questions when:
       * All critical ambiguities resolved early, OR
       * User signals completion ("done", "good", "no more"), OR
       * You reach 5 asked questions.
    - Never reveal future queued questions in advance.

6. Integration after EACH accepted answer (incremental update approach):
    - Maintain in-memory representation of the spec plus raw file contents.
    - For the first integrated answer in this session:
       * Ensure a `## Clarifications` section exists (create it after the overview/context section if missing).
       * Under it, create `### Session YYYY-MM-DD` subheading for today.
    - Append a bullet line: `- Q: <question> → A: <final answer>`.
    - Then immediately apply the clarification to the most appropriate section(s):
       * **For novels**:
         - Plot ambiguity → Update Story Beats or Plot Requirements
         - Character motivation → Update Character Arcs section
         - Foreshadowing → Add/update entry in Foreshadowing Map with ID
         - World-building → Update Key World Elements
         - Timeline → Update Timeline & Pacing section
         - Theme → Update Thematic Requirements
       * **For software**:
         - Functional ambiguity → Update Functional Requirements
         - Data shape → Update Data Model
         - Non-functional → Add measurable criteria
         - Edge case → Add to Edge Cases section
    - If the clarification invalidates an earlier ambiguous statement, replace it instead of duplicating.
    - Save the spec file AFTER each integration (atomic overwrite).
    - Preserve formatting: do not reorder unrelated sections.

7. Validation (performed after EACH write plus final pass):
   - Clarifications session contains exactly one bullet per accepted answer.
   - Total asked (accepted) questions ≤ 5.
   - Updated sections contain no lingering vague placeholders the answer was meant to resolve.
   - No contradictory earlier statement remains.
   - Markdown structure valid.
   - Terminology consistency across sections.

8. Write the updated spec back to `FEATURE_SPEC`.

9. Report completion (after questioning loop ends):
   - Number of questions asked & answered.
   - Path to updated spec.
   - Sections touched (list names).
   - Coverage summary table listing each taxonomy category with Status: Resolved/Deferred/Clear/Outstanding.
   - If any Outstanding or Deferred remain, recommend whether to proceed to `/plan` or run `/clarify` again.
   - Suggested next command.

Behavior rules:
- If no meaningful ambiguities found, respond: "No critical ambiguities detected worth formal clarification." and suggest proceeding.
- If spec file missing, instruct user to run `/specify` first.
- Never exceed 5 total asked questions.
- **For novels**: Avoid asking about prose style unless it affects structural decisions
- **For software**: Avoid speculative tech stack questions unless absence blocks functional clarity
- Respect user early termination signals.

Context for prioritization: {ARGS}
