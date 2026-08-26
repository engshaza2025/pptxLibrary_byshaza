# Changelog

## 2 — August 2026

### Fixed
- **Office stock icons stayed black in PowerPoint.** Microsoft's built-in icons paint through
  CSS classes named `MsftOfcThm_*`, which PowerPoint re-binds to the document theme colour,
  ignoring whatever fill is written in the SVG. The engine now flattens every `<style>` rule
  onto the elements and deletes the classes, so PowerPoint has nothing left to re-bind.

### Added
- **Gradients built from the deck's theme** (T1 monochrome, T2 accent 1→2, T3 accent→50% darker),
  rebuilt automatically whenever the theme changes.
- **Custom gradient builder** — pick any two theme colours. The preset stores the *slot names*
  (`accent1` → `accent2`), not hex values, so the same preset adapts to every client's deck.
- **Gradient direction** — diagonal, linear or radial; stored in the preset.
- **Preset export / import** as a single JSON file, with merge-not-wipe, duplicate skipping
  and strict sanitising of imported values.
- **Numbers up to 99** (was 20), honouring the 60-object batch cap.
- **Floating tooltips** replacing the printed help text in the pane.

### Changed
- Recolouring is always on for the Icons tab; the checkbox is gone. Use the Shapes tab for
  artwork that must keep its original colours.
- Recolouring now uses a perceptual brightness threshold instead of a fixed list of dark colours,
  parses any colour notation, and never touches `clipPath`, `mask` or `filter` subtrees.
- Paint moves to explicit attributes before insertion, which PowerPoint reads more reliably.
- Product name unified as **Shaza Toolkit**; version unified as **2** across `index.html`,
  `manifest.xml` and `package.json`.
