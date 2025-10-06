# Writing Tasks: [ARC NAME]

**Input**: Planning documents from `/specs/[###-arc-name]/`
**Prerequisites**: plan.md (required), scene-breakdown.md, character-states.md, continuity-check.md

## Execution Flow (main)
```
1. Load plan.md from arc directory
   → If not found: ERROR "No chapter plan found"
   → Extract: chapter count, scenes, writing approach
2. Load scene breakdown documents:
   → scene-breakdown.md: Extract all scenes → writing tasks
   → character-states.md: Extract character development → tracking tasks
   → continuity-check.md: Extract foreshadowing/timeline → update tasks
3. Generate tasks by category:
   → Chapter Writing: Scene drafts, scene integration, chapter revision
   → Quality Checks: Foreshadowing updates, timeline updates, character tracking
   → Consistency: Constitution compliance, continuity verification
4. Apply task rules:
   → Different chapters = mark [P] for parallel writing
   → Same chapter scenes = sequential (Scene 1 → 2 → 3)
   → Quality checks after each chapter completion
5. Number tasks sequentially (T001, T002...)
6. Generate dependency graph
7. Create parallel writing examples
8. Validate task completeness:
   → All scenes have writing tasks?
   → All chapters have revision tasks?
   → All tracking updated?
9. Return: SUCCESS (tasks ready for /implement)
```

## Format: `[ID] [P?] Description`
- **[P]**: Can run in parallel (different chapters, no dependencies)
- Include exact file paths in descriptions
- Mark quality/tracking tasks for after-writing execution

## Path Conventions
- **Chapters**: `chapters/###-chapter-title.md` at repository root
- **Tracking**: Update `/foreshadowing/tracker.md`, `/timeline/master.md`, `/characters/[name].md`
- **Quality Docs**: Generated in `specs/[###-arc-name]/` for review

## Phase 3.1: Chapter Writing Setup
- [ ] T001 Create chapter directory structure (`chapters/`)
- [ ] T002 Initialize chapter file templates (001.md through 050.md based on plan)
- [ ] T003 [P] Set up character tracking files in `/characters/`
- [ ] T004 [P] Initialize foreshadowing tracker `/foreshadowing/tracker.md`
- [ ] T005 [P] Initialize timeline `/timeline/master.md`

## Phase 3.2: Scene Writing (First Draft)
**CRITICAL: Write scenes in chapter order, but different chapters can be parallel**

### Chapter 001: [Chapter Title]
- [ ] T006 Write Scene 1 in chapters/001-[chapter-title].md (lines 1-50)
- [ ] T007 Write Scene 2 in chapters/001-[chapter-title].md (lines 51-120)
- [ ] T008 Write Scene 3 in chapters/001-[chapter-title].md (lines 121-180)
- [ ] T009 Integrate scenes for chapter flow
- [ ] T010 Log new foreshadowing from Ch001 in `/foreshadowing/tracker.md`
- [ ] T011 Update timeline with Ch001 events in `/timeline/master.md`
- [ ] T012 Update character states after Ch001 in `/characters/[names].md`

### Chapter 002: [Chapter Title]
- [ ] T013 [P] Write Scene 1 in chapters/002-[chapter-title].md (different chapter = parallel)
- [ ] T014 [P] Write Scene 2 in chapters/002-[chapter-title].md
- [ ] T015 [P] Write Scene 3 in chapters/002-[chapter-title].md
- [ ] T016 Integrate scenes for chapter flow
- [ ] T017 [P] Log foreshadowing from Ch002
- [ ] T018 [P] Update timeline with Ch002
- [ ] T019 [P] Update character states after Ch002

### Chapter 003-050: [Repeat Pattern]
[Generate similar task blocks for all planned chapters]
- Scenes within same chapter: Sequential
- Scenes in different chapters: [P] parallel
- Quality/tracking tasks: After chapter completion

## Phase 3.3: Arc-Level Quality Checks
**Execute after every 10 chapters or at arc completion**

### After Chapters 1-10 (First Arc Section)
- [ ] T0XX Foreshadowing audit: Verify all planted items logged and payoffs scheduled
- [ ] T0XX Timeline consistency check: No chronological contradictions
- [ ] T0XX Character arc verification: Growth aligns with planned trajectory
- [ ] T0XX World consistency check: No rule violations vs `/world-building/rules.md`
- [ ] T0XX Pacing analysis: Balance of high/low tension chapters

### After Chapters 11-20 (Second Arc Section)
- [ ] T0XX [Repeat quality checks]

### After Full Arc Completion (All Chapters)
- [ ] T0XX Comprehensive foreshadowing review: All planted items have payoffs
- [ ] T0XX Full timeline audit: Complete chronological coherence
- [ ] T0XX Character arc completion: All planned developments achieved
- [ ] T0XX Constitution compliance: No violations of writing principles
- [ ] T0XX Thematic coherence: Themes consistently explored

## Phase 3.4: Revision & Polish
- [ ] T0XX Review Chapter 001 for consistency with later reveals
- [ ] T0XX Review Chapter 002 for consistency with later reveals
- [ ] T0XX [Continue for all chapters]
- [ ] T0XX Cross-chapter continuity: Character descriptions, world details match
- [ ] T0XX Prose quality pass: Rhythm, voice, clarity
- [ ] T0XX Final foreshadowing verification: All tracked items resolved or explained

## Dependencies
**Chapter Writing**:
- Scenes within a chapter: Sequential (Scene 1 → Scene 2 → Scene 3)
- Scenes across chapters: Can be parallel [P]
- Integration after all scenes in chapter complete
- Quality checks after chapter integration

**Quality Tasks**:
- Foreshadowing/timeline updates: After each chapter
- Arc-level audits: After 10-chapter blocks
- Revision: After first draft complete

**Critical Path**:
- Setup (T001-T005) → Chapter Writing → Quality Checks → Revision

## Parallel Writing Example
```
# Can write these scenes simultaneously (different chapters):
Task T013: "Write Chapter 002, Scene 1"
Task T020: "Write Chapter 003, Scene 1"  
Task T027: "Write Chapter 004, Scene 1"

# Cannot parallelize (same chapter):
Task T006: "Write Chapter 001, Scene 1"
Task T007: "Write Chapter 001, Scene 2"  <- Must wait for T006
```

## Notes for /implement Command
- **Writing Style**: Follow POV/voice from plan.md Narrative Context
- **Word Count Targets**: Aim for targets in scene-breakdown.md (flexible ±20%)
- **Scene Checklist**: Each scene must have:
  - [ ] Clear POV character (if multiple POVs)
  - [ ] Time and location established
  - [ ] Emotional arc (start → conflict → end)
  - [ ] At least one of: plot advancement, character development, information reveal
  - [ ] Sensory details for immersion
  - [ ] Foreshadowing planted/hinted/paid off as planned
- **After Each Chapter**:
  - [ ] Update foreshadowing tracker
  - [ ] Update timeline
  - [ ] Update character state files
  - [ ] Verify no constitution violations

## Task Generation Rules
*Applied during main() execution*

1. **From Scene Breakdown**:
   - Each scene → writing task
   - Scenes in same chapter → sequential
   - Scenes in different chapters → [P] parallel
   
2. **From Character States**:
   - Each chapter → character update task
   - Execute after chapter integration complete
   
3. **From Continuity Check**:
   - Foreshadowing entries → tracking update tasks
   - Timeline events → timeline update tasks
   - Every 10 chapters → comprehensive audit task

4. **Ordering**:
   - Setup → Chapter 001 scenes → Ch001 quality → Chapter 002 scenes → Ch002 quality → ...
   - Quality checks sequential after their chapter
   - Arc-level audits at 10-chapter intervals

## Validation Checklist
*GATE: Checked by main() before returning*

- [ ] All scenes from scene-breakdown.md have writing tasks
- [ ] All chapters have integration tasks
- [ ] All chapters have tracking update tasks (foreshadowing/timeline/characters)
- [ ] Parallel tasks are truly independent (different chapters)
- [ ] Each task specifies exact file path and line range (if applicable)
- [ ] Quality audit tasks scheduled at appropriate intervals
- [ ] No task overwrites content another [P] task is creating

## Estimated Task Count
For a 50-chapter arc with average 3 scenes per chapter:
- Setup: ~5 tasks
- Chapter writing: ~50 chapters × (3 scenes + 1 integration + 3 tracking) = 350 tasks
- Arc audits: ~25 tasks (every 10 chapters × 5 checks)
- Revision: ~50 tasks (1 per chapter)
- **Total**: ~430 tasks

This ensures **百万字级别** novels maintain quality through systematic tracking and verification at every stage.
