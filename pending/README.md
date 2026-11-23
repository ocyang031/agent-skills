# 待使用与待转正技能

这里保存准备试用的技能快照。在实际跑通并确认归属前，候选包留在 `pending/`。这个目录不进入正式技能索引、注册表或全局部署。

## 当前候选

| 技能 | 上游 | 版本 | 待验证 |
|------|------|------|--------|
| [糖糖 IT 口播逐字稿转换](tangtangit-koubo/SKILL.md) | [tangtang-it/tangtangit-koubo](https://github.com/tangtang-it/tangtangit-koubo) | 提交锁定，上游未声明版本 | 用中文技术文章出一份可朗读的纯逐字稿，检查步骤顺序、数字和技术名词。 |
| [ShortVideo-AI 短视频脚本生成](short-video-script-skill/SKILL.md) | [ShortVideo-AI/short-video-script-skill](https://github.com/ShortVideo-AI/short-video-script-skill) | 0.1.2 | 用已确认的口播稿生成分镜、字幕和发布文案，检查正文未被替换，命令和设置名与原文一致。 |
| [韩叙短视频口播文风助手](hanxu-script-agent/SKILL.md) | [hanxu66/hanxu-short-video-voice](https://github.com/hanxu66/hanxu-short-video-voice) | v0.1.7 | 用本题材料和独立的本人表达样本出稿，改一轮后换题复测；检查能保留表达习惯，同时没有带入旧题事实。 |

[来源锁](source-lock.json)记录每个包的完整上游提交和文件 Git blob SHA-1。候选包按提交原样保存，包含入口和配套文件。本人语料、试录和表达记录放在独立的内容工作区。

## 转正规则

1. 实际试用后，记录场景、输入、可复核的输出和结论。格式校验或下载成功只证明文件可用来开始试验。
2. 由使用者确认是否转正、目标目录和采用版本。按上游原样跟踪的包进入 `community/`，转移来源记录到社区来源锁；需要由本仓维护的定制版本进入 `curated/`，保留来源和改动说明。转正前检查上游授权、配套文件以及同名技能。
3. 转正后更新正式索引和注册表，并从待转正区移除已归档的候选。运行时安装和全局部署另行处理。
