# Fixed Row Height — `display:block` Variant

This lesson demonstrates how to force a table cell to behave like a block box so that its height and overflow rules apply strictly, and why the **visible row** is ~41 px even when `height: 40px` is declared.

## What you'll learn

- How `height` on `<td>` targets the **content box**, not the outer border.
- Why a 40 px content height shows up as ~41 px visible when borders collapse.
- How turning a cell into a block (`display: block`) changes its overflow behavior.
- Trade-offs: fixed clipping vs. loss of true table-cell alignment.

## Explanation

- **Height vs. visible size**

  - `td { height: 40px; }` sets a 40 px content box.
  - With `border-collapse: collapse` and 1 px borders, the row renders as ~41 px visible.
  - Rows will still expand if content wraps unless overflow is managed.

- **Why use `display: block` on a `<td>`**

  - A table cell normally ignores strict overflow and will expand.
  - With `td.clip { display: block; }`, the cell behaves like a block box:
    - It respects the fixed 40 px height.
    - Extra text is hidden (or managed with CSS).
  - Trade-off: the cell is no longer a “true” table cell, which may break alignment in multi-column tables.

- **Overflow control**
  - `overflow: hidden;` keeps the cell visually fixed.
  - `white-space: normal;` allows wrapping inside the box (but clipped).
  - Multi-line ellipsis is not standard; `-webkit-line-clamp` is needed if you want a capped number of lines.

## How to run

Open `index.html` in your browser. You’ll see three rows:

1. Short text — visible height **≈ 41 px** (40 px content + collapsed border).
2. Long text (normal cell) — row **expands beyond ≈ 41 px** because the cell auto-grows.
3. Long text with `td.clip` — the cell is blockified and clipped; the visible row stays **≈ 41 px** regardless of text length.

## Notes

- Table rows **cannot shrink below content** unless you clip or change the box model.
- The `display:block` trick is fine for demos or single-column tables, but for real layouts an inner wrapper is safer.
- If you truly need visible **40 px rows**, set `td { height: 39px; }` or remove borders.
- Expect ±1 px differences due to zoom and device-pixel rounding.
