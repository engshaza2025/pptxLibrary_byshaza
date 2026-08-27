# Shaza Toolkit

**A PowerPoint add-in that turns any folder of SVG icons on your own computer into a searchable
library — recoloured with your presentation's real theme colours, inserted as editable vectors.
No server. No account. Nothing uploaded.**

<p align="right"><b>إضافة بوربوينت تحوّل أي مجلد من ملفات SVG على جهازك إلى مكتبة أيقونات قابلة للبحث،
تُلوَّن بألوان ثيم عرضك وتُدرَج ككائنات متجهة قابلة للتحرير — بلا خادم ولا حساب ولا رفع لأي ملف.</b></p>

---

## What it does

- Point it at **your own** SVG folder — no vendor library, no vendor licence.
- Reads the **real theme colours** of the active slide's theme, following the
  `slide → layout → master → theme` chain, so decks with several slide masters resolve correctly.
- Recolours solid icons, line icons, CSS-class icons, Microsoft's own stock icons, and icons
  carrying no colour information at all.
- Nine container shapes, with outlines, soft shadows and gradients: neutral, built from the deck's
  theme, or from two theme colours you pick yourself.
- A deliberately simple **Logos** tab — size and container shape only. Logo size starts at 150 px
  and runs 50 → 400 px in steps of 50, with a **White logo** switch for dark backgrounds.
- Multi-select up to 60 icons and insert them in one action, laid out to fit the slide.
- Numbered markers 1–99 in the same style.
- Up to 12 saved presets, exportable as a single file for a whole team — a preset built from theme
  slots re-resolves to each new deck's colours automatically.
- Arabic and English interfaces, switchable from a button in the header.

## Requirements

| | |
|---|---|
| Requirement set | `ImageCoercion 1.2` |
| PowerPoint on Windows | Microsoft 365, or Office 2021 and later |
| PowerPoint on Mac | supported |
| PowerPoint on the web | supported |
| PowerPoint on iPad | not supported (the platform cannot insert SVG) |
| Hosting | HTTPS, static files only |

## Repository layout

```
.
├── index.html        الواجهة العربية (RTL)   — served at /
├── manifest.xml      Arabic manifest
├── en/
│   ├── index.html    English interface (LTR) — served at /en/
│   └── manifest.xml  English manifest
├── assets/           ribbon and store icons
├── CHANGELOG.md
└── .nojekyll         keeps GitHub Pages from running Jekyll
```

Each `index.html` is the entire add-in: interface, SVG engine, theme reader and insertion logic.
No build step, no dependencies, no framework. The only external script is Microsoft's own `office.js`.

## Publishing with GitHub Pages

1. Push this repository to GitHub.
2. **Settings → Pages → Source: Deploy from a branch**, branch `main`, folder `/ (root)`.
3. Wait for the first deployment, then confirm both URLs load:
   - `https://<user>.github.io/<repo>/`
   - `https://<user>.github.io/<repo>/en/`
4. If your user or repository name differs from the URLs already in the manifests, update
   `SourceLocation`, `AppDomains`, `IconUrl`, `HighResolutionIconUrl` and `SupportUrl`
   in **both** manifest files.

The language button relies on this layout: Arabic at the root, English one level down at `/en/`.

## Installing the add-in

**Windows** — put the manifest in a folder, share it on the network, then
**File → Options → Trust Center → Trust Center Settings → Trusted Add-in Catalogs**, add the path,
tick *Show in Menu*, restart PowerPoint, and pick it from **Insert → My Add-ins → SHARED FOLDER**.

**Mac** — copy the manifest to
`~/Library/Containers/com.microsoft.Powerpoint/Data/Documents/wef`, then restart PowerPoint.

**Web** — **Insert → My Add-ins → Upload My Add-in**.

**A whole organisation** — Microsoft 365 admin center → Settings → Integrated apps →
Upload custom apps. Requires Exchange Online and up to 24 hours to propagate.

## Privacy

No backend, no accounts, no analytics, no third-party libraries. The add-in reads the SVG folder
you choose (read-only, with your explicit permission) and exactly two parts of the open
presentation — the theme part and the presentation properties — to obtain theme colours and slide
dimensions. Nothing about your icons or your presentations leaves your machine.

## Versioning

The version appears in three places and must stay identical: `APP_VERSION` in `index.html`,
`<Version>` in both manifests, and `version` in `package.json`.
Increasing `<Version>` is what pushes an update to already-installed clients.

---

© Shaza Add-ins
