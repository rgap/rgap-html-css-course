# Table Cellspacing vs Padding

This lesson demonstrates the difference between the old HTML `cellspacing` attribute and modern CSS `padding`.

## What you'll learn

- How `cellspacing` adds space **between table cells**.
- How `padding` adds space **inside table cells**.
- Why `cellspacing` is deprecated and should be replaced with CSS.
- How to achieve the same effect using `border-spacing` in CSS.

## Explanation

- **Cellspacing (old HTML attribute)**
  - Example: `<table cellspacing="10">`.
  - Adds a gap between cells.
  - Deprecated in HTML5 → use CSS instead.
- **Padding (CSS)**
  - Example: `td { padding: 10px; }`.
  - Adds space inside each cell between the text and its border.
- **Border-spacing (CSS)**
  - CSS replacement for `cellspacing`.
  - Example: `table { border-spacing: 10px; border-collapse: separate; }`.

## How to run

Open `index.html` in your browser.  
You’ll see three tables:

1. Using `cellspacing` (legacy).
2. Using `padding` inside cells.
3. Using modern `border-spacing`.

## Notes

- Use **padding** for inner spacing.
- Use **border-spacing** for gaps between cells.
- Avoid `cellspacing` in modern projects — it’s only for backward compatibility.
