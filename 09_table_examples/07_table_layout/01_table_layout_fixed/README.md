# Table Layout Fixed

This lesson shows how to use `table-layout: fixed` to control how column widths are calculated.

## What you'll learn

- The difference between `auto` (default) and `fixed` table layouts.
- How `table-layout: fixed` makes column widths respect `width` settings.
- Why `fixed` improves performance for large tables.

## Explanation

- **Auto (default):**
  - Browser looks at content in all rows to decide column widths.
  - Wider content can force column expansion.
- **Fixed:**
  - Column widths are determined by CSS `width` (or `<col>` definitions).
  - Content that doesn’t fit will wrap or overflow.
  - Layout is calculated faster (useful for big data tables).

## How to run

Open `index.html` in your browser.  
You’ll see two tables:

1. Default auto layout → columns expand to fit text.
2. Fixed layout → columns respect fixed widths, text wraps.

## Notes

- Combine with `<colgroup>` or `th/td { width: … }` to enforce widths.
- Works best with `border-collapse: collapse` and controlled widths.
