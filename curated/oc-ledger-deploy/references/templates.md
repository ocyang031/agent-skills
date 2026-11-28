# 目录结构与模板

## 目录树

```text
010_oc-ledger/
├─ .agents/
│  ├─ adapters/          # 每个 agent 工具一份接入约定
│  ├─ config/            # 工具与机器的复用配置（如各工具接入参数），无内容时可空置
│  ├─ drafts/            # 待分拣的沉淀候选
│  ├─ learnings/         # self-improvement 日志落点，部署时只建空目录
│  ├─ memory/            # 按工具分目录的短期流水
│  ├─ rules/             # 按任务加载的行为规则
│  ├─ scripts/           # agent 辅助脚本，不内嵌秘密值
│  └─ skills/            # 部署产物，版本控制忽略
├─ .artifacts/           # 机器生成、非交付、可重跑的中间产物
├─ 000_Inbox/
│  ├─ 010_Downloads/
│  └─ imported/          # 首次落地时抽取的待判断资料
├─ 050_Knowledge/
│  └─ Obsidian/          # 知识库
├─ 100_Works/
│  ├─ <归属前缀>-<项目名>/
│  └─ _archive/          # 结项项目按年份归档
├─ 200_Digital_assets/
│  ├─ 210_Personal-record/
│  ├─ 220_Docs/
│  ├─ 230_Picture/
│  ├─ 240_E-book/
│  └─ 250_Videos/
├─ 300_Dev/
├─ 400_Code/
├─ 900_ADR/
├─ AGENTS.md
├─ MEMORY.md
├─ CONTEXT.md
├─ DESIGN.md
├─ HANDOFF.md
├─ ONBOARDING.md
└─ README.md
```

## 路径规则

| 路径 | 用途与规则 |
| --- | --- |
| `AGENTS.md` | 唯一外层根。最小内核：工作区身份、访问限制、授权要求、记忆读写、任务路由。知识库内自带的规则文件只细化知识库内部，不得放宽外层。 |
| `MEMORY.md` | 跨会话稳定事实。只追加，每条带来源与日期。 |
| `HANDOFF.md` | 任务账本，记录进行中的目标、未完成和堵塞。单文件、覆盖写。格式规则见 operating-rules.md 记忆与账本一节。 |
| `CONTEXT.md` | 术语表：按主题分组，每条含定义与不推荐称呼（`_Avoid_`），只解释概念，不写实现。 |
| `DESIGN.md` | 三层边界、文件流转、存储与维护原则。 |
| `README.md` | 面向人的入口，登记本机路径映射。 |
| `ONBOARDING.md` | 新机 / 新 agent 接入的唯一入口手册，接入方克隆后先读它；正文模板见本文件「新机接入手册」块。 |
| `.agents/adapters/` | 每个 agent 工具一份接入约定与验收项。 |
| `.agents/drafts/` | 沉淀候选草稿箱：agent 自动写，用户分拣；分拣前不构成权威，版本控制忽略，可由流水重新生成。被否决的草稿移入 `.agents/drafts/rejected/` 保留，不删除。 |
| `.agents/memory/` | 短期流水，按 `<工具名>/<日期>.md` 分文件，只追加。 |
| `.agents/learnings/` | self-improvement 日志（LEARNINGS/ERRORS/FEATURE_REQUESTS）落点；部署时只建空目录，日志文件随该技能接入时生成。 |
| `.agents/rules/` | 按任务路由加载的细则；敏感区限制、删除确认、授权要求不在此列，必须常驻在 `AGENTS.md`。 |
| `.agents/scripts/` | 辅助脚本，不内嵌秘密值。 |
| `.agents/skills/` | 由 skill 事实源仓库部署而来，本身不是事实源，版本控制忽略。 |
| `.artifacts/` | 机器生成的中间产物，可删除、可重跑。按“任务或项目/日期-用途”分目录，默认保留 14 天，放 `.keep` 可豁免；索引只保留 `index.json` 并纳入版本控制；清理先列出待删项再执行。 |
| `000_Inbox/` | 暂存区，不长期堆放，不进清单和备份。 |
| `010_Downloads/` | 下载暂存，定期清空。编号表示它属于“可清空暂存”这一族，后续暂存类别顺延编号。 |
| `imported/` | 抽取证据，例外保留，不随暂存区清空。不编号，以区别于可清空暂存。 |
| `050_Knowledge/Obsidian/` | 知识库：笔记、Daily、长期领域和治理材料。 |
| `100_Works/` | 项目过程资料、项目专属测试内容、执行证据和报告。项目目录命名用 `<归属前缀>-<项目名>`；归属前缀表由用户定，在定下来之前暂行只用项目名，不编前缀。结项后整目录移入 `_archive/<年份>/`，不另设一级归档目录。 |
| `200_Digital_assets/` | 不属于项目、记录或知识主题、需要独立保存的资产；有归属的跟随对象存放，不因格式拆散。 |
| `210_Personal-record/` | 证件资质、财务保障、教育任职资料。默认排除，按任务授权访问；写入版本控制忽略，不进云同步或对象存储，只走加密备份盘；部署与自检显式跳过。 |
| `220_Docs/` `230_Picture/` `240_E-book/` `250_Videos/` | 独立管理的文档、图片、电子书和视频。 |
| `300_Dev/` | 工具清单、安装说明、版本与重建步骤；不放应用本体和真实凭据。机器层承诺到“清单 + 安装脚本”为止，不追求逐字节复现。 |
| `400_Code/` | 外部代码仓库，直接平铺，不设分组子目录。每一项都是一个独立版本控制单元，各自独立版本控制，根版本控制整体忽略。 |
| `900_ADR/` | 决策记录（ADR）：工作区级裁定结论的唯一承载，一条决定一个文件，顺序编号，格式见“决策记录（ADR）”一节。 |

## 编号规则（定死，不再讨论）

- 顶层目录保留编号（000/050/100/200/300/400/900）。编号是顺序：默认排序下正好是工作流顺序（输入、知识、项目、资产、开发、代码），9xx 段为低频治理记录，默认排序居末；留空的号位供后续目录插入而不改动已有目录。
- `400_Code/`、`300_Dev/` 下面的子目录不编号，用 plain 名称。仓库名、工具名就是身份，集合开放，顺序无意义。
- `200_Digital_assets/` 下面的五个子目录保留编号（210–250），因为它们是封闭固定的五类加固定顺序。新增资产类别从 260 起顺延。
- `100_Works/` 下面的项目目录不编号，用归属前缀加项目名。
- `000_Inbox/` 下面保持 `010_Downloads/`（编号）与 `imported/`（不编号）并存，不对称是有意的：编号标记可清空暂存，不编号标记保留证据。不要给 `imported/` 加编号，那会暗示它也可清空。

## 资产清单

`200_Digital_assets/` 的完整性清单：登记该区资产文件的 SHA-256，唯一用途是核验资产没丢、没坏、没被改；不是资产目录（不记标题、作者等元数据），不是备份。

- 文件名与位置：`200_Digital_assets/MANIFEST.sha256`，进根仓库版本控制。
- 格式：标准 sha256sum 格式，一行一个文件：`<sha256>␣␣<相对路径>`（哈希与路径之间两个空格）；路径相对 `200_Digital_assets/`、按路径排序；不写注释行、不写生成时间（生成时间看 git 记录），保证 `sha256sum -c` 干净通过。
- 覆盖范围：210 之外各类（`220_Docs/`、`230_Picture/`、`240_E-book/`、`250_Videos/` 及 260 起新增类别）及其子目录下的全部普通文件；清单文件自身除外。
- 敏感区单独成册：`210_Personal-record/MANIFEST.sha256`，同格式同规则，位于整目录被忽略的敏感区内，不进版本控制，只在本机核验；根清单不得出现 210 下任何路径。
- 生成命令：在 `200_Digital_assets/` 内执行，整表重建，不手改、不增量编辑：

```bash
find . -type f ! -name 'MANIFEST.sha256' ! -path './210_Personal-record/*' -print0 | LC_ALL=C sort -z | xargs -0 sha256sum > MANIFEST.sha256
```

  210 册在其目录内执行：

```bash
find . -type f ! -name 'MANIFEST.sha256' -print0 | LC_ALL=C sort -z | xargs -0 sha256sum > MANIFEST.sha256
```

- 更新时机：覆盖范围内任何新增、删除、改名、改内容之后，重跑生成命令整表重建。
- 核验：在 `200_Digital_assets/` 内执行 `sha256sum -c MANIFEST.sha256`，退出 0 且无 FAILED 即一致；210 册在其目录内同法核验。触发条件：覆盖范围内普通文件数 > 0 时清单必须存在且核验通过；范围内为空（只有 `.gitkeep`）时清单可缺席。
- 边界：资产清单只管 200 区；产物索引归 `.artifacts/index.json`，两套不混。

## 建目录

```bash
mkdir -p "$ROOT/.agents/adapters" "$ROOT/.agents/config" "$ROOT/.agents/drafts" "$ROOT/.agents/learnings" \
  "$ROOT/.agents/memory" "$ROOT/.agents/rules" "$ROOT/.agents/scripts" "$ROOT/.agents/skills" \
  "$ROOT/.artifacts" \
  "$ROOT/000_Inbox/010_Downloads" "$ROOT/000_Inbox/imported" \
  "$ROOT/050_Knowledge/Obsidian" \
  "$ROOT/100_Works/_archive" \
  "$ROOT/200_Digital_assets/210_Personal-record" "$ROOT/200_Digital_assets/220_Docs" \
  "$ROOT/200_Digital_assets/230_Picture" "$ROOT/200_Digital_assets/240_E-book" \
  "$ROOT/200_Digital_assets/250_Videos" \
  "$ROOT/300_Dev" "$ROOT/400_Code" "$ROOT/900_ADR"
```

`050_Knowledge/Obsidian/` 只建空目录，不把别处的知识库搬进来。`900_ADR/` 只建空目录，首次裁定时建 0001。

空目录占位（`.gitkeep`）：git 不跟踪空目录，部署产生的空目录每个放一个空文件 `.gitkeep`，使骨架可经 git 克隆完整复现。分两类：

- 未被根仓库忽略的空目录：`.agents/adapters/`、`.agents/config/`、`.agents/learnings/`、`.agents/memory/`、`050_Knowledge/Obsidian/`、`100_Works/_archive/`、`200_Digital_assets/220_Docs/`、`230_Picture/`、`240_E-book/`、`250_Videos/`、`300_Dev/`、`900_ADR/`。
- 被根仓库忽略的运行时目录：`400_Code/`、`000_Inbox/010_Downloads/`、`000_Inbox/imported/`、`.agents/drafts/`、`.agents/skills/`——其 `.gitkeep` 在 `.gitignore` 里开否定例外放行（见「根仓库配置」一节），目录内容仍整体忽略。
- 例外：`.artifacts/` 不放（已有纳入版本控制的 `index.json`）；敏感区 `200_Digital_assets/210_Personal-record/` 不放（整体不进版本控制，克隆后由建目录一步补建）。

目录有了真实内容后，`.gitkeep` 可留可删，不强制清理。

## 根文件模板

`AGENTS.md`（最小内核，敏感区限制、删除确认、授权要求必须常驻，不得降级）：

```markdown
# AGENTS.md

## 工作区身份
本目录是个人数字工作区收口目录。唯一外层根是本文件；下级目录的规则文件只细化本目录，不得放宽本文件。

## 访问限制
- 敏感区（`200_Digital_assets/210_Personal-record/`）默认不读不写，按任务授权访问。
- 删除附件、原始记录或其他不可重建内容前，检查引用关系并取得用户明确确认。
- 真实凭据值不得进入工作区内的任何文件、日志或命令输出，只存密码管理器或受控运行环境。

## 授权要求
- 未授权的外部写入、发布和范围扩张需要另行确认。
- 涉及钱、绑卡、付款的操作先问人。
- 规则冲突或无法并存时停机报人，不自动选一份继续；裁定结论按 ADR 方案记入 `900_ADR/`。

## 记忆读写
- 权威记忆是根 `MEMORY.md` 与 `.agents/memory/` 流水；agent 工具自身的记忆只是缓存，不作为权威，不备份，不与工作区记忆合并。
- 流水按 `<工具名>/<日期>.md` 只追加；`MEMORY.md` 只追加，每条带来源与日期。
- 检索：默认读根 `MEMORY.md` 与最近 7 天流水；需要更旧上下文时，必须按日期/关键词搜索 `.agents/memory/` 全目录后再下结论，禁止仅凭 7 天窗口断言「没有记录」。
- 冲突：记忆冲突按 `.agents/rules/memory-system.md`——事实新者胜，旧条目加取代标注不改写，裁决以 `900_ADR/` 为准；判不了时 fail-closed，停用争议事实、报人裁决。
- 纠错：记忆纠错按 `.agents/rules/memory-system.md`——发现疑似错误先冻结停用，核源定性后不改史、只加纠错标注，传播追溯查完才算纠完。
- 清除与规模：敏感内容误记走 `.agents/rules/memory-system.md` 清除例外（真删除内容本体、原位留墓碑），不走纠错标注；流水规模触发线（文件数、总字数、grep 命中）同见该模块，触发先报告、经确认才建年度卷册。
- 边界：工作区记忆的系统边界与自含按 `.agents/rules/memory-system.md` 系统边界一节——分域自含，出境只带自含摘要，正文单源留在工作区内。

## 任务路由
- 启动读本文件，读 `MEMORY.md` 与最近 7 天流水，结束写当日流水并覆盖更新 `HANDOFF.md`。
- 进入工作区时，按当前工具读 `.agents/adapters/<工具名>.md` 完成宿主绑定，规范中的泛称目的地以该文件的绑定为准；没有对应 adapter 时，泛称目的地按未绑定处理，涉及晋升等出境动作先报人。
- 按任务需要加载 `.agents/rules/` 下的细则，不要求全量加载；规则读不全时只保留最小内核，敏感区限制、删除确认和授权要求不可丢。
- 作出、修改或查询工作区级决定时，先读 `.agents/rules/decision-records.md`，再写 `900_ADR/`。
- 新建、修改或评估规则、约定、契约时，先读 `.agents/rules/rule-design.md`，过五步再写。
- 审核、晋升或处置 `.agents/drafts/` 草稿时，先读 `.agents/rules/draft-review.md`。
- 做记忆蒸馏、检索旧上下文或处置记忆冲突时，先读 `.agents/rules/memory-system.md`。
- 多机共享同一实例或新机接入时，先读 `.agents/rules/multi-machine.md`。
- 新 agent 接入本工作区时，先读根目录 `ONBOARDING.md`，再按其步骤走。
```

`MEMORY.md`（初始内容，条目区留空）：

```markdown
# MEMORY.md

> 跨会话稳定事实。只追加，每条带来源与日期；一条只记一个稳定事实。

## 格式

每条四个字段：内容、来源（agent + 日期 + 出处）、适用范围、失效条件。

取代标注：新事实取代旧事实时追加新条目，并在旧条目末尾加「[已取代：见 YYYY-MM-DD 条目]」（日期为新条目日期），不改写旧条目正文；细则见 `.agents/rules/memory-system.md`。

判据：如果一条内容明天还成立，就不该留在账本；如果只在今天有意义，就不该进本文件。

## 条目

（暂无条目）
```

`HANDOFF.md`（初始内容，同一时刻只能有一个当前任务）：

```markdown
2026-01-01 00:00 | 工具: 无 | 当前任务: 无

## 当前任务
- 目标：无
- 未完成：无

## 任务队列
- 无

## 堵塞
无
```

首行「工具」字段记最后写入者（工具名），每次覆盖更新时同步改（细则见 operating-rules.md 记忆与账本一节）。

`CONTEXT.md`：按 glossary.md 誊抄规则写。

`DESIGN.md`（三个空段起步，后续按实际填写，不编造内容）：

```markdown
# DESIGN.md

## 三层边界

（内核层、资产层、机器层的划分与取舍。）

## 文件流转

（输入、输出、沉淀、归档四段，每段留下可追溯指针。）

## 存储与维护原则

（根版本控制范围与忽略、资产清单、产物保留。）
```

`README.md`（登记本机主路径）：

```markdown
# 010_oc-ledger

个人数字工作区：规则跟人走，骨架只创建一次。

新机器 / 新 agent 接入本工作区：先读根目录 `ONBOARDING.md`，按其步骤执行。

## 本机路径映射

| 机器 | 主路径 |
| --- | --- |
| <机器名> | <ROOT 的绝对路径> |

周期任务主执行者：<机器（工具）>
```

机器名用部署时人给定的逻辑名，可与该机 hostname 不同；登记后不随 hostname 变化而改。

首批规则模块随骨架一起写（目前有五份），后续新增规则只加一个规则模块并接通路由：

`.agents/rules/decision-records.md`（决策记录细则，照抄）：

```markdown
# 决策记录（ADR）

工作区级裁定结论的唯一承载是工作区根的 `900_ADR/`。本模块定义何时记、记在哪、怎么写。本模块对付的错误：决定记错载体，事后无法溯源。

## 何时记

一条决定值得记入，当且仅当同时满足三条：难逆转（改回去代价高）、无上下文会意外（后人看现状猜不出为什么）、有真实取舍（存在被否决的备选）。三条不全，不记；日常进度与临时约定也按三条判，不另开例外。

## 位置与命名

- 目录：工作区根 `900_ADR/`。9xx 段为低频治理记录，默认排序居末。
- 文件名：`NNNN-英文短名.md`，从 0001 顺序编号，短名用英文 kebab-case；新编号取现有最大号加一。
- 部署时 `900_ADR/` 为空目录，不预填。

## 格式

- 第一行 `# 标题`（中文，写清决定了什么）。
- 正文一至三句话：背景、决定、原因。
- 可选段及条件：`Status`（proposed | accepted | deprecated | superseded by ADR-NNNN）只在被取代时写；备选方案只在有被否决的备选时写；后果只在改回去代价高时写。
- 正文中文，文件名英文。

## 只追加

- 已有 ADR 不修改内容；错字与同日未落地的修正除外，修正时留注。
- 决定变更时写新 ADR，并在旧 ADR 加 Status 标注被新 ADR 取代，不删除旧文件。
- 决定只记入 `900_ADR/`，不追加进其他决定记录载体；不在 `MEMORY.md` 复述决定内容。

## 写入前

- 读 `900_ADR/` 现有编号，取下一号。
- 检查新决定是否与已有 ADR 冲突；冲突时停机报人，不自动覆盖。

## 保活

- 复核随写入前核对一起做：发现编号断裂、重复或格式不符时停机报人，不静默修复。
- 本模块与实际落点不符时暂停执行，停机报人，等裁决后恢复。
```

`.agents/rules/rule-design.md`（规则设计细则，照抄）：

```markdown
# 规则设计

新建、修改或评估一条规则、约定、契约时，先过本模块的五步，交不出答案就停下来问人，不凭感觉写规则。

贯穿原则：骨架外生，参数内生。方法论骨架可以抄，落点、触发、措辞必须从宿主长出来。

一句话总纲：规则的质量不在文本里，在它被哪一层加载、被什么条件触发、命中后做了什么。

自检：能原样搬到另一个仓库还生效的规则，只有骨架、没有参数，两边都不会触发。

## 第一步｜定界：先写“不管什么”

- 回答：管哪些动作、不管哪些、为什么不管；界必须写进文件，只在讨论里说过等于没有。
- 判据：能说出一个明确不归它管的动作，且这条写进了文件。

## 第二步｜选址：落点服从宿主架构

- 回答：这条规则是每次都要跑，还是条件才跑？触发频率等于加载时机。
- 每次操作 → 常驻规则（`AGENTS.md` 内核）；特定条件 → 按需加载模块（`.agents/rules/`）。
- 动作：去宿主里找职责边界声明（通常是一句“本文件只负责 X/Y/Z”），落点不用猜。

## 第三步｜定触发：收支平衡

- 错误代价 × 发生概率 > 触发成本，才值得开口。
- 风险源取并集：宿主已有条文 ∪ 作用域内实际错误史（流水与 agent 自身的教训记录）。
- 判据：每条触发条件对应一种具体的、代价高的写错方式；写不出对应关系的触发条件，删掉。

## 第四步｜定形状：把判断换成格式

- 固定字段数（无则写“无”）；禁用词表（本场景的高频空话）；强制指向具体元素（路径/字段/参数名）；结论词语义唯一。
- 区分产物型与过程型：产物型（约束输出什么）单独成段、字段固定；过程型（约束怎么动作）并入硬规则，不单独成段。
- 判据：两个执行者跑同一任务输出能否逐行对齐？能否机械校验？每条断言能否定位到具体元素？

## 第五步｜保活：三个证据层级

- 活性：它真的被加载并触发过吗？说得出上一次触发的时间与输出，说不出等于不存在。
- fail-closed：命中反例时真的会停吗？没有就是“提示”不是“约束”。
- 未退化：触发后做了真事，还是填了空的？必须单独设计退化检测（如全填“无”时的额外举证）。
- 看执行记录，不看修改记录；零修改也可能是零执行。

## 评估他人规则时的三条元规则

1. 先确认定界，再判成败；用作用域外的错误判失败，是评估方法错。
2. 看执行记录，不看修改记录。
3. 活规则与死字段的唯一分界是 fail-closed。

## 从属

- 本模块不放宽上层规则；新规则不得放宽敏感区限制、删除确认与授权要求。
- 规则冲突无法并存时停机报人，裁定结论按 ADR 方案记入 `900_ADR/`。
```

`.agents/rules/memory-system.md`（记忆系统细则，照抄）：

```markdown
# 记忆系统

本模块管工作区权威记忆的写入、蒸馏、检索、规模触发、冲突、纠错、清除、系统边界与保留：根 `MEMORY.md` 与 `.agents/memory/` 流水。本模块对付的错误：流水只写不提炼、长期事实无人晋升；只凭最近 7 天窗口断言「没有记录」；流水无限累积拖垮检索；新旧事实并存时随手引错旧值；记错的条目无人纠、错值顺引用与晋升扩散；敏感内容误记后只标注不清除、留存即风险；随手清理老流水破坏审计链。

## 定界

- 管：根 `MEMORY.md` 与 `.agents/memory/` 流水的写入纪律、蒸馏回路、检索规则、规模触发线、冲突消解、纠错处置、清除例外、系统边界与保留政策。
- 不管：agent 工具自身的记忆缓存——只是缓存，不作为权威，不备份，不与工作区记忆合并；知识库（Vault，`050_Knowledge/Obsidian/`）内部记忆——归 Vault 自理，两套互不覆盖。
- 草稿箱候选的审核与晋升分流归 `.agents/rules/draft-review.md`；本模块只定蒸馏如何产出候选并交棒，不另设分拣规则。
- 裁决的记录与变更归 `.agents/rules/decision-records.md` 与 `900_ADR/`；本模块只定记忆与裁决冲突时谁赢。
- 前置条件：本模块的蒸馏、抽查与规模核查挂靠周期复核进程，宿主环境须存在周期复核进程（如定时任务）才会触发；无此进程时，这些回路不自动运行。

## 系统边界

- 分域自含：本模块只管工作区记忆；工作区事实的唯一权威是工作区文件本身（根 `MEMORY.md` 与 `.agents/memory/` 流水）。工作区之外的记忆系统不在本模块管辖内：不引用其路径、不假设其存在、不以其内容为裁决依据；本模块的规则在只有工作区本身存在的环境里完整可执行。
- 出境摘要自含：工作区事实被带到工作区之外使用时，只带一句话摘要加来源指针，不带正文。摘要必须自含——指针不可达时（换设备、换系统、指针失效），仅凭摘要本身仍须可独立理解与使用；关键事实不得只存放在指针的另一端。
- 正文单源：事实正文永远只在工作区内留一份，不做跨系统正文镜像；外部需要全文时凭指针回工作区取，不在外部另存正文副本。
- 普适标记：蒸馏候选若具跨项目普适性，分拣时可加「普适」标记，候选仍留在工作区内——这是草稿分拣的一个标注维度，不新增去向。工作区之外的系统是否采纳、如何采纳，由其自身规则决定；本系统不推送、不指定目的地。
- 跨系统冲突：工作区内记录与外部说法不一致时，工作区事实不自动让位、也不自动压过外部说法，按冲突消解的 fail-closed 停用争议事实、报用户裁决；处置不预设外部系统的形态。

## 选址

- 本模块落 `.agents/rules/`，按需加载：根 `AGENTS.md` 任务路由命中记忆蒸馏、检索旧上下文、处置记忆冲突或纠错时先读本模块。
- 不新建记忆索引文件：流水文件名结构 `<工具名>/<日期>.md` 本身即索引，按日期与关键词可直接定位。`.artifacts/index.json` 只管可重建中间产物，与记忆检索无关。

## 写入

- 只追加：流水按 `<工具名>/<日期>.md` 只追加当日事实；根 `MEMORY.md` 只追加，每条带来源与日期，格式四字段（内容、来源、适用范围、失效条件）见根 `MEMORY.md` 格式节。
- 唯一的标注性例外：事实被取代时在旧条目末尾加取代标注（见冲突消解），条目被纠错时加纠错标注（见纠错），均不改写旧条目正文。除此之外任何条目正文不回改。
- 写入后回读校验：每次写入或追加记忆文件（流水、根 `MEMORY.md`）后，回读本次写入段落并与预期内容比对；发现替换字符（U+FFFD）或已知乱码模式，即停止后续写入并报人，不带病继续写。
- 写入前先检索（见检索节）：同一结论已有条目时不重复写，事实变化走取代流程，不另起平行条目。
- 长任务分段写流水：跨多个落地步骤或预计跨会话的长任务，每个步骤完成即追加一段当日流水，不等任务收尾一次性写；中途条目可简记，收尾时在同日文件内补全。

## 蒸馏回路

- 回路挂靠既有每周复核，不另设任务：每次复核扫描已滑出默认 7 天读取窗口的流水，滚动一周一批，不漏检。
- 提炼按起草判据：跨会话仍成立；跨项目适用或写清边界；同一结论被独立写出两次优先起草。固定排除：临时路径、一次性命令、七天内可能变化的状态、带【探针】标记的条目。
- 蒸馏产出只写 `.agents/drafts/` 候选（`review: needs-review`），再走 `draft-review.md` 的分拣晋升：人批准才进根 `MEMORY.md`、知识库或 `.agents/rules/`，否决移入 `.agents/drafts/rejected/` 保留。
- 蒸馏不得直写根 `MEMORY.md`：流水到长期记忆之间只有分拣批准一条路。
- 无候选时，复核报告须记一句「本周无蒸馏候选」，作为回路活性证据（见保活）。

## 检索

- 默认读取：根 `MEMORY.md` 加最近 7 天流水。
- 需要更旧上下文时，必须按日期、关键词搜索 `.agents/memory/` 全目录后再下结论；禁止仅凭 7 天窗口断言「没有记录」。
- 引用流水作依据时注明出处文件与日期；引用到已被取代的条目时按冲突消解节处理，不引用旧值。
- 读到带纠错标注的条目时，必须连同标注指向的纠错条目一起读，不得只凭被纠条目下结论（见纠错）。

## 规模触发线

- 定位：不建索引、流水文件名结构本身即索引的裁决（见选址与检索）不变；本节为该裁决预设失效触发线，避免检索随流水累积悬崖式劣化。触发前不预建任何索引文件。
- 触发条件（任一满足即触发）：① `.agents/memory/` 下流水文件总数 ≥ 300；② 流水总字数 ≥ 200 万字；③ 实际检索中单次全目录 grep 命中 > 50 条且难以筛选（人工判定，记入当周流水）。
- 触发动作：先在每周复核报告中报告，经用户确认后，再在 `.agents/memory/` 下建年度卷册摘要 `<YYYY>-卷册.md`（按月分节，列当月流水文件清单与主题词）；建后检索顺序改为先查卷册定位月份、再定点 grep，未建卷册的年份仍按检索节全目录搜索。
- 触发线参数本身可经新 ADR 调整；未触发前，检索规则按检索节原样执行。

## 冲突消解

- 事实类条目：时间新者胜（newest wins）。以条目所记日期为准，新日期的事实覆盖旧日期的同题事实。
- 裁决类内容：以 `900_ADR/` 为准。流水与根 `MEMORY.md` 的记载不得覆盖 ADR；裁决变更只走新 ADR，不在记忆文件里改口径。
- 取代标注：`MEMORY.md` 事实更新时追加新条目，并在旧条目末尾加标注「[已取代：见 YYYY-MM-DD 条目]」（日期为新条目日期），不改写旧条目正文；引用记忆作依据时禁止引用已标注取代的旧值。
- fail-closed：无法判新旧、同日冲突或证据同级时，停用争议事实、报人裁决，不自动选边（与根 `AGENTS.md`「规则冲突停机报人」同规）；裁决结论记入当日流水，属裁决变更的另走 ADR。

## 纠错

- 三情形定界：旧条目失效分三种——取代（旧值当时为真、后来事实变了，走冲突消解的取代标注）；冲突（判不了谁对，fail-closed 停用争议事实、报人裁决）；纠错（已判明旧条目当时就是错的：记错、引错源、理解错）。本节只管纠错。
- 第一步，冻结：发现疑似错误，先按冲突消解停用该事实、标争议，不许边用边查。纠错是冻结之后的处置流程；未定性前不落纠错条目。
- 第二步，核源定性：宣布一条记忆错了，必须有独立证据——原始出处、用户指令或实测结果——纠错条目必须带证据指针；证据不足的，降级回冲突流程。自证禁止：agent 不得用自己生成的内容给自己作证来纠错。
- 第三步，落条目不改史：流水与根 `MEMORY.md` 的旧条目正文一律不改。新写纠错条目，固定五项：被纠指针（文件 + 日期 + 条目）、错在哪、正确值、证据、错误来源（谁记的、当时依据什么）。旧条目末尾加标注「[已纠错：见 YYYY-MM-DD 条目]」（日期为纠错条目日期），与取代标注同属写入节的标注性例外。
- 第四步，传播追溯：按被纠事实的关键词 grep 整个记忆面（`.agents/memory/` 流水、根 `MEMORY.md`、`.agents/drafts/`、`.agents/rules/`、`HANDOFF.md`），引用点逐个处置——草稿与流水层的引用，在纠错条目中注明即可；已晋升进规则的，走规则修订流程；已写进 ADR 的，不改原文，写新 ADR 记更正并给旧 ADR 加 Status 标注。追溯清单写进纠错条目本身，作为纠错完成判据：没查完不算纠完。
- 触发分级：用户纠正的，即时走完四步，不等每周复核。agent 自查或蒸馏时发现的，只许冻结并报每周复核，用户确认后才落纠错条目；唯一例外是原文级证据（如记录与被引文件逐字不符），可直接落纠错条目，但须在复核报告中留痕。

## 清除例外

- 定位：纠错的标注机制适用于无害错误；敏感内容留存本身即风险，走本节清除例外、真删除内容本体。本节是纠错机制的例外格，不是替代：不在下列范围者一律走纠错标注，不得借清除之名删普通错误。
- 范围卡死三类：① 秘密或密钥片段；② 他人隐私；③ 用户明确要求遗忘的内容。
- 流程：真删除内容本体；在原文件原位置留墓碑条目，只记清除日期、条目位置、类别、依据，绝不记被清内容；再做传播追溯，按纠错第四步的记忆面范围（`.agents/memory/` 流水、根 `MEMORY.md`、`.agents/drafts/`、`.agents/rules/`、`HANDOFF.md`）查引用点，一并清除或改为指向墓碑。
- 分级：秘密类，agent 一经发现可先行清除，事后在最近一次复核或汇报中报告（时效优先）；隐私类与用户遗忘类，须用户确认后执行，用户当面要求遗忘的即为确认。
- git 历史：内容若已提交进 git 历史，删工作区文件不等于清历史，须单独告知用户、按其裁决处理；本机制不自动改写 git 历史。

## 保留

- 流水永留原地：不删除、不归档（敏感内容清除例外见清除例外节）。流水是 append-only 审计链，路径被 `.agents/learnings/` 与 `900_ADR/` 多处引用，文本量小，没有清理收益。
- 根 `MEMORY.md` 被取代条目保留原地、带取代标注，不删除。
- 清理政策只适用于 `.artifacts/` 与 `000_Inbox/` 暂存（见产物归口与保留规则），不扩散到任何记忆文件。

## 保活

- 活性：看每周复核报告里有没有蒸馏记录——候选清单或「本周无蒸馏候选」一句；两者皆无，即回路未触发，只提醒不自动补跑。
- fail-closed：冲突判不了即停用争议事实报人（见冲突消解）；检索未搜全目录即下「没有记录」结论，属违规，命中时撤回结论重搜。
- 未退化：复核抽查取代标注与新条目是否成对出现（有新条目取代旧事实、旧条目必有标注），不成对只提醒不自动修复。
- 未退化（纠错）：每周复核抽查带「[已纠错]」「[已取代]」标注的条目——标注指针可解析、纠错条目的传播追溯清单已闭环；纠错条数记入复核报告。
- 未退化（规模与清除）：每周复核核查流水规模（文件总数与总字数）是否触及规模触发线，触及先报告、经用户确认才建卷册；清除例外执行后，墓碑留存与引用点追溯闭环随纠错抽查一并核查。
- 本模块与实际落点不符时暂停执行，停机报人，等裁决后恢复。

## 探针（回路活性外部验证）

- 定位：回路活性证据（蒸馏留痕、标注抽查）出自执行 agent 自报，无独立 oracle；探针以植入—冷读—盲评提供外部判据，是自证禁止在回路活性层的应用。判据在植入时定死，不由被测会话产生。
- 探针资产：探针条目只写 `.agents/memory/probe/<日期>.md` 专用目录，只用虚构实体，条目带固定标记「【探针 P-<轮次>-<序号>】」；台账（植入位置、题面、判据、评分）存 `400_Code/memory-probes/`，在记忆检索面之外。
- 污染防控：带探针标记的条目永不蒸馏、永不晋升（见蒸馏回路固定排除）；探针文件是测试资产，不入真实流水审计链，轮次结束整文件删除——「流水只追加」只约束各工具的真实流水。
- 三臂：A 窗外检索（事实植入读窗之外的 probe 文件，测全目录检索）；B 标注链跟随（旧条目与纠错条目成对植入，测纠错标注跟随）；C 读窗命中（用真实条目出题、只许默认读窗作答，测读窗质量）。
- 执行：植入者、被测会话（全新上下文）、评分者三方分离；题面自然化，不提测试；每轮 A、B 各 2 条、C 3 条。触发：检索或标注语义的规则大改后必跑，无大改每季度一轮。
- 结果：报告记入当周流水作外部证据；未通过按 learnings 记录被违反的规则，走既有通道处置，探针不直接改规则。
```

`.agents/rules/draft-review.md`（草稿审核细则，照抄）：

```markdown
# 草稿审核

本模块管工作区草稿箱 `.agents/drafts/` 里沉淀候选的起草、审核与晋升。本模块对付的错误：agent 自行批准或否决草稿、把未审候选当权威、否决后删除草稿导致同一候选被重复起草。

## 定界

- 管：`.agents/drafts/` 下候选的起草判据、`review` 状态转换、批准后的晋升分流、否决后的保留。
- 不管：知识库（Vault，`050_Knowledge/Obsidian/`）内部草稿——Vault 草稿归 Vault 自己的 `.agents/rules/agent-drafts.md`，两套互不覆盖、不跨层查找。
- 草稿在分拣前不构成权威，agent 不把草稿当作记忆读取。

## 选址

- 草稿落 `.agents/drafts/<日期>-<主题>.md`，版本控制忽略，可由流水重新生成。
- 本模块落 `.agents/rules/`，按需加载：根 `AGENTS.md` 任务路由命中草稿审核、晋升或处置时先读本模块。

## 起草

- 起草判据两条：跨会话仍成立；跨项目适用或写清边界。同一结论被独立写出两次优先起草。
- 固定排除：临时路径、一次性命令、七天内可能变化的状态。
- 新草稿一律写 `review: needs-review`，并在任务结束自检时报告待分拣数量；超过 7 天未分拣的在全面自检时列出。

## 审核：三态与状态转换

- 状态只有三态：`needs-review`（待人分拣）、`approved`（人已批准，可晋升）、`rejected`（人已否决，保留存档）。
- 状态转换只凭人的明确指令：agent 不得自行设置 `approved`，不得自行设置 `rejected`。
- 状态缺失、非法或与人的指令不一致时，按 `needs-review` 处理并停止晋升，报人裁定。

## 晋升

- 晋升只在 `approved` 后发生，分拣批准是唯一的晋升触发；批准时以分拣决定加流水来源作证据。
- 晋升目标只限四处：根 `MEMORY.md`、`DESIGN.md`、`.agents/rules/`、`100_Works/<项目>/`。
- 正式归属唯一：内容只落一个正式位置，其他位置只放链接指针，不复制正文。
- 草稿的去向（批准、否决、暂缓）记入当日流水。

## 否决：保留不删

- 人否决的候选置 `review: rejected`，移入 `.agents/drafts/rejected/` 保留，不删除。
- 移入时在当日流水记一笔（候选主题与否决日期）。
- 已否决的候选不再重复起草；新证据使同一结论值得重审时，先报人，不自行从 `rejected/` 复活。

## 保活

- 活性：靠任务结束自检报告待分拣数量、全面自检列超期草稿，证明本模块被真实触发。
- fail-closed：状态非法即停晋升；agent 自批、自否即违规，命中时停下报人。
- 未退化：每周复核抽查 `rejected/` 与流水记录是否对得上（有移入必有流水一笔），对不上只提醒不自动修复。
```

`.agents/rules/multi-machine.md`（多机共享与新机接入细则，照抄）：

```markdown
# 多机共享

本模块管同一工作区仓库被多台机器、多个工具共享为同一实例时的协作纪律，以及新机器加入已有实例的接入定式。本模块对付的错误：多机各建实例、内容成双账本终将漂移；新机接入误走部署流程造出第二个实例；周期闭环被多台机器重复执行。

## 多机共享纪律

多机共享纪律：
- 前提：同一工作区仓库可由多台机器、多个工具共享为同一实例；机器与工具的差异只落在 adapter 与根 README 路径映射表，不另建实例、不复制正文。
- 开工先拉：开始工作前先 git pull（快进优先）；拉取失败或本地与远端分叉时先停下报人，不在过期副本上开工。
- 收工必推：收工时 commit 并 push；push 被拒（远端已前进）先 pull 解冲突再推，禁止强推。
- HANDOFF 协调：开始一项任务先在 HANDOFF.md 记当前任务（工具＋机器）；当前任务非空且非己方时，不动同一摊事；收工时更新或清空。
- 流水分写：流水按 .agents/memory/<工具>/ 分目录，各工具只写自己目录；根 MEMORY.md 只追加条目与标注（沿用记忆系统的取代/纠错标注口径）；两边同日追加产生合并冲突时保留双方条目、按时间顺序排列，不删对方内容。
- 路径表加行：根 README 路径映射表一机一行（机器逻辑名＋主路径）；新机器接入时只加自己一行，不改他行。
- adapter 本机性：adapter 一工具一份、绑定的是本机路径，只对本机有效；仓库克隆到新机器后，他机的 adapter 按未绑定处理，涉及晋升等出境动作先报人，直至本机补绑。
- 蓝图分发：技能更新照旧走技能发布通道，各机自行更新技能本体；工作区仓库不分发技能正文。
- 周期任务单点执行：周复核等周期闭环只许一个执行者，执行者（机器＋工具）记入根 README 路径映射表旁注；其余机器不另跑同一闭环，其 adapter 注明缺失的闭环由主执行者代行。

## 新机接入

**新机接入（加入已存在的实例，不走部署流程）：**

接入方先读仓库根 `ONBOARDING.md`，本定式为其规则正本。

1. 备齐 git 身份与凭据：配置本机 user.name/user.email，确认对正本仓库有读写凭据（克隆与推送都要用）；凭据按本机既有方式保管，不写入仓库任何文件。
2. 克隆正本仓库，核对本地 HEAD 与远端一致、工作树干净。
3. 规则体系随仓库自带：按根 AGENTS.md 路由读 .agents/AGENTS.md 与 .agents/rules/，确认在位——接入不需要部署技能。
4. 写本工具的 adapter：绑定本机的人格文件、工具坑文件、自有记忆位置；绑不上的目的地写降级注记。
5. 根 README 路径映射表加本机一行（机器逻辑名＋主路径），不改他行。
6. 技能按需另装：工作区技能正本不随仓库走（.agents/skills/ 被忽略），本机要用的技能从技能发布仓库安装；未发布、本机 harness 不支持或暂缺的，在 adapter 降级注记中列明，涉及那些技能的动作先报人。
7. 周期自动化不随仓库走：周复核等定时闭环由各 harness 自行安排；本机没有的，在 adapter 注明哪些闭环不自动运行。
8. 往返验证即接入完成：pull 成功、首条流水写入 .agents/memory/<本工具>/、commit 并 push 成功、HANDOFF 可读；接入回执报 HEAD、adapter 绑定结果与缺失项。
```

新机接入手册（照抄；花括号为参数，替换后生成为工作区根 `ONBOARDING.md`，接入方克隆后先读它）：

```markdown
# 新机接入手册：加入 {WORKSPACE_DIR} 工作区

> 致接入方 agent：你正在读的这份文件位于正本仓库根目录，是**加入这个已存在的工作区实例**的唯一入口（不是新建部署）。照本手册执行即可，全程不需要部署技能。本手册与仓库内的 `.agents/rules/multi-machine.md` 冲突时，以模块为准——那是多机共享与接入的规则正本，本手册只负责把你送进仓库的规则体系。
>
> 执行纪律：据实操作、报错贴原文、自行假设必须在回执中列出。

## 0. 坐标

- 正本仓库：`{REPO_URL}`（私有，分支 master）
- 本文件位置：仓库根 `ONBOARDING.md`；你克隆得到的目录即工作区根（目录名应为 `{WORKSPACE_DIR}`，实际绝对路径记入回执）

## 1. 前置：git 身份与凭据（唯一需要人配合的一步）

- 配置本机 git `user.name` / `user.email`。
- 确认你对上述仓库有**读写**凭据（提交与推送要用；只读凭据不够）。没有就向人索取，不要猜、不要找别处凑；凭据按本机既有方式保管，**不写入仓库任何文件**。

## 2. 核对克隆

- 核对：本地 HEAD 与远端 master HEAD 一致、工作树干净（克隆动作在你读到本文件前已完成；若本地与远端不一致或工作树不干净，先停下向人报告，不要在过期副本上开工）。
- 记下克隆的绝对路径，第 5 节加行与回执都要用。

## 3. 按序读规则

1. 根 `AGENTS.md`（路由入口）
2. `.agents/AGENTS.md`（约定体系与技能路由）
3. `.agents/rules/multi-machine.md`（多机共享纪律 + 新机接入定式，正本）
4. `HANDOFF.md`（看当前任务是否已被别的机器占用；非空且非己方时，先向人报告，不要动同一摊事，也不要覆盖它的首行登记——见第 7 节）

## 4. 写你自己的 adapter

- 在 `.agents/adapters/` 新建 `<你的工具名>.md`，逐项绑定：人格文件、工具坑文件、你自有记忆位置（写本机实际路径）。结构可参照同目录已有的 adapter。
- 绑不上的目的地写**降级注记**：缺什么、涉及那些目的地的动作先报人，不得假装已绑定。

## 5. README 路径表加一行

- 根 `README.md` 路径映射表加一行：机器逻辑名（向人确认，或用本机已登记的名字）+ 第 2 节的克隆绝对路径。已有的行不改。
- 看一眼表下旁注的「周期任务主执行者」：如果不是你，**不要另跑同一周期闭环**（如周复核），并在你的 adapter 里注明该闭环由主执行者代行。

## 6. 技能按需另装

- `.agents/skills/` 在仓库里是空的（被忽略），技能不随克隆走。本机要用的技能从 `{SKILLS_REPO_URL}` 仓库安装（如 oc-ledger-deploy、self-improvement）。
- 未发布、装不上或本机 harness 不支持的，记入 adapter 降级注记，涉及那些技能的动作先报人。

## 7. 往返验证与首批提交

- 在 `.agents/memory/<你的工具名>/<今天日期>.md` 写首条流水（接入记录：机器、工具、克隆路径、HEAD）。
- `HANDOFF.md` 首行分两种情况：当前任务为「无」或本方任务时，按 `<日期时间> | 工具: <你的工具名> | 当前任务: 无` 更新并注明新机接入完成；被他机占用时**不覆盖首行**（那正是第 3 节要保护的占用登记），接入完成只记入你的流水与回执，HANDOFF 登记待占用结束后再补。
- 把 adapter、README 加行、首条流水、HANDOFF 更新**一次提交并 push**。push 被拒（远端已前进）先 pull 解冲突再推：双方追加的内容都保留；**禁止强推**。
- 至此接入完成：pull 得到、流水写得进、push 推得上、HANDOFF 可读，四项缺一不可。

## 8. 接入回执（发给人，逐项给数）

1. 接入前 HEAD + 首批提交哈希 + push 结果；
2. 克隆绝对路径 + README 加行内容（机器逻辑名与路径）；
3. adapter 绑定逐项结果（人格文件 / 工具坑 / 自有记忆：已绑定或降级注记）；
4. 技能安装情况（装了哪些、缺哪些）；
5. 周期闭环主执行者是谁、你是否已在 adapter 注明代行关系；
6. 新发现的问题或你做的假设（没有写「无」）。

## 禁止事项

- 不运行任何部署流程、不新建实例、不把本机内容覆盖仓库正本；
- 不改他机的 adapter、不改根 `MEMORY.md` 既有条目（只允许追加）；
- 不强推、不改写远端历史。
```

抽取脚本随骨架一起写，供阶段 6 调用（`.agents/scripts/extract.py`）：

```python
#!/usr/bin/env python3
"""010_oc-ledger §4 收编抽取脚本.

按《收口目录部署方案》§4 与 oc_ledger_deploy skill references/adopt.md 执行：
- 只读抽取，不移动任何原物；结果落到 000_Inbox/imported/<工具名>/<日期>/。
- 白名单固定写死在 SOURCES，agent 不临场决定搬哪些文件；新增来源时给白名单加一行。
- 明确排除：sqlite/jsonl 会话日志、缓存、blobs、登录态与凭据文件、设备上的 skill 副本。
- 幂等：imported/<工具名>/ 下已有非空抽取目录时，核数后跳过，不重复抽取；
  抽取目录本身就是已抽取记录，不另建记录文件。
- 抽取后只列清单交人判断归属；未经人工确认，不得分流进正式分区。
- 副本是只读快照（目标文件 chmod 444），不构成权威，agent 不读取它。

根目录说明（方案只给了相对路径，根未定死；本脚本把根做成环境变量，
缺省值见 SOURCES，首次真实抽取前须由用户确认）：
- codex：缺省 ~/.codex（Codex CLI 的常规家目录）。
- codebuddy：缺省 ~/.codebuddy —— 待确认。
- workbuddy：缺省 ~/.workbuddy —— 待确认。
- 三方工具 plans/：无缺省根，须由用户指定 THIRD_PARTY_PLANS_ROOT，否则该来源停用并明示。

用法：
    python3 extract.py [--root $ROOT] [--dry-run|--execute]
缺省为 --dry-run，只列清单、不写任何文件。--execute 才复制并写 MANIFEST.md。
"""
import argparse
import fnmatch
import hashlib
import os
import shutil
import stat
import sys
from datetime import date
from pathlib import Path

EXCLUDE_SUFFIXES = {".db", ".sqlite", ".sqlite3", ".jsonl", ".log", ".pem", ".key"}
EXCLUDE_DIR_NAMES = {"cache", "blobs", ".git", "node_modules", "__pycache__"}
EXCLUDE_NAME_SUBSTRINGS = ("token", "secret", "credential", "passwd", "password")

# 白名单：(工具名, 根目录环境变量, 缺省根, 相对通配, 是否启用)
SOURCES = [
    ("codex", "CODEX_HOME", "~/.codex",
     ["memories/**/*.md", "rollout_summaries/**/*"], True),
    ("codebuddy", "CODEBUDDY_HOME", "~/.codebuddy",
     ["projects/*/memory/*.md"], True),
    ("workbuddy", "WORKBUDDY_HOME", "~/.workbuddy",
     ["memory/*.md"], True),
    ("third-party", "THIRD_PARTY_PLANS_ROOT", None,
     ["**/*.md", "**/*index*"], False),  # 根未定：须用户指定才启用
]


def is_excluded(path: Path) -> str | None:
    """返回排除原因，未排除返回 None。"""
    if path.suffix.lower() in EXCLUDE_SUFFIXES:
        return f"后缀 {path.suffix} 在排除清单"
    if any(part in EXCLUDE_DIR_NAMES for part in path.parts):
        return "位于缓存/blobs 等排除目录"
    lowered = path.name.lower()
    if any(s in lowered for s in EXCLUDE_NAME_SUBSTRINGS):
        return "文件名含凭据类关键词"
    return None


def collect(root: Path, patterns) -> tuple[list[Path], list[tuple[Path, str]]]:
    found, excluded = [], []
    for pattern in patterns:
        for candidate in sorted(root.glob(pattern)):
            if not candidate.is_file() or candidate.is_symlink():
                continue
            reason = is_excluded(candidate.relative_to(root))
            if reason:
                excluded.append((candidate, reason))
            else:
                found.append(candidate)
    # 去重（rollout_summaries/** 等通配可能重叠）
    return sorted(set(found)), excluded


def sha256_of(path: Path) -> str:
    digest = hashlib.sha256()
    with open(path, "rb") as fh:
        for chunk in iter(lambda: fh.read(65536), b""):
            digest.update(chunk)
    return digest.hexdigest()


def main() -> int:
    parser = argparse.ArgumentParser(description="010_oc-ledger §4 抽取脚本")
    parser.add_argument("--root", default=str(Path(__file__).resolve().parents[2]),
                        help="收口目录根目录（缺省由脚本位置推导：.agents/scripts/ 的上两级）")
    mode = parser.add_mutually_exclusive_group()
    mode.add_argument("--dry-run", action="store_true", default=True)
    mode.add_argument("--execute", action="store_true")
    args = parser.parse_args()
    execute = args.execute
    ledger = Path(args.root).expanduser()
    imported = ledger / "000_Inbox" / "imported"
    today = date.today().isoformat()

    total_found = total_copied = total_skipped = 0
    for tool, env_var, default_root, patterns, enabled in SOURCES:
        tool_dir = imported / tool
        if tool_dir.is_dir() and any(tool_dir.iterdir()):
            existing = sum(1 for _ in tool_dir.rglob("*") if _.is_file())
            print(f"[{tool}] 跳过：{tool_dir} 已有抽取目录（{existing} 个文件），按幂等规则不重复抽取")
            total_skipped += existing
            continue
        if not enabled and not os.environ.get(env_var):
            print(f"[{tool}] 停用：未指定 {env_var}（三方工具 plans/ 根目录待用户确认），不抽取")
            continue
        root = Path(os.environ.get(env_var, default_root)).expanduser()
        if not root.is_dir():
            print(f"[{tool}] 无来源：根目录不存在 {root}，跳过")
            continue
        found, excluded = collect(root, patterns)
        for path, reason in excluded:
            print(f"[{tool}] 排除：{path.relative_to(root)}（{reason}）")
        if not found:
            print(f"[{tool}] 无文件：{root} 下白名单无匹配，跳过")
            continue
        total_found += len(found)
        dest_dir = tool_dir / today
        print(f"[{tool}] 待抽取 {len(found)} 个文件 -> {dest_dir}"
              + ("（试运行，不写入）" if not execute else ""))
        for src in found:
            rel = src.relative_to(root)
            print(f"    {rel} ({src.stat().st_size} 字节)")
        if execute:
            manifest_lines = [f"# 抽取清单 {tool} {today}", "",
                              f"来源根：{root}", f"目标：{dest_dir}", "",
                              "| 文件 | 大小 | sha256 |", "|---|---|---|"]
            for src in found:
                rel = src.relative_to(root)
                dest = dest_dir / rel
                dest.parent.mkdir(parents=True, exist_ok=True)
                shutil.copy2(src, dest)
                os.chmod(dest, stat.S_IRUSR | stat.S_IRGRP | stat.S_IROTH)
                manifest_lines.append(
                    f"| {rel} | {src.stat().st_size} | {sha256_of(dest)} |")
                total_copied += 1
            (dest_dir / "MANIFEST.md").write_text("\n".join(manifest_lines) + "\n",
                                                   encoding="utf-8")
            print(f"[{tool}] 已复制 {len(found)} 个文件，清单见 MANIFEST.md")
    print(f"汇总：白名单命中 {total_found} 个，"
          f"本次复制 {total_copied} 个，已有抽取跳过 {total_skipped} 个")
    return 0


if __name__ == "__main__":
    sys.exit(main())
```

## 根仓库配置

根仓库管内核、文档和清单。`400_Code/` 整体忽略，代码仓保持独立，由项目入口文档记录 remote。

```bash
cd "$ROOT"
git init
git config user.name "<姓名>"
git config user.email "<邮箱>"
```

先查机器已有的全局 git 身份，有就不用重设，没有就问人要，不要编造。已存在 git 目录时不重新初始化，已设置本地身份时不覆盖。

`.gitignore` 内容（照抄，不增不减；后续追加需记入决策记录（`900_ADR/`））：

```gitignore
400_Code/*
!400_Code/.gitkeep
.agents/drafts/*
!.agents/drafts/.gitkeep
.agents/skills/*
!.agents/skills/.gitkeep
.artifacts/
000_Inbox/*
!000_Inbox/010_Downloads/
000_Inbox/010_Downloads/*
!000_Inbox/010_Downloads/.gitkeep
!000_Inbox/imported/
000_Inbox/imported/*
!000_Inbox/imported/.gitkeep
200_Digital_assets/210_Personal-record/
__pycache__/
```

忽略口径说明：运行时目录改用「忽略内容（`/*`）加 `.gitkeep` 否定例外」的写法，目录内容仍整体忽略，只有占位文件进版本控制（见「建目录」一节的空目录占位清单）；`.artifacts/` 保持目录级忽略，其 `index.json` 靠首次提交时 `git add -f` 强制加入；敏感区保持目录级忽略且不开任何例外。

`.editorconfig`（只作用于根仓库）：

```editorconfig
root = true

[*]
charset = utf-8
end_of_line = lf
```

`.gitattributes`：

```gitattributes
* text=auto eol=lf
```

编码配置只作用于根仓库。`400_Code/` 被忽略后根配置对其不生效，这是有意的，不复制到子仓；子仓各用自己的配置，项目入口声明“沿用 LF + UTF-8 无 BOM”。

`.artifacts/index.json` 初始内容：

```json
[]
```

首次提交：

```bash
cd "$ROOT"
git add -A
git add -f .artifacts/index.json
git status --short
git commit -m "chore: create workspace skeleton"
```

`.artifacts/index.json` 是索引例外：`.artifacts/` 整体忽略，索引仍须纳入版本控制，提交前用 `git add -f` 强制加入一次，之后它作为已跟踪文件正常提交。重跑时索引已跟踪，强制加入是空操作。

提交前看 `git status` 输出确认：被忽略的目录（`400_Code/`、`.artifacts/`、`000_Inbox/`、`210_Personal-record/`、`.agents/skills/`、`.agents/drafts/`）的内容不得出现在待提交列表里，例外只有强制加入的 `.artifacts/index.json` 与各空目录的 `.gitkeep` 占位。

如果用户明确不要根版本控制仓库：跳过建仓库，资产清单与产物索引暂行放在各项目目录内，根仓库建成后再收进根仓库。不要因此停下整个部署。

## 接入约定模板

每个要接入的 agent 工具，在 `.agents/adapters/<工具名>.md` 写一份接入约定，含四条：启动读 `AGENTS.md`；读 `MEMORY.md` 与最近 7 天流水；按任务路由加载 `.agents/rules/`；结束写当日流水并覆盖更新 `HANDOFF.md`。再加一条本工具的实际写法：它怎么读文件、记忆落在哪、写操作走什么路径。写不出的先空着，标注待真实接入后确认，不编造。

## 决策记录（ADR）

工作区级裁定结论记入工作区根的 `900_ADR/`，一条决定一个文件，格式为 ADR：文件名 `NNNN-英文短名.md`（从 0001 顺序编号，短名用英文 kebab-case）；内容为 `# 标题` 加一至三句话（背景、决定、原因），仅在有增值时加状态、备选方案或后果段。决定值得记入，当且仅当难逆转、无上下文会意外、有真实取舍三者俱全。

只追加：已有 ADR 不修改内容（错字与同日未落地的修正除外，修正时留注）；决定变更时写新 ADR，并在旧 ADR 标注被新 ADR 取代，不删除旧文件。部署时 `900_ADR/` 为空目录，不预填。
