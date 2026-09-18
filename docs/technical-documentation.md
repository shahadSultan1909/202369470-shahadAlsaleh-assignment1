# Technical Documentation

## Overview
This document explains the technical structure, design decisions, and
implementation details of the portfolio website.

---

## 1. Technology Stack
- **HTML** — semantic page structure.
- **CSS** — styling, responsive layout (Flexbox & Grid), CSS custom
  properties (variables) for theming.
- **JavaScript** — no frameworks or libraries; all
  interactivity is handled with plain DOM APIs.
- **Google Fonts** — Fraunces (headings) and Inter (body text), loaded via
  `<link>` in `<head>`.

No build tools, package managers, or external JS libraries are required.

---

## 2. File Structure

| File/Folder | Purpose |
|---|---|
| `index.html` | Main page containing all sections (Navbar, Hero(Introduction)/About, Achievements, Projects, Contact, Footer). |
| `css/styles.css` | All styling, organized by section with CSS variables at the top for the color theme. |
| `js/script.js` | Handles mobile navigation, smooth scrolling, time based greeting, and contact form validation. |
| `assets/images/` | Reserved folder for any future images (currently unused). |
| `docs/ai-usage-report.md` | Documents AI tool usage throughout the assignment. |
| `docs/technical-documentation.md` | This file. |

---

## 3. Design System (CSS Variables)
All colors, radii, and fonts are defined once as CSS custom properties in
`:root` (top of `styles.css`), which makes the theme easy to adjust
consistently across the whole site:

```css
:root {
  --rose: #e39ab2;
  --lilac: #cdb9e6;
  --sage: #a9d2ba;
  --ink: #2b2230;
  --font-display: 'Fraunces', serif;
  --font-body: 'Inter', sans-serif;
  ...
}
```

---

## 4. Responsive Design Approach
- **CSS Grid** is used for the Projects section layout, adapting the
  three-column media/body/link grid to a single column stack on mobile.
- **Flexbox** is used for the navbar, hero content, and About section
  layout.
- Two breakpoints are defined:
  - `@media (max-width: 768px)` — tablet: converts the navbar into a
    slide-in mobile menu.
  - `@media (max-width: 480px)` — mobile: reduces heading sizes, padding,
    and stacks project thumbnails horizontally.

---

## 5. JavaScript Features

### 5.1 Smooth Scrolling
All internal navigation links (`href="#section"`) are intercepted with a
`click` event listener. JavaScript calculates the target section's
position and subtracts the sticky navbar's height, so the section title
is never hidden behind the navbar after scrolling.

### 5.2 Mobile Navigation Toggle
A hamburger button toggles the `.open` class on the `.nav-links` list,
which slides the mobile menu in/out via a CSS `transform` transition.

### 5.3 Time-Based Greeting
On page load, `Date().getHours()` is used to determine the current hour
and display a contextual greeting message ("Good morning", "Good
afternoon", "Good evening", etc.) in the hero (Introduction) badge.

### 5.4 Contact Form Validation
Since the assignment requires no backend, form submission is intercepted
with `event.preventDefault()`. Each field is validated with simple rules:
- **Name**: minimum 2 characters.
- **Email**: matches a basic email regex pattern.
- **Message**: minimum 10 characters.

Invalid fields are highlighted with a red border and an inline error
message. On successful validation, a success message is shown and the
form resets.

---

## 6. Browser Compatibility
Tested manually in Chrome and Edge at various window
sizes using DevTools device emulation. The site relies only on standard,
widely supported CSS/JS features (Flexbox, Grid, CSS variables),
so it is expected to work consistently across modern browsers (Chrome,
Firefox, Edge, Safari).

---

## 7. Known Limitations / Future Improvements
- Contact form does not currently send data anywhere (no backend) — this
  matches the assignment scope, which explicitly does not require one.
- Project thumbnails are represented with custom SVG icons rather than
  real screenshots, since the featured projects (CLI tool, FPGA circuit,
  ML notebook) don't have simple visual screenshots to showcase.
- Dark mode theme toggle was considered but not implemented in this
  version, in favor of the light theme and smooth
  scrolling feature.