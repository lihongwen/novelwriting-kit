---
description: Create or update the story arc outline (plot structure, character arcs, foreshadowing) for a novel volume/arc from a natural language story concept.
scripts:
  sh: scripts/bash/create-new-feature.sh --json "{ARGS}"
  ps: scripts/powershell/create-new-feature.ps1 -Json "{ARGS}"
---

The user input to you can be provided directly by the agent or as a command argument - you **MUST** consider it before proceeding with the prompt (if not empty).

User input:

$ARGUMENTS

The text the user typed after `/specify` in the triggering message **is** the story concept/arc description. Assume you always have it available in this conversation even if `{ARGS}` appears literally below. Do not ask the user to repeat it unless they provided an empty command.

**Context**: This command works for both novel writing and software development. Detect the project type from the user's input:
- **Novel keywords**: plot, character, protagonist, antagonist, chapter, scene, arc, volume, foreshadowing, conflict, theme
- **Software keywords**: feature, API, endpoint, database, user, authentication, frontend, backend, service

Given that story concept/arc description, do this:

1. Run the script `{SCRIPT}` from repo root and parse its JSON output for BRANCH_NAME and SPEC_FILE. All file paths must be absolute.
  **IMPORTANT** You must only ever run this script once. The JSON is provided in the terminal as output - always refer to it to get the actual content you're looking for.

2. Load `templates/spec-template.md` to understand required sections.

3. **Detect project type** from the user input and template content:
   - **If novel writing** (story/plot keywords): Use story arc outline structure with:
     - Story Beats & Character Arcs
     - Plot Requirements (not functional requirements)
     - Foreshadowing Map
     - Timeline & Pacing
     - Character development tracking
   - **If software** (feature/API keywords): Use traditional feature spec structure

4. Write the specification to SPEC_FILE using the template structure, replacing placeholders with concrete details derived from the story concept/arc description (arguments) while preserving section order and headings.

5. **For novel writing projects specifically**:
   - Focus on story structure (Beginning → Middle → End)
   - Map character emotional journeys
   - Identify foreshadowing opportunities with IDs (F001, F002, etc.)
   - Establish timeline (in-story time span, not writing time)
   - Mark any unclear plot points with [NEEDS CLARIFICATION: specific question]
   - Avoid writing prose or dialogue - keep it structural

6. **For software projects specifically**:
   - Focus on user stories and functional requirements
   - Identify API contracts and data entities
   - Mark technical uncertainties with [NEEDS CLARIFICATION]

7. Report completion with branch name, spec file path, and readiness for the next phase.

Note: The script creates and checks out the new branch and initializes the spec file before writing.
