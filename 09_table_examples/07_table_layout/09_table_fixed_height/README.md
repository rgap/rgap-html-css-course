# Fixed Row Height (and why you see \~41 px)

This lesson shows how `height` on table cells targets the **content box** (not the outer edge), so with collapsed borders the **visible** row ends up a bit taller than the declared height.

## What you'll learn

- `height` on `<td>` applies to the **content box** only.
- With `border-collapse: collapse`, top/bottom borders add to the visible height.
- Why DevTools often reports \~**41 px** when you set **40 px**.
- When/why rows still expand if content is taller, and how to clip without extra wrappers.

## Explanation

- **Why 40 px becomes \~41 px**

  - `td { height: 40px; }` sets a 40 px **content** box.

  - With `border-collapse: collapse` and `1px` borders, the visible row is:

    - 40 px (content) + \~1 px (collapsed border overlap) = **≈ 41 px**.

  - That’s why your “40 px rows” measure around 41 px in DevTools.

- **Exact 40 px (visible) — options**

  - Reduce the content height to account for borders, e.g. `td { height: 39px; }`.
  - Or remove borders (no extra pixel).
  - Be aware that fractional zoom/device pixel ratios can still show ±1 px variance.

- **Overflow behavior on table cells**

  - Many browsers treat `overflow` on `table-cell` inconsistently; rows may expand when content wraps.
  - To clip **without wrappers**, apply a class directly to the `<td>`:

```css
/* Use on <td class="clip"> ... */
.clip {
  overflow: hidden;
  white-space: nowrap; /* prevent wrapping */
  text-overflow: ellipsis;
}
```

- **`min-height`**

  - `min-height` is ignored on table cells in most browsers.
  - Prefer `height` + the `.clip` approach (or wrap content in a block element if you’re okay with an inner wrapper).

## How to run

Open `index.html`. You’ll see three rows:

1. Short text — visible height **≈ 41 px** (40 px content + border).
2. Long text (no `.clip`) — row **expands beyond ≈ 41 px** because wrapping makes the cell grow.
3. Long text with `td.clip` — content is **clipped** to the 40 px content box; visible height still **≈ 41 px** due to border.

## Notes

- Table rows **won’t shrink below their content** unless you clip or prevent wrapping.
- For strict fixed-height cells **without extra wrappers**, use a TD class like `.clip`.
- If you truly need a visible **40 px**, compensate for borders (`height: 39px`) or remove borders altogether.
- Small ±1 px differences are normal due to zoom and device-pixel rounding.
