---
description: Perform consistency and quality analysis. For novels - verify foreshadowing resolution, timeline coherence, character consistency, world-building adherence. For software - check spec/plan/tasks cross-artifact alignment and constitution compliance.
scripts:
  sh: scripts/bash/check-prerequisites.sh --json --require-tasks --include-tasks
  ps: scripts/powershell/check-prerequisites.ps1 -Json -RequireTasks -IncludeTasks
---

The user input to you can be provided directly by the agent or as a command argument - you **MUST** consider it before proceeding with the prompt (if not empty).

User input:

$ARGUMENTS

Goal: Identify inconsistencies, plot holes, dangling foreshadowing, timeline contradictions (for novels) OR ambiguities, duplications, underspecified items (for software) across artifacts before or after implementation. This command MUST run only after `/tasks` has successfully produced a complete `tasks.md`.

STRICTLY READ-ONLY: Do **not** modify any files. Output a structured analysis report. Offer an optional remediation plan (user must explicitly approve before any follow-up editing commands would be invoked manually).

Constitution Authority: The project constitution (`/memory/constitution.md`) is **non-negotiable** within this analysis scope. Constitution conflicts are automatically CRITICAL and require adjustment of the spec, plan, or content—not dilution or reinterpretation of the principle.

Execution steps:

1. Run `{SCRIPT}` once from repo root and parse JSON for FEATURE_DIR and AVAILABLE_DOCS. Derive absolute paths:
   - SPEC = FEATURE_DIR/spec.md
   - PLAN = FEATURE_DIR/plan.md
   - TASKS = FEATURE_DIR/tasks.md
   Abort with an error message if any required file is missing (instruct the user to run missing prerequisite command).

2. Load artifacts and **detect project type**:
   - Parse spec.md, plan.md, tasks.md
   - **Novel writing indicators**: Story Beats, Character Arcs, Foreshadowing Map, scene-breakdown.md, character-states.md, chapters/
   - **Software indicators**: Functional Requirements, Technical Context, contracts/, data-model.md, src/

3. **For Novel Writing Projects** - Build semantic models:
   - **Foreshadowing inventory**: Load /foreshadowing/tracker.md
     * All items with IDs (F001, F002, etc.)
     * Setup chapters and payoff chapters
     * Current status: PLANTED / HINTED / RESOLVED / ABANDONED
   - **Timeline model**: Load /timeline/master.md
     * Event sequence with in-story dates
     * Character locations per chapter
     * Duration tracking
   - **Character arcs**: Load /characters/*.md files
     * Character state per chapter
     * Arc progress tracking
     * Relationship evolution
   - **World rules**: Load /world-building/rules.md
     * Magic/tech systems
     * Physical laws
     * Cultural constraints
   - **Chapter content**: Scan chapters/ directory for written content
   - **Constitution rules**: Extract principle names and MUST/SHOULD normative statements

4. **For Novel Writing - Detection passes**:

   A. **Foreshadowing Resolution Check**:
      - Flag any [PLANTED] foreshadowing >50 chapters old without payoff plan
      - Flag any [RESOLVED] items without matching content in chapters
      - Identify Chekhov's Gun violations (important items introduced but never used)
      - Check for premature reveals (payoff before sufficient buildup)

   B. **Timeline Consistency Check**:
      - Detect chronological contradictions (event A after event B in timeline, but reversed in text)
      - Verify character locations are physically possible (travel time realistic)
      - Check for duplicate or conflicting event timestamps
      - Verify flashback/flash-forward anchors are clear

   C. **Character Consistency Check**:
      - Flag personality contradictions (character acts against established traits without justification)
      - Check for knowledge inconsistencies (character knows something they shouldn't)
      - Verify character arc progression is gradual (no sudden unexplained changes)
      - Check relationship evolution logic
      - Flag physical description mismatches across chapters

   D. **World-Building Consistency Check**:
      - Identify magic/tech system rule violations
      - Check geographic consistency (locations, distances, climate)
      - Verify cultural/social rule adherence
      - Flag technology level inconsistencies

   E. **Constitution Alignment (Novels)**:
      - World Consistency violations (rules broken without justification)
      - Character Arc Integrity violations (personality shifts for plot convenience)
      - Foreshadowing Management violations (untracked setups, missing payoffs)
      - Timeline Accuracy violations (contradictions, sync failures)
      - Pacing & Rhythm violations (too many consecutive exposition chapters)

   F. **Plot Logic & Stakes**:
      - Check conflict escalation pattern is maintained
      - Verify stakes remain consistent or escalate
      - Flag plot holes (unexplained events, convenient coincidences)
      - Check for abandoned subplots

   G. **POV & Voice Consistency**:
      - Verify POV doesn't shift mid-scene (unless intentional)
      - Check tense consistency
      - Verify tone matches target from plan.md

5. **For Software Projects** - Build semantic models:
   - Requirements inventory from spec.md
   - Task coverage mapping from tasks.md
   - Constitution rule set from /memory/constitution.md

6. **For Software - Detection passes** (as in original):
   - Duplication detection
   - Ambiguity detection
   - Underspecification
   - Constitution alignment
   - Coverage gaps
   - Inconsistency

7. Severity assignment heuristic:
   - **CRITICAL**: 
     * Violates constitution MUST principle
     * Timeline contradiction affecting plot
     * Major foreshadowing abandoned (setup in first 20% with no resolution)
     * Character knowledge paradox (knows info they shouldn't)
   - **HIGH**: 
     * Minor timeline inconsistency
     * Foreshadowing >30 chapters without hint/payoff
     * Character behavior inconsistency without explanation
     * World rule violation in minor scene
   - **MEDIUM**: 
     * Pacing imbalance (4+ consecutive low-tension chapters)
     * POV slip
     * Terminology drift
   - **LOW**: 
     * Style/wording improvements
     * Minor description mismatches

8. Produce a Markdown report (no file writes) with sections:

   **For Novels**:
   ```markdown
   ### Novel Quality Analysis Report
   
   | ID | Category | Severity | Location(s) | Summary | Recommendation |
   |----|----------|----------|-------------|---------|----------------|
   | F1 | Foreshadowing | HIGH | F023 planted Ch12, no payoff | Magic sword introduced but never used in climax | Add payoff in Ch45-50 or remove setup |
   | T1 | Timeline | CRITICAL | Ch15 vs Ch18 | Character in two places simultaneously | Fix timeline in Ch18 |
   | C1 | Character | HIGH | Ch22, protagonist | Acts cowardly contradicting established bravery | Add justification or rewrite scene |
   | W1 | World Rules | MEDIUM | Ch30 | Magic used without cost, violating established system | Add consequence or explain exception |
   ```

   **Foreshadowing Status Table**:
   | ID | Type | Setup Ch | Status | Payoff Ch | Days Since Setup | Issue? |
   |----|------|----------|--------|-----------|------------------|--------|
   | F001 | Item | 003 | RESOLVED | 045 | - | ✓ |
   | F015 | Prophecy | 018 | PLANTED | - | 32 chapters | ⚠ Need payoff plan |

   **Timeline Verification**:
   | Chapter Range | Issues Found |
   |---------------|--------------|
   | 001-010 | None ✓ |
   | 011-020 | 2 minor inconsistencies |

   **Character Arc Progress**:
   | Character | Planned Arc | Current % | Issues |
   |-----------|-------------|-----------|--------|
   | Protagonist | Growth | 65% | On track ✓ |
   | Antagonist | Fall | 40% | Lagging behind plan |

   **Constitution Compliance**:
   - World Consistency: 2 violations
   - Character Integrity: 1 violation
   - Foreshadowing Management: 3 violations
   - Timeline Accuracy: 1 critical, 2 high
   - Pacing & Rhythm: Within guidelines ✓

   **Metrics**:
   - Total Chapters Analyzed: 50
   - Foreshadowing Items: 23 (18 resolved, 3 pending, 2 abandoned)
   - Timeline Events: 156
   - Critical Issues: 2
   - High Issues: 8
   - Medium Issues: 5
   - Low Issues: 12

9. At end of report, output Next Actions block:
   - If CRITICAL issues exist: **Must resolve before proceeding or publishing**
   - If only HIGH: Strongly recommend addressing
   - If only LOW/MEDIUM: May proceed but fix improves quality
   - Provide explicit fix suggestions

10. Ask the user: "Would you like me to suggest concrete remediation edits for the top N issues?" (Do NOT apply them automatically.)

Behavior rules:
- NEVER modify files
- NEVER hallucinate missing sections—if absent, report them
- KEEP findings deterministic: if rerun without changes, produce consistent IDs and counts
- LIMIT total findings in main table to 50; aggregate remainder in overflow note
- If zero issues found, emit success report with metrics and proceed recommendation
- **For novels**: Foreshadowing and timeline checks are non-negotiable priority
- **For software**: Constitution and coverage checks are non-negotiable priority

Context: {ARGS}
