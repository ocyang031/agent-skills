# 目录结构与模板

## 目录树

```text
010_oc-ledger/
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
├─ 900_ADR/
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
| `.agents/drafts/` | 沉淀候选草稿箱：agent 自动写，用户分拣；分拣前不构成权威，版本控制忽略，可由流水重新生成。被否决的草稿移入 `.agents/drafts/rejected/` 保留，不删除。 |
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
| `900_ADR/` | 决策记录（ADR）：工作区级裁定结论的唯一承载，一条决定一个文件，顺序编号，格式见“决策记录（ADR）”一节。 |

## 编号规则（定死，不再讨论）

- 顶层目录保留编号（000/050/100/200/300/400/900）。编号是顺序：默认排序下正好是工作流顺序（输入、知识、项目、资产、开发、代码），9xx 段为低频治理记录，默认排序居末；留空的号位供后续目录插入而不改动已有目录。
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
  "$ROOT/300_Dev" "$ROOT/400_Code" "$ROOT/900_ADR"
```

`050_Knowledge/Obsidian/` 只建空目录，不把别处的知识库搬进来。`900_ADR/` 只建空目录，首次裁定时建 0001。

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

## 任务路由
- 启动读本文件，读 `MEMORY.md` 与最近 7 天流水，结束写当日流水并覆盖更新 `HANDOFF.md`。
- 按任务需要加载 `.agents/rules/` 下的细则，不要求全量加载；规则读不全时只保留最小内核，敏感区限制、删除确认和授权要求不可丢。
- 作出、修改或查询工作区级决定时，先读 `.agents/rules/decision-records.md`，再写 `900_ADR/`。
- 新建、修改或评估规则、约定、契约时，先读 `.agents/rules/rule-design.md`，过五步再写。
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
# 010_oc-ledger

个人数字工作区：规则跟人走，骨架只创建一次。

## 本机路径映射

| 机器 | 主路径 |
| --- | --- |
| <机器名> | <ROOT 的绝对路径> |
```

首批规则模块随骨架一起写（目前有两份），后续新增规则只加一个规则模块并接通路由：

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
    python3 extract.py [--root ~/workspace/010_oc-ledger] [--dry-run|--execute]
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
    parser.add_argument("--root", default="~/workspace/010_oc-ledger",
                        help="010_oc-ledger 根目录")
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

## 决策记录（ADR）

工作区级裁定结论记入工作区根的 `900_ADR/`，一条决定一个文件，格式为 ADR：文件名 `NNNN-英文短名.md`（从 0001 顺序编号，短名用英文 kebab-case）；内容为 `# 标题` 加一至三句话（背景、决定、原因），仅在有增值时加状态、备选方案或后果段。决定值得记入，当且仅当难逆转、无上下文会意外、有真实取舍三者俱全。

只追加：已有 ADR 不修改内容（错字与同日未落地的修正除外，修正时留注）；决定变更时写新 ADR，并在旧 ADR 标注被新 ADR 取代，不删除旧文件。部署时 `900_ADR/` 为空目录，不预填。
