# 命令文件验证清单

## ✅ 占位符使用检查

| 占位符 | 用途 | 位置 | 状态 |
|--------|------|------|------|
| `{SCRIPT}` | 代表要执行的脚本（sh或ps根据系统） | 命令文档中，运行脚本时 | ✅ 正确 |
| `$ARGUMENTS` | 显示用户输入内容 | 命令文档开头"User input"部分 | ✅ 正确 |
| `{ARGS}` | 传递参数到脚本 | scripts部分（YAML前置）+ 文档末尾context | ✅ 正确 |

## ✅ 脚本引用检查

| 命令 | Bash脚本 | PowerShell脚本 | 状态 |
|------|----------|----------------|------|
| `/specify` | `scripts/bash/create-new-feature.sh --json "{ARGS}"` | `scripts/powershell/create-new-feature.ps1 -Json "{ARGS}"` | ✅ |
| `/clarify` | `scripts/bash/check-prerequisites.sh --json --paths-only` | `scripts/powershell/check-prerequisites.ps1 -Json -PathsOnly` | ✅ |
| `/plan` | `scripts/bash/setup-plan.sh --json` | `scripts/powershell/setup-plan.ps1 -Json` | ✅ |
| `/tasks` | `scripts/bash/check-prerequisites.sh --json --paths-only` | `scripts/powershell/check-prerequisites.ps1 -Json -PathsOnly` | ✅ |
| `/implement` | `scripts/bash/check-prerequisites.sh --json --require-tasks --include-tasks` | `scripts/powershell/check-prerequisites.ps1 -Json -RequireTasks -IncludeTasks` | ✅ |
| `/analyze` | `scripts/bash/check-prerequisites.sh --json --require-tasks --include-tasks` | `scripts/powershell/check-prerequisites.ps1 -Json -RequireTasks -IncludeTasks` | ✅ |
| `/constitution` | 无脚本 | 无脚本 | ✅ |

## ✅ 模板引用检查

| 命令 | 引用的模板文件 | 路径正确性 | 状态 |
|------|---------------|-----------|------|
| `/specify` | `templates/spec-template.md` | ✅ 相对路径 | ✅ |
| `/plan` | `/templates/plan-template.md` | ✅ 绝对路径 | ✅ |
| `/tasks` | `/templates/tasks-template.md` | ✅ 绝对路径 | ✅ |
| `/constitution` | `/memory/constitution.md` | ✅ 绝对路径 | ✅ |
| `/constitution` | 所有模板文件（consistency check） | ✅ | ✅ |

## ✅ 关键逻辑流程检查

### `/specify` 命令
- [x] 1. 运行脚本获取 BRANCH_NAME 和 SPEC_FILE
- [x] 2. 加载 spec-template.md
- [x] 3. 检测项目类型（小说 vs 软件）
- [x] 4. 根据类型使用对应的模板结构
- [x] 5. 写入 SPEC_FILE
- [x] 6. 报告完成

### `/clarify` 命令
- [x] 1. 运行脚本获取 FEATURE_DIR 和 FEATURE_SPEC
- [x] 2. 加载当前 spec 文件
- [x] 3. 检测项目类型
- [x] 4. 根据类型执行不同的模糊检测分类（小说：Plot/Character/Foreshadowing vs 软件：Functional/Data Model）
- [x] 5. 生成最多5个问题
- [x] 6. 顺序提问并集成答案
- [x] 7. 更新 spec 文件
- [x] 8. 报告完成

### `/plan` 命令
- [x] 1. 运行脚本获取 FEATURE_SPEC, IMPL_PLAN, SPECS_DIR, BRANCH
- [x] 2. 检查 Clarifications 是否存在（警告用户）
- [x] 3. 读取并分析 spec
- [x] 4. 检测项目类型
- [x] 5. 读取 constitution
- [x] 6. 根据类型执行对应的规划流程：
   - 小说：Narrative Context + scene-breakdown + character-states + continuity-check
   - 软件：Technical Context + data-model + contracts + quickstart
- [x] 7. 验证完成
- [x] 8. 报告结果

### `/tasks` 命令
- [x] 1. 运行脚本获取路径
- [x] 2. 加载 plan.md
- [x] 3. 检测项目类型
- [x] 4. 根据类型生成任务：
   - 小说：场景写作 + 质量追踪 + 定期审计
   - 软件：Setup + Tests + Implementation + Polish
- [x] 5. 编号任务
- [x] 6. 生成依赖图
- [x] 7. 验证完整性
- [x] 8. 写入 tasks.md
- [x] 9. 报告完成

### `/implement` 命令
- [x] 1. 运行脚本获取路径
- [x] 2. 加载 tasks.md 和 plan.md
- [x] 3. 检测项目类型
- [x] 4. 解析任务结构
- [x] 5. 根据类型执行对应工作流：
   - 小说：Setup → 场景写作 → 质量追踪 → 审计 → 修订
   - 软件：Setup → Tests (TDD) → Implementation → Integration → Polish
- [x] 6. 进度追踪和错误处理
- [x] 7. 标记完成的任务
- [x] 8. 验证完成
- [x] 9. 报告状态

### `/analyze` 命令
- [x] 1. 运行脚本获取路径
- [x] 2. 加载 spec, plan, tasks
- [x] 3. 检测项目类型
- [x] 4. 根据类型执行检查：
   - 小说：伏笔回收 + 时间线一致性 + 角色一致性 + 世界观 + POV
   - 软件：重复 + 模糊 + 覆盖率 + Constitution对齐
- [x] 5. 严重性分级（CRITICAL/HIGH/MEDIUM/LOW）
- [x] 6. 生成Markdown报告
- [x] 7. 输出Next Actions
- [x] 8. 询问是否需要修复建议（READ-ONLY原则）

### `/constitution` 命令
- [x] 1. 加载现有 constitution 模板
- [x] 2. 检测项目类型（从用户输入）
- [x] 3. 识别占位符
- [x] 4. 根据类型收集/推导值：
   - 小说：世界观一致性、角色弧线、伏笔管理、时间线、节奏
   - 软件：Library-First、CLI Interface、Test-First、Simplicity
- [x] 5. 填充模板
- [x] 6. 一致性传播检查（更新所有相关模板和文档）
- [x] 7. 生成Sync Impact Report
- [x] 8. 验证
- [x] 9. 写入 constitution.md
- [x] 10. 输出总结

## ✅ 项目类型检测机制

### 小说写作关键词
```
plot, character, protagonist, antagonist, chapter, scene, arc, volume,
foreshadowing, conflict, theme, world-building, timeline, POV, narrative
```

### 软件开发关键词
```
feature, API, endpoint, database, user, authentication, frontend, backend,
service, code, test, implementation, deployment, architecture
```

### 检测位置
- `/specify`: 从用户输入检测
- `/clarify`: 从 spec.md 内容检测
- `/plan`: 从 spec.md 内容检测
- `/tasks`: 从 plan.md 内容检测
- `/implement`: 从 tasks.md 内容检测
- `/analyze`: 从项目文件结构检测
- `/constitution`: 从用户输入检测

## ✅ 文件路径一致性

所有命令都正确使用：
- `/memory/constitution.md` - Constitution文件
- `/templates/spec-template.md` - Spec模板
- `/templates/plan-template.md` - Plan模板
- `/templates/tasks-template.md` - Tasks模板
- `specs/[###-feature-name]/` - 功能/章节目录
- `/foreshadowing/tracker.md` - 伏笔追踪（小说）
- `/timeline/master.md` - 时间线（小说）
- `/characters/*.md` - 角色档案（小说）
- `/world-building/*.md` - 世界观设定（小说）

## ✅ 关键改进验证

### 1. 双模式支持
- ✅ 所有命令都包含项目类型检测
- ✅ 根据类型使用不同的术语和工作流
- ✅ 小说和软件开发可以共存

### 2. 小说写作特性
- ✅ 伏笔追踪系统（IDs, 状态, 回收计划）
- ✅ 时间线管理（事件序列, 角色位置, 时长）
- ✅ 角色一致性（章节级状态追踪）
- ✅ 质量分级检查（章级/卷级/里程碑级）
- ✅ 并行写作支持（[P]标记）

### 3. Constitution双模式
- ✅ 小说：世界观一致性、角色弧线、伏笔管理、时间线、节奏
- ✅ 软件：Library-First、Test-First、CLI Interface、Simplicity
- ✅ 自动检测并应用对应原则

## 🔍 潜在问题检查

### 检查项
- [x] 所有脚本路径存在且正确
- [x] 占位符格式统一
- [x] 模板引用路径正确
- [x] 逻辑流程完整
- [x] 错误处理存在
- [x] 文件读写权限考虑
- [x] 跨平台兼容性（sh + ps）

### 发现的问题
**无重大问题发现** ✅

## ✅ 最终验证结果

**所有7个命令文件都已验证通过，可以正常执行！**

### 关键验证点
1. ✅ 占位符使用正确（`{SCRIPT}`, `$ARGUMENTS`, `{ARGS}`）
2. ✅ 脚本引用完整（bash + powershell）
3. ✅ 模板路径正确
4. ✅ 逻辑流程完整
5. ✅ 项目类型检测机制健全
6. ✅ 双模式支持完整
7. ✅ 错误处理充分
8. ✅ READ-ONLY原则遵守（/analyze）

### 可执行性确认
- ✅ 所有命令都能正确调用对应的bash/powershell脚本
- ✅ 所有命令都能正确读取和写入文件
- ✅ 所有命令都能正确检测项目类型并应用对应逻辑
- ✅ 所有命令的输入输出流程清晰
- ✅ 命令之间的依赖关系明确（specify → clarify → plan → tasks → implement/analyze）

## 📝 使用建议

1. **首次使用**：按顺序执行 `/constitution` → `/specify` → `/plan` → `/tasks` → `/implement`
2. **质量检查**：在重要里程碑运行 `/analyze`
3. **细化需求**：在 `/plan` 之前运行 `/clarify`（可选但推荐）
4. **项目切换**：框架会自动检测项目类型，无需手动配置

**验证日期**: 2025-10-06
**验证状态**: ✅ PASS

