# tailwindcss-v4 — AI Agent Skill

An AI agent skill that enforces correct **Tailwind CSS v4** usage, especially in Next.js projects. Drop `SKILL.md` into your skills folder and agents will stop generating v3 patterns, unnecessary arbitrary values, and broken dark mode configs.

## What it enforces

| Rule | What it covers |
|------|---------------|
| **1. Always v4** | Install commands, `@import "tailwindcss"`, `@theme {}`, PostCSS for Next.js |
| **2. No arbitrary values** | Opacity modifiers, spacing scale, aspect ratio, fonts, color names, CSS variables |
| **3. Canonical classes** | Shorthand collapsing (`w-5 h-5` → `size-5`), sign placement, renamed scale utilities |
| **4. Dark mode** | `@custom-variant` strategies, semantic token flipping, `next-themes` integration |
| **5. Custom utilities** | `@utility` over `@layer utilities`, `@apply` rules, `@reference` for scoped styles |
| **6. `cn()` pattern** | `clsx` + `tailwind-merge` setup, component `className` prop convention |
| **7. Variant order** | `responsive:dark:state:utility` — never `hover:md:` |
| **8. Next.js setup** | PostCSS, `tw-animate-css`, `@source`, complete `globals.css` template |
| **9. Prettier plugin** | `tailwindStylesheet` entrypoint required for v4 |

## Quick examples

```tsx
// ❌ AI generates this
border-black/[.08]   w-[16px]   aspect-[16/9]   bg-[--brand]   hover:md:flex

// ✅ Skill enforces this
border-black/8       w-4        aspect-16/9      bg-(--brand)   md:hover:flex
```

```tsx
// ❌ AI generates this (v3)
@tailwind base;
tailwind.config.js  →  darkMode: 'class'
shadow              →  (wrong — was 3px ring in v3)
ring                →  (wrong — was 3px in v3)

// ✅ Skill enforces this (v4)
@import "tailwindcss"
@custom-variant dark (&:where(.dark, .dark *))   in globals.css
shadow-sm
ring-3
```

## Installation

Copy `SKILL.md` into your agent's skills directory. The skill description in the frontmatter is used by the agent to decide when to load it — it triggers on `className=`, `class=`, `@apply`, `@utility`, `dark mode`, `cn()`, `twMerge`, or any Tailwind pattern.

## Versions covered

- Tailwind CSS **v4.2.4** (latest as of May 2026)
- `@tailwindcss/postcss` for Next.js
- `@tailwindcss/vite` for Vite
- `prettier-plugin-tailwindcss` with v4 `tailwindStylesheet` option
- `tw-animate-css` (replaces deprecated `tailwindcss-animate`)
- `tailwind-merge` + `clsx` for `cn()` pattern

## Official docs

- https://tailwindcss.com/docs
- https://tailwindcss.com/docs/upgrade-guide
- https://tailwindcss.com/docs/dark-mode
- https://tailwindcss.com/docs/adding-custom-styles
- https://tailwindcss.com/docs/compatibility
