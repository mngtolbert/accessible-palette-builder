# Accessible Color Palette Builder

**A WCAG contrast checker and palette export tool built specifically for instructional designers.**

Live demo → [GitHub Pages link]  
Built by: Michelle Tolbert-Plant | Technical Learning Engineer & AI Solutions Consultant

---

## Why This Exists

Every instructional designer who has ever built a course in Rise 360, Storyline, or Figma has made the same mistake: picked colors that look great on a calibrated monitor, published the course, and then discovered the text is unreadable on a projector, a tablet in a warehouse, or a low-brightness laptop screen.

WCAG contrast compliance isn't a legal checkbox — it's the difference between content that works for everyone and content that silently fails a portion of your audience. I built this tool because I needed it during WCAG 2.1 AA compliance work for Zebra Technologies' global frontline workforce, and nothing I found online was designed for how instructional designers actually work.

---

## What It Does

**Paste in your hex codes → get instant WCAG compliance verdicts → export your palette.**

For each color you input, the tool returns:

- **The contrast ratio** against white and black text (calculated per the WCAG 2.1 specification)
- **A plain-English verdict:**
  - ✓ Safe for all text sizes (CR ≥ 7:1 — AAA)
  - ✓ Safe for body text (CR ≥ 4.5:1 — AA)
  - ✗ Decorative use only — fails for text (CR < 4.5:1)
- **RGB and HSL values** for cross-tool color matching
- **The optimal text color** (white or black) rendered live on the swatch

**Export options:**
- **PNG** — a printable, high-resolution palette sheet with all swatch data. Hand it to a stakeholder or attach it to a design spec.
- **CSS** — ready-to-paste CSS custom properties (`--color-1: #hex;`)
- **JSON** — structured palette data for use in design systems or documentation

---

## Designed For

- Instructional designers building accessible course content in Rise 360, Articulate Storyline, or Lectora
- L&D teams establishing a color system for a client or brand
- Anyone creating diagrams, infographics, or visual job aids who needs to verify contrast before publishing
- Accessibility reviewers doing a quick pre-submission palette audit

---

## WCAG 2.1 Reference

| Level | Contrast Ratio | Use Case |
|-------|---------------|----------|
| AAA   | ≥ 7:1         | All text — enhanced accessibility |
| AA    | ≥ 4.5:1       | Normal text (< 18pt or < 14pt bold) |
| AA Large | ≥ 3:1      | Large text only (≥ 18pt or ≥ 14pt bold) |
| Fail  | < 3:1         | Decorative elements only — never text |

Full specification: [WCAG 2.1 Success Criterion 1.4.3](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)

---

## How to Use

**No install. No dependencies. One file.**

```bash
# Option A: just open it
open index.html

# Option B: serve it locally
python -m http.server 8080
# then visit http://localhost:8080
```

**Input format** — paste hex codes into the text area, one per line. Name is optional:

```
#1A2E4A Navy
#0D6E6E Teal
#C9A84C Gold
#F0F6FF Off-White
#E2E8F0   (no name — that's fine too)
```

Formats accepted: `#RRGGBB`, `#RGB`, `RRGGBB` (hash optional). Names follow the hex, separated by a space or dash.

---

## Technical Notes

**Zero dependencies.** Vanilla HTML, CSS, and JavaScript. No build step, no npm, no framework. The contrast ratio calculation follows the WCAG 2.1 relative luminance formula exactly:

```
Luminance = 0.2126R + 0.7152G + 0.0722B
(where R, G, B are linearized sRGB values)

Contrast Ratio = (L1 + 0.05) / (L2 + 0.05)
(where L1 is the lighter luminance)
```

**PNG export** uses the Canvas API at 2× pixel density for print-quality output. Suitable for including in design documentation, accessibility audit reports, or stakeholder presentations.

---

## Connection to Portfolio Work

This tool was built out of necessity during WCAG 2.1 AA compliance work at Zebra Technologies, where I designed mobile-first certification content for global frontline workers — including operators using devices in direct sunlight, on warehouse floors, and in variable lighting conditions. Contrast wasn't a nicety. It was a functional requirement.

The shade spectrum feature (showing the full range of tints and shades for each input color with contrast ratings) was added specifically for teams building visual templates and diagram systems — where you need to know not just whether *this* color passes, but which adjacent shades are safe to use as alternatives.

---

## Repository Structure

```
accessible-palette-builder/
├── index.html     ← The entire tool. One file.
└── README.md
```

---

## License

MIT — use it, fork it, adapt it for your team's workflow.
