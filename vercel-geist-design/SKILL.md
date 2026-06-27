---
name: vercel-geist-design
description: Apply Vercel's Geist design system to frontend interfaces, mockups, design reviews, CSS tokens, component styling, and product UI copy. Use when the user asks for Vercel-style, Geist-style, developer-focused, minimal, high-contrast SaaS/product interfaces, or asks to convert Vercel design.md guidance into implementation details.
---

# Vercel Geist Design

## Overview

Use this skill to produce interfaces that follow Vercel's Geist light theme: minimal, high-contrast, developer-focused, spacious, and accessible. Prefer token-driven decisions over ad hoc styling.

## Workflow

1. Identify the product surface: marketing page, dashboard, form, settings, table, modal, or component set.
2. Read `references/geist-light-theme.md` when exact colors, typography, spacing, radii, component tokens, or copy rules are needed.
3. Apply Geist tokens directly in CSS, design specs, or component props instead of inventing nearby values.
4. Verify the result against the checklist below before finishing.

## Core Rules

- Use Geist Sans for UI/prose and Geist Mono for code, data, and aligned numbers.
- Use `copy-14` or `label-14` for most product UI text.
- Use the gray scale for hierarchy: `gray-1000` primary text, `gray-900` secondary text/icons, `gray-700` disabled text.
- Keep accent colors meaningful: blue for links/focus/success-like primary signals, red for errors, amber for warnings.
- Use a 4px spacing scale. Default rhythm: 8px inside groups, 16px between groups, 32-40px between sections.
- Keep radii tight: 6px for controls and everyday surfaces, 12px for menus/modals, 16px for fullscreen surfaces, 9999px only for pills/avatars/circular controls.
- Build hierarchy with borders, tonal surfaces, and whitespace before shadows.
- Use motion only to clarify state changes. Prefer instant interactions; keep helpful motion short and honor `prefers-reduced-motion`.
- Use Title Case for labels, buttons, titles, and tabs. Use sentence case for body, helper text, and toasts.

## Component Guidance

- Primary button: use solid `gray-1000` with `background-100` text for the single most important action.
- Secondary button: use `background-100` with a translucent gray border.
- Tertiary button: use transparent fill with `gray-1000` text for low-emphasis actions.
- Error button: use solid `red-800` with white text for destructive actions.
- Inputs: use `background-100`, a translucent border, 6px radius, and `label-14`.
- Size controls consistently: 32px small, 40px default, 48px large.
- Apply hover and active by stepping token scales: `100` to `200` to `300` for fills, `400` to `500` to `600` for borders.
- Show a visible `:focus-visible` ring on every interactive element.

## Copy Rules

- Name actions with a verb and noun, such as `Deploy Project` or `Delete Member`.
- Avoid vague labels such as `OK`, `Confirm`, or bare verbs.
- Write errors as what happened plus what to do next.
- Write toasts as the specific change without a trailing period and without `successfully`.
- Point empty states toward the first useful action.
- Use in-progress text with an ellipsis, such as `Deploying...` or `Saving...`.
- Use numerals for counts and avoid filler, marketing superlatives, and unnecessary `please`.

## Checklist

- Use exact Geist tokens where available.
- Keep color restrained and state-driven.
- Maintain WCAG AA contrast for body text.
- Pair color state with icon or text; never rely on color alone.
- Avoid mixing `gray-*` and `background-*` as if they were the same scale.
- Avoid more than two font weights in one view.
- Avoid decorative gradients, loud shadows, and long looping animations.

## Reference

`references/geist-light-theme.md` contains the fetched source from `https://vercel.com/design.md`, including full color, typography, spacing, radius, component, voice, and usage guidance for the light theme.
