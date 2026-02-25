# CLAUDE.md

## Project Overview

This is a **static HTML marketing website** for Stas Petrov, a digital marketing consultant specializing in paid advertising (PPC) for therapists and coaches in Israel. The site is hosted at `expe.co.il`.

The website is entirely in **Hebrew (RTL)** with no build system, no package manager, and no external dependencies beyond Google Fonts and the Meta (Facebook) Pixel tracking script.

---

## Repository Structure

```
my-lp/
├── images/                     # All image assets
│   ├── hero-bg-stas-rotem.jpg  # Hero section background image
│   ├── early-days-studio.jpg   # Narrative/story section image
│   ├── canada-family-victory.jpg # Success story image
│   ├── late-night-struggle.jpg # Story/narrative image
│   ├── stas.jpg                # Portrait photo (JPG)
│   ├── stas.webp               # Portrait photo (WebP, optimized)
│   └── stas-rotem-portrait.jpg # Additional portrait photo
├── index.html                  # Main landing page (paid marketing services)
├── ppc-for-therapist.html      # Specialized PPC landing page for therapists
├── thank-you.html              # Post-form-submission conversion page
├── privacy.html                # Privacy policy (מדיניות פרטיות)
├── terms.html                  # Terms and conditions (תקנון ותנאי שימוש)
├── accessibility.html          # Accessibility statement (IS 5568 / WCAG 2.0 AA)
├── cancellation.html           # Cancellation/refund policy
├── robots.txt                  # SEO crawler directives
├── sitemap.xml                 # XML sitemap for expe.co.il
├── favicon.ico                 # Browser favicon
├── .gitignore                  # Git ignore rules
└── lead-magnet-draft.md        # Hebrew lead magnet content draft (not published)
```

---

## Technology Stack

- **Markup:** HTML5
- **Styling:** CSS3 — embedded in each `<style>` block per page (no external stylesheet)
- **JavaScript:** Inline only — Meta Pixel tracking snippets; no framework or libraries
- **Fonts:** Google Fonts (Open Sans), loaded via `<link>` tags
- **Tracking:** Meta Pixel ID `2379738449136585` on all pages
- **Language/Direction:** Hebrew (`lang="he"`, `dir="rtl"`)
- **No build tooling:** No Webpack, Vite, npm, or any package manager

---

## HTML Page Conventions

All pages share a consistent structure and conventions:

### Document Setup
```html
<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <!-- Meta Pixel tracking code (inline) -->
  <!-- Facebook domain verification meta tag -->
  <!-- Open Graph / SEO meta tags -->
  <title>...</title>
  <link rel="icon" ...>
  <link href="https://fonts.googleapis.com/css2?family=Open+Sans..." rel="stylesheet">
  <style>/* All page CSS embedded here */</style>
</head>
```

### RTL Layout
- All content is right-to-left. Text flows right-to-left, margins/paddings follow RTL conventions.
- Use CSS logical properties or RTL-aware values when adding new styles.
- Do not introduce LTR-only patterns (e.g., `text-align: left` without RTL override).

### CSS Architecture
- **All CSS is embedded** in `<style>` tags within each HTML file — there is no shared stylesheet.
- CSS custom properties (variables) are defined in `:root` for colors, font sizes, and spacing.
- Responsive typography uses `clamp()` for fluid scaling.
- Layout uses Flexbox extensively; no CSS Grid.
- Breakpoints target mobile (`max-width: 768px`) and occasionally tablet (`max-width: 1024px`).

### Meta Pixel
Every page includes the Meta Pixel base code in the `<head>`. The `thank-you.html` page fires a `Lead` event:
```javascript
fbq('track', 'Lead');
```
Do not remove or modify the Pixel code without confirming with the site owner.

### Forms
Forms submit to a **Google Apps Script** URL (embedded in the HTML action attribute). Do not change form endpoints without confirming the correct Apps Script URL.

---

## Key Identifiers (Do Not Change Without Approval)

| Identifier | Value | Location |
|-----------|-------|----------|
| Meta Pixel ID | `2379738449136585` | All pages, `<head>` |
| Facebook domain verification | Meta tag in `<head>` | `index.html` |
| Sitemap URL | `https://expe.co.il/sitemap.xml` | `robots.txt` |
| Canonical domain | `https://expe.co.il` | `sitemap.xml`, meta tags |

---

## SEO Files

### robots.txt
```
User-agent: *
Allow: /
Sitemap: https://expe.co.il/sitemap.xml
```

### sitemap.xml
Contains 5 URLs with `lastmod` dates and change frequencies. When adding a new public page, add a corresponding `<url>` entry in `sitemap.xml`.

---

## Image Assets

Images are stored in the `images/` directory. All images are referenced with relative paths (e.g., `src="images/stas.jpg"`).

- Prefer **WebP** format for new images where browser support allows; a `.jpg` fallback is included for `stas` (both `stas.jpg` and `stas.webp` exist).
- Large images (`hero-bg-stas-rotem.jpg` at 1.3 MB) are used as CSS background images; optimize before adding new large assets.
- No image CDN or optimization pipeline is in place — images are served directly from the repository.
- When adding new images, place them in the `images/` directory.

---

## Development Workflow

### No Build Step
This project has no build process. Edit HTML files directly and they are ready to deploy. There is no `npm install`, `npm run build`, or compilation step.

### Making Changes
1. Edit the relevant `.html` file directly.
2. Test by opening the file in a browser locally.
3. Commit and push to the appropriate branch.

### Git Branches
- `master` — main development branch (local)
- `main` — remote default branch
- Feature branches follow the pattern: `claude/<description>-<id>`

### No Automated Tests
There are no unit tests, integration tests, or end-to-end tests. Visual/manual browser testing is the only verification method.

### No CI/CD
There is no GitHub Actions, GitLab CI, or any automated pipeline. Deployment is manual.

---

## Content Guidelines

- All user-facing content is in **Hebrew**. Keep all copy in Hebrew.
- The tone is warm, direct, and professional — targeting therapists and coaches as the primary audience.
- The business is "Better Experience" / "בטר אקספיריאנס" operated by Stas Petrov.
- Contact/CTA links use WhatsApp (`wa.me/...`) and the lead capture form.

---

## Accessibility

The site includes an accessibility statement (`accessibility.html`) claiming compliance with **Israeli Standard IS 5568** and **WCAG 2.0 Level AA**. When making UI changes:
- Maintain sufficient color contrast ratios.
- Keep all interactive elements keyboard-accessible.
- Preserve `alt` attributes on images.
- Do not remove ARIA attributes if any exist.

---

## What This Project Does NOT Have

- No JavaScript framework (React, Vue, etc.)
- No CSS preprocessor (Sass, Less)
- No package manager (npm, yarn, pnpm)
- No build tool (Webpack, Vite, Parcel)
- No test suite
- No linter or formatter config
- No CI/CD pipeline
- No Docker or containerization
- No environment variables or `.env` files
- No shared/external CSS stylesheet
- No backend — purely static files
