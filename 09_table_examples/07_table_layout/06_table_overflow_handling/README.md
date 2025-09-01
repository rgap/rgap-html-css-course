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
- **Scroll**  
  Forces scrollbars inside the cell whether needed or not.
- **Auto**  
  Adds scrollbars only if content is larger than the cell.
- **Clip**  
  Like `hidden`, but stricter: no scrollable overflow region is created.

## How to run

Open `index.html` in your browser.  
You’ll see one row with the same long text across five cells, each using a different `overflow` setting. Compare how each cell handles extra content.

## Notes

- `table-layout: fixed` is required for columns to obey defined widths.
- `clip` is newer and behaves similarly to `hidden` but cannot be scrolled.
- For UI design:
  - Use **hidden** with ellipsis (covered in the next lesson) for clean truncation.
  - Use **auto** for cells where scrolling is acceptable.
  - Avoid **scroll** unless you always want scrollbars visible.
