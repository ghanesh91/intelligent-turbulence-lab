# CLAUDE.md — Intelligent Turbulence Lab Website
## Project: https://github.com/ghanesh91/intelligent-turbulence-lab
## Live site: https://ghanesh91.github.io/intelligent-turbulence-lab/

---

## Overview

This is the static website for the **Intelligent Turbulence Lab (ITL)** at the Department of Mechanical Engineering, Indian Institute of Science (IISc), Bangalore. PI: **Dr. Ghanesh Narasimhan**, Assistant Professor.

The site is a **single-page HTML application** (`index.html`) with all CSS and JS inline — no build system, no frameworks, no npm. It deploys via GitHub Pages from the `main` branch.

---

## Repository Structure

```
intelligent-turbulence-lab/
├── index.html          # Main website (all CSS + JS inline)
├── CLAUDE.md           # This file — instructions for Claude Code
├── assets/
│   ├── images/         # Photos: profile pic, lab shots, visualizations
│   │   └── GN_profile.jpg   # PI profile photo (replace placeholder)
│   └── videos/         # Optional: simulation mp4s for hero/research sections
├── data/
│   ├── publications.json    # Structured publication data
│   ├── team.json            # Team member data
│   └── research.json        # Research area descriptions
└── README.md
```

---

## Design System

### Fonts (loaded from Google Fonts)
- **Syne** (800, 700, 600) — headings, labels, UI elements
- **Lora** (400, 600, italic) — body text
- **DM Mono** (300, 400) — labels, metadata, code-style text

### Color Palette (CSS variables in `:root`)
```css
--ink:          #0a0c10   /* primary dark */
--cream:        #f5f2ec   /* primary light background */
--amber:        #d4600a   /* primary accent */
--amber-light:  #f08030   /* hover states */
--teal:         #0a5c6e   /* secondary accent */
--teal-light:   #0e8fa8   /* teal hover */
--dust:         #e8e2d8   /* subtle card hover */
--muted:        #6b6458   /* secondary text */
--border:       rgba(10,12,16,0.12)
```

### Section Backgrounds
- Hero: `--cream` with radial gradient overlays
- About: `--ink` (dark)
- Research: `--cream`
- Publications: `#f0ece5` (slightly darker cream)
- Join: `--teal` (dark teal)
- Footer: `--ink`

### Typography Pattern
Every section follows:
```html
<p class="section-label">// Section Name</p>
<h2 class="section-title">Human Title</h2>
<div class="divider"></div>
```

---

## How to Edit Content

### Add a Publication
Find `<div class="pub-list">` in `index.html` and add a new `.pub-item` block:
```html
<div class="pub-item">
  <div class="pub-year">2024</div>
  <div>
    <p class="pub-journal">Journal Name</p>
    <h3 class="pub-title">
      <a href="DOI_URL" target="_blank">Full Paper Title</a>
    </h3>
    <p class="pub-authors">Author 1, Author 2, and Author 3</p>
    <p class="pub-abstract">One paragraph summary of the paper.</p>
  </div>
</div>
```
Always insert **newest first** (highest year at top).

### Add a Team Member
Find or create a `#team` section. Each member card:
```html
<div class="team-card">
  <div class="team-photo">
    <img src="assets/images/NAME.jpg" alt="Full Name" />
  </div>
  <h3 class="team-name">Full Name</h3>
  <p class="team-role">PhD Student / PostDoc / M.Tech</p>
  <p class="team-bio">Short bio sentence.</p>
</div>
```

### Add a Research Area
Find `<div class="research-grid">` and add a `.research-card`:
```html
<div class="research-card">
  <p class="card-number">07 ——</p>
  <span class="card-icon">🔥</span>
  <h3 class="card-title">New Research Area</h3>
  <p class="card-body">Description of the research focus.</p>
</div>
```

### Update Contact Info
Search for `ghanesh@iisc.ac.in` and replace with the real IISc email when available.

---

## Visualization Guidelines

The site uses **pure CSS + SVG animations** — no canvas, no WebGL by default. When adding new visualizations:

### Preferred: SVG Animations
- Turbulent streamlines: animated `<path>` elements with `<animate>` tags
- Vortex rings: CSS `border-radius: 50%` + `@keyframes spin`
- Flow fields: SVG `<polyline>` or `<path>` with stroke-dashoffset animation
- Keep all SVG inline in `index.html` for zero HTTP requests

### For Complex Visualizations (optional upgrade)
If adding interactive fluid simulations, use **Three.js** or **D3.js** via CDN:
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<!-- or -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/d3/7.8.5/d3.min.js"></script>
```

### Visualization Ideas (priority order)
1. **Interactive velocity field** — D3 particle flow in hero background
2. **Wake visualization** — animated wind turbine wake behind hero vortex
3. **Reynolds number slider** — laminar→turbulent transition animation
4. **LES spectrum plot** — energy cascade (-5/3 Kolmogorov) D3 chart
5. **Wind farm layout** — interactive turbine array with wake overlap

### Animation Performance Rules
- All animations must use `transform` and `opacity` only (GPU composited)
- Never animate `width`, `height`, `top`, `left` (causes layout thrashing)
- Use `will-change: transform` on heavy animated elements
- Keep total SVG animation count < 20 elements for mobile perf

---

## Git Workflow

```bash
# Clone the repo
git clone https://github.com/ghanesh91/intelligent-turbulence-lab.git
cd intelligent-turbulence-lab

# Make changes to index.html
# Then deploy:
git add -A
git commit -m "feat: <description of change>"
git push origin main

# GitHub Pages auto-deploys within ~60 seconds
# Live at: https://ghanesh91.github.io/intelligent-turbulence-lab/
```

### Commit Message Convention
```
feat: add team section with 3 members
fix: correct publication year for PRF 2022 paper
style: improve mobile nav for small screens
viz: add D3 particle flow to hero background
content: add new PhD student John Doe
```

---

## Common Tasks for Claude Code

### "Add my photo"
```bash
# Copy photo to assets/images/
cp ~/Downloads/GN_photo.jpg assets/images/GN_profile.jpg
# Then in index.html, replace the portrait-placeholder div:
# <div class="portrait-placeholder">GN</div>
# with:
# <img src="assets/images/GN_profile.jpg" alt="Dr. Ghanesh Narasimhan" style="width:100%;height:100%;object-fit:cover;" />
```

### "Add a new paper"
Provide: title, journal, year, authors, DOI, abstract. Claude Code will insert the `.pub-item` block in the correct position.

### "Add team member"
Provide: name, role, photo path, short bio, links. Claude Code will create/update the team section.

### "Add a visualization"
Specify: which section, what type (particle flow / vortex / spectrum / etc.), interactive or static. Claude Code will write the SVG/JS and inject it.

### "Check the live site"
```bash
# Verify GitHub Pages deployment status
curl -I https://ghanesh91.github.io/intelligent-turbulence-lab/
```

---

## Sections Roadmap

Current sections (in order):
- [x] Hero — animated vortex, lab identity
- [x] About — PI bio, links
- [x] Research — 6 research area cards
- [x] Publications — 2 papers (PRF 2021, PRF 2022)
- [x] Join — open positions + contact
- [x] Footer

Planned additions:
- [ ] **Team** section — between About and Research
- [ ] **News** section — recent updates, awards, talks
- [ ] **Gallery** — simulation visualizations, lab photos
- [ ] **Teaching** — courses taught at IISc ME
- [ ] **Talks** — conference presentations with slides/video links
- [ ] **Resources** — public code repos, datasets

---

## Performance Targets
- Page load < 2s on 4G
- No external JS dependencies (currently zero)
- Fonts: only load weights actually used
- Images: compress to < 200KB each (use `convert` or `squoosh`)
- Lighthouse score target: > 90 on all metrics

---

## Contact for Site Issues
PI: Dr. Ghanesh Narasimhan
GitHub: https://github.com/ghanesh91
Repo: https://github.com/ghanesh91/intelligent-turbulence-lab
