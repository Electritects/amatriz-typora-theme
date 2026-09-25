# AMatriz Typora Theme

![AMatriz Typora Theme banner](docs/assets/amatriz-banner.png)

AMatriz is a standalone Typora CSS theme with a Matrix-inspired green-on-black visual style. It is intended for engineering documentation, handoff notes, setup guides, and long-form technical writing where high contrast and readable code blocks matter.

## Current Version

- Version: `v1.0.0`
- Project status: Discovery / implemented baseline
- Primary artifact: `coding/amatriz.css`
- Installed Typora copy: `%APPDATA%\Typora\themes\amatriz.css`

## What It Provides

- Dark green-black editor background.
- Neon green body text with softer green secondary text.
- Styled headings, links, lists, blockquotes, tables, inline code, and fenced code blocks.
- Dark sidebar, Files panel, and Outline panel styling.
- Preferences and Export dialog styling coverage for common Typora UI containers.
- Responsive editor width so text does not clip when Typora's sidebar is open.
- Dark PDF export support using print-specific CSS.

## Installation

1. Open Typora
2. Preferences -> Appearance -> Open Theme Folder
3. Copy `amatriz.css`
4. Restart Typora

## PDF Export Behavior

The theme includes print rules designed to keep AMatriz PDF exports dark and readable:

- `print-color-adjust: exact`
- `-webkit-print-color-adjust: exact`
- `@page { margin: 0; background: #030803; }`
- `body { padding: 15mm; }` inside print mode
- Wrapping rules for paragraphs, links, tables, and code fences

The `@page` margin is set to `0` so the PDF page background renders dark edge-to-edge. Readable page spacing is then provided by body padding. This avoids the white side bands that appeared in earlier PDF exports.

## Validation Files

- `docs/Typora Test File.md` is the main Markdown stress test for the theme.
- `docs/Typora Test File.pdf` is the latest local PDF export result.
- `docs/pdf-renders/` contains rendered PDF page previews used to inspect output visually.
- `docs/AMatriz Specifications v1.0.0.md` contains the detailed technical specification.

## Recommended Test Flow

1. Open `docs/Typora Test File.md` in Typora.
2. Select the AMatriz theme.
3. Confirm the editor does not clip text with the sidebar open.
4. Export to PDF.
5. Confirm the PDF has:
   - Dark background on every page edge.
   - Green readable text.
   - Bordered dark code blocks.
   - Readable tables.
   - No white side bands.
   - No major content clipping.

## Source of Truth

Use `coding/amatriz.css` as the project source of truth. After editing it, copy the same file to:

```text
%APPDATA%\Typora\themes\amatriz.css
```

Keep the project source and installed Typora copy synchronized after every theme change.

## Known Limits

- PDF rendering can still vary by Typora version, operating system, and print/PDF engine.
- Preferences and Export dialog internals may use Typora-version-specific classes, so some UI panels may need additional selector coverage.
- The theme intentionally uses system fonts and does not bundle external assets.
