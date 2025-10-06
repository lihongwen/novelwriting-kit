# 📚 Novel Writing Kit 使用指南

> 基于 Spec-Driven Development 框架，专为**百万字级别长篇小说**设计的结构化创作工具包

## 🎯 核心理念

将软件开发的**规范驱动**方法应用于小说创作，通过：
- **世界观宪法**：建立不可违背的创作规则
- **结构化大纲**：清晰的故事架构和角色弧线
- **伏笔追踪系统**：确保所有伏笔都有回收
- **时间线管理**：避免时间线矛盾
- **质量检查点**：每个阶段都有验证机制

**适用于**：百万字网文、系列小说、多卷史诗、复杂世界观作品

---

## 🚀 快速开始

### 1. 初始化项目

```bash
# 安装 Specify CLI
uv tool install specify-cli --from git+https://github.com/lihongwen/novelwriting-kit.git

# 创建小说项目（选择你喜欢的 AI 助手）
specify init my-novel --ai claude
# 或
specify init my-novel --ai cursor
# 或
specify init my-novel --ai copilot
```

### 2. 建立创作准则（Constitution）

使用 `/constitution` 命令建立你的小说世界观规则和写作原则：

```
/constitution 

创建一部玄幻小说的创作准则：
- 世界观：修真体系分为炼气、筑基、金丹、元婴、化神五个大境界，每个境界突破需要特定条件
- 角色设定：主角性格谨慎、重视因果，绝不随意杀戮
- 伏笔规则：所有在前50章出现的重要物品或人物，必须在200章内有明确作用
- 时间线：故事时间跨度约10年，需要详细记录每个重要时间节点
- 叙事风格：第三人称限知视角，以主角视角为主，偶尔切换到配角视角推进支线
```

**这将生成**：`/memory/constitution.md` - 你的小说创作宪法

---

## 📖 完整创作流程

### 阶段 1：故事大纲（/specify）

为一个故事卷/章节创建高层次的情节大纲：

```
/specify

第一卷：崭露头角

主角林轩在小宗门中是一个不起眼的外门弟子，但他意外获得了一块能够吸收他人修炼感悟的神秘玉佩。
他必须小心隐藏这个秘密，同时利用玉佩快速提升实力。

本卷主要冲突：
1. 宗门选拔大比即将来临，他需要在3个月内从炼气三层突破到炼气九层
2. 一位内门师兄发现了他的异常，开始怀疑和调查
3. 魔道势力潜入宗门，策划夺取宗门灵脉

角色发展：
- 林轩从胆怯谨慎的新人，逐渐建立自信，但保持警惕
- 结识好友张阳（憨厚直率）和柳诗音（冰冷外表下温柔）
- 与内门师兄陈默产生敌对关系

伏笔设置：
- 玉佩的来历（提及古代大能）
- 主角身世之谜（父母失踪）
- 魔道为何知晓宗门内部情报（内奸）
```

**这将生成**：`/specs/001-first-volume/spec.md` - 包含：
- 故事节拍（Inciting Incident, Rising Action, Climax等）
- 角色弧线规划
- 情节要点
- **伏笔映射表**（关键！）
- 时间线和节奏目标

### 阶段 2：深化细节（/clarify）

可选但**强烈推荐**，用于解决大纲中的模糊点：

```
/clarify
```

AI 会系统性地问你问题，例如：
- "玉佩吸收感悟的具体机制是什么？有什么限制？"
- "内门师兄陈默怀疑的具体证据是什么？"
- "魔道袭击的时机是在大比之前还是之后？"

这个阶段会更新 spec.md 的 `## Clarifications` 部分。

### 阶段 3：章节规划（/plan）

根据大纲创建详细的章节和场景规划：

```
/plan

本卷预计50章，每章3000-5000字，共计15-25万字。

叙事风格：第三人称限知，主要跟随林轩视角
节奏：快节奏修炼穿插人物互动，每5章一个小高潮

重点章节：
- 第8章：获得玉佩
- 第25章：第一次面对陈默的试探
- 第45章：宗门大比
- 第50章：魔道袭击，卷末高潮
```

**这将生成**：
- `plan.md` - 章节规划总览
- `scene-breakdown.md` - **逐场景详细计划**（每一场的目的、人物、情绪弧线、伏笔）
- `character-states.md` - 角色逐章状态追踪
- `continuity-check.md` - 时间线和伏笔验证表
- `research.md` - 需要研究的历史/技术细节

**重点查看 `scene-breakdown.md`**，它包含每一场景的：
```markdown
### Scene 1: 外门杂务
- 时间：清晨
- 地点：杂务院
- 场景目的：建立主角的平凡背景，种下不甘的种子
- 情绪弧线：麻木疲惫 → 触发事件（被欺负） → 隐忍愤怒
- 伏笔：提及林轩父母曾是宗门精英（F005）
```

### 阶段 4：生成写作任务（/tasks）

将章节计划分解为具体的写作任务：

```
/tasks
```

**这将生成**：`tasks.md` - 包含 200-400 个具体任务，例如：

```markdown
## Phase 3.2: Scene Writing (First Draft)

### Chapter 001: 外门弟子
- [ ] T006 Write Scene 1 in chapters/001-outer-disciple.md
- [ ] T007 Write Scene 2 in chapters/001-outer-disciple.md
- [ ] T008 Write Scene 3 in chapters/001-outer-disciple.md
- [ ] T009 Integrate scenes for chapter flow
- [ ] T010 Log new foreshadowing from Ch001 in /foreshadowing/tracker.md
- [ ] T011 Update timeline with Ch001 events in /timeline/master.md

### Chapter 002: 意外奇遇
- [ ] T013 [P] Write Scene 1 in chapters/002-jade-pendant.md
  ← 可以和其他章节并行写作
```

### 阶段 5：执行写作（/implement）

开始实际写作：

```
/implement
```

AI 会按照 tasks.md 的顺序执行写作任务，并：
- 生成章节内容到 `chapters/001-xxx.md`
- 自动更新 `/foreshadowing/tracker.md`（伏笔追踪）
- 自动更新 `/timeline/master.md`（时间线）
- 自动更新 `/characters/林轩.md` 等角色文件

### 阶段 6：质量检查（/analyze）

**关键步骤！** 在每个卷完成后运行：

```
/analyze
```

这会检查：
- ✅ 所有伏笔是否已记录和回收
- ✅ 时间线是否有矛盾
- ✅ 角色行为是否符合性格设定
- ✅ 世界观规则是否被违反
- ✅ 节奏是否平衡

会生成质量报告，指出需要修正的问题。

---

## 📁 项目文件结构

```
my-novel/
├── memory/
│   └── constitution.md          # 创作宪法（世界观规则、写作原则）
├── specs/
│   ├── 001-first-volume/        # 第一卷
│   │   ├── spec.md              # 故事大纲
│   │   ├── plan.md              # 章节规划
│   │   ├── scene-breakdown.md   # 场景分解（核心文档！）
│   │   ├── character-states.md  # 角色状态追踪
│   │   ├── continuity-check.md  # 连贯性检查
│   │   └── tasks.md             # 写作任务列表
│   ├── 002-second-volume/       # 第二卷
│   └── ...
├── chapters/                    # 实际章节内容
│   ├── 001-outer-disciple.md
│   ├── 002-jade-pendant.md
│   └── ...
├── characters/                  # 角色档案
│   ├── 林轩.md                  # 主角
│   ├── 张阳.md                  # 配角
│   └── ...
├── world-building/              # 世界观设定
│   ├── rules.md                 # 修真体系、魔法规则等
│   ├── locations.md             # 地点描述
│   ├── history.md               # 历史背景
│   └── culture.md               # 文化设定
├── foreshadowing/
│   └── tracker.md               # 伏笔追踪总表（超重要！）
└── timeline/
    └── master.md                # 主时间线
```

---

## 🔑 关键功能详解

### 1. 伏笔追踪系统

**为什么重要**：百万字小说最容易出现的问题就是伏笔挖坑不填。

**怎么用**：
- 在 `/specify` 阶段规划伏笔
- AI 会在 `spec.md` 中生成伏笔映射表
- 在 `/plan` 阶段，每个场景都会标注：
  - `Plant`：新设置的伏笔
  - `Hint`：暗示已有伏笔
  - `Payoff`：回收伏笔
- 写作时，AI 会自动更新 `/foreshadowing/tracker.md`

**示例**：
```markdown
| ID | Type | Setup Chapter | Description | Payoff Chapter | Status |
|----|------|---------------|-------------|----------------|--------|
| F001 | Item | 003 | 神秘玉佩首次出现 | 045 | [RESOLVED] |
| F002 | Character | 012 | 提及主角父亲身世 | 120-130 | [HINTED] |
| F005 | Prophecy | 001 | 父母曾是精英 | 200+ | [PLANTED] |
```

### 2. 时间线管理

**为什么重要**：多POV、多线叙事容易时间混乱。

**怎么用**：
- `/timeline/master.md` 记录所有事件的时间顺序
- 每写完一章，更新时间线
- `/analyze` 会检查时间线矛盾

**示例**：
```markdown
| Chapter | In-Story Date | Events | Duration |
|---------|---------------|--------|----------|
| 001 | 修真历 1205年3月1日 | 林轩在杂务院做工 | 1天 |
| 002 | 1205年3月2日 | 发现玉佩 | 半天 |
| 003 | 1205年3月2日晚-3日 | 尝试使用玉佩 | 1晚 |
```

### 3. 角色一致性检查

**为什么重要**：长篇小说容易出现人物性格前后矛盾。

**怎么用**：
- 在 `/characters/` 目录为每个主要角色创建档案
- 记录：性格特征、成长轨迹、知识状态、情感变化
- AI 会检查角色行为是否符合设定

**示例** (`/characters/林轩.md`):
```markdown
## 核心性格
- 谨慎多疑（因童年经历）
- 重视承诺（父母遗训）
- 不轻易展露实力

## Chapter 015 状态
- 物理：炼气六层，右臂有旧伤
- 情感：对张阳信任加深，对柳诗音有好感
- 知识：已知玉佩能吸收感悟，但不知来历
- 目标：突破到炼气九层，查探父母失踪真相
```

---

## 💡 最佳实践

### 1. 分卷规划
- 每卷 15-30 万字（50-100章）
- 每卷对应一个独立分支（如 `001-first-volume`）
- 一卷完成后再开始下一卷

### 2. 定期质量检查
- **每写完 10 章**：运行一次小范围检查
- **每完成一卷**：运行完整 `/analyze`
- **重点检查**：伏笔状态、时间线、角色一致性

### 3. 利用并行写作
- 不同章节的场景可以并行生成（tasks.md 中的 `[P]` 标记）
- 适合有多个 AI 助手或多次会话的情况

### 4. 保持宪法权威性
- 所有创作决定必须符合 `constitution.md`
- 如果要违反规则，必须在 `Narrative Concerns` 部分记录理由
- 定期回顾宪法，确保没有悄悄违背

### 5. 角色驱动情节
- 在 `/specify` 阶段就规划好角色弧线
- 让情节服务于角色成长，而不是为了情节扭曲角色

---

## 🎨 适配不同小说类型

### 玄幻/修真
- Constitution 重点：修炼体系规则、境界突破条件
- Foreshadowing：宝物、功法、身世、仇敌
- Timeline：修炼时间、年龄增长

### 都市/现代
- Constitution 重点：现实世界规则、人物关系网
- Foreshadowing：商业布局、感情线、反转
- Timeline：精确到小时的时间线

### 科幻
- Constitution 重点：科技设定、物理规则、未来社会
- Foreshadowing：科技伏笔、世界观秘密
- Timeline：可能跨越年份甚至世纪

### 悬疑推理
- Constitution 重点：线索公平性、逻辑严密性
- Foreshadowing：证据链、凶手动机、误导线索
- Timeline：案发时间、人物行踪

---

## 🔧 故障排除

### Q: AI 生成的内容不符合我的风格？
**A**: 在 constitution.md 中详细描述你的叙事风格、用词偏好、避免使用的表达。

### Q: 伏笔太多，管理不过来？
**A**: 
- 使用 `/foreshadowing/tracker.md` 的状态列（PLANTED/HINTED/RESOLVED）
- 每10章做一次伏笔审计
- 对不重要的伏笔标记为 ABANDONED（并在故事中自然淡化）

### Q: 时间线出现矛盾？
**A**:
- 使用 `/analyze` 自动检测
- 手动修正 `/timeline/master.md`
- 回到相关章节调整时间描述

### Q: 角色性格崩塌？
**A**:
- 检查 `/characters/[name].md` 的核心性格设定
- 确保 `character-states.md` 中的变化是渐进的
- 在 constitution.md 中加强"Character Arc Integrity"规则

---

## 🌟 示例项目

查看 `/examples/xianxia-novel/` 目录（如果提供）了解完整的玄幻小说项目示例。

---

## 📚 命令速查表

| 命令 | 用途 | 输出 |
|------|------|------|
| `/constitution` | 建立世界观和写作规则 | `memory/constitution.md` |
| `/specify` | 创建故事卷大纲 | `specs/###-arc/spec.md` |
| `/clarify` | 深化不明确的情节点 | 更新 spec.md 的 Clarifications |
| `/plan` | 详细章节和场景规划 | plan.md, scene-breakdown.md 等 |
| `/tasks` | 生成写作任务列表 | tasks.md |
| `/implement` | 执行写作 | chapters/###.md + 各种追踪文件 |
| `/analyze` | 质量和一致性检查 | 质量报告 |

---

## 🎯 成功案例工作流

**目标**：完成一部 100 万字的玄幻小说（约 10 卷）

**工作流**：

1. **第 0 天**：`/constitution` 建立修真体系、主角性格、世界观规则
2. **第 1 天**：`/specify` 第一卷大纲（崭露头角）
3. **第 2 天**：`/clarify` 完善模糊点，`/plan` 生成 50 章规划
4. **第 3 天**：`/tasks` 生成任务，`/implement` 开始写作前 10 章
5. **第 4-7 天**：持续 `/implement`，完成第一卷（50章，15万字）
6. **第 8 天**：`/analyze` 全面质量检查，修正问题
7. **第 9 天**：开始第二卷 `/specify`...

**10 卷后**：100 万字完成，且质量稳定，伏笔全部回收，无时间线矛盾！

---

**祝你写作愉快！有任何问题请查看 README.md 或提交 issue。**

