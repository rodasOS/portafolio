# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev        # Start dev server (localhost:4321)
npm run build      # Type-check (astro check) then build for production
npm run preview    # Preview the production build locally
```

The `build` command runs `astro check` before building — fix TypeScript errors before the build will succeed.

## Architecture

**Astro 5** static site with **Tailwind CSS** for styling. Single-page portfolio in Spanish, with anchor-based navigation (no client-side routing).

### Structure

```
src/
  pages/index.astro          # Entry point — composes all sections
  layouts/Layout.astro       # HTML shell, accepts `title` prop; sets Onest font globally
  components/
    Header.astro             # Sticky nav with anchor links
    Presentation.astro       # Hero section with avatar and intro text
    Proyects.astro           # Contains three <section> blocks: experience, projects, about
```

All portfolio content lives in components, not pages. Adding a new section means editing `Proyects.astro` and adding the anchor link in `Header.astro`.

### Styling conventions

- Utility-first Tailwind — no custom CSS files
- `dark:` prefix variants throughout; dark mode is set globally via `color-scheme: dark`
- Responsive breakpoints: `md:`, `lg:`, `max-sm:` (mobile-first)
- Inline SVGs for icons (Tabler Icons source)
- Custom Tailwind animation via arbitrary values: `animate-[spin_2s_linear_infinite]`

### TypeScript

`tsconfig.json` extends `astro/tsconfigs/strict`. All components are `.astro` files; props are typed via the `interface Props` / `const { ... } = Astro.props` pattern in the component frontmatter.