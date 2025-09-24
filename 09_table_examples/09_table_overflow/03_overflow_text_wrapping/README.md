# Table Overflow Handling — `visible`, `hidden`, `scroll`, `auto`, `clip`

**What this demo is**

A 5‑column table (fixed layout, 200px tracks) showing how each `overflow` value affects content that exceeds a cell’s width/height. Cells also set different `white-space` values to make the effect obvious.

* **Visible** — content can spill outside the cell box.
* **Hidden** — overflow is clipped (no scrollbars).
* **Scroll** — always shows scrollbars.
* **Auto** — scrollbars only if needed.
* **Clip** — like hidden, but *no* scrollable overflow region.

`table-layout: fixed` ensures columns don’t expand to fit content, so the *overflow behavior* is what you notice.

---

## How each value behaves

### 1) `overflow: visible` (default)

* Content is **not clipped**; it can **paint outside** the cell’s box.
* Useful for tooltips/popovers anchored to content; risky for dense grids because spillover can obscure neighbors.

### 2) `overflow: hidden`

* Content that exceeds the box is **clipped**, **no scrollbars**.
* Combine with **single‑line truncation** if desired:

  ```css
  .truncate-1 {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis; /* shows … when clipped */
  }
  ```
* For multi‑line truncation, prefer an **inner wrapper** and clamping (see recipes below).

### 3) `overflow: scroll`

* Cell **always** shows scrollbars (even if not needed).
* Makes overflow **discoverable**, but visually noisy; generally avoid in production.

### 4) `overflow: auto`

* Adds scrollbars **only when needed**.
* Good default when you must preserve all text **without** expanding row height.

### 5) `overflow: clip`

* Clips like `hidden`, but there is **no scrollable overflow** region.
* Slightly stricter semantics; pairs with `text-overflow` on single‑line blocks.

---

## Key interactions

* **`table-layout: fixed`** keeps column widths **authoritative**; cells won’t widen to fit long text. Choose `overflow` (and `white-space`) to control the outcome.
* **`white-space`** matters:

  * `nowrap` keeps one line → use `hidden/auto` + `text-overflow: ellipsis` for truncation, or `auto` for horizontal scroll.
  * `normal` lets text wrap → less overflow horizontally, but rows may grow vertically.
* **`overflow-wrap`** can prevent horizontal overflow by allowing mid‑word breaks:

  ```css
  th, td { overflow-wrap: break-word; } /* or: anywhere */
  ```

---

## Practical recipes

**A) Single‑line truncation (labels, IDs)**

```css
.cell-1line {
  white-space: nowrap;
  overflow: hidden;            /* or clip */
  text-overflow: ellipsis;
}
```

**B) Scroll inside the cell (preserve all text)**

```css
.cell-scroll-x {
  white-space: nowrap;         /* keep one line */
  overflow-x: auto;            /* show scrollbar if needed */
  overflow-y: hidden;          /* avoid vertical bar */
}
```

**C) Multi‑line clamp (strict row heights)**

> Use an **inner wrapper**; clamping directly on `td` can fight table layout.

```html
<td><div class="clamp2">Long text…</div></td>
```

```css
.clamp2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;       /* visible lines */
  -webkit-box-orient: vertical;
  overflow: hidden;            /* needed to clip */
}
```

**D) Robust wrapping for hostile tokens**

```css
th, td { overflow-wrap: anywhere; } /* guarantees wrap even mid‑word */
```

---

## UX polish

* **Scrollbar gutter** (avoid layout shift as scrollbars appear):

  ```css
  .cell-scroll-x { scrollbar-gutter: stable both-edges; }
  ```
* **Touch friendliness**: add `overscroll-behavior: contain;` on scrollable cells to prevent parent scroll hijacking.
* **Media**: constrain images/iframes in cells with `max-width: 100%; height: auto;`.

---

## Key CSS in this demo

```css
table { table-layout: fixed; border-collapse: collapse; width: 1000px; }
th, td { border: 1px solid #444; padding: 8px; }
col { width: 200px; }

/* Visible (default painting outside box) */
td.visible { overflow: visible; white-space: normal; }

/* Hidden (clip; often with ellipsis for single line) */
td.hidden  { overflow: hidden; white-space: nowrap; }

/* Scroll (always shows bars) */
td.scroll  { overflow: scroll; white-space: nowrap; }

/* Auto (bars only if needed) */
td.auto    { overflow: auto; white-space: nowrap; }

/* Clip (like hidden, but no scrollable overflow region) */
td.clip    { overflow: clip;  white-space: nowrap; }
```

**Takeaway**

Choose `overflow` based on the UX you want:

* **Show everything** → `auto` with internal scroll.
* **Keep layout clean** → `hidden/clip` + truncation.
* **Testing/diagnostics** → `scroll` (always visible bars).
* **Free‑flowing content** → `visible` (use sparingly in dense tables).

Then refine with `white-space`, `overflow-wrap`, and inner wrappers to balance **readability, density, and resilience**.
