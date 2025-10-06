# [NOVEL_TITLE] Writing Constitution
<!-- Example: "魔法纪元" Constitution, "星际流浪者" Constitution, etc. -->

## Core Writing Principles

### I. World Consistency (世界观一致性)
<!-- 世界规则必须内部自洽，一经建立不可随意违背 -->
**Mandatory Rules**:
- Magic systems, technology, or supernatural elements MUST follow consistent internal logic throughout the entire work (including 100万+ word novels)
- World-building rules established in early chapters CANNOT be arbitrarily broken later
- Every supernatural phenomenon MUST have a clear, documented explanation in the world-building notes
- Track all world rules in `/world-building/rules.md` with chapter references

**Quality Gates**:
- [ ] Before writing: Review existing world rules
- [ ] After each chapter: Verify no rule violations
- [ ] Every 10 chapters: Comprehensive consistency audit

### II. Character Arc Integrity (人物弧线完整性) 
<!-- 角色发展必须有清晰轨迹和内在逻辑 -->
**Mandatory Rules**:
- Every major character MUST have a documented character arc with clear motivation and growth trajectory
- Character behavior MUST align with their established personality profile
- Character changes MUST be gradual and justified by story events
- NO sudden personality shifts to serve plot convenience
- Track character states in `/characters/[character-name].md` with chapter-by-chapter evolution

**Quality Gates**:
- [ ] Character actions align with personality profile
- [ ] Growth is gradual and event-driven
- [ ] No out-of-character moments

### III. Foreshadowing Management (伏笔管理 - NON-NEGOTIABLE)
<!-- 伏笔追踪是百万字小说质量的关键 -->
**Mandatory Rules**:
- ALL foreshadowing MUST be tracked in `/foreshadowing/tracker.md` with:
  - Setup chapter number
  - Planned payoff chapter (or range)
  - Current status: [PLANTED] / [HINTED] / [RESOLVED] / [ABANDONED]
- Major foreshadowing MUST be resolved within 50 chapters of planting (adjustable per novel)
- Chekhov's Gun principle: Important items/characters introduced MUST have later significance
- NO dangling plot threads allowed in completed arcs

**Tracking Template**:
```markdown
## Foreshadowing Tracker
| ID | Type | Setup Chapter | Description | Payoff Chapter | Status |
|----|------|---------------|-------------|----------------|--------|
| F001 | Item | 003 | 神秘项链首次出现 | 045 | [RESOLVED] |
| F002 | Character | 012 | 提及主角父亲身世 | 120-130 | [HINTED] |
```

### IV. Timeline Accuracy (时间线准确性)
<!-- 时间线混乱是长篇小说的常见问题 -->
**Mandatory Rules**:
- Maintain a master timeline in `/timeline/master.md` with:
  - Story time (in-world dates/days)
  - Chapter number
  - Major events
  - Character locations
- Multiple POV timelines MUST sync at designated convergence points
- Flashbacks MUST be clearly marked with temporal anchors
- NO timeline contradictions allowed

**Quality Gates**:
- [ ] Every chapter: Update timeline
- [ ] Every arc: Timeline consistency check
- [ ] Multiple POVs: Verify synchronization

### V. Pacing & Rhythm (节奏控制)
<!-- 百万字作品必须保持阅读节奏 -->
**Mandatory Rules**:
- Alternate high-tension and low-tension chapters (adjust ratio per genre)
- Every chapter MUST have:
  - A clear dramatic question or conflict
  - Measurable plot/character progression
  - A hook for the next chapter
- Avoid >3 consecutive chapters of:
  - Pure exposition/worldbuilding
  - Pure dialogue with no action
  - Pure action with no character development

**Rhythm Checklist** (per chapter):
- [ ] Has conflict or dramatic question
- [ ] Advances plot OR develops character
- [ ] Ends with hook/unresolved tension

## World-Building Framework
<!-- 为百万字作品建立详实设定支撑 -->

### Required Documentation
ALL novels MUST maintain:
- `/world-building/rules.md` - Core world mechanics and constraints
- `/world-building/locations.md` - Setting details with maps/descriptions
- `/world-building/history.md` - Timeline of world events (pre-story)
- `/world-building/culture.md` - Social structures, customs, languages

### Consistency Enforcement
- Cross-reference all in-text descriptions with canonical documentation
- Version control all worldbuilding docs (track changes)
- Mark speculative/uncertain details as [NEEDS DEFINITION]

## Quality Assurance System
<!-- 确保百万字级别作品的质量不降低 -->

### Chapter-Level Checks (每章必查)
Before marking chapter complete:
- [ ] No timeline contradictions
- [ ] Characters behave consistently
- [ ] World rules not violated
- [ ] New foreshadowing logged
- [ ] Existing foreshadowing status updated
- [ ] Pacing balanced

### Arc-Level Audits (每10-20章)
Major review points:
- [ ] Character arcs progressing as planned
- [ ] Foreshadowing payoffs on schedule
- [ ] No abandoned plotlines
- [ ] Timeline synchronized across POVs
- [ ] Worldbuilding details consistent

### Milestone Reviews (每卷/50章)
Comprehensive analysis:
- [ ] All planted foreshadowing accounted for
- [ ] Character growth aligns with planned arcs
- [ ] No continuity errors
- [ ] Pacing maintains reader engagement
- [ ] Thematic coherence maintained

## Governance
<!-- 创作规范的执行 -->

**Constitution Authority**:
- This constitution supersedes all improvised plot decisions
- Violations require documented justification in `/deviations/log.md`
- Amendments allowed ONLY with clear rationale and forward planning

**Amendment Process**:
- Propose change with reason and impact analysis
- Document in constitution with amendment date
- Update all affected tracking documents
- Notify in CHANGELOG.md

**Enforcement**:
- Use `/analyze` command to verify compliance before each milestone
- Maintain deviation log for transparency
- Regular constitution reviews every 100k words

**Version**: 1.0.0 | **Ratified**: [CREATION_DATE] | **Last Amended**: [CREATION_DATE]
<!-- Update version on amendments: MAJOR (core principle change), MINOR (new rule), PATCH (clarification) -->