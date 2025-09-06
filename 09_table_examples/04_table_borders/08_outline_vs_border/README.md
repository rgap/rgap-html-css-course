# Outline vs Border

This lesson explains the difference between using **CSS `border`** and **CSS `outline`** on tables.

## What you'll learn

- The difference in behavior between `border` and `outline`.
- How `border` affects layout and takes up space.
- How `outline` draws a line around an element but does **not** affect layout.
- Why outlines are mostly used for focus indicators (e.g., accessibility).

## Explanation

- **Border**
  - Part of the box model → affects element size and layout.
  - Can be applied per side (top, right, bottom, left).
- **Outline**
  - Drawn outside the border edge → does **not** affect layout.
  - Cannot be applied per side (only one outline around the whole element).
  - Commonly used for accessibility focus (`:focus { outline: 2px solid blue; }`).

## How to run

Open `index.html` in your browser.  
You’ll see two identical tables:

1. One using a border.
2. One using an outline.

## Notes

- Use **border** for design.
- Use **outline** for accessibility highlights (like keyboard navigation).
