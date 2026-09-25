# AMatriz Specifications v1.0.1

## 0. Version Status and Intent

- Version: `v1.0.1` (Final Release).
- Status: 100% Complete & Merged Live on Typora Theme Gallery (PR #535 merged by abnerlee).
- License: MIT.
- Copyright: Copyright (c) 2026 Electritects Pty Ltd.
- Intent: Provide standalone Typora themes inspired by Matrix green-on-black, optimized for engineering documentation and high-contrast readability, with a separate white-print variant for printer-friendly PDF output.

## 1. Scope

### 1.1 In Scope

- Typora themes delivered as `.css` files placed in Typora's theme folder and selectable from the Themes menu.
- Theme files:
  - `amatriz.css`: dark editor and dark PDF export.
  - `amatriz-print-white.css`: same dark editor and UI, but white PDF/print output.
- Styling for:
  - Editor content: `#write`, headings, text, links, lists, task lists, blockquotes, tables, code blocks, math, and Mermaid diagrams.
  - Sidebar UI: `#typora-sidebar`, file tree, and outline.
  - Preferences and Export dialog UI: modal and panel controls.
  - Print/PDF behavior through `@media print` and `@page`.
- A4-oriented validation document:
  - `docs/Typora Test File v1.0.0.md`.

### 1.2 Out of Scope

- Adding custom controls to Typora's Export dialog.
- PDF form fields or clickable PDF checkboxes.
- Imposing license terms on user-authored documents, PDFs, notes, products, or services created while using the theme.
- Theme-controlled page numbers, rich running headers, or rich running footers.
- Bundling external fonts or remote assets.
- Reliance on other themes' sub-files via `@import`.
- Guaranteeing identical PDF output across all Typora versions, export pipelines, and OS print renderers.

## 2. Functional Requirements

### 2.1 Standalone Theme Packaging

- The main theme must be named `amatriz.css` and appear as `AMatriz`.
- The white-print variant must be named `amatriz-print-white.css` and appear as `AMatriz Print White`.
- Theme filenames must use lowercase letters and hyphens, with no whitespace, following Typora custom-theme guidance.
- Packaged release source files:
  - `coding/amatriz.css`.
  - `coding/amatriz-print-white.css`.
- The packaged files are synchronized from the installed Typora validation copies:
  - `%APPDATA%\Typora\themes\amatriz.css`.
  - `%APPDATA%\Typora\themes\amatriz-print-white.css`.

### 2.2 Editor Content Styling

- Both themes must keep the Matrix editor palette:
  - Background: very dark green or black.
  - Foreground text: neon green, with softer green for secondary text.
  - Borders: dark green.
- Typography must remain readable for long engineering documents.
- Code blocks and inline code must be clearly separated using background and borders.
- Task list checkboxes must remain visible in editor and PDF output.

### 2.3 Sidebar and Outline Styling

- Sidebar background must match the theme background and avoid default light UI clashes.
- Outline indentation must reflect heading levels from H1 through H6.
- Active item and hover states must be visible and consistent with the Matrix palette.

### 2.4 Preferences and Export UI Styling

- Preferences modal background, nav items, inputs, selects, and buttons must be themed to eliminate mixed light/dark UI.
- Export tab panel regions must be themed because these areas can remain light by default if not explicitly styled.

### 2.5 White Print Variant

- `amatriz-print-white.css` must preserve the dark editor UI.
- In `@media print`, it must export with:
  - White page background on every page edge.
  - Black default Markdown text.
  - Blue links.
  - Yellow highlight support.
  - Light code panels with black text.
  - Gray table and blockquote borders.
  - Preserved inline HTML colors where the document author explicitly sets color, such as `<span style="color: red;">red</span>`.

## 3. Technical Design

### 3.1 Tech Stack

- Primary technology: CSS theme files consumed by Typora.
- Rendering surfaces impacted:
  - Editor: HTML/CSS within Typora's hybrid view.
  - Sidebar and modals: Typora UI elements styled via CSS selectors.
  - Export pipeline: HTML to print/PDF conversion, subject to Chromium/Electron print behavior.

### 3.2 Theme Architecture

- Variable-driven palette: core colors are defined under `:root` and referenced via `var(...)`.
- Layout strategy:
  - Responsive `#write` width with a 1280px maximum.
  - Real `@page` margins for print/PDF output.
  - No fake page margin based on body padding.
  - No document-position-dependent selectors such as section-count-based page breaks.
- Typora guidance alignment:
  - Lowercase, hyphenated filenames.
  - `@media print` for print/PDF-specific behavior.
  - Tag selectors scoped to `#write` where useful.
  - CSS variables for reusable colors and UI values.
- No external imports:
  - The themes remain portable and self-contained.

### 3.3 Typora Component Coverage

#### Editor Surface

- `html, body`: global background, font family, and text color.
- `#write`: content width and margins.
- `h1` through `h6`: typography and separators.
- `a`, `strong`, `em`, `mark`, `kbd`: inline semantic styling.
- `.pill-red`, `.pill-blue`: semantic indicator pills (inline-block spans) for critical rules and optional examples.
- `.md-cursor`, `.CodeMirror-cursor`, `.cm-cursor`, and `caret-color`: neon green editor cursor/caret visibility, including table cells and fenced code editing.
- `code`, `pre.md-fences`: inline and fenced code styling.
- `table`, `thead`, `tbody`, `tr`, `th`, `td`: table grid visibility and print behavior.
- `.md-toc`: in-document table of contents styling with visible contour.
- `.md-math-block`, `.md-mathjax-preview`, and MathJax output: equation editing and export compatibility.
- `.md-diagram-panel`, `svg.mermaid-svg`: Mermaid sizing and print containment.

#### Sidebar and Outline Surface

- `#typora-sidebar`: sidebar background and width.
- `.sidebar-tabs`, `.tab-button.active`: tab highlighting.
- `.outline-item`, `.outline-h1` through `.outline-h6`: outline hierarchy styling.
- `.file-list-item`, `.file-node-content`: file tree text, hover, and active styling.

#### Preferences and Export UI Surface

- `.modal-content`, `.modal-body`: modal background and text.
- `.nav-group-item`, `.nav-group-item.active`: left nav in preferences.
- `.modal-content input`, `.modal-content select`: dark controls with green text.
- `.modal-content .btn`: consistent theme action controls.
- `.panel`, `.form-group`, and container-level overrides: export panel styling intended to eliminate gray panel regions.

## 4. Export and PDF Behavior

### 4.1 Dark Export

`amatriz.css` exports dark PDFs with:

- Dark page background.
- AMatriz green default text.
- Preserved inline HTML colors.
- Red and blue semantic pills rendered inline, preserved in print/PDF exports with structured colors (red/blue) at 10% background opacity.
- Single bordered code block panels.
- Visible table borders.
- Mermaid diagrams constrained to the printable page.
- Rendered math and Mermaid output preserved in export.

### 4.2 White Export

`amatriz-print-white.css` exports white PDFs with:

- White page background.
- Black default Markdown text.
- Blue links.
- Yellow highlights preserved.
- Light gray code panels.
- Gray blockquote and table borders.
- Dashed gray in-document TOC contour when `[TOC]` is used.
- Rendered math and Mermaid output preserved in export.
- Preserved authored inline HTML colors.
- Red and blue semantic pills rendered inline, preserved in print/PDF exports with structured colors (red/blue) at 10% background opacity.


### 4.3 Print Layout Rules

- Both themes use real `@page` margins.
- Table headers use `display: table-header-group` so header rows can repeat across pages.
- Tables and blockquotes are configured to avoid splitting inside pages (`break-inside: avoid`).
- Code fences are configured to allow page splits (`break-inside: auto; page-break-inside: auto`) to support long listings.
- Code block splitting is controlled by page-break settings (e.g., `orphans: 3` and `widows: 3`) to prevent single-line orphans.
- Headings followed immediately by a code fence avoid page splits before the code fence (`h2 + pre, h3 + pre { break-before: avoid; }`).
- Consecutive code blocks have their top border removed (`pre + pre { border-top: 0; }`) to look continuous across pages.
- Mermaid SVGs are constrained with a maximum print height to avoid bottom clipping.
- Compact print table handling is opt-in through table classes such as `amatriz-technical-table`, `amatriz-chemistry-table`, `amatriz-unicode-table`, and `periodic-mini`.
- The theme does not force a page break after `[TOC]`; documents own that pagination decision.

## 5. User-Facing Behavior Notes

- Users choose dark or white PDF output by selecting the corresponding Typora theme before export.
- `[TOC]` creates an in-document Table of Contents block that updates automatically based on headings.
- The validation document owns its own page-break markers for repeatable export checks. The public theme CSS does not hard-code breaks based on this test file's section order.
- Print-only cleanup hides Typora helper UI and footnote backlink arrows that are useful on screen but should not appear in exported PDFs.

## 6. Installation and Configuration

### 6.1 Installation Steps

1. Open Typora Preferences -> Appearance -> Open Theme Folder.
2. Place `amatriz.css` and `amatriz-print-white.css` into the theme folder.
3. Restart Typora.
4. Select `AMatriz` or `AMatriz Print White` from the Themes menu.

### 6.2 Source Locations

Packaged release source:

- `coding/amatriz.css`.
- `coding/amatriz-print-white.css`.

Installed validation copies:

- `%APPDATA%\Typora\themes\amatriz.css`.
- `%APPDATA%\Typora\themes\amatriz-print-white.css`.

### 6.3 Compatibility Assumptions

- Tested target environment: Typora on Windows with Electron-based UI.
- Font assumption: `JetBrains Mono` is preferred if installed, with fallback to `Consolas` and generic monospace fonts.
- PDF output may vary across Typora versions and print engines.

## 7. Quality Criteria

- Editor readability:
  - Heading hierarchy is visually obvious.
  - Code blocks are clearly distinct.
  - Tables have visible borders with consistent spacing.
- UI consistency:
  - Sidebar, outline, preferences, and export screens do not revert to bright or light defaults.
- Print behavior:
  - `amatriz.css` exports dark PDFs.
  - `amatriz-print-white.css` exports white PDFs with black default text.
  - Explicit inline HTML colors remain visible in white-print output.
  - Yellow highlight remains visible in white-print output.
  - Fenced code blocks print as one panel, not as one box per line.
  - Table outside borders remain visible.
  - `[TOC]` renders with a visible contour when present.
  - Math renders as equations rather than raw LaTeX source.
  - Mermaid diagrams do not clip.
  - Mermaid renders as a diagram rather than raw source.
- Portability:
  - No dependency on other themes' sub-files or external resources.

## 8. Validation Artifacts

- Main validation Markdown files:
  - `docs/Typora Test File v1.0.1.md` (Full validation dossier).
  - `docs/Typora Test File v1.0.0.md` (Original baseline).
  - `docs/Sample Showcase.md` (Clean demo version).
- Exported validation PDFs:
  - `docs/Typora Test File v1.0.1 - PDF using Amatriz v1.0.1.pdf` (Dark export, v1.0.1).
  - `docs/Typora Test File v1.0.1 - PDF using Amatriz white print v1.0.1.pdf` (Print-white export, v1.0.1).
  - `docs/Typora Test File v1.0.0 - PDF using Amatriz v1.0.1.pdf` (Baseline dark export, v1.0.1).
  - `docs/Typora Test File v1.0.0 - PDF using Amatriz white print v1.0.1.pdf` (Baseline print-white export, v1.0.1).
- Artwork:
  - `artwork/amatriz.png` at 250x200.
  - `artwork/amatriz-500x400.png` at 500x400.
  - `artwork/amatriz-preview.png`.

## 9. Known Issues and Limits

- PDF export colors may vary on other Typora versions, operating systems, or print renderers.
- Some Preferences and Export sub-panels may require additional selector coverage depending on Typora version or skin.
- Theme CSS cannot add custom controls, toggles, form fields, or page-number controls inside Typora's Export dialog.
- Header/footer/page-number content should be treated as Typora/export configuration, not theme functionality.

## 10. Traceability

- Implemented palette and layout in `:root`, `html/body`, and `#write`.
- Implemented sidebar and outline styling through `#typora-sidebar`, `.outline-*`, and file list selectors.
- Implemented Preferences and Export UI base styling using modal and preferences selectors.
- Implemented dark PDF export in installed `amatriz.css`.
- Implemented white PDF export in installed `amatriz-print-white.css`.
- Reworked the PDF export test document into an A4-oriented validation/template file.
- Added explicit neon green cursor/caret coverage for normal editing, table editing, and fenced code editing.
- Preserved the in-document TOC contour while keeping TOC page-break control in Markdown.
- Restored rendered math and Mermaid behavior in white-print export.
- Added gallery artwork under `artwork/`.
- Copied final installed CSS into `coding/` for the v1.0.1 release package.
- Prepared Typora Theme Gallery submission staging files under `typora-theme-gallery-submission/`.

## 11. Changelog

### v1.0.1

- Defined a complete design system variable set at `:root`.
- Implemented an explicit heading scale for `h1`–`h6`.
- Adjusted default body line height to `1.6` for improved readability.
- Scoped scanline overlay to `@media screen` to isolate it from exports.
- Enhanced table header and row striping contrast (both in screen view and print mode).
- Configured multi-page table pagination (`table { break-inside: auto !important }`) so long tables start immediately without forced empty page gaps, while maintaining row integrity (`tr { break-inside: avoid }`) and repeating headers (`thead { display: table-header-group !important }`).
- Expanded Table 8.1 in `Typora-Test-File-v1.0.1.md` to 50 rows to stress test multi-page table continuation across page breaks.
- Upgraded Section 11 (Chemistry) to document native `mhchem` (`$\ce{...}$`), LaTeX math (`\rightarrow`), and Smart Punctuation reaction arrows.
- Added subtle box-shadow glow and vertical margins to fenced code blocks (`pre.md-fences`).
- Styled inline `code` blocks with borders and a background color using theme variables.
- Added hierarchical border/opacity rules for nested blockquotes.
- Increased link underline thickness to `2px`.
- Optimized the maximum width of the editor container `#write` to `980px`.
- Standardized print-break directives in `@media print` with modern properties.
- Softened the caret/cursor glow size.
- Reduced the sidebar min-width to `240px` to save screen space.
- Added a robust font stack fallback list on `html, body`.
- Submitted Typora Theme Gallery Update Pull Request #535 ([PR #535](https://github.com/typora/theme.typora.io/pull/535)) containing 5 transmittal files (`amatriz.css`, `amatriz-print-white.css`, `Typora-Test-File-v1.0.1.md`, and both sample dark and white PDF exports).

### v1.0.0

- Added `amatriz-print-white.css`.
- Preserved the dark editor UI in the white-print variant.
- Added white PDF/print output with black default text.
- Fixed white PDF header/footer black band behavior.
- Switched print layout to real `@page` margins.
- Preserved explicitly styled inline HTML colors in white-print output.
- Restored yellow highlight visibility.
- Fixed fenced code print styling to avoid per-line boxes.
- Improved table borders and table header repeat behavior.
- Tightened list spacing and improved cursor/caret visibility in editor, table, and code-block contexts.
- Preserved the visible `[TOC]` contour while leaving TOC page breaks to the document.
- Restored rendered math and Mermaid behavior in white-print export.
- Constrained Mermaid diagrams to prevent bottom clipping.
- Reworked the PDF test file as an A4-friendly validation/template document.
- Added publishing artwork under `artwork/`.
- Copied the final accepted CSS into `coding/`.
- Added release license and Typora Theme Gallery submission staging files.

### v1.0.0

- Established the original dark Matrix-inspired editor styling.
- Added sidebar, outline, Preferences, and Export UI styling.
- Corrected dark PDF export with full-page dark background support.

## 12. References

- Typora custom theme guide: <https://theme.typora.io/doc/Write-Custom-Theme/>
- Typora theme support: <https://support.typora.io/About-Themes/>
- Typora submit-a-theme guide: <https://theme.typora.io/doc/Submit-A-Theme/>
- Typora Theme Gallery repository: <https://github.com/typora/theme.typora.io>
- Typora page breaks: <https://support.typora.io/Page-Breaks/>
- Typora table of contents support: <https://support.typora.io/TOC/>
- CSS `print-color-adjust`: <https://css-tricks.com/almanac/properties/p/print-color-adjust/>

## Directory & Output Conventions
- **Binary & Distribution Isolation**: All compiled executables (`*.exe`, `.msi`, installer bundles) and all associated distribution ancillaries / launcher scripts (`*.bat`, `*.cmd`, `*.vbs`, wrapper launchers) must reside exclusively in `dist/`. No executables or launcher batch files may reside in the project root.
- **Temporary File Isolation**: All AI scratch scripts, temporary files, and test runners must be placed in `ai_tools/`.
- **Clean Root**: Root directory must remain clean and conform to standard repository layout (`coding/`, `docs/`, `docs/specs/`, `docs/reviews/`, `ai_tools/`, `dist/`, `artwork/`, `legal/`, `sandbox/`, `similar/`).