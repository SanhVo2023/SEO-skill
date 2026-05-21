---
name: seo-outline
description: Create a Vietnamese SEO content outline (H2/H3 only, not full article) from a keyword + optional secondary keywords + monthly search volume. Auto-researches the live Vietnamese SERP, analyzes how top 5–10 competitors structure their content, identifies the content gaps and angles competitors miss, then produces a clean outline tuned for 2026 Google ranking + AI Overview + Gemini Snippet + Perplexity citation. Scales outline depth to volume (under 400 = short, 400–1000 = medium, over 1000 = detailed). Handles YMYL topics (health, eye care, finance, legal, medical) by inserting an expert-consultation block. Trigger this skill whenever the user gives a keyword and asks for an outline, dàn ý, dàn bài, content brief outline, blog structure, article structure, SEO structure, or "gợi ý cấu trúc bài" — even if they don't say the word "outline". Also trigger when the user gives a keyword with monthly search volume and asks "viết gì cho bài này", "làm bài về…", or "lên dàn ý cho từ khoá…".
---

# SEO Outline Generator (Vietnamese-first, 2026 AEO/GEO-ready)

## What this skill does

Turn a single SEO keyword (plus optional context) into a publish-ready **outline** — H2 and H3 only, no body copy — that a Vietnamese content writer can execute. The outline is shaped by live SERP research, not generic templates, and is engineered for three audiences at once:

1. **Google's traditional ranking algorithm** (semantic coverage, EEAT, on-page signals)
2. **Google AI Overview + Gemini Snippet** (extractable blocks, question-style H2, structured proof)
3. **ChatGPT / Perplexity / Copilot citation** (information gain, brand-friendly structure, FAQ schema)

The outline is **not** an article. It is a skeleton: title proposal, meta proposal, H2 + H3 hierarchy, suggested formats per section (table / list / step / quote), and editorial notes for the writer.

## Inputs

The user must provide:

- **Main keyword** (required, 1 only) — the primary target. Vietnamese with diacritics is preferred.
- **Secondary keywords** (optional, up to 3) — semantic siblings or long-tail variants.
- **Search volume / month** (required) — integer. Drives outline depth. If the user supplies a range, use the midpoint.

If anything required is missing, ask once for it before researching. Don't guess search volume — it determines the entire outline shape.

Optional context the user might add (use if given, don't ask unprompted): target audience, brand the article is for (Mắt Việt by default in this workspace), commercial vs informational lean, deadline.

## Workflow

This is the core loop. Follow it in order. Each step has a clear deliverable before moving on.

### Step 1 — Validate and classify

Confirm the main keyword + volume are present. Then quickly classify the keyword on three axes before doing any research:

- **Intent (provisional)**: Informational / Commercial investigation / Transactional / Navigational. You'll confirm this in Step 2 from the actual SERP — but a provisional guess helps target the right SERP slice.
- **YMYL flag**: Does this keyword touch health, vision, eye disease, medication, finance, legal, or child safety? If yes, flag YMYL=true. This affects how you handle expert sourcing later.
- **Volume tier**: <400 = SHORT, 400–1000 = MEDIUM, >1000 = DETAILED. See the "Outline depth by volume" section below.

### Step 2 — SERP research (live)

Use `WebSearch` (and `web_fetch` when a result clearly contains the structure you need to study) to pull the live Vietnamese SERP. Aim for:

- The top 5 results for the main keyword (always)
- Top 3 for each secondary keyword (if provided) — only if they reveal a different intent or angle
- "People Also Ask" boxes visible on the SERP (these reveal Google's understanding of related questions)
- Any AI Overview / featured snippet visible — note its format (definition, list, table, steps)

For each top result, extract enough to answer five questions. Use a compact internal notes table — you don't show it to the user, but you reference it when building the outline:

| # | URL | Format (guide/list/comparison/how-to) | Main H2 themes (3–5) | What it does well | What it misses / does poorly |
|---|---|---|---|---|---|

**You are studying, not copying.** The point is to understand the search intent the SERP collectively reveals, then build a *different and better* structure. Two failure modes to avoid:

- Mimicking the most common structure (you'll just be the 11th identical article)
- Inventing structure that ignores intent (you'll rank for nothing)

The right move is usually: take the intent the SERP confirms, then improve on the dominant structure by (a) adding the angle competitors miss, (b) restructuring for AI-Overview extractability, (c) layering in unique signals the brand can bring (data, experience, expert quotes).

### Step 3 — Intent + gap synthesis

Before writing the outline, write two short paragraphs of analysis (these appear in the final output as a brief "Intent & Gap Analysis" section so the writer knows *why* the outline looks the way it does):

1. **Confirmed search intent** — one paragraph, plain language. What does the user *really* want when they type this? Buy something? Diagnose a symptom? Compare options? Don't just say "Informational" — say "User has just been told they have early myopia and wants to know if they really need glasses or can wait. Decision-stage informational with a strong commercial lean."

2. **Content gap & angle** — one paragraph. What is *missing* from the current top 5 that the brand can credibly fill? This is the article's reason for existing. Without a credible gap, the article won't outrank — say so honestly if the SERP is saturated and recommend a different keyword.

### Step 4 — Build the outline

Use the volume tier to pick the right structural template (see "Outline depth by volume" below). Then customize the template using the SERP intent and gap analysis. Apply these structural rules regardless of tier:

- **H2 written as natural questions whenever the topic allows.** AI Overview and Gemini Snippet pattern-match user queries against H2 text. "Kính cận chống ánh sáng xanh có thực sự cần thiết?" wins over "Tổng quan về kính chống ánh sáng xanh." Not every H2 needs to be a question — but at least 60% should be, and the first 2–3 H2 almost always should be.
- **Lead Answer block first.** Right under H1, before the first H2, include a labeled "Lead Answer (150–200 words)" instruction. This is the block AI Overview scrapes. Tell the writer: "Answer the keyword's core question directly in sentences 1–2. No throat-clearing. Include one specific number and one brand-credible reference if possible."
- **Key Takeaway box second.** A 3–5 bullet summary right after Lead Answer. This is the second-most-scraped block by AI Overview.
- **Modular H2 blocks.** Each H2 must be a self-contained mini-answer (150–300 words guidance for the writer). Tell the writer in the outline: each section should make sense if pulled out and quoted alone.
- **Structured proof.** Suggest a specific format for each H2: paragraph / bullet list / comparison table / step-by-step / quote box. AI engines prefer extractable structure. At least 1 comparison table or 1 numbered list should appear in any outline ≥ MEDIUM.
- **FAQ block at the end.** 5–8 question/answer pairs, intended for FAQPage schema. Each Q is a real long-tail variant a user would search.
- **EEAT signals.** For YMYL outlines, include an "Expert Consultation" section explicitly. For non-YMYL, include an "Author + Source" instruction at the end. Always include 2+ external citation slots.
- **Internal link slots.** Mark 3 internal link opportunities in the outline (up to pillar, across to cluster, down to product/service). The writer fills the actual URLs from the site map.

### Step 5 — Output

Deliver the outline using the exact format in "Output Format" below. Keep it tight — the outline itself should usually be 250–700 words depending on tier. The writer doesn't need preamble; they need a structure they can start drafting from in 5 minutes.

## Outline depth by volume

Volume signals how much SERP traffic the article can realistically capture, which sets a budget for writing effort. Don't over-engineer low-volume articles.

### SHORT — volume < 400

Single-purpose outline. The keyword has thin demand; ranking is cheap but ROI ceiling is low. Don't waste writer hours.

- 1 Lead Answer (120–150 words)
- 1 Key Takeaway (3 bullets)
- 3–4 H2 (mostly question-style)
- 1 H3 only if absolutely necessary
- 1 small comparison or list block
- FAQ: 3–4 questions
- Target word count: 700–1200 words

### MEDIUM — volume 400–1000

Standard blog depth. Covers the main intent comprehensively without bloating.

- Lead Answer (150–200 words)
- Key Takeaway (3–5 bullets)
- 5–7 H2 (≥ 60% question-style)
- 1–2 H3 under H2 where natural sub-questions emerge
- At least 1 comparison table OR structured list
- FAQ: 5–6 questions
- Target word count: 1500–2200 words

### DETAILED — volume > 1000

This is a money keyword. Article is meant to become a topical authority page or pillar candidate.

- Lead Answer (180–220 words)
- Key Takeaway (4–6 bullets)
- 7–10 H2 (≥ 60% question-style)
- 2–3 H3 under most H2 to capture long-tail variants
- 1 comparison table AND 1 step-by-step section AND 1 quote/case-study block
- "Expert says" or data-snapshot callout in at least 2 H2
- FAQ: 6–8 questions
- Target word count: 2200–3500 words
- Consider pillar treatment: if 2+ secondary keywords belong to the same topic family, suggest making this a pillar page with cluster spinoffs

## YMYL handling

If the keyword touches eye health, medical conditions, medications, child eye care, finance, legal, or anything where bad advice could harm a reader, treat it as YMYL.

**The outline must include**:

- An explicit "Expert Consultation" H2 with this writer note: "Include a quote or sign-off from a licensed professional (KTV khúc xạ, bác sĩ mắt, dược sĩ, etc.). If unavailable, link to a Bộ Y tế / WHO / AAO source for the specific claim."
- A visible disclaimer block near the top: "Bài viết mang tính tham khảo, không thay thế lời khuyên y khoa. Vui lòng tư vấn chuyên gia cho trường hợp cụ thể."
- At least 2 external citation slots pointing to peer-reviewed or authoritative sources (WHO, Bộ Y tế, AAO, Essilor research, etc.) — not just brand blogs.
- Author + Reviewer fields in the closing block, with reviewer credentials.

YMYL outlines should never use "guaranteed", "cures", "100%", or other absolutist language in suggested H2 titles. Use measured phrasing: "Có thể giúp giảm…", "Theo nghiên cứu…", "Được khuyến nghị bởi…".

## Output Format

Use this exact structure. Vietnamese for all writer-facing text. Plain markdown — no tables-as-art, no walls of bold.

```
# DÀN Ý SEO — [Main keyword với dấu]

**Volume/tháng:** [number]  |  **Tier:** SHORT / MEDIUM / DETAILED  |  **YMYL:** Yes / No
**Intent:** [Informational / Commercial / Navigational / Transactional]
**Secondary keywords:** [list, or "—"]

---

## Phân tích Intent & Gap

**Search intent (xác nhận từ SERP):** [1 short paragraph — what user really wants]

**Content gap & góc đánh độc đáo:** [1 short paragraph — what top 5 misses + the angle this article will use to outrank them. If SERP is saturated with no clear gap, say so and recommend a different keyword.]

---

## Đề xuất Title & Meta

**Title (≤ 60 ký tự):** [proposed title with keyword + hook + year if relevant]
**Meta description (140–160 ký tự):** [proposed meta with keyword + USP + CTA]
**URL slug:** [no-diacritic kebab-case slug, ≤ 60 chars]

---

## Cấu trúc bài

### Lead Answer (~150–200 từ — viết ngay sau H1)
> *Hướng dẫn writer:* Trả lời thẳng câu hỏi chính trong 1–2 câu đầu. Gài 1 con số cụ thể + 1 thuật ngữ chuyên ngành. Tuyệt đối không "Trong cuộc sống hiện đại…". Brand mention tự nhiên nếu phù hợp.

### Key Takeaway Box (3–5 bullet ngay sau Lead Answer)
- [Bullet 1 — insight cô đọng]
- [Bullet 2]
- [Bullet 3]
- [Bullet 4 (optional)]

### H2 #1 — [Question-style H2 in Vietnamese]
> *Format:* paragraph / list / table / steps
> *Writer note:* [what this section needs to cover and why]
- H3: [sub-question if MEDIUM/DETAILED]
- H3: [sub-question if MEDIUM/DETAILED]

### H2 #2 — [Question-style H2]
> *Format:* …
> *Writer note:* …

[…repeat for each H2 in the tier…]

### H2 — [Comparison or step-by-step section, depending on tier]
> *Format:* bảng so sánh (suggested columns: …) / steps list
> *Writer note:* …

### H2 — Expert Consultation [ONLY IF YMYL]
> *Writer note:* Quote KTV khúc xạ / chuyên gia mắt. Link tới nguồn y tế chính thống. Thêm disclaimer y khoa.

---

## FAQ block (cuối bài — dán FAQPage schema)
1. [Question 1 — long-tail variant]
2. [Question 2]
3. […]

---

## Internal link slots (writer điền URL khi viết)
- **Up (pillar):** [topic pillar to link to]
- **Across (cluster):** [related cluster article]
- **Down (commercial):** [collection / product / booking page]

## External citation slots
- [Topic / source type — e.g., "Số liệu Essilor về ánh sáng xanh"]
- [Topic / source type — e.g., "WHO khuyến nghị về thị lực học sinh"]

## EEAT signals to weave in
- [Specific brand moat to include — only if brand context provided]
- [Author + Reviewer note]

## Schema đề xuất
Article + BreadcrumbList + FAQPage[ + HowTo if step-by-step present][ + Review if comparing products]

---

**Target word count:** [range based on tier]
**Writer effort estimate:** [hours based on tier — SHORT 3–4h, MEDIUM 5–7h, DETAILED 8–12h]
```

## Quality checks before delivering

Before showing the outline to the user, verify:

- The H2 list does **not** mimic any single competitor's structure. If two of your H2 match competitor #1's H2 word-for-word, rewrite them.
- At least 60% of H2 are question-style.
- A Lead Answer block is present and labeled.
- An FAQ block is present.
- If YMYL=true, an Expert Consultation block exists and a disclaimer is mentioned.
- Outline depth matches the volume tier (don't deliver a 10-H2 outline for a volume-200 keyword — that wastes the writer's time).
- The Gap analysis says something concrete — not "competitors are generic". If you can't articulate a real gap, you didn't research enough.

## What to do when SERP research is thin

Some Vietnamese keywords have weak SERP (only 2–3 relevant results, or mostly forum / Q&A pages). In that case:

- Note it in the Gap analysis ("SERP rất yếu — đây là cơ hội rank top trong 60 ngày").
- Lean more heavily on the brand's unique angle (data, experience).
- Still produce the outline at the appropriate tier — don't downgrade just because SERP is thin.

## What to do when the keyword is wrong

If the SERP reveals the keyword has an intent the user clearly didn't expect (e.g., user wanted to write a commercial buying guide but the SERP is dominated by medical advice), say so before delivering the outline. Recommend either (a) a different keyword that matches user intent, or (b) accepting that the article should match the SERP intent. Don't silently build the outline against the SERP's grain — it won't rank.

## Tone for writer-facing notes

Brief, direct, in Vietnamese. Imagine the writer reads this on Monday morning before drafting. They want clarity, not philosophy. Notes should typically be one or two sentences. Use Vietnamese for all reader-facing copy (titles, H2s, FAQs, writer notes); English is fine in skill-internal labels ("Lead Answer", "Key Takeaway") that have become standard SEO vocabulary.
