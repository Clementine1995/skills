# Codex Skills

Personal Codex skills for design-system selection and UI style guidance.

## Skills

### design-md-selector

Recommend suitable brand design styles from
[VoltAgent/awesome-design-md](https://github.com/VoltAgent/awesome-design-md)
based on a rough product or page brief.

Use it when you have:

- A page or app idea
- Target users
- Core functionality
- Desired mood or style direction

Example prompt:

```text
Use $design-md-selector. I want to build an AI note-taking app with document editing,
a knowledge base, and smart Q&A. The style should feel restrained, premium, and useful
for long work sessions.
```

The skill recommends a short list of candidate brand styles, explains the tradeoffs,
and names one first choice.

### vercel-geist-design

Apply Vercel's Geist design system to frontend interfaces, mockups, component styling,
CSS tokens, and product UI copy.

Use it when you want a developer-focused, minimal, high-contrast product interface.

Example prompt:

```text
Use $vercel-geist-design to design a developer-focused dashboard with Geist tokens.
```

The skill keeps the core workflow compact and stores the full light-theme reference in
`vercel-geist-design/references/geist-light-theme.md`.

## Usage

To install these skills for Codex discovery, copy the skill folders into your Codex
skills directory, usually:

```text
%USERPROFILE%\.codex\skills
```

Keep each skill folder self-contained. Avoid adding extra documentation inside a skill
unless it directly supports the skill's runtime behavior.

## Maintenance

Validate a skill after edits with the Skill Creator validator:

```text
python %USERPROFILE%\.codex\skills\.system\skill-creator\scripts\quick_validate.py <path-to-skill>
```

When `awesome-design-md` accuracy matters, refresh live repository data instead of
treating the bundled `selection-guide.md` as a complete inventory.
