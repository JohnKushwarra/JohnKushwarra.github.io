# Portfolio Site Design — JohnKushwarra.github.io

## Overview

A single-page personal portfolio for John Kushwarra, a sophomore AI Engineering major at Penn State (Class of 2028). The site targets AI engineering recruiters and hiring managers, communicating ambition, focus, and a clear growth trajectory.

**Deployment:** GitHub Pages — static HTML/CSS/JS, no build step, no frameworks.
**Structure:** Single `index.html` file with inline CSS and JS.

---

## Visual Direction: Dark Editorial

A premium, publication-inspired aesthetic that stands apart from typical developer portfolio templates.

### Color Palette

| Token            | Value                          | Usage                        |
|------------------|--------------------------------|------------------------------|
| `--bg`           | `#0f0f0f`                      | Page background              |
| `--text`         | `#f5f0e8`                      | Primary text (warm off-white)|
| `--accent`       | `#f7c948`                      | Amber/gold — links, labels, dots |
| `--accent-hover` | `#ff6b35`                      | Warm orange — hover states   |
| `--muted`        | `#8a8578`                      | Secondary text (warm gray)   |
| `--border`       | `rgba(245, 240, 232, 0.08)`    | Dividers, card borders       |

### Typography

| Role          | Stack                                    | Size (desktop) |
|---------------|------------------------------------------|----------------|
| Headings      | Georgia, "Times New Roman", serif        | h1: 56px, h2: 36px |
| Body / UI     | system-ui, -apple-system, sans-serif     | 16-18px        |
| Labels / Tags | system-ui, sans-serif, small caps, letter-spaced 3-4px | 11-13px |

### Spacing

- Section vertical padding: 120-160px desktop, scaling down on mobile
- Max content width: 720px, centered
- Signature detail: 3px amber gradient line at top and bottom of page

---

## Page Structure

Sectioned scroll layout — each section gets near-full breathing room. Smooth scroll between sections.

### Navigation (Fixed)

- **Left:** "JK" monogram in serif, links to top
- **Right:** "Skills · Contact" in small letter-spaced sans-serif
- Background: transparent at top, transitions to `backdrop-filter: blur(12px)` + semi-transparent dark background on scroll
- Gold underline on hover/active link state
- Mobile: same horizontal layout (no hamburger — only 2 links)
- "Projects" nav link is omitted at launch; added when first project is ready

### Section 1: Hero

Near-full-viewport height, centered content.

Content stack (top to bottom, centered):
1. Label: `AI ENGINEERING` — amber, letter-spaced sans-serif, small
2. **John Kushwarra** — serif, 56px, warm white
3. Thin horizontal rule — ~40px wide, amber
4. One-liner: "Building intelligent systems with modern AI tooling" — muted text, 18px sans-serif
5. Short paragraph (2-3 sentences): "Sophomore at Penn State studying AI Engineering. Spending 10-20 hours a week outside the classroom going deep on LLM APIs, prompt engineering, and the tooling that turns models into real products."
6. Links row: **GitHub · LinkedIn · Email** — small, letter-spaced, amber underline slides in on hover

Links:
- GitHub: https://github.com/JohnKushwarra
- LinkedIn: https://linkedin.com/in/johnkushwarra
- Email: mailto:jfk6111@psu.edu

### Section 2: Skills

Label above header: `WHAT I WORK WITH`
Header: "Skills" in serif

Three columns on desktop, stacking vertically on mobile. Each column has a subtle warm border and generous internal padding.

**Column 1 — Building With**
- Python
- Git & GitHub
- NumPy & Pandas
- Visual: solid amber dot beside each skill name (warm white text)

**Column 2 — Currently Learning**
- LLM APIs (OpenAI & Anthropic)
- Prompt Engineering
- Structured Outputs
- Function Calling / Tool Use
- Visual: pulsing amber dot (CSS animation) beside each skill name (warm white text)

**Column 3 — On My Radar**
- RAG Systems
- AI Agents
- Evaluation Frameworks
- FastAPI
- Vector Databases
- System Design
- Visual: hollow/outlined dot beside each skill name (muted gray text)

Column headers in small caps, letter-spaced, with thin amber underline.

### Section 3: Projects (Hidden at Launch)

The entire section is present in the HTML but commented out. No nav link at launch.

When activated, the section includes:
- Label: `WHAT I'M BUILDING`
- Header: "Projects" in serif
- Project cards with:
  - Project name (serif, ~24px)
  - 1-2 sentence description
  - Tech stack as small amber-tinted pill tags
  - Links: GitHub repo, live demo (if applicable)
  - Subtle warm border, slight lift on hover
- Layout: single column at narrow widths, 2-column CSS grid on desktop
- Adding a project = copying the card HTML template and uncommenting the section

### Section 4: Contact / Footer

Label: `GET IN TOUCH`
Header: "Contact" in serif

- One-liner: "Interested in working together or just want to connect?" — muted text
- Links row (same style as hero): **GitHub · LinkedIn · Email**
- Footer line: `© 2026 John Kushwarra` — muted, small
- Bottom amber gradient line mirrors the top — bookends the page

---

## Interactions & Animations

| Element                     | Animation                                      |
|-----------------------------|-------------------------------------------------|
| Page load                   | Content fades in, 0.6s ease                     |
| Nav on scroll               | Transparent → blur + dark bg transition         |
| Link hover                  | Amber underline slides in from left              |
| "Currently Learning" dots   | Subtle pulse animation (opacity/scale cycle)     |
| Project cards (when added)  | Slight translateY lift on hover                  |

All animations respect `prefers-reduced-motion: reduce` — disabled when user prefers reduced motion.

---

## Responsive Behavior

| Breakpoint    | Behavior                                          |
|---------------|---------------------------------------------------|
| Desktop >768px| 3-column skills grid, 720px centered content       |
| Mobile ≤768px | Single column stack, skills stack vertically, padding/fonts scale down |

Nav stays horizontal at all sizes (only 2 links, no hamburger).

---

## Accessibility

- Semantic HTML5: `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`
- Heading hierarchy: `<h1>` for name, `<h2>` for section titles
- `prefers-reduced-motion` media query disables all animations
- Color contrast: amber (#f7c948) on black (#0f0f0f) passes WCAG AA for large text; warm white (#f5f0e8) on black passes AAA
- Skip-to-content link for keyboard navigation
- All links have meaningful text (no "click here")
- `aria-label` on icon-only links if applicable

---

## File Structure

```
JohnKushwarra.github.io/
├── index.html          # Single file — all HTML, CSS (in <style>), JS (in <script>)
└── docs/               # Design docs (not deployed)
```

No external dependencies. No CDN links. No build step. Works on GitHub Pages as-is.

---

## Content to Finalize

- Hero paragraph copy (draft provided, can be refined)
- LinkedIn URL slug (assumed: /in/johnkushwarra — verify)
- Projects section activated when first project is ready
