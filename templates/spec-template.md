# Story Arc Outline: [ARC/VOLUME NAME]

**Story Branch**: `[###-arc-name]`  
**Created**: [DATE]  
**Status**: Draft | In Progress | Complete  
**Input**: Story concept: "$ARGUMENTS"

## Execution Flow (main)
```
1. Parse story concept from Input
   → If empty: ERROR "No story description provided"
2. Extract key story elements from description
   → Identify: characters, conflicts, settings, themes, plot points
3. For each unclear aspect:
   → Mark with [NEEDS CLARIFICATION: specific question]
4. Fill Story Beats & Character Arcs section
   → If no clear narrative flow: ERROR "Cannot determine story progression"
5. Generate Plot Requirements
   → Each plot point must advance story or develop character
   → Mark ambiguous plot elements
6. Identify Key Characters & World Elements
7. Map Foreshadowing Setup Points
8. Run Review Checklist
   → If any [NEEDS CLARIFICATION]: WARN "Outline has uncertainties"
   → If writing style/prose found: ERROR "Keep outline abstract, not prose"
9. Return: SUCCESS (outline ready for detailed planning)
```

---

## ⚡ Quick Guidelines
- ✅ Focus on WHAT happens and WHY (plot & theme)
- ❌ Avoid HOW to write it (no prose, specific dialogue, detailed descriptions)
- 📖 Written for story structure, not final narrative

### Section Requirements
- **Mandatory sections**: Must be completed for every arc/volume
- **Optional sections**: Include only when relevant to this arc
- When a section doesn't apply, remove it entirely (don't leave as "N/A")

### For AI Generation
When creating this outline from a user prompt:
1. **Mark all ambiguities**: Use [NEEDS CLARIFICATION: specific question] for any assumption you'd need to make
2. **Don't guess character motivations**: If unclear, mark it
3. **Think like a reader**: Every vague plot point should fail the "clear and purposeful" checklist
4. **Common underspecified areas**:
   - Character motivations and goals
   - Conflict escalation patterns
   - Thematic significance of events
   - World-building details that affect plot
   - Timeline and pacing targets
   - Foreshadowing payoff plans

---

## Story Beats & Character Arcs *(mandatory)*

### Primary Plot Thread
[Describe the main story progression in 100-300 words: beginning state → key conflicts → resolution]

### Key Story Beats
1. **Inciting Incident**: [What disrupts the status quo?]
   - **Chapter Range**: [e.g., 001-003]
   - **Character State**: [Protagonist's emotional/situational state]

2. **Rising Action**: [What complications arise?]
   - **Chapter Range**: [e.g., 004-020]
   - **Conflicts Introduced**: [List 2-4 major conflicts]
   - **Character Development**: [How protagonist changes]

3. **Midpoint Turn**: [What major revelation or setback occurs?]
   - **Chapter Range**: [e.g., 021-025]
   - **Stakes Change**: [How the situation intensifies]

4. **Climax**: [What is the final confrontation?]
   - **Chapter Range**: [e.g., 040-045]
   - **Resolution Type**: [Victory/Loss/Bittersweet/Transformation]

5. **Falling Action & Resolution**: [How do consequences play out?]
   - **Chapter Range**: [e.g., 046-050]
   - **Character End State**: [Final emotional/situational position]

### Character Arcs
#### Protagonist: [NAME]
- **Starting Point**: [Beliefs, skills, emotional state, goals]
- **Arc Type**: [Growth/Fall/Flat/Transformation]
- **Key Turning Points**: 
  - Chapter X: [Event that challenges beliefs]
  - Chapter Y: [Decision that shows change]
  - Chapter Z: [Culmination of arc]
- **Ending Point**: [How they've changed OR what they've proven]

#### Supporting Character: [NAME]
- **Role in Story**: [Mentor/Antagonist/Love Interest/Foil/etc.]
- **Arc**: [Brief description of their journey, if any]
- **Relationship to Protagonist**: [How it evolves]

---

## Plot Requirements *(mandatory)*

### Core Plot Points
- **PP-001**: Story MUST establish [protagonist's ordinary world and goals] by Chapter [X]
- **PP-002**: Story MUST introduce [central conflict] in Chapter [X]
- **PP-003**: Story MUST escalate stakes through [specific complications]
- **PP-004**: Story MUST reveal [key information] that changes protagonist's understanding
- **PP-005**: Story MUST resolve [central conflict] while leaving [sequel hooks if applicable]

*Example of marking unclear plot elements:*
- **PP-006**: Antagonist MUST be motivated by [NEEDS CLARIFICATION: revenge? ideology? survival? not specified]
- **PP-007**: Midpoint should reveal [NEEDS CLARIFICATION: what secret/truth changes everything?]

### Thematic Requirements
- **TH-001**: Explore theme of [e.g., "redemption through sacrifice"]
- **TH-002**: Contrast [concept A] with [concept B] through [character/plot device]
- **TH-003**: Culminate thematic journey in [specific scene or realization]

### Key World Elements *(include if story involves world-building)*
- **[Location/Setting]**: [What it represents, key features, how it affects plot]
- **[Magic System/Technology]**: [Rules, limitations, how it drives conflict]
- **[Culture/Society]**: [Social structures, conflicts, how they impact characters]

---

## Foreshadowing Map *(critical for long novels)*

### Foreshadowing to Plant
| ID | Type | Setup Chapter | What to Plant | Payoff Chapter | Importance |
|----|------|---------------|---------------|----------------|------------|
| F001 | Item | 003 | [神秘武器首次出现] | 045 | Critical |
| F002 | Prophecy | 008 | [预言提及的事件] | 060-070 | Major |
| F003 | Character Secret | 015 | [暗示配角的真实身份] | 035 | Major |
| F004 | World Rule | 001 | [建立魔法的代价] | Throughout | Critical |

### Foreshadowing to Resolve (from previous arcs)
- [ ] **F-XXX** from Arc [Y]: [How this arc pays it off]

---

## Timeline & Pacing

### Story Time Span
- **In-World Duration**: [e.g., 3 months, 5 years, one week]
- **Chapter Count Target**: [e.g., 50 chapters]
- **Word Count Target**: [e.g., 150,000 words]

### Pacing Targets
- **Setup Phase**: Chapters 1-10 (20%)
- **Rising Action**: Chapters 11-35 (50%)
- **Climax & Resolution**: Chapters 36-50 (30%)

### Multiple POV Timeline *(if applicable)*
- **POV A**: [Character name] - Chapters [list]
- **POV B**: [Character name] - Chapters [list]
- **Convergence Points**: [Where timelines intersect - chapters X, Y, Z]

---

## Review & Acceptance Checklist
*GATE: Automated checks run during main() execution*

### Narrative Quality
- [ ] No prose or specific dialogue (structure only)
- [ ] Focused on story progression and character development
- [ ] Clear beginning, middle, and end
- [ ] All mandatory sections completed

### Plot Completeness
- [ ] No [NEEDS CLARIFICATION] markers remain
- [ ] Plot points are clear and purposeful
- [ ] Character arcs have beginning and end states
- [ ] Conflicts are well-defined
- [ ] Foreshadowing is mapped
- [ ] Timeline is coherent

### Constitution Compliance
- [ ] No violations of world consistency rules
- [ ] Character arcs align with established personalities
- [ ] Foreshadowing tracking is complete
- [ ] Timeline conflicts resolved
- [ ] Pacing targets are reasonable

---

## Execution Status
*Updated by main() during processing*

- [ ] Story concept parsed
- [ ] Key story elements extracted
- [ ] Ambiguities marked
- [ ] Story beats defined
- [ ] Plot requirements generated
- [ ] Characters & world elements identified
- [ ] Foreshadowing mapped
- [ ] Review checklist passed

---

## Notes for Next Phase
*Guidance for /plan command*
- Particularly complex scenes that need detailed planning: [list]
- Research needed: [historical details, technical accuracy, cultural elements]
- Sensitive topics requiring careful handling: [list]
