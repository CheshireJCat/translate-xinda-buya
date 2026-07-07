# translate-xinda-buya

一个 Codex 翻译 skill，用来做“信达不雅”风格翻译：意思要准，表达要顺，但不要把原文里粗粝、口语、脏话、段子感和冒犯强度洗成漂亮官话。

## 它适合做什么

- 把英文、日文等文本翻成更接地气的简体中文。
- 翻译脏话、吐槽、字幕、meme、互联网黑话、粗口对白。
- 在“不失真”的前提下保留原文的火气、冷幽默、街头感或低雅感。
- 避免把 `bullshit` 翻成“荒谬之言”这种太端着的表达。

它的优先级是：

1. **信**：保留原意、事实、语气、说话人的态度，不乱加料。
2. **达**：译文自然、顺口、好懂。
3. **不雅**：该俗就俗，该脏才脏，粗粝程度跟原文匹配。

## 安装

这个仓库采用可安装 skill 子目录布局，真正的 skill 在 `translate-xinda-buya/` 目录下。

推荐使用 `npx skills`，它能安装到 Codex、Claude Code、Cursor、GitHub Copilot 等支持 Agent Skills 的工具：

```bash
npx skills add CheshireJCat/translate-xinda-buya \
  --skill translate-xinda-buya \
  --agent codex \
  -g
```

如果你使用 GitHub CLI，也可以通过 `gh skill` 安装，并指定 Codex 和用户级作用域：

```bash
gh skill install CheshireJCat/translate-xinda-buya translate-xinda-buya \
  --agent codex \
  --scope user
```

安装前预览：

```bash
gh skill preview CheshireJCat/translate-xinda-buya translate-xinda-buya
```

也可以使用 Codex skill installer，并指定子路径：

```bash
python3 install-skill-from-github.py \
  --repo CheshireJCat/translate-xinda-buya \
  --path translate-xinda-buya \
  --ref main \
  --method git
```

如果你的环境支持用 GitHub URL 安装，目标路径同样应指向 `translate-xinda-buya` 子目录，而不是仓库根目录。

## 使用示例

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

## 风格边界

“不雅”不是无脑加脏话。这个 skill 会按原文的语境选择粗粝程度：

- 正式文本：翻得直白一点，但不强行爆粗。
- 日常吐槽：使用自然口语和常见俗语。
- 粗口对白：保留相近强度的冒犯感。
- meme 和双关：优先翻译效果，不死抠字面。

它也会避免把原文没有的歧视性辱骂、性露骨内容或攻击性额外升级出来。

## 仓库结构

```text
translate-xinda-buya/
  SKILL.md
  agents/openai.yaml
  references/calibration.md
```

- `SKILL.md`：skill 的触发描述、执行流程和安全边界。
- `agents/openai.yaml`：Codex UI 展示用元数据。
- `references/calibration.md`：长文本、脏话对白、meme 翻译时使用的风格校准参考。

## 校验

发布前可用 Codex 的 skill 校验脚本检查：

```bash
python3 quick_validate.py translate-xinda-buya
```

当前版本已通过 `quick_validate.py` 校验。
