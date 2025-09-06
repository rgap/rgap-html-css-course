# Table Overflow Handling — All Values

This lesson demonstrates all major CSS `overflow` values inside table cells.

## What you'll learn

- How each `overflow` value changes how extra content is displayed in a fixed-width table cell.
- The difference between `visible`, `hidden`, `scroll`, `auto`, and `clip`.
- Why controlling overflow is important for stable table layouts.

## Explanation

- **Visible (default)**  
  Content spills out of the cell if it’s too long. The cell itself does not clip text.
- **Hidden**  
  Extra content is cut off (clipped). Combined with `white-space: nowrap` to prevent wrapping.  
  The element is still a _scroll container_ → JavaScript can read and change `scrollWidth`/`scrollLeft` values even though the user sees no scrollbars.
- **Scroll**  
  Forces scrollbars inside the cell whether needed or not.
- **Auto**  
  Adds scrollbars only if content is larger than the cell.
- **Clip**  
  Looks the same as `hidden`, but no scrollable overflow region exists.  
  In JavaScript, `scrollWidth` just equals `clientWidth` and `scrollLeft`/`scrollTop` stay `0`.

## How to run

Open `index.html` in your browser.  
You’ll see one row with the same long text across five cells, each using a different `overflow` setting. Compare how each cell handles extra content.

## Notes

- `table-layout: fixed` is required for columns to obey defined widths.
- The difference between **hidden** and **clip** only matters when working with scroll APIs in JS:
  - **hidden** keeps an overflow region (can be scrolled programmatically).
  - **clip** does not (no scrolling possible).
- For UI design:
  - Use **hidden** with ellipsis (covered in the next lesson) for clean truncation.
  - Use **auto** for cells where scrolling is acceptable.
  - Avoid **scroll** unless you always want scrollbars visible.
