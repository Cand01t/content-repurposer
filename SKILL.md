---
name: content-repurposer
description: "Repurpose long-form articles into a full suite of short-form content assets. Triggers on: 'repurpose this article', 'turn this into social posts', 'create content from this', 'adapt this for LinkedIn', 'write ad copy from this', 'make a TikTok hook from this', 'short-form from long-form', 'content package', or any time the user shares a long piece of writing and wants any kind of short-form output — even if they only ask for one channel, offer the full suite."
---

# Content Repurposer

Turn one long-form article into 7 short-form assets saved as a single `.txt` file.

| Channel | Voice | Default length |
|---|---|---|
| LinkedIn — Company Page | Brand | 300–500 chars |
| LinkedIn — Personal | First-person executive | 800–1,200 chars |
| Facebook — Company Page | Brand, warm | 300–500 chars |
| Facebook — Personal | Casual | 200–400 chars |
| Email Newsletter Snippet | Brand, professional | 100–150 words |
| Meta Ad Copy | Headline + Primary Text + CTA | punchy |
| TikTok/Reel Script | Brand, spoken | 150–200 words |

## Process

**1. Get the article.** Accept raw text, URL (`mcp__workspace__web_fetch`), or file. Don't supplement from other sources. If paywalled or empty, ask user to paste text.

**2. Ask for references — stop and wait.** After fetching the article, ask:

> "Got it! Any reference content to match your brand voice? (URL, pasted text, or file — one for all channels or per-channel.) If not, just say so."

Wait for reply before continuing.

**3. Detect language.** All 7 assets must match the article's language. No translation unless asked.

**4. Process references.** Extract: tone, brand voice markers, target length, structural patterns (opening, closing, use of questions/bullets). Global reference = baseline for all channels; per-channel overrides it. No references = use defaults.

**5. Extract core message and pick emotional hook.** Identify: main insight, 2–3 proof points, target audience, key terms (use article's own words). Then draft 3 distinct emotional hooks — each from a different angle (e.g. FOMO, professional curiosity, contrarian take, personal relevance). Present to user and ask which to build around. Wait for reply.

Every asset teases — it does not summarize. If someone reads the post and feels they already know the article, it failed.

**6. Apply voice defaults** (unless overridden by user or references):

Assume the company owns the article.
- **Company channels** (LinkedIn Co., Facebook Co., Email, Meta Ad): professional, author framing ("here is what we built/believe") — no slang, no excessive emoji.
- **Personal channels** (LinkedIn Personal, Facebook Personal, TikTok): first-person senior executive, with personal stake.

If user says the article is external, company channels react to it; personal channels give a personal take.

**7. Draft all 7.** Use the chosen hook, core message, and reference voice/length for each channel.

Channel rules:
- **LinkedIn Co.:** no "We're excited to share…" openers. One idea, one CTA. 3–5 hashtags.
- **LinkedIn Personal:** open with micro-story or observation. End with genuine question. Max 3 hashtags.
- **Facebook Personal:** most casual. Emoji optional. No hashtags needed.
- **Email:** subject + preview text + body + CTA. No filler.
- **Meta Ad:** Headline / Primary Text / CTA Button labels required.
- **TikTok/Reel:** full spoken script — HOOK (3s) / SETUP (5–10s) / PAYOFF TEASE (10–15s) / CTA (3–5s). Written to be read on camera, not silently.

**8. Humanization check.**
- Vietnamese content + `viet-ai-humanizer` installed → run it.
- Other language + `humanizer` installed → run it.
- Otherwise, fix manually.

Always fix: em dashes → comma/period/colon; banned words (vibrant, tapestry, pivotal, testament, delve, foster, showcase, garner, crucial, intricate, interplay, align with); banned openers ("In today's…", "It's no secret…", "Let's dive in"); forced rule-of-three; "serves as/stands as/boasts" → "is/has". Vary sentence lengths.

**9. Write and deliver.** Save as `content-package-[slug].txt`:

```
[Title] — Content Package
[Date]
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
Subject: / Preview: / [body] / [CTA]
---
Meta Ad
Headline: / Primary Text: / CTA Button:
---
TikTok / Reel Script
HOOK: / SETUP: / PAYOFF TEASE: / CTA:
```

Share the file. No commentary.
