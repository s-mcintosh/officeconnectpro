# OfficeConnect Pro — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build officeconnectpro.com — a Hugo/Docsy wiki with 35 hand-crafted pages documenting Workday Adaptive Planning's OfficeConnect feature for both end users and IT admins.

**Architecture:** Hugo static site using Docsy as a Hugo Module (not a submodule), dark & amber theme via SCSS overrides, task-journey IA (5 sections), GitHub Pages deployment via GitHub Actions. Content is written from scratch using the Workday Adaptive Planning PDF as source material.

**Tech Stack:** Hugo (extended, latest), Docsy v0.11+, Go (required for Hugo Modules), GitHub Actions, GitHub Pages, SCSS.

**Prerequisites:** Install [Hugo extended](https://gohugo.io/installation/) and [Go](https://go.dev/dl/) before starting Task 1. Verify with `hugo version` and `go version`.

---

## File Map

**Created in Task 1 (scaffold):**
- `go.mod` — Hugo module definition, declares Docsy dependency
- `config/_default/config.toml` — Hugo site config, module imports
- `config/_default/params.toml` — Docsy feature flags
- `config/_default/menus.toml` — top nav links
- `assets/scss/_variables_project.scss` — dark & amber color overrides
- `assets/scss/_styles_project.scss` — sidebar, navbar, step/admin-note custom CSS
- `.gitignore` — excludes public/, resources/, .superpowers/
- `.github/workflows/deploy.yml` — GitHub Actions → GitHub Pages

**Created in Task 2 (shortcodes + indexes):**
- `layouts/shortcodes/admin-note.html`
- `layouts/shortcodes/step.html`
- `content/_index.md` — homepage
- `content/get-started/_index.md`
- `content/connect/_index.md`
- `content/build-reports/_index.md`
- `content/share-publish/_index.md`
- `content/troubleshoot/_index.md`

**Created in Tasks 3–9 (all content pages):** 29 markdown files across 5 sections (listed per task).

---

## Task 1: Project Scaffold

**Files:** `go.mod`, `config/_default/config.toml`, `config/_default/params.toml`, `config/_default/menus.toml`, `assets/scss/_variables_project.scss`, `assets/scss/_styles_project.scss`, `.gitignore`, `.github/workflows/deploy.yml`

- [ ] **Step 1: Initialize Hugo module**

Working directory is `/Users/admin/officeconnectpro` (git already initialized with the design spec). Run:

```bash
hugo new site . --force --format toml
```

Then init the Hugo module:

```bash
hugo mod init github.com/officeconnectpro/docs
```

Expected: `go.mod` created with module path and Go version.

- [ ] **Step 2: Add Docsy and tidy**

```bash
hugo mod get github.com/google/docsy@v0.11.0
hugo mod tidy
```

Expected: `go.mod` updated with Docsy require line, `go.sum` created.

- [ ] **Step 3: Write config/_default/config.toml**

Delete the generated top-level `config.toml` if it exists, then:

```bash
mkdir -p config/_default
```

Create `config/_default/config.toml`:

```toml
baseURL = "https://officeconnectpro.com/"
title = "OfficeConnect Pro"
enableRobotsTXT = true
enableGitInfo = true
defaultContentLanguage = "en"

[module]
  proxy = "direct"
  [[module.imports]]
    path = "github.com/google/docsy"
    disable = false
```

- [ ] **Step 4: Write config/_default/params.toml**

Create `config/_default/params.toml`:

```toml
copyright = "OfficeConnect Pro"

github_repo = "https://github.com/officeconnectpro/docs"
github_branch = "main"

offlineSearch = true
algolia_docsearch = false
prism_syntax_highlighting = false

[params.ui]
breadcrumb_disable = false
navbar_logo = false
sidebar_menu_compact = true
sidebar_menu_foldable = true
sidebar_search_disable = false
navbar_translucent_over_cover_disable = true

[params.ui.feedback]
enable = false

[params.ui.readingtime]
enable = false
```

- [ ] **Step 5: Write config/_default/menus.toml**

Create `config/_default/menus.toml`:

```toml
[[main]]
  name = "Get Started"
  url = "/get-started/"
  weight = 10

[[main]]
  name = "Connect"
  url = "/connect/"
  weight = 20

[[main]]
  name = "Build Reports"
  url = "/build-reports/"
  weight = 30

[[main]]
  name = "Share & Publish"
  url = "/share-publish/"
  weight = 40

[[main]]
  name = "Troubleshoot"
  url = "/troubleshoot/"
  weight = 50
```

- [ ] **Step 6: Write SCSS theme overrides**

```bash
mkdir -p assets/scss
```

Create `assets/scss/_variables_project.scss`:

```scss
$primary: #f59e0b;
$secondary: #d97706;

$td-sidebar-bg-color: #18181b;
$td-sidebar-fg-color: #d4d4d8;
$td-sidebar-tree-root-font-weight: 700;

$link-color: $primary;
$link-hover-color: darken($primary, 12%);

$font-family-sans-serif: Inter, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
```

Create `assets/scss/_styles_project.scss`:

```scss
// Navbar
.td-navbar {
  background-color: #18181b !important;
}
.navbar-brand {
  font-weight: 800;
  letter-spacing: 0.5px;
  span { color: $primary; }
}

// Sidebar
.td-sidebar {
  background-color: #18181b;
}
.td-sidebar-nav__section-title a,
.td-sidebar-nav a {
  color: #d4d4d8;
  &:hover { color: $primary; }
}
.td-sidebar-nav .active > a {
  color: $primary;
  font-weight: 600;
}

// Admin note callout
.admin-note {
  border-left: 4px solid $primary;
  background: rgba(245, 158, 11, 0.08);
  padding: 0.75rem 1rem;
  margin: 1.25rem 0;
  border-radius: 0 6px 6px 0;
  strong { color: darken($primary, 10%); }
}

// Step blocks
.step-block {
  display: flex;
  gap: 1rem;
  align-items: flex-start;
  margin-bottom: 1.25rem;
  padding: 1rem;
  background: #f8f9fa;
  border-radius: 6px;
  border-left: 4px solid $primary;
}
.step-number {
  width: 2rem;
  height: 2rem;
  min-width: 2rem;
  background: $primary;
  color: #18181b;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 0.85rem;
}
.step-content {
  flex: 1;
  strong { display: block; margin-bottom: 0.25rem; }
}
```

- [ ] **Step 7: Write .gitignore**

Create `.gitignore`:

```
public/
resources/
.hugo_build.lock
node_modules/
.superpowers/
```

- [ ] **Step 8: Write GitHub Actions deploy workflow**

```bash
mkdir -p .github/workflows
```

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - uses: actions/setup-go@v5
        with:
          go-version: stable

      - uses: peaceiris/actions-hugo@v3
        with:
          hugo-version: latest
          extended: true

      - run: hugo --minify

      - uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          cname: officeconnectpro.com
```

- [ ] **Step 9: Verify the scaffold builds**

```bash
hugo --minify 2>&1
```

Expected output ends with: `Total in NNN ms` and no `ERROR` lines. A warning about missing content is fine at this stage.

- [ ] **Step 10: Commit scaffold**

```bash
git add config/ assets/ .gitignore .github/ go.mod go.sum
git commit -m "feat: Hugo/Docsy scaffold with dark & amber theme"
```

---

## Task 2: Shortcodes and Section Index Pages

**Files:** `layouts/shortcodes/admin-note.html`, `layouts/shortcodes/step.html`, `content/_index.md`, `content/get-started/_index.md`, `content/connect/_index.md`, `content/build-reports/_index.md`, `content/share-publish/_index.md`, `content/troubleshoot/_index.md`

- [ ] **Step 1: Create shortcodes directory and admin-note.html**

```bash
mkdir -p layouts/shortcodes
```

Create `layouts/shortcodes/admin-note.html`:

```html
<div class="admin-note" role="note">
  <strong>🔧 IT Admin</strong>
  {{ .Inner | markdownify }}
</div>
```

- [ ] **Step 2: Create step.html shortcode**

Create `layouts/shortcodes/step.html`:

```html
<div class="step-block">
  <div class="step-number">{{ .Get "n" }}</div>
  <div class="step-content">
    <strong>{{ .Get "title" }}</strong>
    {{ .Inner | markdownify }}
  </div>
</div>
```

- [ ] **Step 3: Write homepage content/_index.md**

```bash
mkdir -p content
```

Create `content/_index.md`:

```markdown
---
title: "OfficeConnect Pro"
linkTitle: "Home"
---

{{< blocks/cover title="OfficeConnect Documentation" image_anchor="top" height="med" color="dark" >}}
<a class="btn btn-lg btn-primary me-3 mb-4" href="/get-started/">
  Get Started <i class="fas fa-arrow-alt-circle-right ms-2"></i>
</a>
<p class="lead mt-3">Step-by-step guides for Workday Adaptive Planning's OfficeConnect add-in — for finance teams and IT admins.</p>
{{< /blocks/cover >}}

{{< blocks/section color="white" type="row" >}}
{{% blocks/feature icon="fa-rocket" title="Get Started" url="/get-started/" %}}
Install OfficeConnect and connect to your Workday instance in minutes.
{{% /blocks/feature %}}

{{% blocks/feature icon="fa-plug" title="Connect" url="/connect/" %}}
Configure tenants, Workday SSO, and multi-instance setups.
{{% /blocks/feature %}}

{{% blocks/feature icon="fa-chart-bar" title="Build Reports" url="/build-reports/" %}}
Add elements, apply filters, and create live Excel reports from Adaptive Planning data.
{{% /blocks/feature %}}
{{< /blocks/section >}}

{{< blocks/section color="light" type="row" >}}
{{% blocks/feature icon="fa-share-alt" title="Share & Publish" url="/share-publish/" %}}
Share reports via Teams, SharePoint, PowerPoint, and Word.
{{% /blocks/feature %}}

{{% blocks/feature icon="fa-wrench" title="Troubleshoot" url="/troubleshoot/" %}}
Fix common errors and get answers to the most frequent questions.
{{% /blocks/feature %}}
{{< /blocks/section >}}
```

- [ ] **Step 4: Write section index pages**

Create `content/get-started/_index.md`:

```markdown
---
title: "Get Started"
linkTitle: "Get Started"
weight: 10
description: >
  Install OfficeConnect and connect to Workday Adaptive Planning from Excel, Word, or PowerPoint.
---

OfficeConnect is a Microsoft Office add-in that pulls live data from Workday Adaptive Planning directly into Excel, Word, and PowerPoint. This section covers everything you need to get up and running — from checking system requirements to installing the add-in and verifying your version.
```

Create `content/connect/_index.md`:

```markdown
---
title: "Connect"
linkTitle: "Connect"
weight: 20
description: >
  Sign in, configure tenants, and manage how OfficeConnect connects to your Workday instance.
---

After installing OfficeConnect, you need to connect it to your Workday tenant. This section covers signing in for the first time, managing multiple instances, and — for IT administrators — deploying tenant configuration across your organization.
```

Create `content/build-reports/_index.md`:

```markdown
---
title: "Build Reports"
linkTitle: "Build Reports"
weight: 30
description: >
  Add elements, apply filters, and build live Excel reports from your Adaptive Planning data.
---

OfficeConnect's core capability is pulling live Adaptive Planning data into Excel. Learn how to use the Reporting pane, add accounts and time elements, filter data, and manage report properties.
```

Create `content/share-publish/_index.md`:

```markdown
---
title: "Share & Publish"
linkTitle: "Share & Publish"
weight: 40
description: >
  Share reports via Teams and SharePoint, and publish data into PowerPoint and Word.
---

Once your report is built, you can share it through Microsoft collaboration tools or push the live data into PowerPoint presentations and Word documents for board reports and stakeholder communications.
```

Create `content/troubleshoot/_index.md`:

```markdown
---
title: "Troubleshoot & FAQ"
linkTitle: "Troubleshoot"
weight: 50
description: >
  Fix common OfficeConnect errors and get answers to frequently asked questions.
---

Step-by-step fixes for the most common OfficeConnect issues, from installation errors to display problems and data formatting questions.
```

- [ ] **Step 5: Verify build**

```bash
hugo --minify 2>&1
```

Expected: builds with 6 pages (home + 5 sections), no `ERROR` lines.

- [ ] **Step 6: Commit**

```bash
git add layouts/ content/
git commit -m "feat: shortcodes and section index pages"
```

---

## Task 3: Get Started Section (5 pages)

**Files:** `content/get-started/what-is-officeconnect.md`, `system-requirements.md`, `install-end-user.md`, `install-admin.md`, `check-version.md`

- [ ] **Step 1: Write what-is-officeconnect.md**

Create `content/get-started/what-is-officeconnect.md`:

```markdown
---
title: "What is OfficeConnect?"
linkTitle: "What is OfficeConnect?"
weight: 1
description: >
  An overview of OfficeConnect — what it does, who it's for, and how it works with Workday Adaptive Planning.
---

OfficeConnect is a Microsoft Office add-in that streams live data from Workday Adaptive Planning directly into Excel, Word, and PowerPoint. Instead of exporting static spreadsheets, your reports stay connected to your planning instance and refresh on demand.

## What OfficeConnect does

- **In Excel:** Build financial reports by dragging and dropping accounts, time periods, versions, and organizational levels into your spreadsheet. Data refreshes from Adaptive Planning with one click.
- **In PowerPoint:** Link tables and charts from your OfficeConnect Excel workbook into presentation slides. Update a presentation for a new period by refreshing the links.
- **In Word:** Link named ranges from Excel into board reports and narratives. Qualitative text (like "increased" or "favorable") can update automatically.

## Who it's for

| Audience | How they use it |
|---|---|
| **End users** (FP&A, finance teams) | Build and refresh Excel reports, share via Teams/SharePoint, publish to PowerPoint and Word |
| **IT admins** | Install the add-in across the organization, configure tenants, manage SSO and registry deployment |

## How it works

OfficeConnect appears as an extra tab in the Excel, Word, and PowerPoint ribbons after installation. In Excel, a **Reporting pane** docks to the side of your worksheet — it contains three tabs:

- **Elements** — browse and drag accounts, time periods, versions, and levels into your report
- **Filters** — apply worksheet and workbook-level filters
- **Review** — inspect exactly which elements are affecting any cell

When you click **Refresh**, OfficeConnect queries your Workday Adaptive Planning instance and populates the connected cells with current data.

## Data sources

OfficeConnect supports two data sources:

- **Adaptive Planning** — your budgets, forecasts, and plan data from Workday Adaptive Planning
- **Financials** — general ledger data from Workday Financial Management (requires separate configuration)

## Next steps

→ [Check system requirements](/get-started/system-requirements/) before installing.
```

- [ ] **Step 2: Write system-requirements.md**

Create `content/get-started/system-requirements.md`:

```markdown
---
title: "System Requirements"
linkTitle: "System Requirements"
weight: 2
description: >
  Hardware and software prerequisites before installing OfficeConnect.
---

Verify your machine meets these requirements before installing OfficeConnect.

## Required software

All of the following must be installed before running the OfficeConnect installer:

| Software | Notes |
|---|---|
| **WebView2 Runtime** | Required for the OfficeConnect sign-in UI |
| **Microsoft .NET Framework 4.8** | [Download from Microsoft](https://dotnet.microsoft.com/download/dotnet-framework/net48) |
| **VSTO 2010** | Visual Studio Tools for Office runtime |
| **Workday Event Log Components** | Installed by the OfficeConnect setup wizard if you have admin rights |

> **Tip:** If you have administrator rights on your machine, the per-user installer handles prerequisites automatically. If you don't, ask your IT team to install these before you run OfficeConnect setup.

## Microsoft Office

- Microsoft Office (Excel, Word, PowerPoint) — 32-bit or 64-bit
- Office 365, Office 2016, Office 2019, or Office 2021 are all supported
- For large reports with many Show Details rows, 64-bit Excel is recommended for performance

## Operating system

- Windows 10 or Windows 11
- OfficeConnect is a Windows-only application

## Network

- HTTPS access to your Workday Adaptive Planning instance
- If your organization uses a proxy or network filtering, work with IT to allowlist the Workday API endpoints

## Next steps

→ [Install OfficeConnect as an End User](/get-started/install-end-user/) if you're setting up your own machine.

→ [Install OfficeConnect as an IT Admin](/get-started/install-admin/) if you're deploying to multiple users.
```

- [ ] **Step 3: Write install-end-user.md**

Create `content/get-started/install-end-user.md`:

```markdown
---
title: "Install as an End User"
linkTitle: "Install (End User)"
weight: 3
description: >
  Install OfficeConnect on your own machine without requiring IT involvement.
---

Follow these steps to install OfficeConnect on your own Windows machine. You'll need administrator rights, or IT must pre-install the prerequisites.

## Prerequisites

- All [system requirements](/get-started/system-requirements/) are met
- You have your Workday Adaptive Planning login credentials

## Steps

{{< step n="1" title="Download the installer" >}}
Go to **Product Downloads** in your Workday Adaptive Planning instance (ask your admin for the link if you don't have it). Download **OfficeConnectSetup.exe** — always use the latest version.
{{< /step >}}

{{< step n="2" title="Run the installer" >}}
Double-click `OfficeConnectSetup.exe`. If you have administrator rights on your machine, Windows will prompt you to allow the installation to run elevated — click **Yes**.

If you don't have admin rights, the installer will stop and tell you to contact IT. In that case, see [Install as an IT Admin](/get-started/install-admin/).
{{< /step >}}

{{< step n="3" title="Complete the setup wizard" >}}
Follow the on-screen prompts. The installer will:
- Install any missing prerequisites (WebView2, .NET 4.8, VSTO 2010)
- Install the OfficeConnect add-in for Excel, Word, and PowerPoint
{{< /step >}}

{{< step n="4" title="Verify the installation" >}}
Open Microsoft Excel. You should see an **OfficeConnect** tab in the ribbon between the regular Excel tabs.

Open Word and PowerPoint to verify the tab also appears there.
{{< /step >}}

## Result

The OfficeConnect tab appears in Excel, Word, and PowerPoint. You're ready to [sign in and create your first tenant](/connect/sign-in-create-tenant/).

## Troubleshooting

If the OfficeConnect tab doesn't appear after installation, see [Task Pane Not Displaying Correctly](/troubleshoot/task-pane-not-displaying/) or [Fix COM Registration Errors](/troubleshoot/com-registration-error/).

## Next steps

→ [Sign in and create your first tenant](/connect/sign-in-create-tenant/)
```

- [ ] **Step 4: Write install-admin.md**

Create `content/get-started/install-admin.md`:

```markdown
---
title: "Install as an IT Admin"
linkTitle: "Install (IT Admin)"
weight: 4
description: >
  Deploy OfficeConnect to multiple users using per-machine installation and group policy or scripts.
---

{{< admin-note >}}
This page is for IT administrators deploying OfficeConnect to multiple users or machines. End users installing on their own machine should see [Install as an End User](/get-started/install-end-user/).
{{< /admin-note >}}

## Two installation modes

| Mode | When to use |
|---|---|
| **Per-user** | Each user installs on their own workstation. Users can install future updates without admin permissions. |
| **Per-machine** | Installed once on a shared machine for all users on that computer. Requires admin permissions for all updates. |

Per-user installation is generally preferred — it lets users self-update and reduces IT overhead.

## Per-machine installation steps

{{< step n="1" title="Prepare prerequisites on target machines" >}}
Before running the per-machine installer, verify these are installed on each target machine:
- WebView2 Runtime
- Microsoft .NET Framework 4.8
- VSTO 2010 runtime
- Workday Event Log Components

Deploy these via your preferred software distribution tool (SCCM, Intune, etc.) if not already present.
{{< /step >}}

{{< step n="2" title="Run the per-machine installer" >}}
Use the **per-machine** setup file (distinct from the per-user `OfficeConnectSetup.exe`). Run it with elevated privileges:

```cmd
OfficeConnectSetup-PerMachine.exe /quiet
```

The installer creates install files, registry entries, and certificates in the machine profile rather than the user profile.
{{< /step >}}

{{< step n="3" title="Deploy tenant configuration" >}}
After installation, users need tenant details to sign in. You can push these via registry rather than having each user configure them manually.

See [Deploy Tenants via Registry](/connect/deploy-tenants-registry/) for the full registry deployment guide.
{{< /step >}}

{{< step n="4" title="Verify on a test machine" >}}
Open Excel on a test machine and confirm the OfficeConnect tab is present. Sign in with a test account and verify you can connect to the tenant.
{{< /step >}}

## Keeping OfficeConnect updated

Make sure your team updates together — users on older versions cannot open workbooks created with a newer version. Coordinate updates and deploy the latest installer to all machines at the same time.

## Next steps

→ [Deploy Tenants via Registry](/connect/deploy-tenants-registry/) — push tenant config to user machines without manual setup
```

- [ ] **Step 5: Write check-version.md**

Create `content/get-started/check-version.md`:

```markdown
---
title: "Check & Update Your Version"
linkTitle: "Check Your Version"
weight: 5
description: >
  How to check which version of OfficeConnect you have and update to the latest release.
---

Keeping OfficeConnect up to date is important — users on different versions may not be able to share workbooks. Check your version regularly and update with your team.

## Check your current version

{{< step n="1" title="Open Excel and click the OfficeConnect tab" >}}
The OfficeConnect tab appears in the Excel ribbon after installation.
{{< /step >}}

{{< step n="2" title="Open the Help menu" >}}
In the OfficeConnect tab, click the **Help** drop-down.
{{< /step >}}

{{< step n="3" title="Click About" >}}
The About dialog shows your current version number (e.g., `2026.104.3019.3004`).
{{< /step >}}

## Understand the version number

OfficeConnect version numbers follow this pattern: `YYYY.release.date.build`

Example: `2026.104.3019.3004` = 2026 release, release 104, built on the 30th of the 19th week.

## Update OfficeConnect

OfficeConnect checks for updates automatically when you sign in. If a newer version is available, you are prompted to install it.

To update manually:
1. Download the latest installer from **Product Downloads** in your Workday Adaptive Planning instance
2. Run the installer — it upgrades your existing installation in place

{{< admin-note >}}
Coordinate updates across your team. A workbook saved with a newer version of OfficeConnect cannot be opened by users on older versions. Plan a coordinated update window so everyone upgrades together.
{{< /admin-note >}}

## Next steps

→ [Sign in and create your first tenant](/connect/sign-in-create-tenant/)
```

- [ ] **Step 6: Verify build**

```bash
hugo --minify 2>&1
```

Expected: `Total in NNN ms`, 11 pages built, no `ERROR` lines.

- [ ] **Step 7: Commit**

```bash
git add content/get-started/
git commit -m "feat: Get Started section (5 pages)"
```

---

## Task 4: Connect Section (5 pages)

**Files:** `content/connect/sign-in-create-tenant.md`, `multiple-instances.md`, `workday-sso.md`, `deploy-tenants-registry.md`, `secure-workbooks.md`

- [ ] **Step 1: Write sign-in-create-tenant.md**

Create `content/connect/sign-in-create-tenant.md`:

```markdown
---
title: "Sign In & Create Your First Tenant"
linkTitle: "Sign In & Create Tenant"
weight: 1
description: >
  Sign in to OfficeConnect for the first time and configure your Workday tenant connection.
---

A **tenant** in OfficeConnect is a saved connection to a Workday instance. You create it once, and OfficeConnect remembers it for future sessions.

## What you'll need

Before you start, gather these details from your Workday administrator:

| Detail | Where to find it |
|---|---|
| **Client ID** | Workday OfficeConnect API client |
| **API Endpoint URL** | Workday OfficeConnect API client |
| **Authorization Endpoint URL** | Workday OfficeConnect API client |

## Steps

{{< step n="1" title="Open Excel and click the OfficeConnect tab" >}}
After installation, the OfficeConnect tab appears in the Excel ribbon.
{{< /step >}}

{{< step n="2" title="Click Log In" >}}
The Workday Adaptive Planning sign-in page opens in a browser panel.
{{< /step >}}

{{< step n="3" title="Click 'Log in with Workday'" >}}
This takes you to the tenant configuration screen.
{{< /step >}}

{{< step n="4" title="Enter your tenant details" >}}
Fill in the tenant form:

| Field | Example | Notes |
|---|---|---|
| **Name** | Production | A friendly name you'll see in the sign-in drop-down |
| **Data Source** | Adaptive Planning | Choose **Financials** only if you're connecting to Workday Financial Management |
| **Client ID** | `abc0MjQw...` | From your Workday API client |
| **API Endpoint URL** | `https://example.myworkday.com/ccx/api/v1/tenant` | From your Workday API client |
| **Authorization Endpoint URL** | `https://example.myworkday.com/tenant/authorize` | From your Workday API client |

Click **Save**.
{{< /step >}}

{{< step n="5" title="Sign in with your Workday credentials" >}}
After saving the tenant, the Workday sign-in page appears. Enter your Workday username and password.
{{< /step >}}

## Result

OfficeConnect connects to your tenant. The Reporting pane appears in Excel with your instance's accounts, time periods, and levels available.

The tenant name appears in the sign-in drop-down for future sessions — you won't need to re-enter these details.

## Add additional tenants (optional)

From the Log In drop-down, select **Manage Tenants** to add, edit, or remove tenants. Your organization can mix Adaptive Planning and Financials tenants.

## Next steps

→ [Work with Multiple Instances](/connect/multiple-instances/) if your organization has sandbox or multi-instance setups
```

- [ ] **Step 2: Write multiple-instances.md**

Create `content/connect/multiple-instances.md`:

```markdown
---
title: "Work with Multiple Instances"
linkTitle: "Multiple Instances"
weight: 2
description: >
  How to switch between production, sandbox, and multi-instances in OfficeConnect.
---

If your user ID has access to more than one Workday instance — a sandbox, a linked multi-instance hierarchy, or simply multiple tenants — OfficeConnect handles them through an **Instance** drop-down in the Reporting and Planning panes.

## Types of multiple instances

| Type | Description |
|---|---|
| **Sandbox** | A clone of your production instance. Use it for testing reports and what-if scenarios without affecting live data. |
| **Multi-instances** | Linked instances in a hierarchical relationship that share data through account and dimension mapping. |

## Switching instances

When your user ID has access to multiple instances, an **Instance** drop-down appears in the Reporting pane.

- The drop-down defaults to your default instance
- Select a different instance to load elements from that instance
- Once you add any elements to a worksheet, **the instance locks** for that workbook

## Key rules

| Scenario | Behavior |
|---|---|
| New workbook | Default instance selected; you can switch before adding elements |
| Existing workbook | Instance is locked — it already has elements from a specific instance |
| Multiple open workbooks | You can open workbooks connected to different instances simultaneously |
| Copy/paste between instances | Not supported — you cannot copy, cut, paste, or merge data across instances |

## Changing instance mid-session

If you're working locally in an Excel report for Instance A and then sign in to Instance B, OfficeConnect will prompt you:

> *"Log in to OfficeConnect — would you like to update this Excel report to work with the current instance?"*

If you click **No**, the file closes and unsaved changes are lost. Save your work before switching instances.

## Change your default instance

1. Click **User Settings** from the OfficeConnect ribbon
2. In the **Connection** section, select your preferred default instance
3. Click **OK**

The new default applies to all new workbooks you create.
```

- [ ] **Step 3: Write workday-sso.md**

Create `content/connect/workday-sso.md`:

```markdown
---
title: "Set Up Workday SSO"
linkTitle: "Workday SSO"
weight: 3
description: >
  Configure OfficeConnect to use Workday Single Sign-On for your organization.
---

{{< admin-note >}}
This page requires Workday Security Administrator access. End users don't need to do anything — SSO is configured at the tenant level by admins.
{{< /admin-note >}}

## What Workday SSO does for OfficeConnect

With SSO enabled, users sign in to OfficeConnect using their existing Workday credentials through your identity provider. They don't need a separate Adaptive Planning username and password.

## Prerequisites

- Workday Security Administrator role
- OfficeConnect API client set up in Workday (done before enabling SSO)

## Steps

{{< step n="1" title="Enable OfficeConnect in Workday" >}}
In Workday, run the **Enable Features After User Sync** task and enable the OfficeConnect feature for your tenant.
{{< /step >}}

{{< step n="2" title="Generate the OfficeConnect API client" >}}
In Workday, create an API client specifically for OfficeConnect. This produces:
- **Client ID**
- **Authorization Endpoint URL**
- **REST API Endpoint URL**

Record all three — users and IT will need them when configuring tenants.
{{< /step >}}

{{< step n="3" title="Assign the Access OfficeConnect permission" >}}
In Workday, ensure users who need OfficeConnect access have the **Access OfficeConnect** permission in their security permission set.
{{< /step >}}

{{< step n="4" title="Configure the Connection user setting (optional)" >}}
If your users are automatically signed in by your identity provider, enable the **Show tenant selector at sign-in** option in OfficeConnect user settings. This prompts users to select their tenant when signing in, which is useful when:
- Multiple tenants are configured for SSO
- Your identity provider auto-signs users in
- Users work with both Financials and Adaptive Planning data sources
{{< /step >}}

## Result

Users can sign in to OfficeConnect using their Workday credentials. They'll see the Workday sign-in page when they click **Log In** in the OfficeConnect tab.

## Next steps

→ [Deploy Tenants via Registry](/connect/deploy-tenants-registry/) to push tenant configuration to user machines automatically
```

- [ ] **Step 4: Write deploy-tenants-registry.md**

Create `content/connect/deploy-tenants-registry.md`:

```markdown
---
title: "Deploy Tenants via Registry"
linkTitle: "Deploy via Registry"
weight: 4
description: >
  Push OfficeConnect tenant configuration to user machines using the Windows registry.
---

{{< admin-note >}}
This is an IT Admin task. It requires access to Windows group policy, deployment scripts, or software distribution tools (e.g., SCCM, Intune).
{{< /admin-note >}}

Instead of having each user manually enter tenant details, you can deploy tenant configuration directly to the Windows registry. This is the recommended approach for organizations with many users.

## Registry locations

Choose one:

| Location | Scope |
|---|---|
| `HKEY_LOCAL_MACHINE\Software\Adaptive Insights` | All users on the machine (preferred) |
| `HKEY_CURRENT_USER\Software\Adaptive Insights` | The current user only |

## Configuration file format

Create an XML configuration file with your tenant details:

```xml
<connections>
  <connection name="Adaptive Planning - Production">
    <Type>adaptiveplanning</Type>
    <WorkdayAuthorizationUrl>https://example.myworkday.com/prodtenant/authorize</WorkdayAuthorizationUrl>
    <WorkdayRestApiUrl>https://example.myworkday.com/ccx/api/v1/prodtenant</WorkdayRestApiUrl>
    <WorkdayClientId>YOUR_CLIENT_ID_HERE</WorkdayClientId>
  </connection>
  <connection name="Adaptive Planning - Sandbox">
    <Type>adaptiveplanning</Type>
    <WorkdayAuthorizationUrl>https://example.myworkday.com/sandboxtenant/authorize</WorkdayAuthorizationUrl>
    <WorkdayRestApiUrl>https://example.myworkday.com/ccx/api/v1/sandboxtenant</WorkdayRestApiUrl>
    <WorkdayClientId>YOUR_SANDBOX_CLIENT_ID_HERE</WorkdayClientId>
  </connection>
</connections>
```

For Workday Financial Management (Financials) connections, use `<Type>financials</Type>`.

## Deployment steps

{{< step n="1" title="Add the registry key" >}}
In the desired registry hive, create the key:
`SOFTWARE\Adaptive Insights\Connections`
{{< /step >}}

{{< step n="2" title="Deploy using your preferred method" >}}
Add the XML configuration using any standard deployment method:
- **Group Policy** — create a GPO that writes the registry key on login
- **PowerShell script** — push via Intune or SCCM
- **Registry .reg file** — import on each machine

Example PowerShell snippet:
```powershell
$regPath = "HKLM:\Software\Adaptive Insights\Connections"
New-Item -Path $regPath -Force
Set-ItemProperty -Path $regPath -Name "Config" -Value (Get-Content connections.xml -Raw)
```
{{< /step >}}

{{< step n="3" title="Verify on a test machine" >}}
Open Excel on a test machine. Click **Log In** in the OfficeConnect tab. Your deployed tenant names should appear in the sign-in drop-down without the user needing to enter any details.
{{< /step >}}

## Note on authentication URLs

Authorization URLs and API endpoint URLs vary based on your Workday data center location. Get the exact URLs from your Workday Security Administrator or from the OfficeConnect API client in Workday.
```

- [ ] **Step 5: Write secure-workbooks.md**

Create `content/connect/secure-workbooks.md`:

```markdown
---
title: "Secure OfficeConnect Workbooks"
linkTitle: "Secure Workbooks"
weight: 5
description: >
  How OfficeConnect handles security, timeouts, and data clearing to protect sensitive financial data.
---

## Automatic timeout

OfficeConnect uses a session timeout to keep your reports secure. If you haven't refreshed your report in **60 minutes** (or your configured timeout period), OfficeConnect prompts for your password the next time you try to refresh.

The timeout duration is set by your Adaptive Planning administrator.

## Data clearing on save

By default, OfficeConnect **clears all data when you save** a workbook. Connected cells display a placeholder (default: `n/a`) until the next refresh. This means:

- A saved workbook sent to someone who doesn't have OfficeConnect shows placeholder text, not live financial data
- The recipient needs OfficeConnect and appropriate Adaptive Planning permissions to see actual numbers

### Change the placeholder text

{{< step n="1" title="Open User Settings" >}}
From the OfficeConnect ribbon tab, click **User Settings**.
{{< /step >}}

{{< step n="2" title="Update the security block text" >}}
On the **General** tab, find the **Security block result text** field. Enter whatever text you want (e.g., `[Refresh to load data]`).
{{< /step >}}

{{< step n="3" title="Click OK" >}}
The new text replaces `n/a` the next time you clear data or save the workbook.
{{< /step >}}

### Disable data clearing for a specific workbook

If you want a workbook to retain data on save (not recommended for sensitive data):

1. Open the workbook
2. Click **Workbook Properties** in the OfficeConnect ribbon
3. On the **General** tab, set **Clear Data** to **Never clear data upon save**

## User-based data access

OfficeConnect respects Adaptive Planning's security model. Each user sees only the data their Adaptive Planning permission set allows. A user who can only access data from a specific organizational level will only see that level's data when they refresh — even if the report template was designed with broader access.

## Sharing workbooks

See [Share Reports via Teams, SharePoint & OneDrive](/share-publish/share-teams-sharepoint-onedrive/) for guidelines on sharing workbooks through Microsoft collaboration tools.
```

- [ ] **Step 6: Verify build**

```bash
hugo --minify 2>&1
```

Expected: 16 pages built, no `ERROR` lines.

- [ ] **Step 7: Commit**

```bash
git add content/connect/
git commit -m "feat: Connect section (5 pages)"
```

---

## Task 5: Build Reports — Part 1 (5 pages)

**Files:** `reporting-pane-tour.md`, `add-elements.md`, `time-and-contexts.md`, `filter-data.md`, `cut-copy-move-elements.md`

- [ ] **Step 1: Write reporting-pane-tour.md**

Create `content/build-reports/reporting-pane-tour.md`:

```markdown
---
title: "Interface Tour: The Reporting Pane"
linkTitle: "Reporting Pane Tour"
weight: 1
description: >
  A quick tour of the OfficeConnect interface in Excel — the ribbon tab and the Reporting pane.
---

OfficeConnect adds two things to Excel: a **ribbon tab** and a **Reporting pane** that docks to the side of your worksheet.

## The OfficeConnect ribbon tab

The OfficeConnect tab appears between your standard Excel tabs. Key buttons include:

| Button | What it does |
|---|---|
| **Log In / Log Out** | Connect to or disconnect from your Workday tenant |
| **Refresh** | Pull the latest data from Adaptive Planning into all connected cells |
| **Show Reporting Pane** | Toggle the Reporting pane open or closed |
| **Workbook Properties** | Set rounding, data clearing, and filter defaults for the workbook |
| **User Settings** | Set your personal defaults (rounding, default instance, etc.) |
| **Find / Replace** | Find and replace elements across sheets |
| **Labels** | Add dynamic text labels (report date, level name, etc.) |
| **Help** | Access version info, documentation, and the troubleshooting tool |

## The Reporting pane

The Reporting pane docks to the right side of your worksheet by default. It has three tabs:

### Elements tab

Displays the full hierarchy of your Adaptive Planning instance:

- **Accounts** — GL accounts, custom accounts, metric accounts, modeled accounts
- **Time** — calendar years, quarters, months; also components and contexts
- **Level** — your organization's hierarchy (company, division, cost center, etc.)
- **Versions** — actuals and planning versions
- **Currencies** — if multi-currency is enabled
- **Custom Dimensions** — any additional dimensions in your model

Browse by expanding nodes in the tree. Drag elements into your worksheet, or right-click and select **Apply to Selection**.

### Filters tab

Apply worksheet-level or workbook-level filters. Use the **Enable Filters** toggle to activate or deactivate them without losing your selections.

### Review tab

Select a cell, row, or column and the Review tab shows exactly which elements are affecting that data point — broken down by Net, Row, Column, Worksheet filters, Workbook filters, and User Defaults.

## Undocking the Reporting pane

Click the icon in the upper-right corner of the Reporting pane and select **Move** to undock it. Drag it anywhere, or hover at an edge of the worksheet to re-dock it.

If you lose a floating pane, click **Show Reporting Pane** in the OfficeConnect ribbon — it will reappear.

## Next steps

→ [Add Elements to Rows, Columns & Cells](/build-reports/add-elements/) to start building your first report
```

- [ ] **Step 2: Write add-elements.md**

Create `content/build-reports/add-elements.md`:

```markdown
---
title: "Add Elements to Rows, Columns & Cells"
linkTitle: "Add Elements"
weight: 2
description: >
  How to drag accounts, time periods, versions, and levels into your Excel report.
---

Elements are the building blocks of an OfficeConnect report. You add them to rows, columns, or cells in your worksheet to define what data appears at each intersection.

> **Best practice:** Add elements to entire rows and columns rather than individual cells. When applied to a row or column, a bolded (parent) element also expands its children — each child gets its own row or column automatically.

## Basic steps

{{< step n="1" title="Select your target in the grid" >}}
Click to select the cells, rows, or columns where you want data to appear. To select an entire row or column, click the row number or column letter.
{{< /step >}}

{{< step n="2" title="Open the Elements tab in the Reporting pane" >}}
Click **Show Reporting Pane** if the pane is hidden, then click the **Elements** tab.
{{< /step >}}

{{< step n="3" title="Browse to the element you want" >}}
Expand the element tree to find what you need:
- **Accounts** → expand to find specific accounts or account groups
- **Time** → expand to find years, quarters, or months
- **Level** → find your organizational level
- **Versions** → select actuals, budget, or forecast versions
{{< /step >}}

{{< step n="4" title="Apply the element" >}}
Use any of these methods:
- **Drag and drop** the element onto your selected row, column, or cell
- **Right-click** the element → **Apply to Selection**
- Click the element and click **Apply to Selection** in the Elements pane toolbar
{{< /step >}}

{{< step n="5" title="Click Refresh" >}}
Click **Refresh** in the OfficeConnect ribbon to load the data.
{{< /step >}}

## Add multiple elements to one row or column

1. Select the target row or column
2. Hold **Ctrl** and click each element you want
3. Drag them all at once into the selection
4. Click **Refresh**

All selected elements populate into the single row or column. Data rolls up by the elements.

## Expand and collapse elements

In the Elements pane, right-click a parent element:
- **Expand All** — shows all children and descendants of that element
- **Collapse All** — hides children, showing only the top-level item and its siblings

## Element groups

Applying a bolded parent element creates an **element group** — each child gets its own row or column and the report updates dynamically when your Adaptive Planning structure changes. See [Create and Manage Element Groups](/build-reports/add-elements/) for details.

## Next steps

→ [Work with Time & Contexts](/build-reports/time-and-contexts/) to add time periods and period-to-date comparisons
```

- [ ] **Step 3: Write time-and-contexts.md**

Create `content/build-reports/time-and-contexts.md`:

```markdown
---
title: "Work with Time & Contexts"
linkTitle: "Time & Contexts"
weight: 3
description: >
  Add time periods to your report and use contexts like YTD, QTD, and Beginning Balance.
---

Time elements define which periods display in your report. Contexts add a calculation lens to those periods — like showing the year-to-date total instead of a single month's value.

## Time element types

| Type | Description | Example |
|---|---|---|
| **Absolute time** | A fixed, named period | `FY 2025`, `Q1 2025`, `Jan 2025` |
| **Relative time** | A period relative to today's date | `Current Month`, `Prior Year` |
| **Components** | Year/quarter/month components that combine at their intersection | Apply `FY 2025` to a row and `Q3` to a column → resolves to Q3 of FY 2025 |

## Add a time element

{{< step n="1" title="Select a column (or row)" >}}
Time is most commonly applied to columns so each column shows a different period.
{{< /step >}}

{{< step n="2" title="In the Elements tab, expand Time" >}}
Expand the calendar hierarchy to find the period you want: Year → Quarter → Month.
{{< /step >}}

{{< step n="3" title="Drag the time element to your selection" >}}
Drop it onto the selected column. Click **Refresh**.
{{< /step >}}

## Add a context

Contexts layer a calculation on top of a time element. You apply a context in the same location as the time element, or as a worksheet/workbook filter.

{{< step n="1" title="In the Elements tab, expand Time → Contexts" >}}
Available contexts depend on your calendar configuration.
{{< /step >}}

{{< step n="2" title="Drag the context to the same column, row, or cell as your time element" >}}
Or apply it to a cell within the time element's column or row.
{{< /step >}}

{{< step n="3" title="Refresh" >}}
The column now shows the context calculation for that time period.
{{< /step >}}

## Common contexts explained

| Context | What it shows |
|---|---|
| **Beginning Balance** | The balance at the start of the time period (= end of prior period) |
| **YTD** | Year-to-date: sum from the start of the fiscal year to the end of this period |
| **YTD Balance** | The balance as of the last month of the prior fiscal year |
| **QTD** | Quarter-to-date: sum from the start of the quarter to the end of this period |
| **QTD Balance** | The balance as of the last month of the prior quarter |

> **Best practice:** For period-to-date contexts, use time elements *smaller* than the context period. Use QTD or YTD with monthly time elements. Using Month-to-Date with a quarter element doesn't make logical sense and OfficeConnect will correct it.

## Relative time

Relative time elements automatically advance as time passes. For example, **Current Month** always shows the current calendar month when you refresh — no manual updates needed for rolling reports.

To lock a relative date (make it absolute), right-click the time element in the **Review** pane and select **Switch to Absolute**.

## Next steps

→ [Filter Your Data](/build-reports/filter-data/) to limit report data by level, version, or custom dimension
```

- [ ] **Step 4: Write filter-data.md**

Create `content/build-reports/filter-data.md`:

```markdown
---
title: "Filter Your Data"
linkTitle: "Filter Data"
weight: 4
description: >
  Apply worksheet and workbook filters to limit which data appears in your report.
---

Filters let you restrict report data by accounts, levels, versions, currencies, attributes, or custom dimensions — without adding those elements to rows or columns.

## Worksheet vs workbook filters

| Filter type | Scope | Precedence |
|---|---|---|
| **Worksheet filter** | Applies to one sheet only | Overrides workbook filters |
| **Workbook filter** | Applies to all sheets in the workbook | Lower precedence than worksheet filters |

## Apply a worksheet filter

{{< step n="1" title="Open the Filters tab in the Reporting pane" >}}
In the Reporting pane, click the **Filters** tab.
{{< /step >}}

{{< step n="2" title="Click Worksheet Filters" >}}
The Worksheet Filters dialog opens. It shows any previously selected filters.
{{< /step >}}

{{< step n="3" title="Search or browse for elements to filter by" >}}
Example: To filter by two specific levels, expand the Level hierarchy and select `Company A` and `Company B`.
{{< /step >}}

{{< step n="4" title="Click OK" >}}
Your selected elements appear in the Filters tab as a subset.
{{< /step >}}

{{< step n="5" title="Enable the filters" >}}
In the Filters tab, click **Enable Filters**, then check the specific elements you want active.
{{< /step >}}

{{< step n="6" title="Refresh" >}}
The report now shows data only for the filtered elements.
{{< /step >}}

## Turn filters off without losing selections

In the Filters tab, uncheck **Enable Filters**. Your filter selections are remembered — they're just inactive. Re-check **Enable Filters** to reapply them later.

## Multi-select filters

You can select multiple elements at once by right-clicking an element in the filter list and using the context menu. When a parent is in **Collapse All** state, selecting it selects all its descendants too.

## Review active filters

To verify which filters are active on a worksheet:
1. In the Reporting pane, click the **Review** tab
2. Expand **Worksheet** to see active worksheet filters
3. Expand **Workbook** to see active workbook filters

Applied filters are listed under **Elements** in each section.

## Next steps

→ [Cut, Copy & Move Elements](/build-reports/cut-copy-move-elements/) to rearrange elements in your report
```

- [ ] **Step 5: Write cut-copy-move-elements.md**

Create `content/build-reports/cut-copy-move-elements.md`:

```markdown
---
title: "Cut, Copy & Move Elements"
linkTitle: "Cut, Copy & Move"
weight: 5
description: >
  How to move OfficeConnect elements within and between rows, columns, and cells.
---

> **Important:** Always use OfficeConnect's own cut/copy/paste commands — not Excel's standard Ctrl+C/Ctrl+V. Excel's clipboard doesn't carry the OfficeConnect element metadata; only OfficeConnect commands do.

## Three ways to cut, copy, and paste

**Ribbon buttons:** Use the functions in the **OfficeConnect** tab, not the Home tab.

**Right-click menu:** Right-click the cell, row, or column → **OfficeConnect** → **Cut Elements** or **Copy Elements**, then **Paste Elements**.

**Keyboard shortcuts:**
| Action | Shortcut |
|---|---|
| Cut | `Shift + Ctrl + Alt + X` |
| Copy | `Shift + Ctrl + Alt + C` |
| Paste | `Shift + Ctrl + Alt + V` |

## What you can paste where

| Cut/Copy from | Can paste into |
|---|---|
| Cells | Cells, rows, or columns |
| Rows | Rows or columns |
| Columns | Rows or columns |

## Steps

{{< step n="1" title="Select the source" >}}
Select the entire row, column, or cell containing the elements you want to move. Highlight the full row or column — not just a few cells within it.
{{< /step >}}

{{< step n="2" title="Cut or copy" >}}
Use the ribbon, right-click menu, or keyboard shortcut to cut or copy.
{{< /step >}}

{{< step n="3" title="Select the destination" >}}
Highlight the entire destination row, column, or cell.
{{< /step >}}

{{< step n="4" title="Paste" >}}
Use the ribbon, right-click menu, or keyboard shortcut to paste.
{{< /step >}}

## Append vs replace when dragging

When you drag and drop an element into a location that already has an element:

- OfficeConnect asks whether to **Append** (add to existing) or **Replace** (overwrite existing)
- Choose **Replace** to swap one element for another
- Choose **Append** to combine elements at that location

## Note on merged cells

If your workbook uses merged cells, OfficeConnect cannot update or refresh elements applied to those merged cells. Avoid merging cells that contain OfficeConnect elements.
```

- [ ] **Step 6: Verify build**

```bash
hugo --minify 2>&1
```

Expected: 21 pages built, no errors.

- [ ] **Step 7: Commit**

```bash
git add content/build-reports/reporting-pane-tour.md content/build-reports/add-elements.md content/build-reports/time-and-contexts.md content/build-reports/filter-data.md content/build-reports/cut-copy-move-elements.md
git commit -m "feat: Build Reports section part 1 (5 pages)"
```

---

## Task 6: Build Reports — Part 2 (5 pages)

**Files:** `review-applied-elements.md`, `workbook-worksheet-properties.md`, `repeating-reports.md`, `financials-vs-adaptive-planning.md`, `cell-explorer-drill-down.md`

- [ ] **Step 1: Write review-applied-elements.md**

Create `content/build-reports/review-applied-elements.md`:

```markdown
---
title: "Review & Verify Applied Elements"
linkTitle: "Review Applied Elements"
weight: 6
description: >
  Use the Review tab to see exactly which elements are affecting any cell, row, or column.
---

The **Review tab** in the Reporting pane shows you a complete picture of what's driving data in your report. Use it to verify elements are applied correctly before sharing or distributing a report.

## What the Review tab shows

Select a cell, row, or column, then click the **Review** tab. The sections you see depend on your selection:

| Section | Shown when | What it displays |
|---|---|---|
| **Net** | Cell selected | All elements *actively affecting* that cell's data — the combined result of all applied elements |
| **Rows** | Cell or row selected | All elements applied to that row |
| **Columns** | Cell or column selected | All elements applied to that column |
| **Worksheet** | Cell selected | Active worksheet filters |
| **Workbook** | Cell selected | Active workbook filters |
| **User Defaults** | Cell selected | Default elements from your User Settings |

> **Note:** The Net section only appears for single-cell selections. It's the most useful for diagnosing unexpected data — it shows what's *actually* driving the number.

## Basic steps

{{< step n="1" title="Click Refresh" >}}
Make sure the data is current before reviewing.
{{< /step >}}

{{< step n="2" title="Select a single cell, row, or column" >}}
The Review tab only shows useful information for a single selection — don't select multiple cells.
{{< /step >}}

{{< step n="3" title="Click the Review tab" >}}
In the Reporting pane, click **Review**.
{{< /step >}}

{{< step n="4" title="Expand sections to investigate" >}}
Click any section header (Net, Rows, Columns, etc.) to expand it and see the elements listed.
{{< /step >}}

## Review element sources

If the Net section shows an unexpected element, expand **Rows** and **Columns** to see where it was added. Expanding **Worksheet** and **Workbook** shows if a filter is contributing.

## Switch time elements between relative and absolute

From the Review tab, you can also change how time elements behave:
1. Right-click the time element metadata line
2. Select **Switch to Absolute** or **Switch to Relative**
3. Refresh to see the effect

## Identify element groups

If a row or column is part of an expansion (element group), the Review tab shows an expansion `[+]` icon next to the element.
```

- [ ] **Step 2: Write workbook-worksheet-properties.md**

Create `content/build-reports/workbook-worksheet-properties.md`:

```markdown
---
title: "Workbook & Worksheet Properties"
linkTitle: "Workbook Properties"
weight: 7
description: >
  Configure rounding, data clearing, filters, and display options for your reports.
---

OfficeConnect has three levels of settings that control report behavior, each overriding the one above it:

1. **User Settings** — your personal defaults for all new workbooks
2. **Workbook Properties** — settings for the current workbook (overrides User Settings)
3. **Selection Properties** — settings for a specific row, column, or cell (overrides Workbook Properties)

## User Settings

Access via **OfficeConnect ribbon → User Settings**.

| Setting | Default | Description |
|---|---|---|
| **Round to** | Thousands | How to round numbers. Options: Hundreds, Thousands, Ten Thousands, …, Billions, No Rounding |
| **Show zero in cells with no data** | On | Shows `0` instead of blank for empty cells |
| **Security block result text** | `n/a` | The placeholder text shown in linked cells after data is cleared on save |
| **Show refresh errors** | On | Shows a list of cell errors after refresh |
| **Show refresh warnings** | On | Shows a list of warnings after refresh |

User Settings apply to all new workbooks you create. They don't change existing open workbooks.

## Workbook Properties

Access via **OfficeConnect ribbon → Workbook Properties**.

### General tab

| Setting | Description |
|---|---|
| **Clear Data** | *Always clear data upon save* — replaces data with security text on save (recommended for sensitive data). *Never clear data upon save* — retains data when saving. |
| **Include update groups in refresh** | Auto-updates element groups when you refresh |

### Filters tab

| Setting | Description |
|---|---|
| **Enable filters** | Toggles workbook-level filters on/off |
| **Display unknown elements** | Shows elements that aren't accessible or don't exist in the hierarchy for a given date |

### Format tab

| Setting | Description |
|---|---|
| **Round to** | Overrides User Settings rounding for this workbook only. Applies to all sheets. After changing, click **Refresh > All Sheets**. |
| **Report date** | Sets the date displayed by `{Report Date}` labels |

## Selection Properties

Access by right-clicking a row, column, or cell → **OfficeConnect → Row/Column/Cell Properties**.

Selection Properties override Workbook Properties for the selected area. Useful for:
- Suppressing rounding on specific cells that contain percentages
- Controlling row/column display (hide zeros, hide blanks) for part of a report

## Precedence summary

`Selection Properties > Workbook Properties > User Settings`

The most specific setting always wins.
```

- [ ] **Step 3: Write repeating-reports.md**

Create `content/build-reports/repeating-reports.md`:

```markdown
---
title: "Create Repeating Reports"
linkTitle: "Repeating Reports"
weight: 8
description: >
  Automatically generate one copy of a report per department, region, or any other level.
---

The **Repeating Reports** feature copies a finished report worksheet once for each element you choose — for example, one sheet per cost center or one sheet per region. Each copy is automatically filtered to show data for its element.

## What it does

When you create repeating reports, OfficeConnect:
- Copies the worksheet for each selected element
- Applies one element as a filter to each copy
- Optionally refreshes each copy automatically
- Names each worksheet based on your naming convention
- Preserves all Excel formatting, formulas, and OfficeConnect metadata

Once created, each repeating report is **independent** — it's not linked to the original. To update them with new report formatting, delete and recreate them.

## Steps

{{< step n="1" title="Build and finalize the original report" >}}
Complete the report on one worksheet — all elements applied, formatting done, formulas in place. This is the template that gets copied.

Optionally shorten the worksheet name (e.g., rename `Profit and Loss` to `P&L`) — the copies will be named based on this.
{{< /step >}}

{{< step n="2" title="(Optional) Add a repeating report label" >}}
If you want each copy to show the name of its filter element (e.g., the department name), add a label:

1. Select the cell where you want the label
2. Click **Labels** in the OfficeConnect ribbon
3. Set **Label Type** to `System Variable` and **Label Type Value** to `{Repeating Report Element}`
4. Click **Add Expression**

This label is blank on the original but populates on each copy during the creation process.
{{< /step >}}

{{< step n="3" title="Open Repeating Reports" >}}
In the OfficeConnect ribbon, click **Repeating Reports**.
{{< /step >}}

{{< step n="4" title="Select the filter element type" >}}
Choose what to copy by — e.g., filter by Level to create one sheet per organizational level.
{{< /step >}}

{{< step n="5" title="Select which elements to include" >}}
Check the specific elements (levels, versions, etc.) you want copies for.
{{< /step >}}

{{< step n="6" title="Set the naming convention and refresh option" >}}
Define how worksheets will be named. Optionally choose to refresh all copies immediately after creation.
{{< /step >}}

{{< step n="7" title="Click Create" >}}
OfficeConnect creates one worksheet per selected element and refreshes each one (if you chose auto-refresh).
{{< /step >}}

## Updating repeating reports

Repeating reports don't stay linked to the original. To incorporate structural changes to the report:
1. Delete the existing repeating report worksheets
2. Update the original template
3. Re-run the Repeating Reports process
```

- [ ] **Step 4: Write financials-vs-adaptive-planning.md**

Create `content/build-reports/financials-vs-adaptive-planning.md`:

```markdown
---
title: "Financials vs. Adaptive Planning Data Sources"
linkTitle: "Data Source Differences"
weight: 9
description: >
  Key differences in OfficeConnect behavior depending on whether you're using the Adaptive Planning or Financials data source.
---

OfficeConnect supports two data sources. Most organizations use **Adaptive Planning** (budget and forecast data). Organizations using Workday Financial Management also have access to the **Financials** data source (general ledger actuals).

The data source is set when you configure your tenant. Some OfficeConnect features behave differently depending on which source is active.

## Feature comparison

| Feature | Adaptive Planning | Financials |
|---|---|---|
| **Elements hierarchy** | Accounts, Level, Custom Dimensions | Ledger Accounts, Company, Dimensions |
| **Minimum valid intersection** | Version + Level + Time + Account | Version + Company + Time + Ledger Account |
| **Default rounding** | Thousands | No Rounding |
| **Make new time elements relative** | On by default | Off by default |
| **Always clear data upon save** | On by default | Off by default |
| **Element groups** | Available | Not available |
| **Cell Details** | Explore Cell (drill into cell data) | Show Details (contributing journal lines; drill through to Workday) |
| **Default version** | Depends on your model | Actuals |
| **Exclude elimination on expand** | Not available | Available (in user settings and Expand dialog) |

## Which data source am I using?

Check your tenant configuration: in the OfficeConnect sign-in drop-down, each tenant shows its data source type.

## Effective dates (Financials only)

When using the Financials data source, you can select an **effective date** for your report. This reflects your organization's structure as of that date — useful for reporting after reorganizations.

{{< admin-note >}}
Effective date support requires configuration in Workday's financial reporting data model. Contact your Workday Security Administrator to verify it's enabled.
{{< /admin-note >}}

## Alternate hierarchies (Financials only)

If your administrator configures alternate hierarchies for dimensions in the financial reporting data model, you can select different hierarchy views in your OfficeConnect report — useful for viewing company, ledger account, or cost center dimensions from multiple perspectives.
```

- [ ] **Step 5: Write cell-explorer-drill-down.md**

Create `content/build-reports/cell-explorer-drill-down.md`:

```markdown
---
title: "Cell Explorer & Drill-Down"
linkTitle: "Cell Explorer"
weight: 10
description: >
  Explore the data behind any cell to understand what's driving the numbers.
---

When a number in your report looks unexpected, **Explore Cell** lets you drill into the contributing details to find the source.

## What Explore Cell shows

For any cell with data, Explore Cell reveals:

| Detail | Description |
|---|---|
| **Contributing rows** | The specific data intersections driving the value |
| **Account details** | Rollup values and links to child accounts |
| **Level details** | Rollup values and links to child levels |
| **Time details** | Breakdown by time period |
| **Audit trail** | Change history (if Audit Trail is enabled in Adaptive Planning) |
| **Other sheets** | Links to other sheets that show the same value |
| **Source drills** | Drill into Transactions, Workday objects, or NetSuite (if configured) |

> **Note:** Explore Cell applies to the **Adaptive Planning** data source. For the **Financials** data source, use **Show Details** instead, which shows contributing journal line and plan line details.

## Use Explore Cell

{{< step n="1" title="Select the cell you want to investigate" >}}
Click on any cell in your OfficeConnect report that contains data.
{{< /step >}}

{{< step n="2" title="Right-click and select Explore Cell" >}}
Or use the **Explore Cell** button in the OfficeConnect ribbon.
{{< /step >}}

{{< step n="3" title="Review the contributing details" >}}
Explore Cell opens showing the breakdown. Expand sections to drill deeper — you can open nested Explore Cell views to follow the data chain.
{{< /step >}}

## Zeros and blanks in Explore Cell

Explore Cell automatically suppresses rows with all zeros or blanks by default — only rows that actually contribute to the value are shown. To see zero rows:
1. Clear the **Suppress Rows if all Zeros or Blanks** setting on the Explore Cell page
2. Note: This setting resets each time you launch Explore Cell

## Show Details (Financials data source)

For Financials data source users, **Show Details** is the equivalent feature:
1. Right-click any report cell with data
2. Select **Show Details**
3. A new Excel worksheet opens showing contributing journal lines and plan lines
4. From there you can drill through to Workday to view related journals and transactions

> For large worksheets, Show Details performs better with 64-bit Excel.
```

- [ ] **Step 6: Verify build**

```bash
hugo --minify 2>&1
```

Expected: 26 pages built, no errors.

- [ ] **Step 7: Commit**

```bash
git add content/build-reports/review-applied-elements.md content/build-reports/workbook-worksheet-properties.md content/build-reports/repeating-reports.md content/build-reports/financials-vs-adaptive-planning.md content/build-reports/cell-explorer-drill-down.md
git commit -m "feat: Build Reports section part 2 (5 pages)"
```

---

## Task 7: Share & Publish Section (3 pages)

**Files:** `share-teams-sharepoint-onedrive.md`, `officeconnect-for-powerpoint.md`, `officeconnect-for-word.md`

- [ ] **Step 1: Write share-teams-sharepoint-onedrive.md**

Create `content/share-publish/share-teams-sharepoint-onedrive.md`:

```markdown
---
title: "Share Reports via Teams, SharePoint & OneDrive"
linkTitle: "Share via Teams & SharePoint"
weight: 1
description: >
  Save and share OfficeConnect workbooks through Microsoft Teams, SharePoint, or OneDrive.
---

You can save OfficeConnect reports to shared locations in Microsoft Teams, SharePoint, or OneDrive so multiple colleagues can access them.

> **Limitation:** OfficeConnect does not support multiple users editing the same file simultaneously. There's always a risk of data loss if two people work on the same file at the same time.

## How to share a report

{{< step n="1" title="Finish building and refreshing your report" >}}
Make sure the report is complete and you've clicked **Refresh** to load the latest data.
{{< /step >}}

{{< step n="2" title="Save to a shared location" >}}
Use Excel's standard **File → Save As** to save the workbook to a Teams channel folder, SharePoint document library, or OneDrive shared folder.
{{< /step >}}

{{< step n="3" title="Share the link" >}}
Use the Teams or SharePoint sharing feature to send a link to colleagues. They can open the workbook and refresh it themselves if they have OfficeConnect installed and appropriate Adaptive Planning permissions.
{{< /step >}}

## What recipients need

For a colleague to open and refresh a shared OfficeConnect report, they need:
- OfficeConnect installed (same version or newer)
- Access to the same Workday Adaptive Planning tenant
- Appropriate Adaptive Planning permissions for the data in the report

## Concurrent access risks

| Scenario | Risk |
|---|---|
| User A opens and signs in; User B opens read-only | Low risk — User B sees the file but can't save changes |
| Both users sign in and make changes | High risk — the last save wins; earlier changes can be overwritten |

**Best practice:** Treat shared OfficeConnect files like shared Excel files — coordinate with colleagues to avoid simultaneous editing.

## Data clearing on shared files

By default, OfficeConnect clears data on save (replacing it with `n/a`). When someone without OfficeConnect opens a shared file, they'll see placeholder text rather than financial data. This is intentional — it prevents sensitive data from being visible to users who haven't authenticated.

Recipients with OfficeConnect can click **Refresh** to load their data view.

## Next steps

→ [OfficeConnect for PowerPoint](/share-publish/officeconnect-for-powerpoint/) — embed live charts and tables in presentations
```

- [ ] **Step 2: Write officeconnect-for-powerpoint.md**

Create `content/share-publish/officeconnect-for-powerpoint.md`:

```markdown
---
title: "OfficeConnect for PowerPoint"
linkTitle: "For PowerPoint"
weight: 2
description: >
  Link live data from your OfficeConnect Excel workbook into PowerPoint slides.
---

OfficeConnect for PowerPoint lets you link tables and charts from your Excel workbook directly into PowerPoint slides. When the underlying Excel data refreshes, you can update the presentation with one click — no copy-pasting.

## How it works

1. You define **named ranges** in your OfficeConnect Excel workbook (a named range is a labeled group of cells)
2. In PowerPoint, you link those named ranges into slides as tables or charts
3. When you're ready to update the presentation (e.g., for a new reporting period), refresh the links

## Start OfficeConnect for PowerPoint

{{< step n="1" title="Open PowerPoint" >}}
After OfficeConnect is installed, an **OfficeConnect** tab appears in PowerPoint's ribbon.
{{< /step >}}

{{< step n="2" title="Click Log In" >}}
Enter your Adaptive Planning credentials, or click **Log in with Workday**. If you're already signed in to OfficeConnect for Excel, PowerPoint logs you in automatically.
{{< /step >}}

## Create a named range in Excel

Before linking to PowerPoint, you need to name the range in Excel:

{{< step n="1" title="Select the cells in your OfficeConnect Excel report" >}}
Select the table or chart data range you want to embed in PowerPoint.
{{< /step >}}

{{< step n="2" title="Click in the Name Box" >}}
The Name Box is the cell reference field at the top-left of the Excel grid (usually shows something like `A1`). Click it so the contents are selected.
{{< /step >}}

{{< step n="3" title="Type a name and press Enter" >}}
Enter a descriptive name (e.g., `Q3_Revenue_Summary`) with no spaces. The named range is created.
{{< /step >}}

## Link a named range into a PowerPoint slide

{{< step n="1" title="In PowerPoint, navigate to the slide" >}}
Go to the slide where you want to insert the linked data.
{{< /step >}}

{{< step n="2" title="In the OfficeConnect tab, click Link from Excel" >}}
Browse to your OfficeConnect Excel workbook and open it.
{{< /step >}}

{{< step n="3" title="Select the named range to link" >}}
Choose from the available named ranges in the workbook.
{{< /step >}}

{{< step n="4" title="The table or chart appears on the slide" >}}
It's now a live link — formatted exactly as it appears in Excel.
{{< /step >}}

## Update for a new period

When you're ready to update the presentation (e.g., for the next month's board deck):

1. Update the data in your OfficeConnect Excel workbook (change the time element or refresh)
2. In PowerPoint, go to the OfficeConnect tab and click **Refresh Links**
3. Go to the linked slides and verify the data has updated
4. Save the presentation

## Disconnect a link

If you want to stop a slide's data from updating:
1. In PowerPoint, go to **File → Info → Edit Links to Files**
2. Select the link you want to disconnect
3. Click **Break Link**

The table or chart remains as a static object on the slide.
```

- [ ] **Step 3: Write officeconnect-for-word.md**

Create `content/share-publish/officeconnect-for-word.md`:

```markdown
---
title: "OfficeConnect for Word"
linkTitle: "For Word"
weight: 3
description: >
  Link live financial data from OfficeConnect Excel into Word reports and board narratives.
---

OfficeConnect for Word lets you embed live tables and single-cell values from your OfficeConnect Excel workbook into Word documents. Board reports, investor letters, and executive narratives can update automatically when the underlying data changes.

## What you can link

- **Tables** — complete tables from named ranges in Excel, formatted exactly as they appear in Excel
- **Single cells** — individual values (e.g., a total revenue figure or a percentage)
- **Qualitative text** — words like "increased" or "decreased" that update based on cell values

## Start OfficeConnect for Word

{{< step n="1" title="Open Word" >}}
After OfficeConnect is installed, an **OfficeConnect** tab appears in Word's ribbon. An **OfficeConnect links pane** docks to the left side.
{{< /step >}}

{{< step n="2" title="Click Log In" >}}
Enter your Adaptive Planning credentials, or click **Log in with Workday**. If you're already signed in to OfficeConnect for Excel, Word logs you in automatically.
{{< /step >}}

## Connect to an Excel workbook

{{< step n="1" title="In the OfficeConnect tab, click Link to Workbook" >}}
Browse to and open your OfficeConnect Excel workbook. The workbook's named ranges appear in the OfficeConnect links pane under **Table Links** (multi-cell ranges) and **Single Links** (single cells).
{{< /step >}}

## Link a table into Word

{{< step n="1" title="Place your cursor in the document" >}}
Click where you want the table to appear.
{{< /step >}}

{{< step n="2" title="In the links pane, find the table link" >}}
Right-click the named range under **Table Links** and select **Apply to Selection**.
{{< /step >}}

The table appears formatted exactly as it looks in Excel. No reformatting required (unless the table is wider than the Word document margins, in which case OfficeConnect proportionally scales it down).

## Refresh the document for a new period

When source data changes (e.g., for a new month's report):

{{< step n="1" title="Update the linked Excel workbook" >}}
In Excel, update time elements or refresh from Adaptive Planning.
{{< /step >}}

{{< step n="2" title="In Word, click Refresh in the OfficeConnect tab" >}}
All linked data updates from the Excel workbook.
{{< /step >}}

## Change the source file for a new period

If you save your Excel workbook under a new filename for each period (e.g., `Board_Report_Q3_2025.xlsx`):

1. In the OfficeConnect tab, click **Manage Links**
2. Check the links you want to update
3. Click **Change Source** and browse to the new file
4. Click **Close**

Because the new file is a copy of the old one, the named ranges are identical and the links transfer cleanly.

## Disconnect a link

1. In the OfficeConnect tab, click **Manage Links**
2. Check the link(s) to disconnect
3. Click **Break Link**

The data remains in the document as static text/table, but no longer updates from Excel.
```

- [ ] **Step 4: Verify build**

```bash
hugo --minify 2>&1
```

Expected: 29 pages built, no errors.

- [ ] **Step 5: Commit**

```bash
git add content/share-publish/
git commit -m "feat: Share & Publish section (3 pages)"
```

---

## Task 8: Troubleshoot Section — Part 1 (6 pages)

**Files:** `com-registration-error.md`, `update-errors.md`, `task-pane-not-displaying.md`, `numbers-not-shifting.md`, `suppress-zeros-blanks.md`, `remove-elements.md`

- [ ] **Step 1: Write com-registration-error.md**

Create `content/troubleshoot/com-registration-error.md`:

```markdown
---
title: "Fix COM Registration Errors"
linkTitle: "COM Registration Error"
weight: 1
description: >
  How to resolve COM registration errors when installing or updating OfficeConnect.
---

**Symptom:** You receive an error like the following when trying to install or update OfficeConnect:

```
System.InvalidCastException: Unable to cast COM object of type 'System.__ComObject'
to interface type 'Microsoft.Office.Core.IRibbonUI'.
```

## Why this happens

OfficeConnect is an Excel COM add-in that relies on Excel objects registered correctly by your Microsoft Office installation. This error occurs when:

- Excel's COM objects aren't registered correctly
- You have multiple versions of Microsoft Office installed (e.g., Project 2016 and Excel 2013), leading to conflicting versions of the MS-VSTO library

## Fix option 1: Repair Microsoft Office

Many users resolve this by repairing the Office installation:

{{< step n="1" title="Open Windows Settings" >}}
Go to **Start → Settings → Apps & Features**.
{{< /step >}}

{{< step n="2" title="Find Microsoft Office and click Modify" >}}
Select **Microsoft Office** from the list and click **Modify**.
{{< /step >}}

{{< step n="3" title="Choose Online Repair" >}}
Select **Online Repair** (not Quick Repair) and click **Repair**. This fully reinstalls Office components and re-registers COM objects.
{{< /step >}}

{{< step n="4" title="Try installing OfficeConnect again" >}}
After the repair completes, run the OfficeConnect installer again.
{{< /step >}}

## Fix option 2: Registry key correction

If the repair doesn't work, the troubleshooting tool will identify the specific registry key causing the problem. Your IT department can make adjustments to the registry keys listed in the tool's output.

See [Run the Troubleshooting Tool](/troubleshoot/troubleshooting-tool/) to generate a diagnostic log.

## Fix option 3: Disable conflicting add-ins

{{< step n="1" title="Open Excel and go to Options" >}}
**File → Options → Add-Ins**.
{{< /step >}}

{{< step n="2" title="Change Manage to COM Add-ins and click Go" >}}
This shows all active COM add-ins.
{{< /step >}}

{{< step n="3" title="Uncheck all add-ins except Adaptive Planning for Excel" >}}
Click **OK**, then close and reopen Excel.
{{< /step >}}

{{< step n="4" title="Try signing in to OfficeConnect" >}}
If this resolves the issue, re-enable add-ins one at a time to identify the conflict.
{{< /step >}}
```

- [ ] **Step 2: Write update-errors.md**

Create `content/troubleshoot/update-errors.md`:

```markdown
---
title: "Resolve OfficeConnect Update Errors"
linkTitle: "Update Errors"
weight: 2
description: >
  How to fix errors that occur when updating OfficeConnect to a new version.
---

**Symptom:** When updating OfficeConnect, you see:

```
An error occurred while downloading the update. Details: The underlying connection
was closed: An unexpected error occurred on a send.
```

## Common causes and fixes

### Cause 1: Network or proxy blocking the update

Your corporate network or proxy may be blocking the update download.

**Fix:** Work with your IT team to allowlist the Workday update servers. Alternatively, download the latest installer manually from **Product Downloads** in Workday and install it directly — bypassing the auto-update.

### Cause 2: TLS version too old (Windows 7)

If you're on Windows 7, your system may be using TLS 1.0 or 1.1. Workday dropped support for these between 2017 and 2019.

**Fix:** Work with IT to enable TLS 1.2 as the default on Windows 7 (see Microsoft's documentation for instructions). Or upgrade to Windows 10/11.

### Cause 3: Corrupted installation

Sometimes a partial update leaves OfficeConnect in a broken state.

**Fix:**

{{< step n="1" title="Uninstall OfficeConnect" >}}
Go to **Start → Settings → Apps & Features**, find **OfficeConnect**, and click **Uninstall**.
{{< /step >}}

{{< step n="2" title="Download the latest installer" >}}
Get the current `OfficeConnectSetup.exe` from **Product Downloads** in your Workday Adaptive Planning instance.
{{< /step >}}

{{< step n="3" title="Run the installer" >}}
Install fresh. This eliminates any partial-update state.
{{< /step >}}

## Still stuck?

Run the [Troubleshooting Tool](/troubleshoot/troubleshooting-tool/) to generate a diagnostic log and send it to Workday Support.
```

- [ ] **Step 3: Write task-pane-not-displaying.md**

Create `content/troubleshoot/task-pane-not-displaying.md`:

```markdown
---
title: "Task Pane Not Displaying Correctly"
linkTitle: "Task Pane Issues"
weight: 3
description: >
  How to fix the OfficeConnect Reporting pane when it's not showing or displaying incorrectly.
---

## Symptom: Reporting pane is invisible or blank

If the OfficeConnect Reporting pane disappears or shows as blank, it's usually a display rendering issue in Excel.

**Fix:**

{{< step n="1" title="Open Excel Options" >}}
Go to **File → Options → General**.
{{< /step >}}

{{< step n="2" title="Change the rendering setting" >}}
Find the option **"Optimize for best appearance"** and change it to **"Optimize for compatibility"**.
{{< /step >}}

{{< step n="3" title="Close and reopen Excel" >}}
The Reporting pane should now display correctly.
{{< /step >}}

## Symptom: Floating pane has disappeared

If you undocked the Reporting pane and lost it:

**Fix:** In the OfficeConnect ribbon, click **Show Reporting Pane** — even if it's already checked. The pane will reappear.

## Symptom: OfficeConnect tab is missing from the ribbon

If the entire OfficeConnect tab is gone from the ribbon:

{{< step n="1" title="Check if the add-in is disabled" >}}
Go to **File → Options → Add-Ins**. Change **Manage** to **Disabled Items** and click **Go**. If OfficeConnect appears there, select it and click **Enable**.
{{< /step >}}

{{< step n="2" title="Check COM Add-ins" >}}
Change **Manage** to **COM Add-ins** and click **Go**. Make sure **Adaptive Planning for Excel** is checked.
{{< /step >}}

{{< step n="3" title="Reinstall if needed" >}}
If the add-in isn't listed, it may need reinstalling. See [Install as an End User](/get-started/install-end-user/).
{{< /step >}}
```

- [ ] **Step 4: Write numbers-not-shifting.md**

Create `content/troubleshoot/numbers-not-shifting.md`:

```markdown
---
title: "Numbers Not Shifting After Inserting Rows"
linkTitle: "Numbers Not Shifting"
weight: 4
description: >
  Why OfficeConnect elements don't move when you insert Excel rows, and how to fix it.
---

**Symptom:** You insert rows into your Excel worksheet, but OfficeConnect data in rows below the insertion point doesn't shift down — the elements stay in their original positions.

## Why this happens

OfficeConnect element metadata is attached to specific cells. When you use standard Excel **Insert Rows**, Excel moves the cell values but the OfficeConnect element assignments don't follow — they remain anchored to the original row numbers.

## Fix: Use OfficeConnect's Insert/Delete functions

Instead of Excel's native Insert Rows/Delete Rows, always use OfficeConnect's equivalent:

{{< step n="1" title="Select the row where you want to insert" >}}
Click the row number to select the entire row.
{{< /step >}}

{{< step n="2" title="Right-click and use OfficeConnect → Insert Row" >}}
From the right-click context menu, select **OfficeConnect → Insert Row** (not Excel's standard Insert).
{{< /step >}}

This inserts a row and correctly shifts all OfficeConnect element assignments.

## If you already inserted rows with Excel's native function

1. Undo the insert with **Ctrl+Z** (undo until you're back to the pre-insert state)
2. Reinsert using OfficeConnect's Insert Row function

If undo isn't available, you'll need to re-apply elements to the affected rows manually.
```

- [ ] **Step 5: Write suppress-zeros-blanks.md**

Create `content/troubleshoot/suppress-zeros-blanks.md`:

```markdown
---
title: "Suppress & Hide Zeros and Blanks"
linkTitle: "Hide Zeros & Blanks"
weight: 5
description: >
  How to hide rows with all zeros or blank values in your OfficeConnect workbook.
---

Zero suppression in OfficeConnect is a two-part system: **Workbook Properties** controls the *default state*, and the **Hide Zeros & Blanks** ribbon button is a *toggle* on top of that default.

## How it works

| Workbook property | Effect |
|---|---|
| **Hide rows with all zeroes** is **checked** | Zero suppression is enabled by default. The **Hide Zeros & Blanks** button on the ribbon toggles it on/off. |
| **Hide rows with all zeroes** is **unchecked** | Zero suppression is disabled. The **Hide Zeros & Blanks** button will not work after refresh. |

## Enable zero suppression

{{< step n="1" title="Open Workbook Properties" >}}
In the OfficeConnect ribbon, click **Workbook Properties**.
{{< /step >}}

{{< step n="2" title="Check 'Hide rows with all zeroes'" >}}
In the **Row Display** section, check the **Hide rows with all zeroes** option.
{{< /step >}}

{{< step n="3" title="Click Refresh" >}}
After refreshing, click **Hide Zeros & Blanks** in the OfficeConnect ribbon to activate suppression.
{{< /step >}}

## Per-row overrides

With the workbook default set, you can configure individual rows to behave differently:
1. Select the row
2. Right-click → **OfficeConnect → Row Properties**
3. Set a different zero suppression behavior for that specific row

This lets some rows follow the workbook default while others always show (or always hide) zeros.

## Zero suppression and Excel's Hide Rows

Within OfficeConnect-linked data ranges, you can also use Excel's native **Hide** capability on rows and columns. These behave independently from OfficeConnect's zero suppression.
```

- [ ] **Step 6: Write remove-elements.md**

Create `content/troubleshoot/remove-elements.md`:

```markdown
---
title: "Remove Elements"
linkTitle: "Remove Elements"
weight: 6
description: >
  How to clear OfficeConnect elements from cells, rows, or columns.
---

**Question:** How do I remove OfficeConnect elements from a range of cells?

## Steps

{{< step n="1" title="Select the row, column, or cell" >}}
Select the area where the element is applied. For best results, select the entire row or column (not just individual cells within it).
{{< /step >}}

{{< step n="2" title="Right-click and choose Clear Design Elements" >}}
From the right-click context menu, select **OfficeConnect → Clear Design Elements**.
{{< /step >}}

## What gets cleared

- The OfficeConnect element metadata is removed from the selection
- The cells become plain Excel cells — no longer linked to Adaptive Planning
- **Labels** you added remain in place (they're plain text, not elements)
- The visual contents of the cells remain until you delete them manually or the next refresh would have populated them

## Remove elements from multiple locations

To remove elements from several rows or columns at once:
1. Hold **Ctrl** and click each row number or column letter
2. Right-click any of the selected rows/columns
3. Select **OfficeConnect → Clear Design Elements**

## Find all instances of an element first

If you want to find everywhere a specific element is used before removing it:
1. From the OfficeConnect ribbon, click **Find** (in the Find drop-down)
2. Search for the element
3. Use **Find All** to see all instances across the workbook

Then clear each one individually or use **Replace** to swap it with a different element.
```

- [ ] **Step 7: Verify build**

```bash
hugo --minify 2>&1
```

Expected: 35 pages built, no errors.

- [ ] **Step 8: Commit**

```bash
git add content/troubleshoot/com-registration-error.md content/troubleshoot/update-errors.md content/troubleshoot/task-pane-not-displaying.md content/troubleshoot/numbers-not-shifting.md content/troubleshoot/suppress-zeros-blanks.md content/troubleshoot/remove-elements.md
git commit -m "feat: Troubleshoot section part 1 (6 pages)"
```

---

## Task 9: Troubleshoot Section — Part 2 (6 pages)

**Files:** `change-rounding-settings.md`, `display-percentage-values.md`, `fixed-date-columns.md`, `trailing-12-month-report.md`, `link-external-excel-files.md`, `troubleshooting-tool.md`

- [ ] **Step 1: Write change-rounding-settings.md**

Create `content/troubleshoot/change-rounding-settings.md`:

```markdown
---
title: "Change Rounding Settings"
linkTitle: "Rounding Settings"
weight: 7
description: >
  How to change how numbers are rounded in OfficeConnect reports.
---

OfficeConnect defaults to **Thousands** rounding for Adaptive Planning data sources — so `100,000` displays as `100` and `1,000` displays as `1`. You can change this at three levels.

## Rounding levels (highest to lowest precedence)

1. **Selection Properties** — for a specific row, column, or cell
2. **Workbook Properties** — for the current workbook
3. **User Settings** — your personal default for all new workbooks

## Change rounding in User Settings (affects new workbooks)

{{< step n="1" title="Click User Settings in the OfficeConnect ribbon" >}}
{{< /step >}}

{{< step n="2" title="In the Round to drop-down, select the rounding level" >}}
Options: Hundreds, Thousands (default), Ten Thousands, Hundred Thousands, Millions, Ten Millions, Hundred Millions, Billions, No Rounding.
{{< /step >}}

{{< step n="3" title="Click OK" >}}
This applies to all new workbooks. The current open workbook is not affected.
{{< /step >}}

## Change rounding for the current workbook

{{< step n="1" title="Click Workbook Properties in the OfficeConnect ribbon" >}}
{{< /step >}}

{{< step n="2" title="On the Format tab, change the Round to setting" >}}
{{< /step >}}

{{< step n="3" title="Click OK, then Refresh → All Sheets" >}}
The new rounding applies to the entire workbook across all worksheets.
{{< /step >}}

## Change rounding for a specific row, column, or cell

{{< step n="1" title="Select the row, column, or cell" >}}
{{< /step >}}

{{< step n="2" title="Right-click → OfficeConnect → Row/Column/Cell Properties" >}}
{{< /step >}}

{{< step n="3" title="Change the Round to setting and click OK" >}}
This overrides the workbook setting for this specific selection only.
{{< /step >}}

## Rounding and percentage values

If your report includes percentages, rounding to Thousands will distort them — `25.25%` becomes `0.0002525`. See [Display Percentage Values](/troubleshoot/display-percentage-values/) for the fix.
```

- [ ] **Step 2: Write display-percentage-values.md**

Create `content/troubleshoot/display-percentage-values.md`:

```markdown
---
title: "Display Percentage Values Correctly"
linkTitle: "Percentage Values"
weight: 8
description: >
  How to prevent rounding from distorting percentage values in OfficeConnect.
---

**Problem:** Percentage values from Adaptive Planning appear as tiny decimals in OfficeConnect. For example, `25.25%` shows as `0.0002525` when workbook rounding is set to Thousands.

This happens because OfficeConnect stores percentages as decimals (`0.2525`) and then applies the workbook's rounding setting on top — Thousands rounding divides by 1,000, making it `0.0002525`.

## Fix option 1: Set rounding to No Rounding (whole workbook)

{{< step n="1" title="Open Workbook Properties" >}}
In the OfficeConnect ribbon, click **Workbook Properties**.
{{< /step >}}

{{< step n="2" title="On the Format tab, set Round to No Rounding" >}}
{{< /step >}}

{{< step n="3" title="Format the percentage cells in Excel" >}}
Select the cells and use Excel's **Format Cells → Percentage** to display them correctly.
{{< /step >}}

{{< step n="4" title="Refresh" >}}
{{< /step >}}

**Trade-off:** This removes rounding from the entire workbook. All other numbers will display without rounding too.

## Fix option 2: Suppress rounding on specific cells only

{{< step n="1" title="Select the cells that contain percentages" >}}
{{< /step >}}

{{< step n="2" title="In the OfficeConnect ribbon, open Row/Column/Cell Properties" >}}
Right-click → **OfficeConnect → Cell Properties** (or Row/Column Properties for a full row/column).
{{< /step >}}

{{< step n="3" title="Enable Suppress Rounding (Do Not Round Amounts)" >}}
{{< /step >}}

{{< step n="4" title="Format those cells as percentages using Excel" >}}
Select the cells → **Home tab → Number format → Percentage** (or use the `%` button).
{{< /step >}}

{{< step n="5" title="Refresh" >}}
{{< /step >}}

**Advantage:** The rest of the workbook keeps its rounding. Only the percentage cells display without rounding.
```

- [ ] **Step 3: Write fixed-date-columns.md**

Create `content/troubleshoot/fixed-date-columns.md`:

```markdown
---
title: "Create Fixed Date Columns"
linkTitle: "Fixed Date Columns"
weight: 9
description: >
  How to prevent date columns from rolling forward when using relative time elements.
---

**Problem:** You've set up a report with relative time elements (like "Current Month," "Prior Month") so it always shows recent data. But you want certain columns to stay fixed at a specific historical date — not roll forward with time.

## Why relative dates roll

When you create a report using relative time elements, OfficeConnect automatically advances them when you refresh — "Current Month" always shows the current month. This is great for rolling reports but not for fixed comparisons.

## Fix: Switch the time element to Absolute

{{< step n="1" title="In the report, select the column with the date you want to fix" >}}
{{< /step >}}

{{< step n="2" title="In the Reporting pane, click the Review tab" >}}
{{< /step >}}

{{< step n="3" title="Find the time element in the left pane" >}}
Right-click on the calendar element listed under that column.
{{< /step >}}

{{< step n="4" title="Select View/Edit" >}}
{{< /step >}}

{{< step n="5" title="Uncheck 'Make Date Relative to Book'" >}}
{{< /step >}}

{{< step n="6" title="Click OK and refresh" >}}
The column now shows a fixed date that won't advance when you refresh.
{{< /step >}}

## Using Component Dates for fixed period combinations

Component dates let you create combinations like "Q4 of FY 2024" without locking a single absolute date:

1. Apply a **year** element (e.g., `FY 2024`) to a row
2. Apply a **quarter component** (e.g., `Q4`) to a column
3. The intersection resolves to Q4 2024 specifically

See the **Components** section under Time in the Elements tab. Components are listed under `Time → Components` in the Reporting pane.
```

- [ ] **Step 4: Write trailing-12-month-report.md**

Create `content/troubleshoot/trailing-12-month-report.md`:

```markdown
---
title: "Create a Trailing 12-Month Report"
linkTitle: "Trailing 12-Month Report"
weight: 10
description: >
  How to build a report that always shows the most recent 12 months of data.
---

A trailing 12-month (T12M) report shows the 12 most recent calendar months and advances automatically each month. This is a common layout for rolling actuals analysis.

## How to build it

The key is using **relative time elements** for each of the 12 columns — each column is defined as "N months ago" relative to today.

{{< step n="1" title="Set up your rows with account elements" >}}
Apply your account elements (e.g., Revenue, COGS, Gross Profit) to rows as usual.
{{< /step >}}

{{< step n="2" title="For the first column, apply 'Current Month - 11'" >}}
In the Elements tab, expand **Time → Relative**. Find the relative time element for 11 months prior (the oldest month in your T12M window) and apply it to column C.
{{< /step >}}

{{< step n="3" title="For each subsequent column, apply the next relative month" >}}
Continue applying relative months across columns:
- Column C: `Current Month - 11`
- Column D: `Current Month - 10`
- Column E: `Current Month - 9`
- …
- Column N: `Current Month` (most recent)
{{< /step >}}

{{< step n="4" title="Refresh" >}}
The report shows 12 months of data. Each month you refresh, the window advances by one month automatically.
{{< /step >}}

## Add a YTD column

After the 12 monthly columns, add a YTD column:
1. Select the column after your last month
2. Apply `Current Month` as the time element
3. Apply `YTD` as a context element in the same column
4. Refresh — this column shows the year-to-date sum as of the current month

## Formatting tip

Use Excel's column headers to show friendly month names using an OfficeConnect label:
1. Select the header cell above a monthly column
2. In the OfficeConnect ribbon, click **Labels**
3. Select **Time** as the Label Type and the appropriate format for the Label Type Value
4. Refresh — the header automatically shows the correct month name
```

- [ ] **Step 5: Write link-external-excel-files.md**

Create `content/troubleshoot/link-external-excel-files.md`:

```markdown
---
title: "Link to External Excel Files"
linkTitle: "Link External Excel Files"
weight: 11
description: >
  How to link to a plain Excel file from within an OfficeConnect workbook.
---

**Question:** Can I create a link from my OfficeConnect workbook to a regular (non-OfficeConnect) Excel file?

## Yes — use Excel's standard external link

OfficeConnect workbooks are Excel files. You can use Excel's standard external reference syntax to pull data from any other Excel file:

```excel
=[OtherWorkbook.xlsx]Sheet1!$A$1
```

This creates a standard Excel external link — it's not an OfficeConnect-managed link, so it works just like any other Excel cross-workbook reference.

## Create an Excel copy without OfficeConnect links

If you need to send a colleague a version of your OfficeConnect report that doesn't contain any live OfficeConnect connections (e.g., they don't have OfficeConnect installed and you want them to see the data, not `n/a` placeholders):

{{< step n="1" title="Refresh the report so all data is loaded" >}}
Click **Refresh** to populate all cells with current data.
{{< /step >}}

{{< step n="2" title="Copy the entire worksheet" >}}
Right-click the sheet tab → **Move or Copy** → check **Create a copy** → place at end.
{{< /step >}}

{{< step n="3" title="On the copy, select all cells (Ctrl+A) and copy" >}}
{{< /step >}}

{{< step n="4" title="Paste as values only" >}}
Right-click → **Paste Special → Values**. This replaces the OfficeConnect-linked cells with static values.
{{< /step >}}

{{< step n="5" title="Save the copy as a new Excel file" >}}
**File → Save As** → give it a different name. This file has no OfficeConnect dependencies.
{{< /step >}}
```

- [ ] **Step 6: Write troubleshooting-tool.md**

Create `content/troubleshoot/troubleshooting-tool.md`:

```markdown
---
title: "Run the Troubleshooting Tool"
linkTitle: "Troubleshooting Tool"
weight: 12
description: >
  How to use the OCSystemChecker tool to generate a diagnostic log for Workday Support.
---

When standard troubleshooting steps don't resolve your issue, the **OCSystemChecker** tool gathers detailed diagnostic information from your machine to help Workday Support investigate.

## When to use it

- You're getting an error during installation or startup that other fixes haven't resolved
- Workday Support asks you to run the tool as part of a support case
- You want a diagnostic log before reaching out to Support

## Steps

{{< step n="1" title="Download OCSystemChecker.zip" >}}
Download the `OCSystemChecker.zip` file from the Workday Community or ask your Workday Support contact for the link. Save it to your Desktop.
{{< /step >}}

{{< step n="2" title="Extract the zip file" >}}
Right-click `OCSystemChecker.zip` → **Extract All**. Open the extracted folder.
{{< /step >}}

{{< step n="3" title="Launch OCSystemChecker.exe" >}}
Double-click `OCSystemChecker.exe`. Windows may prompt you to allow it to run — click **Yes**.
{{< /step >}}

{{< step n="4" title="Select the application with the error" >}}
Choose **OfficeConnect for Excel** (or the appropriate application) and click **Next**.
{{< /step >}}

{{< step n="5" title="Select the type of issue" >}}
Choose the closest match (installation error, refresh error, startup error, etc.). If it's file-specific, attach the problematic file when prompted. Click **Next**.
{{< /step >}}

{{< step n="6" title="Reproduce the error on the 'Re-create Issue' page" >}}
**Important:** While the Re-create Issue page is open, perform the action that causes the error. For example:
- If the error happens when installing, run the installer now
- If the error happens when refreshing a file, open and refresh the file now

Then click **Next**.
{{< /step >}}

{{< step n="7" title="Finish and find your log file" >}}
Click **Finish**. Your Temp folder opens automatically, containing a file named `AdaptiveEnvironmentInfoPackage`.
{{< /step >}}

{{< step n="8" title="Send the log to Support" >}}
Attach `AdaptiveEnvironmentInfoPackage` to your active support ticket in the Workday Customer Center.
{{< /step >}}
```

- [ ] **Step 7: Verify final build**

```bash
hugo --minify 2>&1
```

Expected: **41 pages** built (home + 5 section indexes + 35 content pages), no `ERROR` lines, output ends with `Total in NNN ms`.

- [ ] **Step 8: Commit**

```bash
git add content/troubleshoot/change-rounding-settings.md content/troubleshoot/display-percentage-values.md content/troubleshoot/fixed-date-columns.md content/troubleshoot/trailing-12-month-report.md content/troubleshoot/link-external-excel-files.md content/troubleshoot/troubleshooting-tool.md
git commit -m "feat: Troubleshoot section part 2 (6 pages) — site complete"
```

---

## Task 10: Final Verification & GitHub Pages Setup

- [ ] **Step 1: Run local server and spot-check all sections**

```bash
hugo server --minify 2>&1
```

Open `http://localhost:1313` in a browser. Verify:
- [ ] Homepage loads with two rows of feature cards
- [ ] Top navigation shows all 5 sections
- [ ] Dark navbar and amber accents display correctly
- [ ] Sidebar is dark with light text
- [ ] Each section's left sidebar shows its pages
- [ ] At least one `{{< admin-note >}}` and one `{{< step >}}` shortcode renders correctly (check `install-admin.md`)
- [ ] Lunr.js search box appears; searching "tenant" returns relevant results
- [ ] Breadcrumbs appear on content pages

Stop server with `Ctrl+C` when done.

- [ ] **Step 2: Set up the GitHub repository**

Create a new GitHub repository named `officeconnectpro` (or `docs`) under your GitHub account or organization.

Update `config/_default/params.toml` to point to your actual repo:

```toml
github_repo = "https://github.com/YOUR_USERNAME/officeconnectpro"
github_project_repo = "https://github.com/YOUR_USERNAME/officeconnectpro"
```

Also update `go.mod` module path if needed:
```
module github.com/YOUR_USERNAME/officeconnectpro
```

- [ ] **Step 3: Push to GitHub**

```bash
git remote add origin https://github.com/YOUR_USERNAME/officeconnectpro.git
git push -u origin main
```

- [ ] **Step 4: Enable GitHub Pages**

In the GitHub repository:
1. Go to **Settings → Pages**
2. Set **Source** to **Deploy from a branch**
3. Set **Branch** to `gh-pages` / `/ (root)`
4. Click **Save**

The GitHub Actions workflow will create the `gh-pages` branch on first push. It may take 1–2 minutes after the first Action run completes.

- [ ] **Step 5: Configure custom domain**

In **Settings → Pages**, add `officeconnectpro.com` as the custom domain. GitHub will validate it via a CNAME check.

At your DNS provider, add:
```
CNAME  www   YOUR_USERNAME.github.io
A      @     185.199.108.153
A      @     185.199.109.153
A      @     185.199.110.153
A      @     185.199.111.153
```

- [ ] **Step 6: Verify live site**

After DNS propagates (up to 24 hours), open `https://officeconnectpro.com` and confirm:
- Site loads over HTTPS
- Homepage renders with all sections
- Search works
- No broken links in the top nav

- [ ] **Step 7: Final commit**

```bash
git add config/_default/params.toml go.mod
git commit -m "chore: point github_repo to live repository URL"
git push
```

---

## Self-Review Notes

**Spec coverage check:**
- ✅ Hugo/Docsy scaffold with Go modules — Task 1
- ✅ Dark & amber theme via SCSS overrides — Task 1
- ✅ Two custom shortcodes (admin-note, step) — Task 2
- ✅ GitHub Actions deploy with setup-go step — Task 1
- ✅ .gitignore including .superpowers/ — Task 1
- ✅ All 5 section index pages — Task 2
- ✅ All 5 Get Started pages — Task 3
- ✅ All 5 Connect pages (2 admin-only tagged) — Task 4
- ✅ All 10 Build Reports pages — Tasks 5 & 6
- ✅ All 3 Share & Publish pages — Task 7
- ✅ All 12 Troubleshoot pages — Tasks 8 & 9
- ✅ Lunr.js search enabled via params.toml — Task 1
- ✅ GitHub Pages + custom domain — Task 10
- ✅ Total: 35 content pages + 6 index pages + homepage = 42 pages
