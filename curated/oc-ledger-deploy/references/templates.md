# 目录结构与模板

## 目录树

```text
Oc-Ledger/
├─ .agents/
│  ├─ adapters/          # 每个 agent 工具一份接入约定
│  ├─ config/            # 工具与机器的复用配置
│  ├─ drafts/            # 待分拣的沉淀候选
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
├─ AGENTS.md
├─ MEMORY.md
├─ CONTEXT.md
├─ DESIGN.md
├─ HANDOFF.md
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
| `.agents/adapters/` | 每个 agent 工具一份接入约定与验收项。 |
| `.agents/drafts/` | 沉淀候选草稿箱：agent 自动写，用户分拣；分拣前不构成权威，版本控制忽略，可由流水重新生成。 |
| `.agents/memory/` | 短期流水，按 `<工具名>/<日期>.md` 分文件，只追加。 |
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

## 编号规则（定死，不再讨论）

- 顶层目录保留编号（000/050/100/200/300/400）。编号是顺序：默认排序下正好是工作流顺序（输入、知识、项目、资产、开发、代码），留空的号位供后续目录插入而不改动已有目录。
- `400_Code/`、`300_Dev/` 下面的子目录不编号，用 plain 名称。仓库名、工具名就是身份，集合开放，顺序无意义。
- `200_Digital_assets/` 下面的五个子目录保留编号（210–250），因为它们是封闭固定的五类加固定顺序。新增资产类别从 260 起顺延。
- `100_Works/` 下面的项目目录不编号，用归属前缀加项目名。
- `000_Inbox/` 下面保持 `010_Downloads/`（编号）与 `imported/`（不编号）并存，不对称是有意的：编号标记可清空暂存，不编号标记保留证据。不要给 `imported/` 加编号，那会暗示它也可清空。

## 建目录

```bash
mkdir -p "$ROOT/.agents/adapters" "$ROOT/.agents/config" "$ROOT/.agents/drafts" "$ROOT/.agents/memory" \
  "$ROOT/.agents/rules" "$ROOT/.agents/scripts" "$ROOT/.agents/skills" \
  "$ROOT/.artifacts" \
  "$ROOT/000_Inbox/010_Downloads" "$ROOT/000_Inbox/imported" \
  "$ROOT/050_Knowledge/Obsidian" \
  "$ROOT/100_Works/_archive" \
  "$ROOT/200_Digital_assets/210_Personal-record" "$ROOT/200_Digital_assets/220_Docs" \
  "$ROOT/200_Digital_assets/230_Picture" "$ROOT/200_Digital_assets/240_E-book" \
  "$ROOT/200_Digital_assets/250_Videos" \
  "$ROOT/300_Dev" "$ROOT/400_Code"
```

`050_Knowledge/Obsidian/` 只建空目录，不把别处的知识库搬进来。

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
- 规则冲突或无法并存时停机报人，不自动选一份继续；裁定结论追加进 `.agents/config/decisions.md` 决定记录。

## 记忆读写
- 权威记忆是根 `MEMORY.md` 与 `.agents/memory/` 流水；agent 工具自身的记忆只是缓存，不作为权威，不备份，不与工作区记忆合并。
- 流水按 `<工具名>/<日期>.md` 只追加；`MEMORY.md` 只追加，每条带来源与日期。

## 任务路由
- 启动读本文件，读 `MEMORY.md` 与最近 7 天流水，结束写当日流水并覆盖更新 `HANDOFF.md`。
- 按任务需要加载 `.agents/rules/` 下的细则，不要求全量加载；规则读不全时只保留最小内核，敏感区限制、删除确认和授权要求不可丢。
```

`MEMORY.md`（初始内容，条目区留空）：

```markdown
# MEMORY.md

> 跨会话稳定事实。只追加，每条带来源与日期；一条只记一个稳定事实。

## 格式

每条四个字段：内容、来源（agent + 日期 + 出处）、适用范围、失效条件。

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
# Oc-Ledger

个人数字工作区：规则跟人走，骨架只创建一次。

## 本机路径映射

| 机器 | 主路径 |
| --- | --- |
| <机器名> | <ROOT 的绝对路径> |
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

`.gitignore` 内容（照抄，不增不减；后续追加需记入决定记录）：

```gitignore
400_Code/
.agents/drafts/
.agents/skills/
.artifacts/
000_Inbox/
200_Digital_assets/210_Personal-record/
```

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

提交前看 `git status` 输出确认：被忽略的目录（`400_Code/`、`.artifacts/`、`000_Inbox/`、`210_Personal-record/`、`.agents/skills/`、`.agents/drafts/`）不得出现在待提交列表里，唯一的例外是强制加入的 `.artifacts/index.json`。

如果用户明确不要根版本控制仓库：跳过建仓库，资产清单与产物索引暂行放在各项目目录内，根仓库建成后再收进根仓库。不要因此停下整个部署。

## 接入约定模板

每个要接入的 agent 工具，在 `.agents/adapters/<工具名>.md` 写一份接入约定，含四条：启动读 `AGENTS.md`；读 `MEMORY.md` 与最近 7 天流水；按任务路由加载 `.agents/rules/`；结束写当日流水并覆盖更新 `HANDOFF.md`。再加一条本工具的实际写法：它怎么读文件、记忆落在哪、写操作走什么路径。写不出的先空着，标注待真实接入后确认，不编造。

## 决定记录初始内容

首次裁定时创建 `.agents/config/decisions.md`，初始内容：

```markdown
# 决定记录

只追加，裁定结论与后续规则变更按时间写入，不修改已有条目。每条含：日期、决定、适用范围。

| 日期 | 决定 | 适用范围 |
| --- | --- | --- |
| （空） |  |  |
```
