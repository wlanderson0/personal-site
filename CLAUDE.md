# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal portfolio website for William L. Anderson built with Astro 5. The site is statically generated and deployed to wlanderson.com. It's a single-page application focused on presenting research, education, leadership, policy work, and personal information.

## Development Commands

```bash
npm run dev        # Start dev server at localhost:4321
npm run build      # Build production site to ./dist/
npm run preview    # Preview production build locally
npm run astro ...  # Run Astro CLI commands (e.g., astro check)
```

## Architecture

### Framework: Astro

- **Static Site Generation**: The entire site is pre-rendered at build time
- **No client-side framework**: Uses vanilla JavaScript for interactivity
- **TypeScript**: Configured with strict mode (`astro/tsconfigs/strict`)

### Project Structure

```
src/
├── layouts/
│   └── Layout.astro          # Base layout (currently unused - see note below)
├── pages/
│   └── index.astro           # Main page (self-contained, includes its own layout)
├── components/               # Currently empty
├── styles/
│   └── global.css           # All CSS (variables, navbar, sections, responsive)
├── assets/                  # Images and static assets (favicons, profile pic, etc.)
public/
└── resume.pdf               # Static file served directly
```

### Important Architectural Notes

1. **Single-Page Design**: The entire site is contained in `src/pages/index.astro`. This file is self-contained and does not use the Layout component in `src/layouts/Layout.astro`.

2. **Inline Structure**: `index.astro` includes:
   - All HTML structure
   - Complete navbar with mobile menu
   - All content sections (hero, research, education, leadership, policy-work, talks, awards, mentors, personal)
   - All JavaScript for email obfuscation and mobile menu functionality
   - Imports for global.css and all assets

3. **CSS Architecture**:
   - All styles are in `src/styles/global.css`
   - Uses CSS custom properties (`:root` variables) for theming
   - Mobile-first responsive design with breakpoints at 800px and 480px
   - Additional brand name breakpoint at 950px (switches to short name)
   - Fixed navigation bar with blur backdrop effect

4. **Asset Handling**: Astro's built-in image optimization is used via `astro:assets` and the `Image` component

5. **JavaScript Functionality**:
   - Email obfuscation: Constructs email from parts to avoid scraping
   - Mobile menu toggle: Handles hamburger menu on smaller screens
   - Click-outside-to-close: Mobile menu closes when clicking outside

### Deployment Configuration

- `site` is set to `https://wlanderson.com` in `astro.config.mjs`
- Build output goes to `./dist/`
- Git repository is clean with recent commits related to talks and resume updates

## Key Design Patterns

1. **Email Protection**: Email address is split into parts and assembled via JavaScript to prevent scraper bots
2. **Responsive Navigation**: Desktop shows full links, mobile shows hamburger menu
3. **Progressive Enhancement**: `<noscript>` fallback for email display
4. **TypeScript in Astro**: Inline TypeScript is used in the mobile menu event listener (type assertion for `event.target as Node`)

## Styling System

CSS variables defined in `:root`:
- `--primary-color`: #526e8e (muted blue)
- `--bg-color`: #fafafa (off-white)
- `--text-color`: #333333
- `--accent-color`: #e6e6e6
- `--transition`: all 0.3s ease
- `--nav-height`: 70px

Typography: Georgia, 'Times New Roman', serif

## Content Sections

The site includes these main sections (in order):
1. Hero (profile pic, name, email, intro)
2. Research
3. Education
4. Leadership & Involvement
5. Policy Work
6. Talks
7. Awards & Fellowships
8. Mentorship Acknowledgements
9. Personal

Each section follows a consistent pattern with h2 headings, intro paragraph, and bulleted lists.
