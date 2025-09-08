# Text Wrapping with overflow-wrap

This lesson demonstrates how `overflow-wrap` (previously `word-wrap`) handles long unbroken strings in table cells.

## What you'll learn

- Why long words or codes can break table layouts.
- How `overflow-wrap: break-word` forces text to wrap inside the cell.
- The difference between normal wrapping and break-word behavior.

## Explanation

- **Without overflow-wrap**  
  Long unbroken strings (like IDs, tracking numbers, or URLs) stay on one line and may overflow the cell.
- **With overflow-wrap: break-word**  
  The browser is allowed to break long words across lines to keep them inside the cell.

## How to run

Open `index.html` in your browser.  
You’ll see two columns:

- Normal → long string overflows.
- Break-word → long string wraps inside the cell.

## Notes

- Always use `overflow-wrap: break-word;` for columns that may contain long tokens (IDs, file names, URLs).
- Combine with `table-layout: fixed` for predictable column sizing.
