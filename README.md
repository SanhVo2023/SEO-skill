# SEO Outline Skill — Mắt Việt Content Team

A Claude skill that turns a Vietnamese SEO keyword + monthly search volume into a publish-ready content outline. Built for the Mắt Việt content team, optimized for 2026 Google ranking + AI Overview + Gemini Snippet + Perplexity citation.

## What it does

Give Claude a keyword like:

> Lên dàn ý cho từ khoá "kính chống ánh sáng xanh có cần thiết", volume 720/tháng

…and the skill will:

1. Live-search the Vietnamese Google SERP for that keyword
2. Analyze how the top 5 competitors structure their content (and where they're weak)
3. Classify search intent + flag YMYL topics (health, finance, legal)
4. Build an outline sized to the volume tier:
   - **< 400/mo** → SHORT outline (3–4 H2, ~700–1200 words)
   - **400–1000/mo** → MEDIUM outline (5–7 H2, ~1500–2200 words)
   - **> 1000/mo** → DETAILED outline (7–10 H2, ~2200–3500 words)
5. Deliver H2/H3 only (not the full article) — title/meta proposals, Lead Answer + Key Takeaway blocks, FAQ schema, internal/external link slots, schema recommendations, and writer notes in Vietnamese

For health/eye-care keywords it automatically adds an Expert Consultation section + medical disclaimer.

## Installation

Two ways to install — pick whichever fits your workflow.

### Option 1 — Install the `.skill` file (recommended for non-developers)

1. Download `seo-outline.skill` from this repo (or `git clone` the whole repo)
2. Open Claude (Cowork mode / Claude Desktop / Claude Code)
3. Drag the `seo-outline.skill` file into your conversation, or use **Settings → Skills → Install from file** and select it

After install, the skill auto-triggers whenever you ask for an outline — no need to invoke it manually.

### Option 2 — Copy the skill folder directly (for Claude Code users)

```bash
git clone https://github.com/SanhVo2023/SEO-skill.git
cp -r SEO-skill/seo-outline ~/.claude/skills/user/
```

On Windows:

```powershell
git clone https://github.com/SanhVo2023/SEO-skill.git
xcopy /E /I SEO-skill\seo-outline %APPDATA%\Claude\skills\user\seo-outline
```

Restart Claude after copying.

## How to use it

The smallest prompt that gets a full outline:

```
Lên dàn ý cho từ khoá "kính áp tròng dùng 1 ngày", volume 350. Brand: Mắt Việt.
```

The skill needs only two things: a **main keyword** + a **monthly search volume**. Anything else is optional context the skill uses if you provide it:

- Secondary keywords (up to 3)
- Target audience / persona
- Brand context (default: Mắt Việt)
- Commercial vs informational lean

If you forget to provide volume, the skill will ask once before proceeding — search volume determines outline depth and writing-effort budget.

## What you get back

A markdown outline with this structure:

```
# DÀN Ý SEO — [keyword]

Volume | Tier | YMYL flag | Intent | Secondary keywords

## Phân tích Intent & Gap
- Confirmed search intent (1 paragraph)
- Content gap + unique angle (1 paragraph)

## Title & Meta proposal
- Title (≤60 ký tự)
- Meta description (140–160 ký tự)
- URL slug (không dấu)

## Cấu trúc bài
- Lead Answer block (writer instructions)
- Key Takeaway box (3–5 bullets)
- H2 (question-style) + H3
- Comparison table / step-by-step / quote suggestions
- Expert Consultation block (if YMYL)

## FAQ block (5–8 Q&A — FAQPage schema)

## Internal link slots (up / across / down)
## External citation slots
## EEAT signals to weave in
## Schema markup recommendation

Target word count | Writer effort estimate
```

## Files in this repo

```
SEO-skill/
├── README.md                  ← you are here
├── seo-outline.skill          ← installable package (drag into Claude)
└── seo-outline/
    └── SKILL.md               ← the skill instructions (source)
```

## Updating the skill

If the team wants to tune the skill (different tier thresholds, additional output sections, etc.):

1. Edit `seo-outline/SKILL.md`
2. Repackage: `python -m scripts.package_skill ./seo-outline` (requires the skill-creator skill installed)
3. Commit + push the new `.skill` file
4. Team members reinstall by dragging the new file in

## Credits

Built for the Mắt Việt Content Team — Chuỗi cửa hàng mắt kính chính hãng lớn nhất Việt Nam.

Tested on three real keywords (SHORT, MEDIUM, DETAILED+YMYL tiers) with a +27pt pass-rate improvement over baseline Claude (86.8% vs 59.8%).
