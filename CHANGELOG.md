# Changelog

## 2 — August 2026

### Fixed
- **Office stock icons stayed black in PowerPoint.** Microsoft's built-in icons paint through CSS
  classes named `MsftOfcThm_*`, which PowerPoint re-binds to the document theme colour, ignoring
  whatever fill is written in the SVG. The engine now flattens every `<style>` rule onto the
  elements and deletes the classes, so PowerPoint has nothing left to re-bind.
- The gradient builder no longer reappears on its own when switching back to the Icons tab.

### Added
- **Gradients built from the deck's theme** — T1 monochrome, T2 accent 1 to 2, T3 accent to 50%
  darker — rebuilt whenever the theme changes.
- **Custom gradient builder**: pick any two theme colours. The preset stores the *slot names*
  (`accent1` → `accent2`), not hex values, so the same preset adapts to every client's deck.
- **Gradient direction** — diagonal, linear or radial; stored in the preset.
- **Preset export / import** as one JSON file: merge-not-wipe, duplicate skipping, strict sanitising.
- **Numbers up to 99** (was 20), honouring the 60-object batch cap.
- **Container shapes for logos** — all nine shapes, outline, shadow and gradients.
- **White logo** switch: knocks a whole logo out to white for dark backgrounds.
- **Language button** in the header, switching between the Arabic interface and the English one.

### Changed
- **Printed help text removed from the pane.** Controls carry a standard `title` and PowerPoint
  renders the tooltip itself — the add-in draws no tooltip box of its own, so no empty black box
  can appear and nothing follows the cursor. The theme-reading status lives on the ⓘ badge.
- **Logo size scale**: the Logos tab now starts at **150 px** and its quick-pick list runs
  **50 → 400 px in steps of 50**. Icons and Shapes keep 10 → 200 px in steps of 10.
- The Logos tab is trimmed to size and container shape only — no presets, theme colour row,
  gradients, direction buttons or target chips.
- Recolouring is always on for the Icons tab; the checkbox is gone. Use the Shapes tab for artwork
  that must keep its original colours.
- Recolouring uses a perceptual brightness threshold instead of a fixed list of dark colours, parses
  any colour notation, and never touches `clipPath`, `mask` or `filter` subtrees.
- Paint moves to explicit attributes before insertion, which PowerPoint reads more reliably.
- Swatch rows start from the right in Arabic, from the left in English, and wrap at six per row.
- Product name unified as **Shaza Toolkit**; version unified as **2**.
