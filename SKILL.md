---
name: human-writing-editor
description: Use when rewriting, auditing, humanizing, de-AI-ing, or scoring text so it sounds human, specific, natural, and publish-ready instead of generic or AI-generated. Includes a Bahasa Indonesia mode with plain language, EYD, inclusive language, and the RASA gate (Ritmis, Akurat, Sarat Makna, Alami).
version: 2.0.0
author: Feyber, with Hermes Agent and DeepSeek
license: MIT
metadata:
  hermes:
    tags: [writing, editing, humanize, anti-ai-slop, ai-isms, voice, scoring, bahasa-indonesia, eyd, plain-language, rasa]
    related_skills: [avoid-ai-writing, humanizer, bahasa-indonesia-plain]
---

# Human Writing Editor

## Overview

Human Writing Editor rewrites text so it sounds like a person wrote it. It combines two jobs:

1. Remove AI writing patterns: filler, inflated phrasing, chatbot artifacts, generic transitions, vague authority, and over-polished structure.
2. Add human voice: stronger rhythm, sharper specificity, a real point of view, and enough imperfection to avoid the sterile "LLM final answer" feel.

The goal is not to make text informal by default. The goal is to make it fit the context. A tweet should sound like a tweet. A memo should sound like a memo. A script should sound like someone could actually say it out loud.

Version 2.0.0 adds a Bahasa Indonesia mode. It keeps the same two jobs and adds Indonesian norms: plain language, EYD, inclusive language, trauma-aware communication, and the RASA gate. Use the English rules for English text and the Indonesian rules for Indonesian text. Do not mix the conventions in one document.

## When to Use

Use this skill when the user asks to:

- humanize text
- remove AI writing patterns
- make writing sound less like ChatGPT
- rewrite a tweet, caption, comment, script, email, article, README, PR description, or landing page
- audit text for AI tells
- score a rewrite
- generate multiple options and pick the strongest one
- match a provided writing sample
- write or edit Indonesian text in a plain, natural, and inclusive style
- check Indonesian copy against EYD
- run a RASA check: Ritmis, Akurat, Sarat Makna, Alami

Do not use it to invent facts. If the text needs current or factual claims, verify those with tools first. This skill edits voice and structure; it does not replace research.

## Operating Modes

### Quick rewrite mode

Use for most short requests.

Return:

```text
Final:
<rewritten text>

Score: <total>/50
- Directness: <1-10>
- Rhythm: <1-10>
- Trust: <1-10>
- Authenticity: <1-10>
- Density: <1-10>

Why it works:
<one or two short bullets>
```

### Options mode

Use when the user asks for alternatives.

Return 3-7 options, each with a score. Pick the best one.

```text
Option 1:
<text>
Score: 42/50

Option 2:
<text>
Score: 45/50

Best pick:
Option 2, because <reason>.
```

### Detect-only mode

Use when the user says "audit", "scan", "detect", "flag only", or "don't rewrite".

Return:

```text
Issues found:
- "<quoted phrase>" -> <why it sounds AI-generated>

Assessment:
<what matters most and what can be ignored>
```

### Full edit mode

Use for long-form writing, README files, emails, scripts, articles, and anything the user plans to publish.

Return:

1. Issues found
2. Rewrite
3. Score
4. Second-pass audit
5. Final version if the second pass changed anything

## Scoring System

Score every final rewrite when useful, and always score when the user asks.

Each category is 1-10 points.

Dimension names are bilingual. Use the Indonesian labels when the text is Indonesian: Lugas, Ritmis, Akurat, Padat, Alami. Padat is the Density dimension and carries Sarat Makna.

### Directness / Lugas

Does the writing say the thing without throat-clearing?

High score:
- Starts with the point.
- Avoids "let's dive in", "here is", "it is worth noting", "in today's world".
- Does not restate the prompt.

Low score:
- Opens with broad context.
- Announces what it will explain.
- Uses filler before the actual point.

### Rhythm / Ritmis

Does it sound natural when read aloud?

High score:
- Mixes short and long sentences.
- Allows fragments when they fit.
- Does not feel symmetrical or overly polished.

Low score:
- Every sentence is the same length.
- Every paragraph lands the same way.
- Sounds like a text-to-speech script with no friction.

### Trust / Akurat

Does it respect the reader?

High score:
- Makes specific claims.
- Avoids overexplaining.
- Avoids fake certainty and fake balance.
- Names sources when making sourced claims.

Low score:
- Uses vague authority like "experts say".
- Hedges too much.
- Inflates ordinary points into historic moments.

### Authenticity / Alami

Does it sound like a real person with a point of view?

High score:
- Has voice.
- Has a clear angle.
- Uses first person when appropriate.
- Feels context-specific, not reusable anywhere.

Low score:
- Feels neutral, polished, and generic.
- Could be pasted under any similar post.
- Has no opinion or edge.

### Density / Padat (Sarat Makna)

Is every word doing work?

High score:
- Tight.
- Specific.
- No filler.
- No decorative phrasing.

Low score:
- Uses phrases that can be cut without changing meaning.
- Repeats ideas.
- Adds generic conclusions.

### Score Guide

- 45-50: excellent, publish-ready
- 40-44: strong, usually publish-ready
- 35-39: usable, but one more pass may help
- 25-34: still generic or over-polished
- below 25: rewrite from scratch

## Editing Rules

### Remove AI vocabulary

Flag these aggressively unless the context makes them necessary:

- delve / delve into
- landscape as a metaphor
- realm
- tapestry
- robust
- comprehensive
- cutting-edge
- leverage as a verb
- utilize
- pivotal
- seamless
- transformative
- game-changer / game-changing
- impactful
- actionable
- holistic
- thriving ecosystem
- at its core
- it is worth noting that
- in today's world
- let's dive in

Replace them with simpler words or rewrite the sentence around a specific claim.

### Remove chatbot artifacts

Cut:

- Great question!
- Certainly!
- Absolutely!
- I hope this helps.
- Let me know if you need anything else.
- Here is an overview.
- To answer your question.

Published text should not sound like a chat response pasted into a document.

### Cut signposting

Avoid announcing the structure.

Bad:

```text
Let's break this down.
Here is what you need to know.
In this article, we will explore...
```

Better:

```text
Start with the actual point.
```

### Fix fake significance

AI often makes ordinary points sound historic.

Cut or rewrite:

- marks a pivotal moment
- serves as a testament to
- underscores the importance of
- reflects a broader shift
- the future looks bright
- only time will tell

State what happened. Let the reader decide how important it is.

### Remove vague authority

Do not keep claims like:

- Experts believe...
- Industry leaders agree...
- Studies show...
- Observers have noted...

Name the source or remove the attribution.

### Avoid formulaic contrast

Use sparingly:

```text
It is not just X, it is Y.
This is not about X, it is about Y.
```

These can work once in a while, but they are overused by AI. Prefer a direct sentence.

### Avoid rule-of-three padding

AI likes neat triads:

```text
fast, reliable, and scalable
innovation, collaboration, and growth
```

Keep the triad only if all three items matter. Otherwise use one strong phrase or a more specific sentence.

### Repeat the right word

Do not use synonym cycling just to avoid repetition.

Bad:

```text
The developer fixed the bug. The engineer then updated the issue. The practitioner shipped the patch.
```

Better:

```text
The developer fixed the bug, updated the issue, and shipped the patch.
```

### Vary sentence length

If every sentence is 15-25 words, the rewrite will still feel AI-generated. Mix short lines with longer lines. Fragments are allowed when the context supports them.

### Keep useful personality

Do not polish away all voice. Real writing can be slightly uneven, opinionated, funny, skeptical, or blunt.

Good humanization adds a pulse, not just grammar correction.

## Bahasa Indonesia Mode (RASA)

Switch to this mode when the text is Indonesian, the user asks for Bahasa Indonesia, or the user mentions RASA, EYD, or plain language.

The goal does not change: text that a person would write for a specific reader. This mode adds four checks: plain language, EYD, inclusion, and the RASA gate.

### Plain language

- Put the main point first in the document, section, paragraph, and sentence.
- One idea per sentence. One topic per paragraph.
- Keep sentences to 12-20 words, with 25 as the ceiling.
- Use active voice and name the actor.
- Cut nominalizations and office words. Write "mempercepat", not "melakukan pengoptimalan".
- Prefer everyday words: memakai, membantu, bekerja sama, membuat, soal, agar, mulai, selesai, memperbaiki.
- Cut filler: "pada dasarnya", "perlu diketahui bahwa", "sebagaimana diketahui", "dalam rangka", "terkait hal tersebut".
- No Latin abbreviations. Write "misalnya", "yaitu", "dan sebagainya".
- Write "dan", not "&", except in brand names.
- Address the reader as "kamu" or "Anda". Pick one per document. Use "kami" for the organization.
- Use "dia" for a singular subject of unknown gender.

### EYD quick rules

- Use sentence case for headings, labels, and buttons. Capitalize proper nouns and the first word of a sentence.
- Do not use capital letters or bold text for emphasis.
- Dates: "4 Juni 2026". Ranges: "4 sampai 8 Juni 2026". Times: "10.00-11.30". Write "tengah hari", not "12.00 siang".
- Numbers: "50%", "Rp75.000", "1.500.000", "Rp5 miliar". Use "hingga" or "sampai" for ranges.
- Use one exclamation mark at most, and only for genuine celebration.
- "di" as a preposition is separate: "di kantor". As a prefix it is joined: "ditulis". The same rule applies to "ke".
- "pun" is separate in "apa pun" and "kapan pun", joined in "walaupun" and "meskipun".
- Common fixes: praktik, analisis, risiko, izin, zaman, mengubah, silakan, nomor, kualitas, apotek, objek, aktivitas, sekadar, memengaruhi, antre.
- Use descriptive link text. Never "klik di sini".
- No FAQ section unless the user explicitly asks.

### Inclusion and safety

- People first: "pengguna dengan disabilitas", not a label.
- Avoid stigma words: gila, bodoh, lambat, lemah, cacat, abnormal.
- Do not treat one family form as "normal".
- No humor built on stereotypes of ethnicity, gender, religion, or body.
- Error messages state what happened, do not blame the user, and name the next step.
- Destructive actions name the consequence and offer control.
- No fake urgency. Use real deadlines only.
- Sensitive topics: acknowledge the emotional weight without dramatizing, and offer a way out.
- Numbers: no piles. Add a concrete comparison and use sequence words.
- Do not assume a Jakarta context, fast internet, a new phone, or a bank account.
- Use diverse names and examples.

### RASA gate

Run this after rewriting. Every dimension must pass before delivery.

- Ritmis: read the text aloud. Vary sentence length. Remove clusters and stumbles.
- Akurat: every word carries the intended meaning. No vague qualifiers, no unsourced authority, no fake certainty.
- Sarat makna: every line earns its place. Cut lines that only fill space.
- Alami: it sounds like a person in this context. Formal can be natural. Remove translationese.

If one dimension fails, rewrite and run the gate again. A high score does not excuse a failed gate.

Gate rule: total at least 40/50, no dimension below 7, all four RASA dimensions pass, and no invented facts. A single fabricated claim cancels the score.

### Indonesian output

When the user writes in Indonesian, return the Indonesian labels:

```text
Hasil:
<teks>

Skor: <total>/50
- Lugas: <1-10>
- Ritmis: <1-10>
- Akurat: <1-10>
- Padat: <1-10>
- Alami: <1-10>

RASA: <lulus atau gagal, sebut yang gagal>
Kenapa lebih baik:
- <alasan singkat>
```

## Voice Matching

If the user provides a writing sample, analyze it first:

- sentence length
- punctuation habits
- level of slang or formality
- paragraph rhythm
- humor and edge
- how direct the writer is
- recurring words or phrases

Then rewrite the target text using that voice. Do not copy exact phrases unless the user asks.

## Examples

### Generic investment comment

Before:

```text
This highlights the importance of long-term conviction and patience in investing.
```

After:

```text
Everyone wants the 100x. Almost nobody wants to sit through the decade of pain before it.
```

Score: 44/50

- Directness: 9
- Rhythm: 9
- Trust: 8
- Authenticity: 9
- Density: 9

Why it works: it keeps the investment point, removes generic phrasing, and adds a specific human angle.

### Product copy

Before:

```text
Our cutting-edge platform leverages AI to streamline your content creation workflow and deliver seamless results.
```

After:

```text
The app turns a rough idea into usable content without making you bounce between five tools.
```

Score: 41/50

- Directness: 8
- Rhythm: 8
- Trust: 8
- Authenticity: 8
- Density: 9

Why it works: it replaces buzzwords with a concrete workflow benefit.

### Email

Before:

```text
I hope this message finds you well. I wanted to reach out to explore a potential collaboration opportunity.
```

After:

```text
I wanted to ask about a possible collaboration between our teams.
```

Score: 39/50

- Directness: 8
- Rhythm: 7
- Trust: 8
- Authenticity: 7
- Density: 9

Why it works: it cuts the greeting filler and gets to the point.

### Indonesian product copy

Brief: package delivery app. The old flow had seven steps, the new one has three. Readers are new users.

Before:

```text
Di era digital yang berkembang pesat, kami menghadirkan solusi pengiriman yang seamless dan inovatif untuk memenuhi kebutuhan pelanggan.
```

After:

```text
Kirim paket sekarang tiga langkah: isi alamat, pilih kurir, bayar. Dulu tujuh.
```

Score: 44/50

- Lugas: 9
- Ritmis: 9
- Akurat: 8
- Padat: 9
- Alami: 9

Why it works: it drops the warm-up, uses the numbers from the brief, and mixes a long instruction with a short line.

### Indonesian error message

Brief: the form saves drafts automatically. The connection dropped.

Before:

```text
Terjadi kesalahan yang tidak terduga. Mohon ulangi proses pengiriman formulir Anda.
```

After:

```text
Formulir belum terkirim. Periksa koneksi internet, lalu coba lagi. Jawabanmu tetap tersimpan.
```

Score: 43/50

- Lugas: 9
- Ritmis: 8
- Akurat: 9
- Padat: 9
- Alami: 8

Why it works: it does not blame the user, names the next step, and says what is safe.

## Common Pitfalls

1. **Making everything casual.** Human does not always mean slangy. Match the context.

2. **Only swapping words.** Replacing "leverage" with "use" helps, but rhythm and structure matter more.

3. **Over-polishing.** Perfect grammar and perfect symmetry can make text sound more AI-generated.

4. **Ignoring context.** A comment must respond to the actual post. A script must sound speakable. A README must stay clear.

5. **Inventing specificity.** Add concrete details only if they are in the source or verified.

6. **Scoring without improving.** If a rewrite scores below 35, do another pass or rewrite from scratch.

## Verification Checklist

Before finalizing, check:

- [ ] No chatbot artifacts remain.
- [ ] No obvious AI vocabulary remains unless context requires it.
- [ ] The opening starts with the point.
- [ ] The rhythm varies.
- [ ] The text is specific to the context.
- [ ] The rewrite preserves the original meaning.
- [ ] Any factual claims are sourced or already provided.
- [ ] Score is included when requested or useful.
- [ ] If the score is below 35, another pass is done.
- [ ] Indonesian mode: plain language and EYD are checked.
- [ ] Indonesian mode: no translationese or office jargon remains.
- [ ] Indonesian mode: the text is inclusive and trauma-aware.
- [ ] Indonesian mode: all four RASA dimensions pass.

## Attribution

This skill combines concepts from `avoid-ai-writing` and `humanizer`. The humanizer pattern set is based on Siqi Chen's `blader/humanizer` project and Wikipedia's "Signs of AI writing" cleanup guidance.

The Bahasa Indonesia mode adapts the plain-language rules and the RASA framework (Ritmis, Akurat, Sarat Makna, Alami) from the [Bahasa Indonesia plain skill gist](https://gist.github.com/orepras/3e1ca8974fc51d11825f142fa6a66635) by [orepras](https://x.com/orepras).

Version 2.0.0 was prepared by Feyber with Hermes Agent and DeepSeek. Preserve attribution and compatible licensing when publishing publicly.
