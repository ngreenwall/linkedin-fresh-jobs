---
date: 2026-07-23
type: reference
tags:
  - KnowledgeNote
---
# Branding Reference: match the Fresh Jobs look

This tool is a separate standalone project from `fresh-jobs` (see `fresh-jobs-link-generator-spec.md` for why), but Nate wants it to *look* like part of the same family: same colors, same font, same rounded/flat style. This doc has the exact values pulled from the Fresh Jobs GUI so this plain-HTML tool can match without needing Tailwind, Next.js, or any of that GUI's actual dependencies.

**What this is:** a copy-paste palette and style reference, not shared code. This project stays a single static HTML file per its spec; just recreate the look with plain CSS.

## Colors

Fresh Jobs uses a chartreuse/citron primary color (a bright yellow-green) defined in the OKLCH color format. OKLCH is just a more precise way of writing a color (lightness, chroma/intensity, hue angle) that keeps colors looking consistent across light and dark backgrounds. Any modern browser supports `oklch()` directly in CSS, no library needed.

Dark mode is the default look (matches Fresh Jobs). Light mode is supported there too, include it if you want the toggle, skip it if dark-only is fine for this tool.

**Dark theme (default):**
```css
--background: oklch(0.15 0.012 130);       /* near-black page background */
--foreground: oklch(0.94 0.01 110);        /* main text color */
--card: oklch(0.19 0.014 130);             /* panel/card background, slightly lighter than page */
--primary: oklch(0.88 0.22 115);           /* chartreuse — buttons, links, highlights */
--primary-foreground: oklch(0.2 0.04 125); /* text color ON primary-colored buttons */
--muted-foreground: oklch(0.68 0.02 120);  /* secondary/dimmer text (labels, hints) */
--border: oklch(1 0 0 / 10%);              /* white at 10% opacity — subtle hairline borders */
--ring: oklch(0.8 0.19 115);                /* focus outline color (keyboard nav / clicked inputs) */
```

**Light theme (optional):**
```css
--background: oklch(0.985 0.006 110);
--foreground: oklch(0.21 0.02 130);
--card: oklch(1 0 0);
--primary: oklch(0.86 0.21 115);
--primary-foreground: oklch(0.24 0.05 125);
--muted-foreground: oklch(0.5 0.02 125);
--border: oklch(0.9 0.01 115);
--ring: oklch(0.74 0.17 115);
```

The primary color is the same chartreuse hue (115) in both modes, just tuned brighter/dimmer. That hue is the one number to keep consistent if you ever adjust anything.

## Font

Fresh Jobs uses **Geist** (body text) and **Geist Mono** (for anything code/URL-like — this tool's generated link output is a good candidate for the mono font). Both are free and load easily via Google Fonts:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Geist:wght@400;500;600&family=Geist+Mono:wght@400;500&display=swap" rel="stylesheet">
```
```css
body { font-family: 'Geist', sans-serif; }
code, .url-output { font-family: 'Geist Mono', monospace; }
```

## Shape and spacing

- Border radius: `10px` on cards/panels, `8px` (`10px - 2px`) on buttons/inputs. Fresh Jobs derives a few radius sizes from one root value, but for a one-file tool just hardcode 8-10px, close enough.
- No box-shadows anywhere in Fresh Jobs. Depth comes from a subtle 1px border/ring plus the card background being a shade lighter than the page background, not shadows. Keep this tool flat the same way.
- Buttons: solid chartreuse background, dark text on top (per `--primary-foreground` above), no border. On hover, drop the button's opacity to ~80% (`opacity: 0.8` or a slightly darker chartreuse) rather than changing the whole color.
- Buttons also have a tiny "press" effect: shift down 1px on click (`:active { transform: translateY(1px); }`). Small detail but it's in the Fresh Jobs button style, worth matching.
- Panels/cards: background = `--card`, outline = 1px `--border` (not a heavier box-shadow border).

## Dark-mode toggle (if you add one)

Fresh Jobs defaults to dark and toggles a `.dark` class on `<html>` (no "system preference" auto-detection, it's an explicit user toggle). For a plain HTML/JS version:

```js
// on load, restore saved preference (default: dark)
const saved = localStorage.getItem('theme') || 'dark';
document.documentElement.classList.toggle('dark', saved === 'dark');

// toggle button
function toggleTheme() {
  const isDark = document.documentElement.classList.toggle('dark');
  localStorage.setItem('theme', isDark ? 'dark' : 'light');
}
```
```css
:root { /* light values here */ }
.dark { /* dark values here, override the same variable names */ }
```

## Quick summary for whoever builds this

Dark near-black background, chartreuse/lime accent color for buttons and links, Geist font, flat design (no shadows, thin borders/rings only), slightly rounded corners (~8-10px), buttons nudge down 1px when clicked. That's the whole look.
