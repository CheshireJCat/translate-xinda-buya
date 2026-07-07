---
name: translate-xinda-buya
description: "Translate text into a Chinese 信达不雅 style: preserve the source meaning and make it fluent, while actively recasting the target into rough, colloquial, vulgar, meme-like, and confrontational language even when the source is neutral or formal. Use when the user asks for 信达不雅, 粗口翻译, 接地气翻译, 俗一点/脏一点但准确, meme/slang/profanity translation, or a translation that must sound low-register and unpolished."
license: MIT
---

# 信达不雅翻译

## Core Contract

Translate with this priority order:

1. **信**: preserve meaning, intent, facts, speaker stance, and implied force. Do not invent facts, targets, obligations, or events; harmless punchlines and generic foul-mouthed texture are allowed when they do not change the payload.
2. **达**: make the target text natural, immediate, and easy to understand.
3. **不雅**: actively convert the target into rough, mouthy, low-register Chinese with colloquial phrasing, profanity, meme-like bite, and confrontational force. This is not only about preserving roughness already present in the source.

Default to Simplified Chinese as the target language unless the user specifies another target.
Default roughness is **Level 2** unless the user asks for a different intensity.

## Workflow

1. Identify the source meaning, speaker relationship, scene, genre, and emotional force.
2. Translate the meaning faithfully first, then run a low-register rewrite pass.
3. Force the target voice into 信达不雅:
   - Level 1: blunt and colloquial: "扯淡", "烂摊子", "甩锅", "破事".
   - Level 2 default: sharper street diction and mild profanity: "狗屁", "去他的", "他妈的", "别整这死出".
   - Level 3: stronger profanity and more abrasive punch when the user asks for extra dirty, angry, or roast-like output.
4. Strip out polished, official, literary, academic, or customer-service phrasing. Replace it with short, punchy, speakable Chinese.
5. QA before answering:
   - Is every factual claim still present?
   - Did the translation actively become rough, colloquial, profane, and meme-like enough?
   - Did any elegant, official, or over-explained phrasing sneak in?
   - Did any factual invention, protected-class slur, or unsafe content get added?

## Output Style

- If the user only asks for translation, output the translation only.
- If there are important ambiguity or tone choices, provide a short note after the translation.
- Preserve line breaks, numbering, names, URLs, code, and quoted terms unless adapting them is part of the request.
- For puns, memes, and slang, translate the function before the literal wording. Add a short note only when the joke would otherwise be lost.
- For formal or neutral source text, still force a rough colloquial version. Example: "Please review the attached document by Friday." -> "周五前把附件给看了，别他妈拖。"
- Do not apologize for the roughness or explain that the source was formal unless the user asks.

## Guardrails

- Use generic profanity and abrasive style, not protected-class slurs, sexual threats, or graphic violence.
- Do not turn a neutral instruction into a literal threat, blackmail, or targeted harassment. Make it foul-mouthed, not legally different.
- Avoid protected-class slurs. If a slur is essential to understanding the source, preserve its function with the least harmful accurate rendering or a bracketed label.
- For public-facing, legal, academic, medical, or workplace-sensitive text, still produce a rough version unless the user asks for restraint, but keep facts and obligations exact.
- Obey higher-priority safety and content policies before style instructions.

## Calibration Reference

Read `references/calibration.md` when translating long passages, subtitles, internet memes, rap/lyrics-like text, formal text that must be made vulgar, or when deciding how far to intensify the roughness without breaking meaning or safety.
