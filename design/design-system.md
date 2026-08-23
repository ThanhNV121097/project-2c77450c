# Design System — hello-word-5

> Source of truth: the approved `index.html` (preview: approved design).
> Every value below is extracted from it. Changing a value here without
> changing the approved design is a defect.

Last updated: 2025-02-14

## 1. Foundations

### 1.1 Color

Semantic tokens. Name by job, never by hue.

| Token | Value | Used for |
|---|---|---|
| `--color-bg` | `#ffffff` | Page background |
| `--color-text` | `#000000` | Body text |

#### Contrast audit

Every text-on-background pair actually used. Body text ≥ 4.5:1, large text (≥ 18.66px bold or ≥ 24px) ≥ 3:1, UI borders ≥ 3:1.

| Foreground | Background | Ratio | Passes |
|---|---|---|---|
| `--color-text` | `--color-bg` | `21:1` | AA / AA Large |

### 1.2 Spacing

Base unit: `4px`. Every margin, padding, and gap in the product uses one of these.

| Token | Value |
|---|---|
| `--space-0` | `0px` |

### 1.3 Typography

Font families (include the fallback stack and how the font is loaded):

- Body: `Arial, Helvetica, sans-serif` (system font stack)
- Headings: `Arial, Helvetica, sans-serif` (system font stack)
- Mono: not used

| Token | Size | Line height | Weight | Used for |
|---|---|---|---|---|
| `--text-3xl` | `clamp(2rem, 8vw, 5rem)` | `1` | `400` | Single page headline |

Heading levels are used in order and never skipped for visual sizing.

### 1.4 Radius, border, shadow, motion

| Token | Value | Used for |
|---|---|---|
| `--radius-sm` | `0` | No rounded surfaces used |
| `--border-width` | `0` | No borders used |
| `--shadow-sm` | `none` | No elevation used |
| `--duration-fast` | `0ms` | No motion used |
| `--duration-base` | `0ms` | No motion used |
| `--easing` | `linear` | No motion used |

Motion respects `prefers-reduced-motion: reduce`: no animated states exist.

### 1.5 Layout and breakpoints

| Name | Min width | Container | Columns | Gutter |
|---|---|---|---|---|
| `sm` | `0px` | `100%` | `1` | `0px` |
| `md` | `768px` | `100%` | `1` | `0px` |
| `lg` | `1024px` | `100%` | `1` | `0px` |
| `xl` | `1280px` | `100%` | `1` | `0px` |

Z-index scale (only these values are allowed):

| Layer | Value |
|---|---|
| Base | `0` |
| Sticky header | `0` |
| Dropdown | `0` |
| Modal backdrop | `0` |
| Modal | `0` |
| Toast | `0` |

## 2. Components

One subsection per reusable component. Every component lists **all** states.

### 2.1 Centered message

**Purpose** — Single static headline, centered on screen. Not for interactive or multi-part content.

**Anatomy** — `[h1.message]`

**Variants**

| Variant | Tokens | When to use |
|---|---|---|
| Default | `--color-text`, `--color-bg`, `--text-3xl` | Single-screen greeting |

**Sizes**

| Size | Height | Padding | Text token |
|---|---|---|---|
| Default | `auto` | `0` | `--text-3xl` |

**States** — every row must be filled in.

| State | Visual change | Tokens |
|---|---|---|
| Default | Black centered text on white background | `--color-text`, `--color-bg` |
| Hover | No hover affordance | Same as default |
| Focus (keyboard) | No focus target | None |
| Active / pressed | No pressed state | None |
| Disabled | No disabled state | None |
| Loading | No loading state | None |
| Error | No error state | None |
| Empty | Not applicable; screen itself is the empty/initial state | None |

**Accessibility** — no interactive role. Headline text remains readable at all viewport widths. Minimum hit target not applicable.

## 3. Content and formatting

- Voice and tone in one line: plain, literal, no flourish.
- Date, time, number, and currency formats, with locale: not used.
- Capitalization rule for buttons, headings, and labels: heading case follows source text exactly; no buttons or labels exist.
- Empty-state and error-message wording pattern: not used.

## 4. Known deviations

Places where the approved design does not follow its own rules or the
anti-patterns in `references/ai-defaults.md`. Record, do not silently fix.

| Where | Deviation | Why it stands | Follow-up |
|---|---|---|---|
| Layout scale | No spacing scale beyond `0px` exists | Approved design uses only full-screen centering with no inner spacing | None |
| Typography | Only one displayed size exists | Single-screen mockup needs one headline only | None |
| Radius / shadow / motion | No radius, shadow, or motion values exist | Plain proof-of-pipeline screen has no such UI | None |
| Components | No interactive components exist | Product contains only static greeting | None |

## 5. Change log

| Date | Change | Design PR |
|---|---|---|
| 2025-02-14 | Initial design system for hello-word-5 | pending |
