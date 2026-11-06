# Humanizer 中文增强版

让 AI 写作少些套话，保留事实，也保留你的语气。

Humanizer 是一个用于文字润色的 Agent Skill，适合文章、工作汇报、实验报告、技术文档和个人写作。本版本以中文为主，保留上游 26 类编辑规则，补充中文示例、文体判断和成稿复核；需要时也可以处理英文。

## 改写效果

原文：

> 本月我们持续深入推进流程优化，全面赋能团队协同。审批环节从五个减少到三个，平均处理时间从四天缩短到两天，充分彰显了提质增效的重要成果。

改写后：

> 本月我们将审批环节从五个减到三个，平均处理时间从四天缩短到两天。

删除空泛评价，保留具体行动和两组数据。更多示例见[中文编辑参考](references/chinese-editing.md)。

## 能帮你做什么

| 功能 | 具体处理 |
|---|---|
| 中文去 AI 味 | 处理空泛开场、机械过渡、刻意升华、四字词堆叠，以及“赋能”“全面深入”等缺少具体含义的表达。 |
| 保留事实与证据边界 | 核对数字、日期、单位、引用、比较对象和限定条件；缺少细节时提示补充或简化表述，避免编造经历与承诺。 |
| 匹配作者语气 | 可以提供自己的文字样本，按样本调整句长、用词、标点和节奏，保留个人偏好与情绪。 |
| 按文体润色 | 工作汇报保留进度与困难，学术和技术文本保留术语与不确定性，个人随笔保留真实感受。 |
| 编辑 Markdown 与 Obsidian | 只修改范围内的文字，保护 YAML 属性、代码、链接目标、`[[双链]]`、嵌入、块标识、标签和引用键。 |
| 直接交付成稿 | 默认先给最终改写稿；需要时补充简短说明。也支持只诊断问题，或按要求展示修改理由。 |
| 复核最终文字 | 改写后再次核对事实、文风和格式，检查是否仍有重复总结、套话或翻译腔。 |

这些规则用于辅助编辑。必要的步骤、专业术语、真实对比和作者习惯应当保留，不能仅凭某个词判断一句话需要重写。

## 安装

### 使用 Skills CLI

安装本仓库的中文增强版：

```bash
npx skills add Bryce1188/humanizer --global
```

去掉 `--global` 可安装到当前项目。安装时选择你使用的 Agent，完成后重新加载技能。

### 手动安装

下载本仓库，或克隆到本地：

```bash
git clone https://github.com/Bryce1188/humanizer.git
```

将整个 `humanizer` 文件夹放进所用 Agent 的技能目录。必须保留 `references/`，中文编辑规则会从中读取；只复制 `SKILL.md` 会缺少这部分内容。

### Claude Code 插件

在支持该插件格式的 Claude Code 中执行：

```text
/plugin marketplace add Bryce1188/humanizer
/plugin install humanizer@humanizer
```

插件调用方式为 `/humanizer:humanizer`。其他支持 `SKILL.md` 的 Agent，可使用 Skills CLI 或手动安装。

## 使用示例

安装后，可在支持相应调用语法的 Agent 中使用 `$humanizer` 或 `/humanizer`，也可以直接说明需要用 Humanizer 润色。

### 润色一段文字

```text
请用 humanizer 润色下面这段中文，保留全部事实和我的语气，直接给最终稿：

[粘贴原文]
```

### 按自己的风格改写

```text
请用 humanizer 改写，参考我下面的文字样本。
保留样本的用词和节奏，不要替我补充经历。

我的文字样本：
[粘贴自己的文章片段]

需要改写的内容：
[粘贴待改写文字]
```

### 编辑文档或 Obsidian 笔记

```text
请用 humanizer 润色这篇 Markdown 笔记，只修改正文。
保留 YAML、代码、链接、双链、嵌入、标签和引用键。

文件路径：[填写文件路径]
```

### 只检查，不改写

```text
请用 humanizer 检查下面文字的 AI 味，指出具体问题和理由，暂时不要改写。

[粘贴原文]
```

也可以明确要求轻度润色、调整结构、保留篇幅，或解释关键修改。

## 如何处理文字

先通读原文，找出影响表达的句式与结构；再根据文体改写，核对事实与限定条件，最后复核成稿。长文优先保持连贯段落，清单和操作步骤按实际用途保留。

例如，实验结果中的“可能有关”不能改成“证明有效”，没有统计检验的结果不能写成“显著提升”。原文没有提供功能、数据或个人经历时，润色也不能补上。

本 Skill 用于改善表达，不承诺通过 AI 检测器。

<details>
<summary>查看 26 类编辑规则</summary>

## The 26 patterns

保留上游规则名称，便于与 [SKILL.md](SKILL.md) 对照。规则按强度和频率排序；标注为弱线索的表达需要结合上下文判断。

| # | 规则名 | 处理重点 |
|---|---|---|
| 1 | **Not X but Y** | 减少没有实际对比内容的“不是……而是……”。 |
| 2 | **One-line closers and dramatic fragments** | 删除重复总结、刻意停顿和碎片化升华。 |
| 3 | **Sayings that sound deep** | 将故作深刻的金句改成具体观点。 |
| 4 | **Staged run-up before the point** | 去掉宣布“接下来要讲什么”的空泛开场。 |
| 5 | **Arguing with no one** | 删除对不存在的异议所作的辩解。 |
| 6 | **Forced triads** | 按信息需要列举，不为了完整感硬凑三项。 |
| 7 | **Repeated sentence openings** | 调整机械重复的句首与节奏。 |
| 8 | **Dashes as the universal connector** | 检查过度使用破折号，尊重作者样本和实际用途。 |
| 9 | **Stacked qualifiers** | 精简叠加的限定词，保留真实的不确定性。 |
| 10 | **Hyphenated pairs everywhere** | 减少英文中不必要的连字符，保留固定用法。 |
| 11 | **Passive voice and missing subjects** | 在有助于理解时说明谁做了什么。 |
| 12 | **Overused AI words** | 用具体、常见的词替换成串的模板词汇。 |
| 13 | **Inflated significance** | 去掉缺少依据的重要性宣告与前景拔高。 |
| 14 | **Vague connection or association** | 有依据时说清关系，不擅自补充身份或角色。 |
| 15 | **Shallow -ing riders** | 检查英文句尾附带的空泛解释与意义延伸。 |
| 16 | **Sales language** | 将缺乏事实支撑的宣传用语改为平实描述。 |
| 17 | **Borrowed authority** | 删除无来源的专家背书和装饰性的媒体名单。 |
| 18 | **Avoiding is, are, and has** | 让英文中的简单关系使用简单动词。 |
| 19 | **Bold as decoration** | 减少装饰性加粗和没有信息作用的标签。 |
| 20 | **Decorative headings** | 让标题说明内容，减少装饰性符号和夸张措辞。 |
| 21 | **Curly quotation marks** | 按作者习惯和目标格式处理英文引号。 |
| 22 | **Chatbot residue** | 清除混入正文的问候、恭维和追加服务话术。 |
| 23 | **Knowledge-limit disclaimers and guesses** | 删除模型知识声明与无依据猜测。 |
| 24 | **A heading repeated in the first sentence** | 去掉正文对标题的重复。 |
| 25 | **Writing about the document instead of its subject** | 减少对文稿自身布局和编写过程的无用说明。 |
| 26 | **Re-explaining what the reader knows** | 对话回复先给结论，只补充影响判断的新信息。 |

</details>

## 文件说明

| 文件 | 用途 |
|---|---|
| [SKILL.md](SKILL.md) | 技能入口、处理流程和 26 类通用规则。 |
| [references/chinese-editing.md](references/chinese-editing.md) | 中文规则、例外、改写示例和交付前检查。 |
| [agents/openai.yaml](agents/openai.yaml) | 兼容 Agent 的技能显示信息与默认提示词。 |
| [.claude-plugin/](.claude-plugin/) | Claude 插件及 marketplace 配置。 |
| [.cursor-plugin/](.cursor-plugin/) | Cursor 插件配置。 |
| [CHANGELOG.md](CHANGELOG.md) | 版本记录。 |
| [scripts/validate-package.py](scripts/validate-package.py) | 检查版本、规则编号与插件配置是否一致。 |

## 版本与来源

本版本基于 [blader/humanizer](https://github.com/blader/humanizer) **3.1.0**，中文修订为 **cn.2**。导入基线提交为 `0ef9fe5bc3572734fd3ae6c448fe00a30cd5dcf0`，中文增强版由 [Bryce1188](https://github.com/Bryce1188) 维护。

中文示例组织、速查与编辑自评参考 [Humanizer-zh](https://github.com/op7418/Humanizer-zh)，其速查与评分部分注明参考 [stop-slop](https://github.com/hardikpandya/stop-slop)。本仓库的中文示例已重新编写；编辑自评用于检查文字，不代表检测器结果。

上游通用规则参考维基百科的 [Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)。

## 许可证

采用 [MIT License](LICENSE)，保留上游作者 Siqi Chen 的版权声明。
