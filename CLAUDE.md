# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a portfolio website built with **SvelteKit** using **Svelte 5** (with runes) and **Tailwind CSS v4**. The project uses TypeScript with strict mode enabled.

## Technology Stack

- **Framework**: SvelteKit v2 with Svelte 5.39+
- **Styling**: Tailwind CSS v4.1+ (modern CSS-first approach)
- **Language**: TypeScript (strict mode)
- **Package Manager**: Uses Bun (bun.lock present)
- **Adapter**: Auto-adapter for deployment

## Development Commands

```bash
# Start development server
bun run dev

# Start dev server and open in browser
bun run dev -- --open

# Build for production
bun run build

# Preview production build
bun run preview

# Type checking
bun run check

# Type checking in watch mode
bun run check:watch

# Format code (Prettier)
bun run format

# Lint (Prettier check + ESLint)
bun run lint
```

## Project Structure

```
src/
├── app.css              # Tailwind CSS imports
├── app.html             # HTML template
├── app.d.ts             # TypeScript declarations
├── lib/
│   ├── assets/          # Static assets (favicon, etc.)
│   └── index.ts         # Library exports
└── routes/
    ├── +layout.svelte   # Root layout with global CSS import
    └── +page.svelte     # Home page
```

## Framework-Specific Details

### Svelte 5 Runes
This project uses Svelte 5 with the modern runes API:
- Use `$props()` for component props (see `+layout.svelte:5`)
- Use `{@render}` for rendering children/snippets (see `+layout.svelte:12`)
- Prefer runes over legacy reactive declarations

### Tailwind CSS v4
- Uses the modern CSS-first approach via `@import 'tailwindcss'`
- Configured as a Vite plugin in `vite.config.ts`
- Typography plugin enabled via `@plugin '@tailwindcss/typography'`
- No `tailwind.config.js` file needed (v4 convention)

### SvelteKit Conventions
- File-based routing in `src/routes/`
- `+page.svelte` for page components
- `+layout.svelte` for layout components
- `$lib` alias maps to `src/lib/`
- Path aliases handled by SvelteKit configuration

## Code Quality Standards

### TypeScript
- Strict mode enabled (`strict: true`)
- Check JS files (`checkJs: true`)
- Module resolution: bundler
- ESLint rule: `no-undef` is disabled (recommended for TypeScript projects)

### Linting & Formatting
- ESLint with TypeScript and Svelte support
- Prettier for formatting with Svelte and Tailwind plugins
- ESLint configured to respect `.gitignore`
- Run `bun run lint` before committing

## Important Notes

- This is a **Svelte 5** project - use runes syntax, not legacy reactive statements
- Tailwind v4 uses a different configuration approach than v3
- The project uses **Bun** as the package manager (not npm/yarn/pnpm)
- Adapter is set to auto-detect deployment platform
