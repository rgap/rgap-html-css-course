# Table Text Overflow: Ellipsis

This lesson demonstrates how to truncate overflowing text with an ellipsis (`…`).

## What you'll learn

- How `text-overflow: ellipsis` works.
- The required CSS properties for it to function correctly.
- Why it’s often paired with `nowrap`.

## Explanation

To make ellipsis work, you need:

1. A fixed width (via column or table width).
2. `overflow: hidden` to clip text.
3. `white-space: nowrap` to prevent wrapping.
4. `text-overflow: ellipsis` to show `…`.

If any of these are missing, ellipsis won’t appear.

## How to run

Open `index.html` in your browser.  
You’ll see three columns:

1. Normal wrap (text flows onto multiple lines).
2. Hidden overflow (text clipped with no indicator).
3. Ellipsis (truncated text with `…` at the end).

## Notes

- Ellipsis is widely used in dashboards, product lists, and file browsers.
- Best combined with a tooltip (hover to see full content).
- Works horizontally — not for vertical overflow.
