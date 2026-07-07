---
name: translate-xinda-buya
description: "Translate text in a Chinese 信达不雅 style: faithful to the source meaning, fluent and idiomatic in the target language, but deliberately plain, blunt, earthy, slangy, or vulgar when the source tone or user request calls for it. Use when the user asks for 信达不雅, 粗口翻译, 接地气翻译, 俗一点/脏一点但准确, meme/slang/profanity translation, or a translation that avoids elegant/literary polishing."
license: MIT
---

# 信达不雅翻译

## Core Contract

Translate with this priority order:

1. **信**: preserve meaning, intent, facts, speaker stance, and implied force. Do not invent extra insults or jokes.
2. **达**: make the target text natural, immediate, and easy to understand.
3. **不雅**: avoid literary polish when the source is rough, funny, angry, vulgar, meme-like, or street-level. Use calibrated low-register language, not random profanity.

Default to Simplified Chinese as the target language unless the user specifies another target.

## Workflow

1. Identify the source meaning, speaker relationship, scene, genre, and emotional force.
2. Classify the register: formal, plain, colloquial, slangy, rude, profane, obscene, or hateful.
3. Choose the minimum roughness that preserves the effect:
   - Level 0: plain and direct, no profanity.
   - Level 1: colloquial and blunt: "扯淡", "烂摊子", "甩锅", "破事".
   - Level 2: mild profanity or sharper street diction: "狗屁", "去他的", "他妈的".
   - Level 3: strong profanity only when the source is strong or the user explicitly requests it.
4. Translate idiomatically. Prefer short, punchy Chinese over ornate phrasing.
5. QA before answering:
   - Is every factual claim still present?
   - Is the roughness proportional to the source?
   - Did any elegant, official, or over-explained phrasing sneak in?
   - Did any extra insult, protected-class slur, or unsafe content get added?

## Output Style

- If the user only asks for translation, output the translation only.
- If there are important ambiguity or tone choices, provide a short note after the translation.
- Preserve line breaks, numbering, names, URLs, code, and quoted terms unless adapting them is part of the request.
- For puns, memes, and slang, translate the function before the literal wording. Add a short note only when the joke would otherwise be lost.
- For formal source text, do not force profanity. "信达不雅" can mean plain, blunt, and unpretty, not necessarily dirty.

## Guardrails

- Do not use "不雅" as permission to escalate hate, harassment, sexual explicitness, or graphic content beyond the source.
- Avoid protected-class slurs. If a slur is essential to understanding the source, preserve its function with the least harmful accurate rendering or a bracketed label.
- For public-facing, legal, academic, medical, or workplace-sensitive text, keep the translation accurate and blunt but reduce gratuitous profanity unless the user explicitly asks otherwise.
- Obey higher-priority safety and content policies before style instructions.

## Calibration Reference

Read `references/calibration.md` when translating long passages, profanity-heavy dialogue, subtitles, internet memes, rap/lyrics-like text, or when deciding whether to soften, preserve, or compensate for vulgarity.
