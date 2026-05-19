# OfficeConnectPro

Documentation site for [OfficeConnect](https://officeconnectpro.com) — a Microsoft Office add-in for Workday Adaptive Planning and Workday Financials. Written for finance teams and IT admins who need clear, step-by-step guidance without digging through Workday's official docs.

Live at **[officeconnectpro.com](https://officeconnectpro.com)**

---

## What's covered

| Section | Description |
|---|---|
| [Get Started](content/get-started/) | System requirements, installation (admin and end-user), first sign-in, tenant setup, SSO, registry deployment, and Financials data model setup |
| [Build Reports](content/build-reports/) | Adding elements, filters, time contexts, cell explorer, workbook properties, sharing, and publishing to PowerPoint and Word |
| [Troubleshoot](content/troubleshoot/) | Common errors and fixes |

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
- `admin-note` — highlights steps that require admin access
- `step` — numbered step block used in procedural content

## Links

- [YouTube](https://www.youtube.com/@officeconnectpro)
- [Ko-fi](https://ko-fi.com/smcintosh)
- [GitHub](https://github.com/s-mcintosh)
