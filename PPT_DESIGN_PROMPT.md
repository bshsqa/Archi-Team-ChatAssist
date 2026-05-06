# PPT Design System Prompt

## Purpose

Use this prompt when generating presentation decks for this repository. The target visual language is inspired by Apple's web presence: restrained, photography-first, quiet typography, alternating light and dark full-bleed sections, and a single blue accent. The output should feel premium, calm, and highly intentional, while still supporting dense architecture content.

## Core Direction

Create a 16:9 presentation deck with an Apple-inspired editorial product-tile aesthetic. The design should feel like a quiet product gallery: full-bleed light and dark canvases, confident typography, minimal UI chrome, precise spacing, and one consistent blue accent for emphasis. The slides are for software architecture content, so clarity and information hierarchy matter more than decorative realism.

Do not use any logos, including Apple logos, company logos, product logos, or invented brand marks. The deck should be brand-neutral.

## Non-Negotiable Constraints

- Use 16:9 slides only.
- Use exactly one font family throughout the entire deck for visual consistency.
- Prefer `Aptos` or `Inter` as the single font family. If neither is available, use the system sans-serif fallback.
- Do not use logos.
- Do not use decorative gradients.
- Do not use decorative shadows on cards, text, or UI elements.
- Use a single accent color only: Action Blue `#0066cc`.
- Keep chapter label, title, and subtitle in the same position on every slide.
- Avoid leaving the lower body area empty. Fill the slide with useful content density while preserving visual calm and readability.
- Use Mermaid-style diagrams only when producing Markdown source. For PPT visuals, translate diagrams into clean native shapes if possible.

## Visual Character

Apple's web presence is a masterclass in reverent product presentation framed by near-invisible UI. For this deck, translate that language into architecture communication:

- Content is the product.
- Each slide should feel like a full-bleed tile.
- Alternate light and dark surfaces to create rhythm.
- Let surface color changes act as section dividers.
- Keep UI decoration almost invisible.
- Use generous whitespace, but do not make slides sparse.
- Use precise typography and alignment to create authority.
- Use blue only for emphasis, callouts, page markers, or small CTA-like labels.

## Color System

### Accent

- Action Blue: `#0066cc`
- Focus / bright blue, only when needed on dark surfaces: `#2997ff`

### Surfaces

- Pure White: `#ffffff`
- Parchment: `#f5f5f7`
- Near Black 1: `#272729`
- Near Black 2: `#2a2a2c`
- Near Black 3: `#252527`
- Pure Black: `#000000`, reserved for true voids or very small navigation strips

### Text

- Ink on light: `#1d1d1f`
- Muted ink: `#6e6e73`
- Body on dark: `#ffffff`
- Muted body on dark: `#cccccc`

### Borders

- Hairline: `#e0e0e0`
- Soft divider: `rgba(0, 0, 0, 0.08)`

## Typography

Use one font family only. The preferred deck font is:

`Aptos, Inter, system-ui, -apple-system, BlinkMacSystemFont, sans-serif`

Use the same family for all text. Vary only size, weight, line height, and color.

### Recommended Type Scale for 16:9 Slides

| Role | Size | Weight | Line Height | Use |
| --- | --- | --- | --- | --- |
| Chapter label | 13-15px | 600 | 1.1 | Persistent top-left or top-right label |
| Slide title | 34-44px | 600 | 1.08-1.15 | Main slide title |
| Subtitle | 18-22px | 400 | 1.35 | One-line slide framing |
| Section heading | 21-26px | 600 | 1.2 | Major content block title |
| Body | 15-18px | 400 | 1.35-1.5 | Main explanatory text |
| Table / card text | 13-16px | 400 | 1.25-1.4 | Dense structured content |
| Caption | 11-13px | 400 | 1.2 | Footnotes, source notes, page labels |

### Typography Rules

- Use weight 600 for titles and section headings.
- Use weight 400 for body text.
- Avoid weight 500.
- Avoid weight 700 unless a single strong emphasis is truly needed.
- Use slight negative letter spacing for large titles only if supported by the tool.
- Keep titles compact and calm; avoid marketing-like slogans unless the slide is an opening slide.

## Layout System

### Slide Format

- Format: 16:9 only.
- Use consistent margins across the deck.
- Recommended safe margin: 56-72px on desktop-like slides.
- Keep chapter label, title, and subtitle locked to the same coordinates on every slide.
- Use the body region below the subtitle as a structured content area.

### Header Rhythm

Every slide should follow this header structure:

1. Chapter label: small, muted, consistent location.
2. Title: large, confident, same baseline across slides.
3. Subtitle: one sentence, same width and position across slides.

Do not move these elements around from slide to slide unless a dedicated cover or divider slide requires it.

### Body Density

The body area should be meaningfully filled. Avoid a large empty lower half. Use one of the following patterns:

- Two-column explanation and diagram
- Three-column architecture driver cards
- Dense but readable table
- Timeline or pipeline flow
- Matrix with short labels
- Large central diagram with bottom annotations

The slide should never feel crowded, but it should feel complete.

## Slide Surface Patterns

Use alternating surfaces to create rhythm:

1. Light title / problem slide on Pure White or Parchment
2. Dark architecture driver slide on Near Black
3. Light structured table slide
4. Dark pipeline or system flow slide
5. Parchment summary / decision slide

### Light Slides

- Background: `#ffffff` or `#f5f5f7`
- Text: `#1d1d1f`
- Muted text: `#6e6e73`
- Accent: `#0066cc`
- Use hairline borders sparingly for tables or utility cards.

### Dark Slides

- Background: `#272729`, `#2a2a2c`, or `#252527`
- Text: `#ffffff`
- Muted text: `#cccccc`
- Accent: `#2997ff` or `#0066cc` if sufficiently visible
- Avoid heavy outlines. Use spacing and contrast instead.

## Components

### Product Tile Equivalent

Use a full-slide tile as the base. No rounded slide container, no outer frame, no drop shadow.

### Utility Cards

Use cards only when they organize repeated content such as stakeholders, use cases, or quality attributes.

- Radius: 12-18px
- Border: 1px hairline
- Shadow: none
- Padding: 20-24px
- Background: white on parchment, or slightly lighter near-black on dark slides

### Pills and Chips

Use pill shapes for small labels only:

- Quality attribute names
- FR / NFR tags
- Use Case IDs
- Short status labels

Primary pill:

- Fill: `#0066cc`
- Text: white
- Radius: full pill

Secondary pill:

- Fill: transparent
- Border: `#0066cc`
- Text: `#0066cc`

### Tables

Tables should be quiet and precise:

- No heavy grid.
- Use hairline dividers.
- Use muted headers.
- Keep row height comfortable.
- Use blue only for key labels or IDs.

### Diagrams

For PPT output:

- Use clean native shapes.
- Prefer horizontal pipeline diagrams, layered architecture diagrams, sequence-like flows, and matrices.
- Avoid decorative icons unless they directly improve comprehension.
- Use thin lines and small blue emphasis points.

For Markdown source:

- Use Mermaid diagrams.

## Content Rules for Architecture Decks

- Prefer architecture terms over marketing language.
- Use short, precise titles.
- Keep subtitles explanatory, not promotional.
- Use ISO/IEC 25010 terms when discussing quality attributes.
- Use `Functional Suitability`, `Performance Efficiency`, `Compatibility`, `Usability`, `Reliability`, `Security`, `Maintainability`, and `Portability` as the top-level QA vocabulary.
- Keep FR, NFR, QA, Use Case, Stakeholder labels consistent across slides.
- For dense slides, prefer structured tables or grids over paragraphs.

## Do

- Use one font family across the entire deck.
- Use 16:9 only.
- Keep title and subtitle positions consistent.
- Use alternating light and dark full-slide surfaces.
- Use Action Blue as the only accent.
- Fill the lower body area with meaningful structured content.
- Use clean architecture diagrams.
- Keep slides calm, premium, and highly legible.

## Do Not

- Do not use logos.
- Do not use decorative gradients.
- Do not use decorative shadows.
- Do not use multiple accent colors.
- Do not move chapter/title/subtitle positions randomly.
- Do not leave the bottom half empty unless the slide is an intentional chapter divider.
- Do not use dense paragraphs when a table, matrix, or diagram would communicate better.
- Do not use playful or illustrative visuals for serious architecture content.

## Default Deck Structure

When no deck structure is specified, use this 5-slide architecture structure:

1. Problem and Background
2. Target Service and Stakeholders
3. Key Use Cases
4. Functional Scope and SPRAG Pipeline
5. Quality Attributes and Architecture Drivers

For larger decks, expand in this order:

6. Detailed Use Case Flow
7. Offline Pipeline
8. Online Retrieval Pipeline
9. Security and ACL Policy
10. FR / NFR Traceability

## Output Expectations

The resulting deck should look like an Apple-inspired architecture briefing, not a corporate template. It should be quiet, spacious, dense enough to be useful, and consistent across all pages. Every slide should have a clear information hierarchy, stable header positions, and a filled but uncluttered body area.
