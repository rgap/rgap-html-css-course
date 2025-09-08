# Border Spacing

This lesson explores the **`border-spacing`** property, which controls the distance between table cells.

## What you'll learn

- How to use `border-spacing: Xpx` for equal spacing.
- How to use `border-spacing: horizontal vertical` for different spacing values.
- Why `border-spacing` only works with `border-collapse: separate`.

## Explanation

- `border-spacing` adds empty space **between cells**.
- It accepts **one value** (applies to both horizontal & vertical)  
  or **two values** (`horizontal vertical`).
- It has **no effect** when `border-collapse: collapse`.

## How to run

Open `index.html` in your browser.  
You’ll see three examples:

1. Default (collapsed).
2. Separate with equal spacing.
3. Separate with different horizontal/vertical spacing.

## Notes

- Use this for “card-like” layouts where cells should not touch.
- For grid-style tables, stick with `collapse`.
