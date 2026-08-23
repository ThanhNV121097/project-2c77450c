# SRS — home

Module: `home`
Last updated: 2025-02-14
Design: [View the approved design](http://localhost:8080/design/2c77450c-afa1-46e0-bda9-f647abb6c7e6)
Design system: `design/design-system.md`

> One file per module, at `docs/{module}/SRS.md`. It covers only the functions that belong to this module. Never write `docs/SRS.md`.

## 1. Purpose

`home` shows one plain greeting page. Guest users open the app and see stored text centered on white background, with black text and no extra UI. If this module does not exist, product has no visible end-to-end proof that backend, database, and frontend work together.

## 2. Actors

| Actor | Who they are | What they may do in this module |
|---|---|---|
| Guest | Any visitor | Open home page and read greeting text |
| Operator | Project maintainer | Verify page reflects stored greeting text through normal app flow |

## 3. Scope

**In scope** — the functions specified below, by their plan titles:

- Render centered greeting

**Out of scope** — name what a reader would reasonably expect here and say where it lives instead.

- Editing greeting text — belongs to another module if added later; not built in this project.
- Authentication, user accounts, and admin tools — not built; this project is public only.
- Visual variants, themes, motion, or extra content — deliberately not built; product goal is plain pipeline proof only.

## 4. Functional requirements

### 4.1 Render centered greeting

**Requirement HOME-001 — Show stored greeting**

*As a* Guest, *I want to* see greeting text read from backend data, *so that* page proves text comes from PostgreSQL rather than hardcoded frontend copy.

Behaviour:

1. Guest opens home page.
2. App requests greeting text through backend API.
3. Backend returns stored row from PostgreSQL.
4. Page renders returned text exactly as stored.

**Requirement HOME-002 — Center greeting on plain screen**

*As a* Guest, *I want to* see greeting centered on plain white screen, *so that* page matches minimal design.

Behaviour:

1. Guest opens home page.
2. Page shows one line of black text on white background.
3. Text sits centered horizontally and vertically in viewport.
4. Page shows no extra controls, images, borders, or animation.

**Acceptance criteria** — each maps one-to-one onto a test case in `docs/home/test-cases/render-centered-greeting.md`.

| # | Given | When | Then |
|---|---|---|---|
| AC-1 | PostgreSQL row contains `Hello Word` | Guest loads home page | Page displays `Hello Word` and same text comes from backend path, not frontend constant |
| AC-2 | Stored greeting exists | Guest loads home page | Text is black, screen is white, and greeting is centered both horizontally and vertically |
| AC-3 | Stored greeting exists | Guest loads home page | Page shows no extra UI, animation, or decorative content |

**Failure, boundary and permission behaviour**

| Case | Condition | Expected behaviour |
|---|---|---|
| Invalid input | Stored greeting text is empty | Page shows empty center state or configured fallback from backend, not frontend hardcoded text; no crash |
| Boundary | Greeting text is very short or very long | Text still renders and stays within page bounds; wrapping is allowed, horizontal overflow is not |
| Not found | Greeting row is missing | Page shows explicit error state instead of blank page |
| Not permitted | Guest opens page | Access is allowed; no login wall or permission prompt |
| Conflict | Greeting row changes during page load | Page shows one consistent response from one request cycle; reload picks up later value |
| Upstream failure | Backend or database unavailable | Page shows error state with retry path; no partial or stale write occurs |

**Data touched** — the fields this function reads and writes, in product terms.

| Field | Type | Required | Rule |
|---|---|---|---|
| Greeting text | text | yes | Stored in one row; plain text only; displayed exactly as returned |

### 4.2 Centered presentation

**Requirement HOME-003 — Use approved minimal palette**

*As a* Guest, *I want to* see the approved minimal look, *so that* page stays plain and distraction free.

Behaviour:

1. Guest opens home page.
2. Page uses white background and black text only.
3. Page uses no palette, no animation, and no extra layout chrome.

**Acceptance criteria**

| # | Given | When | Then |
|---|---|---|---|
| AC-1 | Page loads successfully | Guest views home page | Background is white and text is black |
| AC-2 | Page loads successfully | Guest views home page | No animation or decorative UI appears |

**Failure, boundary and permission behaviour**

| Case | Condition | Expected behaviour |
|---|---|---|
| Invalid input | Browser or device uses unusual viewport size | Layout still keeps greeting centered without horizontal scroll |
| Boundary | Viewport is 320px wide | Content remains readable and centered |
| Not found | Design assets are unavailable | Page still renders plain default minimal state |
| Not permitted | Guest attempts unsupported edit | No edit surface exists in product |
| Conflict | Two renders occur close together | Latest successful render wins visually |
| Upstream failure | Styling asset fails to load | Page still renders plain white/black fallback |

**Data touched** — the fields this function reads and writes, in product terms.

| Field | Type | Required | Rule |
|---|---|---|---|
| Background color | visual token | yes | White only |
| Text color | visual token | yes | Black only |

## 5. Screens

| Screen | Section in the design | Functions it serves | States that must exist |
|---|---|---|---|
| Home | Home | HOME-001, HOME-002, HOME-003 | default, loading, empty, error |

## 6. Non-functional requirements

| Area | Requirement |
|---|---|
| Performance | Home page starts rendering within 2s on typical connection after backend responds |
| Accessibility | Greeting remains readable with keyboard focus not required because no interactive controls exist; contrast is at least 4.5:1 |
| Responsive | Works at 320px and up with no horizontal page scroll |
| Localisation | Copy is in English |
| Privacy | No personal data stored or shown in this module |

## 7. Dependencies and assumptions

- **Depends on:** backend API and PostgreSQL, for reading stored greeting text.
- **Assumption:** stored greeting is a single plain-text row. If false, backend and data contract must expand.

| Open question | Proposed default | Who decides |
|---|---|---|
| What exact fallback appears if greeting row is missing? | Explicit error state with retry | Stakeholder / TL |
| Should greeting preserve line breaks if stored text contains them? | Yes, render text as plain text with normal browser wrapping | Stakeholder / TL |

## 8. Traceability

| Plan item | Requirement ids | Test cases |
|---|---|---|
| Render centered greeting | HOME-001, HOME-002, HOME-003 | `test-cases/render-centered-greeting.md` |
