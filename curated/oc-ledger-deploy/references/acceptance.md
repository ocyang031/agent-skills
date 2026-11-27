# 验收

部署完成的标准是“零人工讲解”三条，逐条核对，全绿才算完成：

1. 新 agent 不需要人工讲解，能答出：方案位置、最近记录、写入路径。
2. 一次试写入落在正确目录：在 `100_Works/` 下建一个试项目目录并写入试文件，核对落点无误后删除该试目录；流水写入不做试写，以部署收尾产生的真实首条流水为验证凭据，不写试流水、不删除任何流水（流水永留，见 templates.md 的 memory-system 模板保留节）。
3. 自检全绿：目录结构与 templates.md 一致；根 `README.md` 路径映射正确；记忆落点正确（`MEMORY.md` 格式四字段、流水按工具分文件、账本当前任务唯一）；资产清单哈希一致（如有）；敏感区与草稿箱已忽略（`git status` 不出现 `210_Personal-record/` 与 `.agents/drafts/`）；`MEMORY.md` 无重复结论；抽取脚本 `.agents/scripts/extract.py` 在位且 `--dry-run` 退出 0；空目录骨架完整：`git ls-files` 含全部应占位空目录的 `.gitkeep`（清单见 templates.md「建目录」一节）。

自检命令示例：

```bash
cd "$ROOT"
find . -maxdepth 2 -not -path "./400_Code/*" -not -path "./.git" -not -path "./.git/*" | sort
git status --short
git check-ignore -v --no-index 400_Code .artifacts 000_Inbox 200_Digital_assets/210_Personal-record .agents/skills .agents/drafts
git ls-files | grep -c '\.gitkeep$'
```

自检不验证 skill，连版本号也不查；skill 收口归事实源仓库。自检只查结构、路径映射、记忆落点、资产哈希、敏感区忽略、`MEMORY.md` 格式和抽取脚本。

验收通过后做一次收尾：写当日流水，`HANDOFF.md` 覆盖更新为当前任务无、队列空，提交根仓库。

```bash
cd "$ROOT"
git add -A
git commit -m "chore: workspace deployed and verified"
```

收尾提交只在工作区有改动时执行。重跑验收时工作区干净、无新提交，即证明幂等成立。
