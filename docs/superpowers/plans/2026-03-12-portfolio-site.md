# Portfolio Site Implementation Plan

> **For agentic workers:** REQUIRED: Use superpowers:subagent-driven-development (if subagents available) or superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking. Use @frontend-design skill when writing HTML/CSS.

**Goal:** Build a single-page portfolio site for John Kushwarra (JohnKushwarra.github.io) with a dark editorial aesthetic.

**Architecture:** Single `index.html` file with inline `<style>` and `<script>`. No frameworks, no build step, no external dependencies. Sectioned scroll layout: Hero → Skills → Projects (hidden) → Contact.

**Tech Stack:** HTML5, CSS3 (custom properties, grid, flexbox, animations), vanilla JS (scroll listener for nav).

**Spec:** `docs/superpowers/specs/2026-03-12-portfolio-site-design.md`

---

## Chunk 1: Foundation and All Sections

### Task 1: Initialize repo and create index.html with CSS foundation

**Files:**
- Create: `index.html`
- Create: `.gitignore`

- [ ] **Step 1: Initialize git repo**

```bash
cd C:\Users\jfkus\desktop\JohnKushwarra.github.io
git init
```

- [ ] **Step 2: Create .gitignore**

```
.superpowers/
.DS_Store
```

- [ ] **Step 3: Create index.html with DOCTYPE, meta tags, CSS custom properties, and base styles**

Write the full `<!DOCTYPE html>` document shell with:
- `<html lang="en">`
- `<meta charset="UTF-8">`, viewport meta, title "John Kushwarra — AI Engineer"
- `<meta name="description" content="John Kushwarra — Sophomore AI Engineering major at Penn State. Building intelligent systems with modern AI tooling.">`
- Open Graph meta tags (title, description, type)
- `<style>` block containing:
  - CSS reset (box-sizing, margin/padding reset)
  - CSS custom properties on `:root` matching the spec palette:
    - `--bg: #0f0f0f`
    - `--text: #f5f0e8`
    - `--accent: #f7c948`
    - `--accent-hover: #ff6b35`
    - `--muted: #8a8578`
    - `--border: rgba(245, 240, 232, 0.08)`
  - `html` — `scroll-behavior: smooth; background: var(--bg); color: var(--text)`
  - `body` — font stack: `system-ui, -apple-system, "Segoe UI", sans-serif`, line-height 1.6, font-size 17px
  - Serif font variable: `--serif: Georgia, "Times New Roman", serif`
  - `.container` — `max-width: 720px; margin: 0 auto; padding: 0 24px`
  - Section base — `padding: 140px 0` desktop
  - `.label` — small caps, letter-spacing 3px, font-size 12px, color var(--accent), sans-serif, margin-bottom 16px
  - `h1` — font-family var(--serif), 56px, line-height 1.1, color var(--text)
  - `h2` — font-family var(--serif), 36px, margin-bottom 48px, color var(--text)
  - Responsive media query (max-width 768px): reduce section padding to 80px, h1 to 40px, h2 to 28px
  - Amber gradient line: `body::before` — fixed top, 3px height, full width, `linear-gradient(90deg, var(--accent), var(--accent-hover), var(--accent))`, z-index 1000
  - Amber gradient line bottom: `body::after` — same but fixed bottom
  - Page load fade-in: `@keyframes fadeIn { from { opacity: 0; transform: translateY(12px); } to { opacity: 1; transform: translateY(0); } }` and `main { animation: fadeIn 0.6s ease both; }`
- Empty `<body>` with placeholder for nav, `<main id="main">`, placeholder for footer

- [ ] **Step 4: Verify file opens in browser**

Open `index.html` in browser. Should see: black page with amber gradient lines at top and bottom.

- [ ] **Step 5: Commit**

```bash
git add index.html .gitignore
git commit -m "feat: initialize portfolio with CSS foundation and design tokens"
```

---

### Task 2: Navigation

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add nav HTML**

Inside `<body>`, before `<main>`, add:

```html
<header class="nav" id="nav">
  <nav class="container nav-inner">
    <a href="#" class="nav-logo" aria-label="Back to top">JK</a>
    <div class="nav-links">
      <a href="#skills">Skills</a>
      <a href="#contact">Contact</a>
    </div>
  </nav>
</header>
```

- [ ] **Step 2: Add nav CSS**

```css
.nav {
  position: fixed;
  top: 3px; /* below amber line */
  left: 0;
  right: 0;
  z-index: 100;
  padding: 20px 0;
  transition: background 0.3s ease, backdrop-filter 0.3s ease;
}
.nav.scrolled {
  background: rgba(15, 15, 15, 0.85);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
}
.nav-inner {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.nav-logo {
  font-family: var(--serif);
  font-size: 20px;
  color: var(--text);
  text-decoration: none;
}
.nav-links {
  display: flex;
  gap: 32px;
}
.nav-links a {
  color: var(--muted);
  text-decoration: none;
  font-size: 13px;
  letter-spacing: 2px;
  text-transform: uppercase;
  position: relative;
}
.nav-links a::after {
  content: '';
  position: absolute;
  bottom: -4px;
  left: 0;
  width: 0;
  height: 1px;
  background: var(--accent);
  transition: width 0.3s ease;
}
.nav-links a:hover::after,
.nav-links a:focus::after {
  width: 100%;
}
.nav-links a:hover,
.nav-links a:focus {
  color: var(--text);
}
```

- [ ] **Step 3: Add nav scroll JS**

At the bottom of `<body>`, add `<script>`:

```javascript
const nav = document.getElementById('nav');
window.addEventListener('scroll', () => {
  nav.classList.toggle('scrolled', window.scrollY > 40);
});
```

- [ ] **Step 4: Verify** — nav visible, transparent initially, blurs on scroll.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: add fixed navigation with scroll blur effect"
```

---

### Task 3: Hero Section

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add hero HTML**

Inside `<main>`, add:

```html
<section class="hero" id="hero">
  <div class="container hero-content">
    <p class="label">AI Engineering</p>
    <h1>John Kushwarra</h1>
    <div class="hero-rule" aria-hidden="true"></div>
    <p class="hero-tagline">Building intelligent systems with modern AI tooling</p>
    <p class="hero-bio">Sophomore at Penn State studying AI Engineering. Spending 10–20 hours a week outside the classroom going deep on LLM APIs, prompt engineering, and the tooling that turns models into real products.</p>
    <div class="hero-links">
      <a href="https://github.com/JohnKushwarra" target="_blank" rel="noopener noreferrer">GitHub</a>
      <span class="hero-links-sep" aria-hidden="true">·</span>
      <a href="https://linkedin.com/in/johnkushwarra" target="_blank" rel="noopener noreferrer">LinkedIn</a>
      <span class="hero-links-sep" aria-hidden="true">·</span>
      <a href="mailto:jfk6111@psu.edu">Email</a>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add hero CSS**

```css
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding-top: 80px; /* clear nav */
}
.hero-content {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.hero-rule {
  width: 40px;
  height: 2px;
  background: var(--accent);
  margin: 24px 0;
}
.hero-tagline {
  font-size: 18px;
  color: var(--muted);
  margin-bottom: 16px;
}
.hero-bio {
  font-size: 16px;
  color: var(--muted);
  max-width: 520px;
  line-height: 1.7;
  margin-bottom: 32px;
}
.hero-links {
  display: flex;
  align-items: center;
  gap: 12px;
}
.hero-links a {
  color: var(--text);
  text-decoration: none;
  font-size: 13px;
  letter-spacing: 2px;
  text-transform: uppercase;
  position: relative;
}
.hero-links a::after {
  content: '';
  position: absolute;
  bottom: -3px;
  left: 0;
  width: 0;
  height: 1px;
  background: var(--accent);
  transition: width 0.3s ease;
}
.hero-links a:hover::after,
.hero-links a:focus::after {
  width: 100%;
}
.hero-links-sep {
  color: var(--muted);
  font-size: 14px;
}
```

- [ ] **Step 3: Verify** — hero fills viewport, centered content, links have hover animation.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add hero section with bio and social links"
```

---

### Task 4: Skills Section

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add skills HTML**

After the hero section inside `<main>`:

```html
<section class="section" id="skills">
  <div class="container">
    <p class="label">What I Work With</p>
    <h2>Skills</h2>
    <div class="skills-grid">
      <div class="skills-col">
        <h3 class="skills-col-header">Building With</h3>
        <ul class="skills-list">
          <li class="skill-item skill-current"><span class="skill-dot solid" aria-hidden="true"></span>Python</li>
          <li class="skill-item skill-current"><span class="skill-dot solid" aria-hidden="true"></span>Git &amp; GitHub</li>
          <li class="skill-item skill-current"><span class="skill-dot solid" aria-hidden="true"></span>NumPy &amp; Pandas</li>
        </ul>
      </div>
      <div class="skills-col">
        <h3 class="skills-col-header">Currently Learning</h3>
        <ul class="skills-list">
          <li class="skill-item skill-learning"><span class="skill-dot pulse" aria-hidden="true"></span>LLM APIs (OpenAI &amp; Anthropic)</li>
          <li class="skill-item skill-learning"><span class="skill-dot pulse" aria-hidden="true"></span>Prompt Engineering</li>
          <li class="skill-item skill-learning"><span class="skill-dot pulse" aria-hidden="true"></span>Structured Outputs</li>
          <li class="skill-item skill-learning"><span class="skill-dot pulse" aria-hidden="true"></span>Function Calling / Tool Use</li>
        </ul>
      </div>
      <div class="skills-col">
        <h3 class="skills-col-header">On My Radar</h3>
        <ul class="skills-list">
          <li class="skill-item skill-planned"><span class="skill-dot hollow" aria-hidden="true"></span>RAG Systems</li>
          <li class="skill-item skill-planned"><span class="skill-dot hollow" aria-hidden="true"></span>AI Agents</li>
          <li class="skill-item skill-planned"><span class="skill-dot hollow" aria-hidden="true"></span>Evaluation Frameworks</li>
          <li class="skill-item skill-planned"><span class="skill-dot hollow" aria-hidden="true"></span>FastAPI</li>
          <li class="skill-item skill-planned"><span class="skill-dot hollow" aria-hidden="true"></span>Vector Databases</li>
          <li class="skill-item skill-planned"><span class="skill-dot hollow" aria-hidden="true"></span>System Design</li>
        </ul>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add skills CSS**

```css
.skills-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 32px;
}
.skills-col {
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 32px 28px;
}
.skills-col-header {
  font-family: system-ui, sans-serif;
  font-size: 12px;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 24px;
  padding-bottom: 12px;
  border-bottom: 1px solid var(--accent);
  font-weight: 500;
}
.skills-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 14px;
}
.skill-item {
  display: flex;
  align-items: center;
  gap: 12px;
  font-size: 15px;
}
.skill-current { color: var(--text); }
.skill-learning { color: var(--text); }
.skill-planned { color: var(--muted); }
.skill-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  flex-shrink: 0;
}
.skill-dot.solid {
  background: var(--accent);
}
.skill-dot.pulse {
  background: var(--accent);
  animation: pulse 2s ease-in-out infinite;
}
.skill-dot.hollow {
  background: transparent;
  border: 1.5px solid var(--muted);
}
@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.5; transform: scale(0.85); }
}
```

- [ ] **Step 3: Add responsive override for skills grid**

Inside the `@media (max-width: 768px)` block:

```css
.skills-grid { grid-template-columns: 1fr; }
```

- [ ] **Step 4: Verify** — three columns on desktop, stacked on narrow window. Dots animate for "learning" column.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: add skills section with three-tier progression"
```

---

### Task 5: Projects Section (Commented Out)

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add commented-out projects HTML**

After skills section, inside `<main>`, add a comment block:

```html
<!--
=== PROJECTS SECTION ===
Uncomment this section and add "Projects" to nav when first project is ready.
Also add to nav: <a href="#projects">Projects</a>

<section class="section" id="projects">
  <div class="container">
    <p class="label">What I'm Building</p>
    <h2>Projects</h2>
    <div class="projects-grid">

      <article class="project-card">
        <h3 class="project-title">Project Name</h3>
        <p class="project-desc">One or two sentences about what this project does and why it matters.</p>
        <div class="project-tags">
          <span class="project-tag">Python</span>
          <span class="project-tag">OpenAI API</span>
        </div>
        <div class="project-links">
          <a href="#" target="_blank" rel="noopener noreferrer">GitHub</a>
          <a href="#" target="_blank" rel="noopener noreferrer">Live Demo</a>
        </div>
      </article>

    </div>
  </div>
</section>
=== END PROJECTS SECTION ===
-->
```

- [ ] **Step 2: Add projects CSS (active, not commented out — ready when section is uncommented)**

```css
.projects-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 24px;
}
@media (min-width: 769px) {
  .projects-grid { grid-template-columns: repeat(2, 1fr); }
}
.project-card {
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 32px 28px;
  transition: transform 0.2s ease, border-color 0.2s ease;
}
.project-card:hover {
  transform: translateY(-3px);
  border-color: rgba(245, 240, 232, 0.15);
}
.project-title {
  font-family: var(--serif);
  font-size: 24px;
  margin-bottom: 12px;
  color: var(--text);
}
.project-desc {
  font-size: 15px;
  color: var(--muted);
  line-height: 1.6;
  margin-bottom: 16px;
}
.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 20px;
}
.project-tag {
  font-size: 11px;
  letter-spacing: 1px;
  text-transform: uppercase;
  padding: 4px 12px;
  border-radius: 20px;
  background: rgba(247, 201, 72, 0.08);
  border: 1px solid rgba(247, 201, 72, 0.2);
  color: var(--accent);
}
.project-links {
  display: flex;
  gap: 16px;
}
.project-links a {
  color: var(--text);
  text-decoration: none;
  font-size: 13px;
  letter-spacing: 1px;
  text-transform: uppercase;
  position: relative;
}
.project-links a::after {
  content: '';
  position: absolute;
  bottom: -3px;
  left: 0;
  width: 0;
  height: 1px;
  background: var(--accent);
  transition: width 0.3s ease;
}
.project-links a:hover::after,
.project-links a:focus::after {
  width: 100%;
}
```

- [ ] **Step 3: Verify** — projects section is NOT visible on page. CSS loads without errors.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add projects section template (commented out for launch)"
```

---

### Task 6: Contact Section and Footer

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add contact HTML**

After the projects comment block, still inside `<main>`:

```html
<section class="section" id="contact">
  <div class="container contact-content">
    <p class="label">Get In Touch</p>
    <h2>Contact</h2>
    <p class="contact-text">Interested in working together or just want to connect?</p>
    <div class="hero-links">
      <a href="https://github.com/JohnKushwarra" target="_blank" rel="noopener noreferrer">GitHub</a>
      <span class="hero-links-sep" aria-hidden="true">·</span>
      <a href="https://linkedin.com/in/johnkushwarra" target="_blank" rel="noopener noreferrer">LinkedIn</a>
      <span class="hero-links-sep" aria-hidden="true">·</span>
      <a href="mailto:jfk6111@psu.edu">Email</a>
    </div>
  </div>
</section>
```

After `</main>`, add:

```html
<footer class="footer">
  <div class="container">
    <p class="footer-text">&copy; 2026 John Kushwarra</p>
  </div>
</footer>
```

- [ ] **Step 2: Add contact/footer CSS**

```css
.contact-content {
  text-align: center;
}
.contact-text {
  color: var(--muted);
  font-size: 18px;
  margin-bottom: 28px;
}
.footer {
  padding: 40px 0 60px; /* extra bottom for amber line clearance */
  text-align: center;
}
.footer-text {
  color: var(--muted);
  font-size: 13px;
  letter-spacing: 1px;
}
```

- [ ] **Step 3: Verify** — contact section centered with links, footer at bottom with copyright.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add contact section and footer"
```

---

### Task 7: Final Polish and Accessibility

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add skip-to-content link**

As the very first child of `<body>`:

```html
<a href="#main" class="skip-link">Skip to main content</a>
```

CSS (if not already added in Task 1):

```css
.skip-link {
  position: absolute;
  top: -100%;
  left: 16px;
  background: var(--accent);
  color: var(--bg);
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 14px;
  z-index: 1001;
  text-decoration: none;
}
.skip-link:focus {
  top: 8px;
}
```

- [ ] **Step 2: Ensure prefers-reduced-motion covers all animations**

Verify the media query disables:
- `fadeIn` on main
- `pulse` on skill dots
- `scroll-behavior: smooth`
- All `transition` properties

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

- [ ] **Step 3: Test keyboard navigation**

Tab through the entire page. Verify:
- Skip link appears on first Tab
- All links are focusable in logical order
- Focus styles are visible (the `::after` underline works on focus too)

- [ ] **Step 4: Test responsive layout**

Resize browser to ~375px width. Verify:
- Nav stays horizontal
- Hero text is readable, not overflowing
- Skills grid stacks to single column
- Contact section centered
- No horizontal scroll

- [ ] **Step 5: Final commit**

```bash
git add index.html
git commit -m "feat: add accessibility features and final polish"
```

---

## Summary

| Task | What it builds | Commit |
|------|---------------|--------|
| 1 | CSS foundation, design tokens, file structure | `feat: initialize portfolio...` |
| 2 | Fixed nav with scroll blur | `feat: add fixed navigation...` |
| 3 | Hero section | `feat: add hero section...` |
| 4 | Skills three-column grid | `feat: add skills section...` |
| 5 | Projects template (hidden) | `feat: add projects section template...` |
| 6 | Contact + footer | `feat: add contact section...` |
| 7 | Accessibility + polish | `feat: add accessibility features...` |
