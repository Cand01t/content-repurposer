---
name: content-repurposer
description: "Repurpose long-form articles into a full suite of short-form content assets. Use this skill whenever the user wants to transform, adapt, or reformat an article, blog post, essay, or any long-form text into shorter content for distribution channels. Triggers on: 'repurpose this article', 'turn this into social posts', 'create content from this', 'make posts from this article', 'adapt this for LinkedIn', 'write ad copy from this', 'create an email snippet from this', 'make a TikTok hook from this', 'social media content from article', 'short-form from long-form', 'content package', or any time the user shares a long piece of writing and wants any kind of short-form output — even if they only ask for one channel, offer the full suite."
---

# Content Repurposer

Turn one long-form article into 7 short-form assets across social, email, and paid channels — saved as a single `.txt` file.

Uses the `marketing:draft-content` skill for each channel.

## The 7 outputs

| Channel | Voice | Default length |
|---|---|---|
| LinkedIn — Company Page | Brand, community-oriented | 300–500 chars |
| LinkedIn — Personal | First-person executive | 800–1,200 chars |
| Facebook — Company Page | Brand, warm | 300–500 chars |
| Facebook — Personal | Casual, friend-like | 200–400 chars |
| Email Newsletter Snippet | Brand voice, professional, scannable | 100–150 words |
| Meta Ad Copy | Headline + Primary Text + CTA Button | punchy |
| TikTok/Reel Hook | Spoken, pattern interrupt | max 30 words |

Default lengths apply only when no reference is provided for that channel.

## Process

**1. Get the article.** Accept raw text, URL (fetch with `mcp__workspace__web_fetch`), or uploaded file. Only use the provided content — no supplementing from other sources. If a URL is paywalled or empty, ask the user to paste the text.

**2. Detect the language.** All 7 assets must be in the same language as the article. No translation unless the user asks.

**3. Collect per-channel references.** Ask if the user has reference posts for any channel (a past LinkedIn post, a Facebook post that worked, an email snippet). Accept URL, pasted text, or file — for any or all channels. A single global reference applies to all channels as baseline.

From each reference, extract: tone (formal/casual), brand voice markers, approximate length (treat as target), and structural patterns (how it opens, closes, whether it uses questions or bullets).

**4. Extract the core message.** Identify: the main insight, 2–3 proof points, the emotional hook (what makes a reader care), the target audience, and key terms from the article. Use the article's own words — don't paraphrase into synonyms.

Every asset's job is to make the reader click through to the full article — not summarize it. Tease the tension, hint at the payoff, stop before giving it away. If someone reads the post and feels they already know the article, it failed.

**5. Apply default voice assumptions.** Unless told otherwise:

Assume the article was written and released by the company themselves.

- Company channels (LinkedIn Company Page, Facebook Company Page, Email Newsletter, Meta Ad) = the company introducing their own content, idea, or initiative. Professional tone throughout. They are the author, not a commentator. Frame it as "here is what we built / believe / are doing" — not reacting to external news.
- Personal channels (LinkedIn Personal, Facebook Personal, TikTok/Reel Hook) = a senior executive of that company, first-person, with a real stake in the topic.

If the user explicitly says the article is from an external source (a news outlet, third-party blog, etc.), company channels react to it and personal channels give a personal take. Otherwise, assume the company owns the content.

If the user specifies a different author or company context, override these defaults entirely.

**6. Draft all 7 using `marketing:draft-content`.** Pass: content type, core message, audience, proof points, tone (from reference or defaults), length (from reference or defaults), brand voice (from reference if provided). After each draft, check it against the reference and tighten.

All company channels (LinkedIn Company, Facebook Company, Email, Meta Ad) must stay professional in tone — no slang, no excessive emoji, no casual phrasing. They represent the brand.

Channel notes beyond what draft-content handles:
- LinkedIn Company: no "We're excited to share..." openers. One idea, one CTA. 3–5 hashtags at end.
- LinkedIn Personal: micro-story or personal observation to open. End with a genuine question. 3 hashtags max.
- Facebook Personal: most casual of all. Emoji optional. No hashtags needed.
- Email: brand voice, professional. Subject line + preview text + body + CTA. No filler sentences.
- Meta Ad: label clearly as Headline / Primary Text / CTA Button.
- TikTok: spoken word. Label as `HOOK (spoken):`. Pattern interrupt openers work best.

**7. Humanization check.** Before writing the file, scan every asset and fix:
- Em dashes (replace with period, comma, or colon)
- Banned words: vibrant, tapestry, pivotal, testament, underscore, highlight (verb), delve, foster, showcase, garner, crucial, enduring, intricate, interplay, align with
- Banned openers: "In today's..." / "It's no secret..." / "Let's dive in" / "It's not just about X, it's about Y"
- Rule of three (don't force ideas into threes)
- "Serves as" / "stands as" / "boasts" (use "is" / "has")
- Uniform sentence lengths (vary deliberately — short punches after longer setups)

Use specific details from the article. Take a position. Let incomplete thoughts land when they land naturally.

**8. Write the .txt file** using the Write tool directly:

```
[Article Title] — Content Package
[Today's date]

---

LinkedIn — Company Page

[copy]

---

LinkedIn — Personal

[copy]

---

Facebook — Company Page

[copy]

---

Facebook — Personal

[copy]

---

Email Newsletter

Subject: [subject line]
Preview: [preview text]

[body]

[CTA]

---

Meta Ad

Headline: [headline]
Primary Text: [body]
CTA Button: [label]

---

TikTok / Reel Hook

HOOK (spoken): [script]
```

Emoji: use for Facebook Personal and TikTok when it fits. Follow the reference if one was provided. LinkedIn Company and Email usually don't need them.

Save as `content-package-[slug].txt` to the outputs directory.

**9. Deliver.** Share the file. No commentary.
