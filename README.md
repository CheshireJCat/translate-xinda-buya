# translate-xinda-buya

一个遵循 Agent Skills 标准的通用翻译 skill，用来做“信达不雅”风格翻译：意思要准，表达要顺，同时强制把译文改写成粗粝、口语、带脏话、段子感和冒犯强度的低雅风格。目标语言不限；用户不指定目标语言时，默认翻译成中文。

## 它适合做什么

- 把英文、日文等文本强制翻成更粗、更口语、更有火气的目标语言版本。
- 把正式、平淡、礼貌的原文改写成低雅、带脏话和段子味的译文。
- 未指定目标语言时默认中文；指定英文、日文、粤语、西语等目标语言时，按指定语言输出。
- 翻译脏话、吐槽、字幕、meme、互联网黑话、粗口对白。
- 避免把 `bullshit` 翻成“荒谬之言”这种太端着的表达。

它的优先级是：

1. **信**：保留原意、事实、语气、说话人的态度，不乱加料。
2. **达**：译文自然、顺口、好懂。
3. **不雅**：默认就要俗、要糙、要口语、要有脏话和段子味，而不是只在原文粗糙时才粗糙。

## 安装

这个仓库采用可安装 skill 子目录布局，真正的 skill 在 `translate-xinda-buya/` 目录下。

推荐使用 `npx skills`，它能安装到 Codex、Claude Code、Cursor、GitHub Copilot 等支持 Agent Skills 的工具。下面以 Codex 为例，其他工具可替换 `--agent`：

```bash
npx skills add CheshireJCat/translate-xinda-buya \
  --skill translate-xinda-buya \
  --agent codex \
  -g
```

如果你使用 GitHub CLI，也可以通过 `gh skill` 安装。下面同样以 Codex 的用户级作用域为例：

```bash
gh skill install CheshireJCat/translate-xinda-buya translate-xinda-buya \
  --agent codex \
  --scope user
```

安装前预览：

```bash
gh skill preview CheshireJCat/translate-xinda-buya translate-xinda-buya
```

在 Codex 环境里，也可以使用 Codex skill installer，并指定子路径：

```bash
python3 install-skill-from-github.py \
  --repo CheshireJCat/translate-xinda-buya \
  --path translate-xinda-buya \
  --ref main \
  --method git
```

如果你的环境支持用 GitHub URL 安装，目标路径同样应指向 `translate-xinda-buya` 子目录，而不是仓库根目录。

## 使用示例

未指定目标语言时，默认中文：

```text
Use $translate-xinda-buya to translate:
Please review the attached document by Friday.
```

输出倾向：

```text
周五前把附件给看了，别他妈拖。
```

```text
Use $translate-xinda-buya to translate:
This is bullshit.
```

输出倾向：

```text
这就是扯淡。
```

```text
Use $translate-xinda-buya to translate:
He threw me under the bus.
```

输出倾向：

```text
他把锅全甩我身上了。
```

```text
Use $translate-xinda-buya to translate:
Screw this. I'm out.
```

输出倾向：

```text
去他的，我不干了。
```

指定其它目标语言时，按指定语言输出，但仍保持信达不雅风格：

```text
Use $translate-xinda-buya to translate into English:
请在周五前查看附件。
```

输出倾向：

```text
Check the damn attachment by Friday. Don't drag your feet.
```

## 风格边界

“不雅”不是无脑加脏话，但它确实会主动低雅化。这个 skill 默认把译文压到 Level 2 粗糙度：

- 正式文本：也要翻成口语、粗粝、带点脏的目标语言版本。
- 日常吐槽：使用自然口语、常见俗语和互联网表达。
- 粗口对白：可以进一步加重冒犯感。
- meme 和双关：优先翻译效果，不死抠字面。

它会避免把原文没有的事实、歧视性辱骂、性露骨内容、真实威胁或违法含义额外加进去。

## 仓库结构

```text
translate-xinda-buya/
  SKILL.md
  agents/openai.yaml
  references/calibration.md
```

- `SKILL.md`：skill 的触发描述、执行流程和安全边界。
- `agents/openai.yaml`：OpenAI/Codex 客户端展示用元数据；不代表这个 skill 只能给 Codex 用。
- `references/calibration.md`：长文本、脏话对白、meme 翻译时使用的风格校准参考。

## 校验

发布前可用 Agent Skills / Codex 的 skill 校验脚本检查：

```bash
python3 quick_validate.py translate-xinda-buya
```

当前版本已通过 `quick_validate.py` 校验。
