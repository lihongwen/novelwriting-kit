---
description: "Chapter planning template for detailed scene and narrative development"
scripts:
  sh: scripts/bash/update-agent-context.sh __AGENT__
  ps: scripts/powershell/update-agent-context.ps1 -AgentType __AGENT__
---

# Chapter Plan: [ARC NAME]

**Branch**: `[###-arc-name]` | **Date**: [DATE] | **Outline**: [link to spec.md]
**Input**: Story arc outline from `/specs/[###-arc-name]/spec.md`

## Execution Flow (/plan command scope)
```
1. Load story arc outline from Input path
   → If not found: ERROR "No story outline at {path}"
2. Fill Narrative Context (scan for NEEDS CLARIFICATION)
   → Detect POV style, narrative voice, chapter structure
   → Set Writing Approach based on genre and tone
3. Fill the Constitution Check section based on writing constitution
4. Evaluate Constitution Check section below
   → Check: World consistency, Character integrity, Foreshadowing tracking
   → If violations exist: Document in Narrative Concerns
   → Update Progress Tracking: Initial Constitution Check
5. Execute Phase 0 → research.md
   → Research historical/technical details for accuracy
   → Resolve all [NEEDS CLARIFICATION] from outline
6. Execute Phase 1 → scene-breakdown.md, character-states.md, continuity-check.md
   → Create detailed scene-by-scene breakdown
   → Document character emotional states and development
   → Cross-reference timeline and foreshadowing
7. Re-evaluate Constitution Check section
   → Verify no new consistency issues introduced
   → Update Progress Tracking: Post-Planning Constitution Check
8. Plan Phase 2 → Describe writing task generation approach (DO NOT create tasks.md)
9. STOP - Ready for /tasks command
```

**IMPORTANT**: The /plan command STOPS at step 8. Phase 2 is executed by /tasks command:
- Phase 2: /tasks command creates tasks.md (writing tasks breakdown)
- Phase 3: /implement command executes actual writing

## Summary
[Extract from arc outline: main plot thread + key character developments + major themes]

## Narrative Context
**POV Style**: [First Person / Third Person Limited / Third Person Omniscient / Multiple POV or NEEDS CLARIFICATION]  
**Narrative Voice**: [Past Tense / Present Tense, tone: formal/casual/poetic or NEEDS CLARIFICATION]  
**Chapter Structure**: [Standard chapters / Scene breaks / Date/location headers or NEEDS CLARIFICATION]  
**Target Chapter Count**: [e.g., 50 chapters or NEEDS CLARIFICATION]  
**Target Word Count per Chapter**: [e.g., 3000-5000 words or NEEDS CLARIFICATION]
**Genre Conventions**: [e.g., Mystery requires clue planting, Romance requires emotional beats or NEEDS CLARIFICATION]  
**Tone**: [Dark/Light/Humorous/Serious/Epic or NEEDS CLARIFICATION]  
**Pacing Strategy**: [Fast-paced action / Slow-burn character study / Balanced or NEEDS CLARIFICATION]  
**Worldbuilding Density**: [High (extensive description) / Medium / Low (minimal exposition) or NEEDS CLARIFICATION]

## Constitution Check
*GATE: Must pass before Phase 0 research. Re-check after Phase 1 planning.*

### World Consistency Gate
- [ ] No contradictions with established world rules from `/world-building/rules.md`
- [ ] New locations/magic systems align with existing canon
- [ ] Technology/supernatural elements follow documented constraints
- [ ] Timeline events don't conflict with prior chapters

### Character Arc Integrity Gate
- [ ] Character behaviors align with personality profiles in `/characters/`
- [ ] Character growth is gradual and event-justified
- [ ] No out-of-character actions for plot convenience
- [ ] Relationships evolve logically from previous states

### Foreshadowing Management Gate
- [ ] All foreshadowing setups logged in `/foreshadowing/tracker.md`
- [ ] Planned payoffs are within acceptable chapter range (<50 chapters)
- [ ] Previous arc foreshadowing addressed or explicitly deferred
- [ ] No Chekhov's Gun violations (unused important elements)

### Timeline Accuracy Gate
- [ ] Events align with master timeline in `/timeline/master.md`
- [ ] Multiple POV timelines synchronized at convergence points
- [ ] Flashback temporal anchors are clear
- [ ] No chronological contradictions

### Pacing & Rhythm Gate
- [ ] High/low tension chapters balanced
- [ ] Each chapter has clear conflict or progression
- [ ] No more than 3 consecutive exposition-heavy chapters
- [ ] Chapter hooks maintain reader engagement

## Story Documentation Structure

### Planning Documents (this arc)
```
specs/[###-arc-name]/
├── spec.md                 # Story arc outline (from /specify command)
├── plan.md                 # This file (/plan command output)
├── research.md             # Phase 0: Historical/technical research
├── scene-breakdown.md      # Phase 1: Detailed scene-by-scene plan
├── character-states.md     # Phase 1: Character emotional journey tracking
├── continuity-check.md     # Phase 1: Timeline & foreshadowing verification
└── tasks.md                # Phase 2: Writing tasks (/tasks command output)
```

### Story Content (repository root)
```
chapters/
├── 001-opening.md          # Chapter content (from /implement command)
├── 002-inciting-incident.md
├── 003-first-complication.md
└── ...

characters/
├── protagonist-name.md     # Character profile & arc tracking
├── antagonist-name.md
└── ...

world-building/
├── rules.md                # World mechanics and constraints
├── locations.md            # Setting descriptions
├── history.md              # Pre-story timeline
└── culture.md              # Social structures

foreshadowing/
└── tracker.md              # Master foreshadowing log

timeline/
└── master.md               # Chronological event tracker
```

## Phase 0: Research & Clarification

**Purpose**: Resolve all uncertainties and gather necessary knowledge for authentic writing

### Research Tasks
1. **Extract unknowns from Narrative Context** above:
   - For each NEEDS CLARIFICATION → research task
   - For historical settings → accuracy verification
   - For technical details → expert consultation or reading

2. **Generate research queries**:
   ```
   For each NEEDS CLARIFICATION in outline:
     Task: "Research {topic} for {story context}"
   For each historical/technical element:
     Task: "Verify accuracy of {element} in {time period/domain}"
   For each cultural element:
     Task: "Understand {cultural practice} to avoid stereotypes"
   ```

3. **Consolidate findings** in `research.md` using format:
   - **Topic**: [What was researched]
   - **Findings**: [Key facts/details discovered]
   - **Application**: [How it informs the story]
   - **Sources**: [References for fact-checking]

**Output**: research.md with all NEEDS CLARIFICATION resolved

## Phase 1: Detailed Scene Planning

*Prerequisites: research.md complete, all uncertainties resolved*

### 1. Scene Breakdown (`scene-breakdown.md`)

For each chapter, create detailed scene plans:

```markdown
## Chapter [X]: [Chapter Title]

### Scene 1: [Scene Name]
- **Time**: [Morning/Afternoon/Evening, specific if relevant]
- **Location**: [Specific place, referencing /world-building/locations.md]
- **POV Character**: [If multiple POVs]
- **Scene Purpose**: 
  - [ ] Advance plot (which thread: [main/subplot A/subplot B])
  - [ ] Develop character ([which character], [what aspect])
  - [ ] Reveal information ([what information])
  - [ ] Plant foreshadowing ([Foreshadowing ID])
- **Characters Present**: [List with roles in scene]
- **Emotional Arc**: [Starting emotion] → [Conflict/catalyst] → [Ending emotion]
- **Key Events**:
  1. [Event 1 - what happens physically]
  2. [Event 2 - dialogue/revelation]
  3. [Event 3 - decision/action point]
- **Foreshadowing**:
  - **Plant**: [New foreshadowing - assign ID, log in tracker]
  - **Hint**: [Existing foreshadowing to subtly reference]
  - **Payoff**: [Foreshadowing to resolve - mark in tracker]
- **Continuity Check**:
  - Character locations align with timeline: [ ]
  - Character knowledge consistent: [ ]
  - World state accurate: [ ]
- **Sensory Details to Include**: [Key sensory anchors for immersion]
- **Tone**: [How this scene feels - tense/tender/ominous/hopeful]
- **Estimated Word Count**: [e.g., 800-1200 words]

### Scene 2: [Scene Name]
[Same structure repeated]
```

### 2. Character State Tracking (`character-states.md`)

Track character progression chapter-by-chapter:

```markdown
## [Character Name] - Emotional Journey

### Chapter [X]: [Chapter Title]
- **Physical State**: [Injured/Healthy/Exhausted/Rested]
- **Emotional State**: [Primary emotion and why]
- **Knowledge**: [What they now know that they didn't before]
- **Relationships**: [Changes in how they relate to others]
- **Goals**: [Current objective - has it changed?]
- **Internal Conflict**: [Psychological struggle]
- **Arc Progress**: [Where are they in their character arc? X%]
- **Key Quote/Action**: [Defining moment from this chapter]
```

### 3. Continuity Verification (`continuity-check.md`)

Cross-reference all story elements:

```markdown
## Continuity Check for Chapters [Range]

### Timeline Verification
| Chapter | In-Story Date | Events | Character Locations | Duration |
|---------|---------------|--------|---------------------|----------|
| 001 | Day 1, Morning | [Events] | [Who is where] | 3 hours |
| 002 | Day 1, Afternoon | [Events] | [Who is where] | 2 hours |

### Foreshadowing Status
| ID | Setup Chapter | Type | Status | Payoff Plan |
|----|---------------|------|--------|-------------|
| F001 | 003 | Item | PLANTED | Chapter 045 |
| F012 | [Previous arc] | Prophecy | HINTED | This arc, ch 030-035 |

### World Consistency Check
- [ ] No magic system rule violations
- [ ] Geography consistent (travel times realistic)
- [ ] Technology level consistent
- [ ] Cultural practices align with `/world-building/culture.md`

### Character Consistency Check
- [ ] No personality contradictions
- [ ] Skills/knowledge track correctly (no sudden expertise)
- [ ] Physical descriptions match across chapters
- [ ] Speech patterns consistent
```

## Phase 2: Writing Task Planning Approach
*This section describes what the /tasks command will do - DO NOT execute during /plan*

**Task Generation Strategy**:
- Load `/templates/tasks-template.md` as base
- Generate writing tasks from Phase 1 scene breakdowns
- Each scene → writing task [P] (parallelizable if different chapters)
- Each chapter → revision task (after all scenes complete)
- Quality checks → foreshadowing update, timeline update, character state update

**Task Ordering Strategy**:
- Chronological chapter order (001 → 002 → 003...)
- Within chapter: Scene 1 → Scene 2 → Scene 3 → Integration → Revision
- Mark [P] for scenes in different chapters (can be written in parallel)
- Sequential for scenes in same chapter

**Estimated Output**: 150-200 writing tasks for 50-chapter arc

**IMPORTANT**: This phase is executed by the /tasks command, NOT by /plan

## Phase 3+: Future Execution
*These phases are beyond the scope of the /plan command*

**Phase 3**: Writing task execution (/tasks command creates tasks.md)  
**Phase 4**: First draft writing (/implement command executes tasks.md)  
**Phase 5**: Revision & consistency audit (automated checks + human review)

## Narrative Concerns
*Fill ONLY if Constitution Check has violations that must be justified*

| Concern | Justification | Alternative Rejected Because |
|---------|---------------|------------------------------|
| [e.g., Character acts out-of-character] | [Specific story reason] | [Why consistent behavior wouldn't work] |
| [e.g., Timeline compressed unrealistically] | [Narrative pacing need] | [Why realistic pacing would hurt story] |

**NOTE**: Aim for ZERO entries. Concerns should be resolved in planning, not justified.

## Progress Tracking
*This checklist is updated during execution flow*

**Phase Status**:
- [ ] Phase 0: Research complete (/plan command)
- [ ] Phase 1: Scene planning complete (/plan command)
- [ ] Phase 2: Task planning approach described (/plan command)
- [ ] Phase 3: Writing tasks generated (/tasks command)
- [ ] Phase 4: First draft complete (/implement command)
- [ ] Phase 5: Revisions complete

**Gate Status**:
- [ ] Initial Constitution Check: PASS
- [ ] Post-Planning Constitution Check: PASS
- [ ] All NEEDS CLARIFICATION resolved
- [ ] Narrative concerns addressed (ideally ZERO)
- [ ] Foreshadowing fully mapped
- [ ] Timeline verified
- [ ] Character arcs tracked

**Quality Metrics**:
- Total Chapters Planned: [X]
- Total Scenes: [Y]
- Foreshadowing Planted: [Z]
- Foreshadowing Resolved: [W]
- Character Arcs Tracked: [N]

---
*Based on Novel Writing Constitution v1.0 - See `/memory/constitution.md`*
