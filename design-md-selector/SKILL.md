---
name: design-md-selector
description: Recommend suitable brand design styles from VoltAgent/awesome-design-md for web pages, apps, dashboards, landing pages, portfolios, and UI concepts. Use when the user describes a page idea, product function, target user, desired mood, or visual style and wants candidate DESIGN.md references, brand-style recommendations, tradeoffs, or a project-level DESIGN.md/Skill derived from a selected style.
---

# Design.md Selector

## Purpose

Use this skill to turn a rough product/page idea into 3-5 suitable brand design style recommendations from `VoltAgent/awesome-design-md`.

Do not treat this skill as a visual-design generator by itself. Use it to choose the right design language before implementation, then read the selected brand's `DESIGN.md` when exact tokens or rules are needed.

## Source

Primary repository:

`https://github.com/VoltAgent/awesome-design-md`

Design directories live under:

`https://github.com/VoltAgent/awesome-design-md/tree/main/design-md/<brand>`

Raw design file pattern:

`https://raw.githubusercontent.com/VoltAgent/awesome-design-md/main/design-md/<brand>/DESIGN.md`

When current accuracy matters, fetch the live repository directory or selected `DESIGN.md` instead of relying only on the bundled reference. The bundled reference is a practical routing guide, not a complete or permanent inventory.

## Workflow

1. Extract the user's brief:
   - Page or app type
   - Core functions
   - Target users
   - Desired mood
   - Domain constraints, such as AI, finance, productivity, commerce, media, developer tools, mobile, luxury, or enterprise

2. If the brief is too vague, ask at most one concise clarification. Otherwise make a reasonable assumption and state it.

3. Read `references/selection-guide.md` for the default style map.

4. Recommend 3-5 candidate brand styles.

5. Give one clear first choice and explain why it fits better than the alternatives.

6. If the user chooses a brand or asks for implementation, fetch/read that brand's `DESIGN.md` and apply it directly.

## Recommendation Rules

- Prefer functional fit over surface aesthetics.
- For SaaS, dashboards, admin tools, and productivity workflows, bias toward restrained product systems such as Linear, Vercel, Stripe, Airtable, Notion, Supabase, Sentry, or Superhuman.
- For developer tools, AI tools, CLIs, coding surfaces, or technical docs, consider Vercel, Cursor, Warp, Raycast-like choices if present, Supabase, HashiCorp, Sentry, ClickHouse, or x.ai.
- For finance, payments, crypto, or trust-heavy data products, consider Stripe, Coinbase, Wise, Binance, IBM, or Bloomberg-like choices if present.
- For consumer, lifestyle, travel, food, music, and marketplace pages, consider Airbnb, Apple, Spotify, Starbucks, Uber, Nike-like choices if present, or Shopify.
- For editorial, publishing, content-heavy, and media experiences, consider WIRED, The Verge, Notion, Apple, or Webflow.
- For premium hardware, automotive, luxury, or dramatic product launches, consider Apple, Tesla, BMW, BMW M, Ferrari, Bugatti, or SpaceX.
- Avoid choosing a highly expressive consumer brand for dense operational tools unless the user explicitly wants a bold or campaign-like direction.
- Avoid choosing a quiet dashboard style for brand-led marketing pages unless clarity and enterprise trust matter more than memorability.

## Output Format

When recommending styles, use this format:

```markdown
**Assumption**
I am treating this as ...

**Shortlist**
1. Brand - why it fits; what it would emphasize; main risk.
2. Brand - why it fits; what it would emphasize; main risk.
3. Brand - why it fits; what it would emphasize; main risk.

**My Pick**
Choose Brand because ...

**How I Would Use It**
Use Brand's structure/tokens for ...; optionally mix with Brand B for ...
```

Keep the recommendation practical. Name the tradeoff in plain language: clarity vs personality, density vs atmosphere, trust vs energy, editorial vs operational, consumer polish vs developer utility.

## Follow-On Actions

If the user asks to continue after selecting a style:

- `Copy as project DESIGN.md`: fetch the selected `DESIGN.md`, adapt only project-specific names or constraints, and save it as a project-level `DESIGN.md`.
- `Create a style Skill`: create a focused Skill for the selected brand using the skill-creator workflow.
- `Implement UI`: read the selected `DESIGN.md` first, then build the page using its visual rules and tokens.
- `Compare styles`: fetch the relevant `DESIGN.md` files and compare only the dimensions that affect the user's task.

## Validation

Before finishing:

- Recommend no more than 5 styles unless the user asks for a broad survey.
- Include one explicit first choice.
- Explain at least one downside or mismatch for each candidate.
- Do not claim the repository inventory is current unless it was fetched during the turn.
- Provide source links when live repository or raw `DESIGN.md` files were used.
