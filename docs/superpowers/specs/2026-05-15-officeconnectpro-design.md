# officeconnectpro.com — Design Spec

**Date:** 2026-05-15  
**Status:** Approved  
**Source material:** Workday Adaptive Planning Documentation (670-page PDF, May 14 2026)  
**OfficeConnect coverage:** 76 pages extracted from PDF

---

## 1. Goal

Build a public documentation website at **officeconnectpro.com** that provides clear, step-by-step instructions for Workday Adaptive Planning's OfficeConnect feature in an easy-to-use wiki format. The content is hand-crafted from the source PDF — written for humans, not converted from raw PDF output.

---

## 2. Audience

Both end users and IT administrators, with equal weight. The two audiences share the same site but are clearly distinguished throughout:

- **End users** — FP&A / finance professionals using OfficeConnect in Excel, PowerPoint, or Word to build and share reports
- **IT admins** — deploying OfficeConnect, managing tenants, configuring SSO, pushing updates via group policy

Admin-specific content is tagged with an `{{< admin-note >}}` shortcode callout wherever it appears.

---

## 3. Technology Stack

| Layer | Choice | Reason |
|---|---|---|
| Static site generator | Hugo (latest, extended) | Fast builds, excellent Docsy support |
| Theme | Docsy (Hugo Module) | Purpose-built for documentation wikis |
| Hosting | GitHub Pages | Free, integrates with Hugo via GitHub Actions |
| Search | Lunr.js (Docsy built-in) | Full-text, no external service required |
| CI/CD | GitHub Actions | Push to `main` → live in ~60 seconds |
| Local build dep | Go (for Hugo Modules) | Required to resolve Docsy as a Hugo Module |

Docsy is installed as a **Hugo Module** (not a git submodule) for cleaner dependency management.

---

## 4. Information Architecture

Content is organized into 5 task-journey sections matching how users think about their work — not by feature category.

### 4.1 Get Started (5 pages)
| Page | Audience |
|---|---|
| What is OfficeConnect? | Both |
| System Requirements | Both |
| Install as an End User | End User |
| Install as an IT Admin | IT Admin |
| Check & Update Your Version | Both |

### 4.2 Connect (5 pages)
| Page | Audience |
|---|---|
| Sign In & Create Your First Tenant | Both |
| Work with Multiple Instances | Both |
| Set Up Workday SSO | IT Admin |
| Deploy Tenants via Registry | IT Admin |
| Secure OfficeConnect Workbooks | Both |

### 4.3 Build Reports (10 pages)
| Page | Audience |
|---|---|
| Interface Tour: The Reporting Pane | End User |
| Add Elements to Rows, Columns & Cells | End User |
| Work with Time & Contexts | End User |
| Filter Your Data | End User |
| Cut, Copy & Move Elements | End User |
| Review & Verify Applied Elements | End User |
| Workbook & Worksheet Properties | End User |
| Create Repeating Reports | End User |
| Financials vs. Adaptive Planning Data Sources | Both |
| Cell Explorer & Drill-Down | End User |

### 4.4 Share & Publish (3 pages)
| Page | Audience |
|---|---|
| Share Reports via Teams, SharePoint & OneDrive | End User |
| OfficeConnect for PowerPoint | End User |
| OfficeConnect for Word | End User |

### 4.5 Troubleshoot & FAQ (12 pages)
| Page | Audience |
|---|---|
| Fix COM Registration Errors | Both |
| Resolve OfficeConnect Update Errors | Both |
| Task Pane Not Displaying Correctly | Both |
| Numbers Not Shifting After Insert | End User |
| Suppress & Hide Zeros / Blanks | End User |
| Remove Elements | End User |
| Change Rounding Settings | End User |
| Display Percentage Values | End User |
| Create Fixed Date Columns | End User |
| Create a Trailing 12-Month Report | End User |
| Link to External Excel Files | End User |
| Run the Troubleshooting Tool | Both |

**Total: ~35 pages** — all hand-crafted from the source PDF.

---

## 5. Visual Design

**Direction:** Dark & Amber — distinct identity, not Workday-branded.

| Token | Value | Role |
|---|---|---|
| `$primary` | `#f59e0b` | Amber — links, active nav, CTAs, accents |
| `$td-sidebar-bg` | `#18181b` | Near-black sidebar |
| `$td-sidebar-fg` | `#d4d4d8` | Light grey sidebar text |
| `$navbar-dark-bg` | `#18181b` | Matching top navbar |
| `$body-bg` | `#fafafa` | Light content area for readability |
| `$link-color` | `#f59e0b` | Amber links in content |
| `$font-family` | `Inter, system-ui` | Clean, modern sans-serif |

Implemented via `assets/scss/_variables_project.scss` — no theme fork required.

---

## 6. Project Directory Structure

```
officeconnectpro/
├── config/
│   └── _default/
│       ├── config.toml         # baseURL, title, theme (hugo module)
│       ├── params.toml         # Docsy feature flags (search, edit links, etc.)
│       └── menus.toml          # top nav items
├── content/
│   ├── _index.md               # homepage hero
│   ├── get-started/
│   │   ├── _index.md
│   │   ├── what-is-officeconnect.md
│   │   ├── system-requirements.md
│   │   ├── install-end-user.md
│   │   ├── install-admin.md
│   │   └── check-version.md
│   ├── connect/
│   │   ├── _index.md
│   │   ├── sign-in-create-tenant.md
│   │   ├── multiple-instances.md
│   │   ├── workday-sso.md
│   │   ├── deploy-tenants-registry.md
│   │   └── secure-workbooks.md
│   ├── build-reports/
│   │   ├── _index.md
│   │   ├── reporting-pane-tour.md
│   │   ├── add-elements.md
│   │   ├── time-and-contexts.md
│   │   ├── filter-data.md
│   │   ├── cut-copy-move-elements.md
│   │   ├── review-applied-elements.md
│   │   ├── workbook-worksheet-properties.md
│   │   ├── repeating-reports.md
│   │   ├── financials-vs-adaptive-planning.md
│   │   └── cell-explorer-drill-down.md
│   ├── share-publish/
│   │   ├── _index.md
│   │   ├── share-teams-sharepoint-onedrive.md
│   │   ├── officeconnect-for-powerpoint.md
│   │   └── officeconnect-for-word.md
│   └── troubleshoot/
│       ├── _index.md
│       ├── com-registration-error.md
│       ├── update-errors.md
│       ├── task-pane-not-displaying.md
│       ├── numbers-not-shifting.md
│       ├── suppress-zeros-blanks.md
│       ├── remove-elements.md
│       ├── change-rounding-settings.md
│       ├── display-percentage-values.md
│       ├── fixed-date-columns.md
│       ├── trailing-12-month-report.md
│       ├── link-external-excel-files.md
│       └── troubleshooting-tool.md
├── assets/
│   └── scss/
│       └── _variables_project.scss   # dark & amber theme overrides
├── layouts/
│   └── shortcodes/
│       ├── admin-note.html           # IT Admin callout block
│       └── step.html                 # numbered step block
├── static/
│   └── images/
├── go.mod                            # Hugo module deps (Docsy)
├── go.sum
├── .gitignore                        # includes .superpowers/
└── .github/
    └── workflows/
        └── deploy.yml                # GitHub Actions → GitHub Pages
```

---

## 7. Custom Shortcodes

### `{{< admin-note >}}`
Renders an amber-bordered callout block for IT Admin-specific steps. Used inline within pages that serve both audiences.

```
{{< admin-note >}}
Requires registry access. Contact your IT administrator if you don't have permissions.
{{< /admin-note >}}
```

### `{{< step n="1" title="Open Excel" >}}`
Renders a styled numbered step block for step-by-step guides — consistent across all 35 pages.

```
{{< step n="1" title="Open Excel" >}}
Start Excel and look for the **OfficeConnect** tab in the ribbon.
{{< /step >}}
```

---

## 8. GitHub Actions Deployment

```yaml
# .github/workflows/deploy.yml
name: Deploy to GitHub Pages
on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-go@v5
        with:
          go-version: stable          # required: Docsy is a Hugo Module
      - uses: peaceiris/actions-hugo@v3
        with:
          hugo-version: latest
          extended: true
      - run: hugo --minify
      - uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

Push to `main` → GitHub Actions builds Hugo → publishes to `gh-pages` branch → live at officeconnectpro.com in ~60 seconds.

---

## 9. Docsy Feature Configuration (`params.toml`)

```toml
# Search
offlineSearch = true           # Lunr.js, no external service

# Edit links
github_repo = "https://github.com/<your-org>/officeconnectpro"
github_branch = "main"

# UI features
ui.breadcrumb_disable = false
ui.sidebar_menu_compact = true
ui.sidebar_menu_foldable = true
ui.navbar_logo = true
```

---

## 10. Content Authoring Standard

Each page follows this structure:

1. **Front matter** — `title`, `linkTitle`, `description`, `weight` (controls sidebar order)
2. **One-sentence intro** — what this page covers and who it's for
3. **Prerequisites** (if any) — software, permissions, prior steps
4. **Steps** — using `{{< step >}}` shortcodes throughout
5. **Result** — what success looks like
6. **Next steps** — links to the logical next page in the journey

Admin-only content within a mixed-audience page uses `{{< admin-note >}}` to clearly delineate.

---

## 11. Out of Scope

- Comments or community features
- Algolia search (Lunr.js is sufficient)
- Content beyond OfficeConnect (e.g., broader Adaptive Planning docs)
- Localization / i18n
- PDF generation from the wiki
