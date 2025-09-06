# Table Cell Padding vs Margin

This lesson explains how `padding` and `margin` behave differently in table cells.

## What you'll learn

- `padding` adds space **inside** the cell, between the content and the cell border.
- `margin` normally adds space **outside** an element, but table cells don’t behave like block elements.
- Why margins on `<td>` and `<th>` are usually ignored.
- How to properly space content inside table cells.

## Explanation

- **Padding**
  - Works consistently in table cells.
  - Expands the clickable/content area.
  - Commonly used to add breathing room around text.
- **Margin**
  - On `<td>` and `<th>`, margins generally don’t work (CSS spec).
  - Instead, use `padding`, `border-spacing`, or wrapper elements inside the cell for spacing.

## How to run

Open `index.html` in your browser.  
You’ll see two rows:

1. A cell with extra padding (clear space inside the border).
2. A cell with a child `<div>` that has margin (the margin affects the child, not the `<td>`).

## Notes

- Always prefer **padding** to control spacing inside cells.
- Use `border-spacing` or nested wrappers for outer spacing.
