# OfficeConnectPro

Independent documentation site for Workday OfficeConnect — written for finance teams and IT admins who need clear, step-by-step guidance without digging through Workday's official docs.

Live at **[officeconnectpro.com](https://officeconnectpro.com)**

---

## What's covered

| Section | Description |
|---|---|
| [Get Started](content/get-started/) | Installation, first report, system requirements, SSO, registry deployment, build reports, data entry/write-back, Word & PowerPoint, performance, and admin configuration |
| [Reference](content/reference/) | Troubleshooting guides, release notes, version compatibility, element types, glossary, and resources |
| [About](content/about/) | Why this site exists |

---

## Tech stack

- **Framework:** [Hugo](https://gohugo.io/) with the [Docsy](https://www.docsy.dev/) theme
- **Hosting:** GitHub Pages with a custom domain
- **CSS pipeline:** PostCSS + Autoprefixer
- **Deployed on push to `main`** via GitHub Actions

## Local development

**Prerequisites:** Hugo extended (v0.161+), Go, Node.js 22+

```bash
# Install dependencies
npm ci

# Serve locally with live reload
hugo server

# Build for production
hugo --minify
```

The local server runs at `http://localhost:1313`.

## Contributing

Content lives in `content/` as Markdown files with Hugo front matter. Each section has an `_index.md` for the section landing page, plus individual topic pages.

Custom shortcodes are in `layouts/shortcodes/`:
- `step` — numbered step block for procedural content
- `admin-note` — highlights steps that require admin access
- `tip`, `warning`, `deprecated`, `new-in-release` — callout blocks
- `audience-badge` — inline pill for FP&A / Admin / Consultant / Executive content
- `related` — related articles module used at article footers

## Links

- [officeconnectpro.com](https://officeconnectpro.com)
- [YouTube](https://www.youtube.com/@officeconnectpro)
- [Ko-fi](https://ko-fi.com/smcintosh)
