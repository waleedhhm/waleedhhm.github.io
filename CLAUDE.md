# Waleed's Portfolio — Project Notes

## What this is

A personal portfolio site for Waleed, MA UX Design student at UAL.
Built with Astro, deployed to GitHub Pages.

The tone is editorial and restrained — not a flashy dev portfolio.
Think: well-considered, quiet, confident.

---

## Tech stack

- **Framework:** Astro (v6)
- **Styling:** Plain CSS inside `.astro` files (no Tailwind, no CSS modules)
- **Fonts:** Inter via Google Fonts (weights 300, 400, 500, 600)
- **Deployment:** GitHub Pages via Astro's static build

---

## What's been built

### Homepage (`src/pages/index.astro`)

Two-panel layout with a scroll-triggered transition:

**Panel 1 — Hero**
- Name in top-left corner ("Waleed")
- Large "Hello." heading with tagline (UAL intro)
- Video invite placeholder (marked "coming soon")
- Scroll hint arrow

**Panel 2 — Projects**
- Appears as you scroll down (threshold: 70px)
- Two entries: "UAL" and "Self-initiated"
- Both currently link to `#` (placeholder — case study pages not built yet)

**Background scene**
- Fixed SVG landscape: sun, mountains, river, trees
- Two atmospheric states that transition on scroll:
  - **Day** (hero panel): steel-blue sky, green ground, pale mountains
  - **Sunset** (projects panel): deep plum sky, ember tones, dark silhouettes
- Parallax shift on state change (nearer layers move more)
- Smooth CSS transitions throughout (0.65s ease)

### Layout (`src/layouts/Layout.astro`)
- Standard HTML shell
- Inter font loaded
- Global CSS reset

---

## Folder structure

```
Portfolio/
  src/
    assets/
      case-studies/     ← optimised images (JPG, PNG, WebP)
    layouts/
      Layout.astro
    pages/
      index.astro
  public/
    videos/             ← video files (MP4 etc.) — not processed, served as-is
    favicon.svg
    favicon.ico
  CLAUDE.md             ← this file
```

---

## Media workflow

### Images → `src/assets/case-studies/`

Astro optimises images placed here (converts to WebP, prevents layout shift).
Use the built-in `<Image />` component to reference them.

**To add an image:**
1. Drop the file into `src/assets/case-studies/`
2. Name it with lowercase and hyphens: `ual-hero.jpg`, not `UAL Hero FINAL (2).jpg`
3. Tell Claude what it's for and where it should appear
4. Claude writes the code

**Example usage (Claude handles this):**
```astro
---
import { Image } from 'astro:assets';
import hero from '../../assets/case-studies/ual-hero.jpg';
---
<Image src={hero} alt="UAL project hero" />
```

### Videos → `public/videos/`

Videos can't be optimised by Astro so they live in `public/` and are served directly.

**To add a video:**
1. Drop the `.mp4` into `public/videos/`
2. Tell Claude what it's for
3. Claude writes the code

**Example usage (Claude handles this):**
```html
<video autoplay muted loop playsinline>
  <source src="/videos/intro.mp4" type="video/mp4" />
</video>
```

---

## To-do

### Immediate
- [ ] Build UAL case study page (`src/pages/ual/index.astro` or similar)
- [ ] Build Self-initiated case study page
- [ ] Wire up the two project entry links on the homepage
- [ ] Record and add intro video (currently placeholder)

### Design decisions still open
- [ ] What does a case study page look like? (layout, sections, image treatment)
- [ ] Does clicking a project entry open a new page or expand inline?
- [ ] Is there a separate "about" page or is it woven into the homepage?
- [ ] Mobile responsiveness pass (not done yet beyond basic breakpoints)

### Nice to have later
- [ ] Page transitions between routes
- [ ] OG image / social metadata
- [ ] Favicon update (currently Astro default)

---

## Working style notes

- Waleed is not a developer — Claude handles all code
- Waleed drops media files into the right folder and describes what they're for
- Claude wires everything up
- Keep the aesthetic minimal and editorial — no decorative flourishes unless asked
- CSS lives in the `.astro` file it belongs to (not separate stylesheets)
- No component libraries, no Tailwind — plain CSS only
