# Responsive Layout — CSS `position` Implementation (No Flexbox / No Grid)

A responsive multi-breakpoint web layout built strictly with CSS **`position`** (`relative` and `absolute`) and standard box-model properties (`display: block`, `display: inline-block`, margins, and transforms) — with **zero `display: flex`** and **zero `display: grid`**.

---

## Project Structure

```text
.
├── index.html   # Semantic HTML5 markup structured for mobile-first DOM stacking
├── styles.css   # Responsive stylesheet using CSS position & media queries
└── README.md    # Technical documentation and architecture overview
```

---

## Breakpoints & Layout Behavior

### 1. Desktop View (`1440px` — Default)
- **Container (`.page-wrapper`)**: `max-width: 1440px`, centered horizontally (`margin: 0 auto`) with outer viewport padding.
- **Header (`.site-header`)**: `height: 80px`, `position: relative`.
  - **Left**: Brand logo pinned via `position: absolute; left: 24px; top: 50%; transform: translateY(-50%);`.
  - **Right**: Navigation links (`Home`, `Projects`, `About`, `Contact`) and `Get Started` button aligned via `position: absolute; right: 24px; top: 50%; transform: translateY(-50%);` with `display: inline-block` items.
- **Sidebar (`.sidebar`)**: `width: 280px`, pinned to the left edge of `.content-area` via `position: absolute; top: 0; left: 0; bottom: 0;`, automatically matching the height of `.main-content`. Vertical navigation items (`Dashboard`, `Projects`, `Settings`, `Help`) use `display: block` with `margin-bottom: 12px`.
- **Main Content (`.main-content`)**: Positioned beside the sidebar via `margin-left: 288px` (`280px` sidebar + `8px` gutter within the `1440px` frame). The `560 × 320px` media placeholder is anchored to the right via `position: absolute; right: 32px; top: 50%; transform: translateY(-50%);`.
- **Footer (`.site-footer`)**: `height: 64px`, `position: relative`, with copyright text positioned on the left (`left: 24px`) and secondary links (`Privacy`, `Terms`, `Contact`) positioned on the right (`right: 24px`).

### 2. Tablet View (`max-width: 1024px` — Target: `768px`)
- **Container**: `max-width: 768px`.
- **Header**: `height: 64px`. Desktop navigation links and `Get Started` button are hidden (`display: none`) and replaced by an interactive pure-CSS hamburger menu (`position: absolute; right: 16px`) that opens a collapsible navigation drawer containing the links and action button.
- **Sidebar**: Width reduced to `200px`.
- **Main Content**: Adjusted to `margin-left: 208px` (fitting the remaining `568px` column space). The `368 × 240px` media placeholder switches to `position: relative` so it stacks cleanly below the `Learn More` CTA button.

### 3. Mobile View (`max-width: 767.98px` — Target: `375px`)
> **Breakpoint Note:** Using `max-width: 767.98px` (just below `768px`) ensures that viewing at an exact `768px` viewport renders the **Tablet (`768px`)** layout, while viewports below `768px` (including `375px`) trigger the **Mobile (`375px`)** layout.
- **Container**: `max-width: 375px`.
- **DOM Order Stacking**: `<main class="main-content">` is placed before `<aside class="sidebar">` in `index.html`. On mobile, `.sidebar` resets from `position: absolute` to `position: relative`, naturally stacking underneath `.main-content` without Flexbox/Grid `order`.
- **Main Content & Footer**: Full-width responsive padding (`24px 16px`), full-width CTA button, `200px`-tall media placeholder, and vertically stacked footer elements.

---

## Design Tokens

| Token / Element | Value |
| :--- | :--- |
| **Header Background** | `#DBEAFE` |
| **Sidebar Background** | `#E9D5FF` |
| **Main Content Background** | `#D1FAE5` |
| **Footer Background** | `#FED7AA` |
| **Primary Action Color** | `#1D4ED8` |
| **Font Family** | `'Inter', 'Roboto', sans-serif` |
| **Logo Typography** | `20px / 700` |
| **Nav Links Typography** | `16px / 500` |
| **Main Heading Typography** | `32px / 700` (scales down on tablet/mobile) |
| **Paragraph Typography** | `16px / 400` |
| **Button Typography** | `16px / 600` |
| **Footer Typography** | `14px / 400` |
| **Border Radius** | `8px` |

---

## How to Run

1. Open `index.html` directly in any modern browser (Chrome, Firefox, Safari, Edge).
2. Open **Browser DevTools** (`F12` or `Cmd + Option + I`) and toggle **Device Toolbar** (`Ctrl + Shift + M` / `Cmd + Shift + M`).
3. Test the three target viewports:
   - **Desktop**: `1440px`
   - **Tablet**: `768px`
   - **Mobile**: `375px`
