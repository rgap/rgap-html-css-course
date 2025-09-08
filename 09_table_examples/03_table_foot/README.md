# Table Head, Body & Foot

This lesson adds **`<tfoot>`** to the structure you built with `<thead>` and `<tbody>`.

## Why `<tfoot>` is useful

- **Summaries & totals**: Put roll-ups (totals, taxes, grand totals, “last updated” notes) in a consistent, semantic place.
- **Better printing**: Browsers can repeat the **header** at the top and the **footer** at the bottom of each printed page if you add a small `@media print` rule — we’ll cover that later.
- **Accessibility & structure**: Screen readers can identify the footer group, and your markup communicates intent (not just presentation).

> Note: HTML allows placing `<tfoot>` before `<tbody>` in the source (historically for streaming). Browsers still render it at the bottom of the table.

## What you’ll learn

- Where `<tfoot>` fits in the table structure.
- Common footer content (totals, notes).
- How to enable header/footer repetition in print.

## How to run

Open `index.html` in your browser.
You’ll see the same product/price table with a **Total** row in the footer.
