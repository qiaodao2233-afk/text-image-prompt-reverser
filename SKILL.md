---
name: text-image-prompt-reverser
description: Reverse-engineer spoken ideas, normal speech, text, image references, sketches, screenshots, character sheets, posters, or videos into reusable AI generation prompts. Use when the user asks for "说的话变成提示词", "口语转提示词", "把我说的话变提示词", "正常说的话变成提示词", "文字反推", "图片反推", "反推提示词", "拆这张图", "拆这段文字", "拆这个视频", "每10秒一段提示词", "每15秒一段提示词", "30秒视频提示词", "Seedance 2.0", "豆包视频", "Dreamina", "fast版本", "快速版", "普通版", "正常版", "人物一致性", "角色一致性", "连续性", "上一段最后一帧", "角色锁定", "太AI了", "去AI味", "不像AI", "人工修图感", "IP化", "IP主视觉", "参考模型", "按模型出提示词", "参考模型出提示词", "可灵", "Runway", "Pika", "按这个模型写提示词", "图生视频怎么说", "按文字和图片写正向/反向提示词", or needs model-specific positive and negative prompts from spoken ideas, casual language, text, or visual references for image, video, scene, character, style, segmented video, consistency-locked long video, character identity locking, continuity chaining, fast/quality video mode, anti-AI visual polish, IP concept development, or image-to-video generation.
---

# 文图反推提示词

## Purpose

Turn text, images, and videos into clear reusable prompts. This skill is for reverse prompting: read or observe the reference, decide what must be preserved, and output copy-ready positive and negative prompts.

It should feel direct and practical: understand the reference, assign priorities, give the prompt, then stop.

## Core Rules

- Prefer Chinese output unless the user asks for English.
- Always separate `正向提示词` and `反向提示词`.
- For spoken or casual-language prompting, preserve the user's real meaning, clean up vague wording, infer missing visual basics conservatively, and turn it into a copy-ready prompt without making it feel unrelated.
- For text reverse prompting, extract the hidden subject, scene, mood, style, audience, and output goal from the provided text.
- For image/video reverse prompting, describe observable visual facts first, then infer style, mood, and intent.
- When text and images are both provided, assign roles clearly: text as story/intent, image as composition/style/detail, or whichever priority the user states.
- Keep the positive prompt focused on the desired result. Put mistakes, unwanted layouts, missing elements, text, watermarks, and wrong formats in the negative prompt.
- Do not invent exact camera model, lens, platform, copyrighted source, character name, or production details unless the user provides them.
- For long video generation, support segmented prompts by duration. If the user gives a total duration and interval, split exactly by that interval. If no interval is given, choose a practical interval: 10 seconds for detailed motion, 15 seconds for normal scenes, 30 seconds for simple or long continuous scenes.
- For segmented video prompts, keep a shared style/continuity lock first, then write each time range as a separate prompt that can be generated independently and stitched later.
- If the user names a target model, adapt the prompt format to that model. If the model is unfamiliar, keep the prompt general and state that it is a model-neutral version.
- For Seedance 2.0, prefer natural cinematic scene descriptions, clear subject continuity, camera motion, lighting, and one action goal per clip. Split long videos into <=15 second segments unless the user explicitly requests another interval.
- For Doubao/Dreamina/Seedance fast or quick modes, make prompts stricter and shorter than normal mode: 4-8 seconds per clip by default, one main action, one camera move, fewer new objects, and stronger identity/style locks. Normal or quality mode can use 10-15 second clips when motion is stable.
- For 30+ second videos, never rely on one long prompt. Output generation-ready segment prompts and a separate "reference lock" that repeats the character, outfit, scene, color, and ending state. Mention that later segments often drift unless each segment is generated from a reference frame or previous ending frame.
- When the user reports character consistency or continuity problems, switch to a production prompt pack: `人物锁定`, `可变/不可变信息`, `连续帧衔接`, `分段提示词`, and `统一反向提示词`.
- For character consistency, separate immutable details from flexible details. Immutable details include face shape, age range, hair color/style, outfit, key props, body proportion, art style, and color palette. Flexible details include small pose changes, expression, camera distance, snow/dust/light particles, and background motion.
- For continuity, every segment must name its first frame and last frame. The last frame should be designed as the next segment's reference frame. Do not rely only on "continue from previous segment."
- Prefer fewer story changes over richer detail when consistency matters. A stable character with simple motion is better than a complex prompt that causes drift.
- When the user says an output looks too AI-generated, too plastic, too generic, or not suitable as an IP, switch to anti-AI/IP polish. Diagnose the AI smell, lock the repeatable IP features, reduce meaningless decorative detail, and write a prompt that feels like an AI base cleaned up with manual retouching.
- For anti-AI/IP prompts, prefer strong silhouette, limited palette, clear material logic, fewer props, imperfect handmade edges, and emotional readability. Avoid overusing "8K", "ultra detailed", "cinematic", "dreamy glow", "masterpiece", and long piles of style adjectives.
- When using visual references or model references, extract reusable prompt rules: lighting contrast, composition logic, material treatment, color restraint, negative space, brushwork, narrative device, model name, duration, aspect ratio, and positive/negative prompt shape.
- Do not over-explain. The prompt is the deliverable.

## Workflow

1. Identify the task:
   - text reverse prompt
   - spoken idea / casual language to prompt
   - image reverse prompt
   - video reverse prompt
   - segmented video prompt
   - model-specific prompt
   - text + image fusion prompt
   - image-to-video prompt
   - style-only reverse prompt
   - character consistency / continuity repair prompt
   - anti-AI / IP polish prompt

2. Assign reference roles:
   - spoken idea: user intent, rough subject, desired feeling, missing details, output model or medium
   - text: story, mood, message, character intent, scene logic, product meaning
   - image: composition, color, style, character detail, clothing, prop, pose
   - video: motion, timing, camera movement, action sequence, rhythm
   - segmented video: total duration, interval length, continuity, per-segment action
   - model-specific: target model, max clip length, reference inputs, aspect ratio, output language
   - fast/quality mode: fast uses shorter, simpler clips; normal/quality supports longer, more detailed clips
   - consistency repair: immutable character lock, continuity frames, allowed changes, forbidden drift
   - anti-AI/IP polish: IP identity, silhouette, material, palette, emotional hook, human overpaint direction

3. Extract only useful prompt material:
   - subject and key objects
   - user's plain-language intent
   - scene and environment
   - composition and viewpoint
   - action, pose, or motion
   - clothing, props, material, texture
   - lighting, color palette, mood
   - medium or visual style
   - things to avoid
   - immutable identity details vs flexible animation details
   - IP anchor details: silhouette, signature prop, material, color, facial mood, repeatable symbol
   - anti-AI constraints: reduce plastic gloss, random detail, perfect symmetry, noisy decorations, over-polished lighting

4. Output the useful version:
   - spoken/text/image: `我理解你的意思` + `正向提示词` + `反向提示词` + optional `最需要保留`
   - video: `视频提示词` + `反向提示词` + optional `分镜`
   - segmented video: `统一风格锁定` + `分段提示词` + `统一反向提示词`
   - model-specific: `模型` + `统一风格锁定` + model-ready prompts
   - image-to-video: preserve first frame and add controlled motion
   - consistency repair: `人物锁定` + `连续性方案` + `分段提示词` + `统一反向提示词`
   - anti-AI/IP polish: `AI味诊断` + `IP锁定` + `人工修图方向` + `正向提示词` + `反向提示词`

For exact output templates, read `references/templates.md` when needed.

## Model-Specific Prompting

Use when the user says which generation model they will use.

1. State the target model briefly.
2. Convert the same visual idea into that model's preferred prompt shape.
3. Keep the original creative intent, but change formatting, segment length, and emphasis.
4. If the user is a customer asking "I use X model", output directly for X without explaining the whole theory.

### Seedance 2.0

Use Seedance 2.0 format when the user mentions Seedance, Seedance 2.0, or ByteDance video generation.

Seedance 2.0 prompt style:

- Use coherent natural-language paragraphs instead of only keyword lists.
- Keep each generated clip focused on one main action or camera movement.
- For long videos, split into 10-15 second segments by default.
- For 30-60 second videos, use `统一风格锁定` plus separate segment prompts.
- Include subject identity, outfit, environment, lighting, camera movement, mood, and ending state in each segment.
- If the user provides a reference image or first frame, say to preserve it as character/first-frame reference.
- Use a short `反向提示词` only for common errors: identity drift, outfit drift, scene jump, subtitles, watermark, face/body distortion, excessive camera shake.

Fast vs normal/quality mode:

- Fast/quick mode prioritizes speed and low latency. Use it for preview, simple shots, and testing. Keep each clip 4-8 seconds, avoid complex multi-shot story, avoid many props, avoid big scene changes, and repeat the subject identity in every segment.
- Normal/quality mode is better for final output, detailed motion, complex lighting, and stronger prompt adherence. Use 10-15 second clips only when the action is simple and the subject is stable.
- If the user says a Doubao/Seedance result becomes strange later in the timeline, rewrite as shorter clips with a first-frame/reference-frame instruction for each later segment.
- For character consistency, write each segment as if it may be generated independently: repeat the exact character description, outfit, key prop, environment, and the start/end state. Do not rely only on "continue from the previous segment."
- For image-to-video or video continuation, tell the user to use the last good frame of the previous segment as the reference/first frame for the next segment when the platform supports it.

Avoid asking the user for more details unless the model, duration, or target output is impossible to infer.

## Character Consistency and Continuity

Use when the user says the character changes, the later video gets strange, the next segment does not connect, or they need the same character across video segments.

Output a production prompt pack, not a short summary prompt.

Required sections:

1. `人物锁定`: exact visual identity that must repeat in every segment.
2. `不可变信息`: face, age range, hair, outfit, key prop, body proportion, art style, main palette.
3. `可变信息`: expression, tiny pose changes, camera distance, particles, cloth/hair motion, background movement.
4. `连续性方案`: how each segment starts, ends, and passes a reference frame to the next segment.
5. `分段提示词`: each segment repeats the character lock and has one main action.
6. `统一反向提示词`: include identity drift, outfit drift, face drift, scene jump, and timeline break.

Rules:

- If a platform supports first-frame or reference-frame generation, tell the user to use the last good frame of segment N as the reference frame for segment N+1.
- Do not make segment 2+ depend only on memory of segment 1. Repeat the full identity lock in every segment.
- Keep fast-mode segments 4-8 seconds. Keep normal-mode segments 8-12 seconds when identity consistency is more important than cinematic complexity.
- Use close-up and medium shots sparingly. Frequent camera angle changes can change the face.
- Avoid new props, new outfits, new locations, new lighting schemes, and new characters unless the user explicitly asks.
- If the reference is a character sheet, prioritize the sheet over text. If the reference is a finished image, prioritize the face, outfit, pose relationship, and palette.

## Anti-AI and IP Polish

Use when the user says the output is too AI, too generic, not like an IP, needs human retouching, needs model-reference prompting, or should feel like "AI base + manual cleanup."

Output a production prompt pack, not a generic beautiful-image prompt.

Required sections:

1. `AI味诊断`: 1-3 short reasons the current idea may look AI-generated.
2. `IP锁定`: 3-6 repeatable identity anchors that must stay stable across images/videos.
3. `人工修图方向`: how to make it feel edited by a human: simplify, rebalance, add material logic, keep intentional imperfections.
4. `正向提示词`: the improved generation prompt.
5. `反向提示词`: include AI smell terms and common generation mistakes.

Rules:

- Build an IP around repeatable cues, not just "pretty style": silhouette, color pair, signature object, facial mood, material, symbol, or scene ritual.
- Make the image easier to redraw by hand. A good IP prompt should have fewer core elements and stronger recognition.
- Prefer "manual retouching", "hand-adjusted composition", "intentional asymmetry", "controlled detail density", and "real material wear" when the user wants AI + human editing.
- Keep reference-model prompts practical: name the target model, adapt segment length and format, and output copy-ready positive and negative prompts.
- Put the unwanted AI traits in the negative prompt: plastic toy feel, over-smooth face, random ornaments, meaningless detail pile, over-sharpened edges, perfect symmetry, warped hands, fake text, watermark, logo.

## Text Reverse Prompt

Use when the user provides text, a rough paragraph, a story, copywriting, a scene description, a character description, or an existing prompt and asks to reverse it into a better prompt.

## Spoken Idea To Prompt

Use when the user says something informal, incomplete, or conversational and wants it turned into a usable prompt.

Rules:

- Preserve the user's idea first. Do not replace it with a different concept just because the original wording is simple.
- Turn vague words into practical visual details: subject, scene, action, mood, style, composition, lighting, and output type.
- If important details are missing, make a reasonable default and keep it visible in the prompt. Ask only when the missing detail changes the whole result.
- Keep the output copy-ready. The user should be able to paste the prompt directly into an image or video model.
- If the user names a model, adapt the format to that model.

Output:

```text
我理解你的意思是：...

正向提示词：
...

反向提示词：
...

最需要保留：
...
```

Output:

```text
我理解这段文字的核心是：...

正向提示词：
...

反向提示词：
...

最需要保留：
...
```

## Image Reverse Prompt

Use when the user uploads an image, sketch, screenshot, poster, reference sheet, or illustration and asks how to generate something like it.

Output:

```text
我理解这张图的核心是：...

正向提示词：
...

反向提示词：
...

最需要保留：
...
```

## Video Reverse Prompt

Use when the user uploads a video, animation, shot, or moving reference and asks how to describe or recreate it.

Output:

```text
我理解这段视频的核心是：...

视频提示词：
...

反向提示词：
...
```

Add a short storyboard only if the user asks for multi-shot output or the clip has important sequential actions.

## Segmented Video Prompt

Use when the user wants prompts for a long video split into generation-friendly parts, such as a 60-second video split every 10 seconds or 15 seconds, or a 30-second clip split into several smaller prompts.

If the user provides both duration and interval, split exactly:

- 60 seconds, every 10 seconds: 00:00-00:10, 00:10-00:20, 00:20-00:30, 00:30-00:40, 00:40-00:50, 00:50-01:00
- 60 seconds, every 15 seconds: 00:00-00:15, 00:15-00:30, 00:30-00:45, 00:45-01:00
- 30 seconds, every 10 seconds: 00:00-00:10, 00:10-00:20, 00:20-00:30

If the user provides only duration, choose:

- 30 seconds: split into 4-6 short clips for fast mode, or 3 x 10s / 2 x 15s for normal mode depending on action density
- 60 seconds: split into 8-12 short clips for fast mode, 6 x 10s for detailed motion, or 4 x 15s for smoother normal-mode scenes
- longer than 90 seconds: prefer 30s sections unless the scene changes quickly

Output:

```text
统一风格锁定：
...

分段提示词：
00:00-00:10：
...

00:10-00:20：
...

统一反向提示词：
...
```

Each segment should include: scene goal, subject state, action, camera movement, lighting/color, mood, and continuity from the previous segment. Keep character identity, clothing, location, color palette, and style stable across all segments.

For long videos where the user reports drift, add:

- `参考锁定`: the exact identity, clothing, prop, setting, color, and style that must not change.
- `每段起始画面`: what the first frame of the segment should look like.
- `每段结尾画面`: what frame should be used as the next segment reference.
- Shorter segments for fast mode, usually 4-8 seconds.
- Negative prompt terms for later drift: later-segment drift, identity drift, outfit drift, timeline collapse, random scene change, unrelated objects, over-complicated action.

## Text + Image Fusion

When the user provides text and image together, state reference roles before the prompt:

```text
参考分工：
文字：作为剧情/设定/情绪方向，保留...
图片：作为构图/风格/细节参考，保留...
```

Then write one unified prompt. If one reference should dominate, say so in the positive prompt and put the wrong output direction in the negative prompt.

## Image-To-Video

Use when the user asks "这张图做视频怎么说", "图生视频", or wants motion from a still image.

Preserve:

- subject identity
- clothing and props
- pose relationship
- color palette
- background
- overall mood

Add only controlled motion unless the user asks for a bigger change: hair fluttering, cloth moving, blinking, light particles, slow camera push, breathing, wing movement, or subtle environmental motion.
