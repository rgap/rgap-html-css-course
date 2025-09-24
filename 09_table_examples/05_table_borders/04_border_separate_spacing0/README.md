# Border Collapse vs Separate (Zero Spacing)

This lesson shows how **`border-collapse: separate` with `border-spacing: 0`** behaves compared to the default “collapsed” model—and why borders can look **thicker**.

## Explanation

- **Collapsed model (`border-collapse: collapse`)**
  Adjacent cell borders **merge** into a single border, so a 1px grid looks truly 1px.

- **Separate model (`border-collapse: separate; border-spacing: 0`)**
  Cells **do not merge** borders. Each cell draws its own 1px edge, so adjacent edges sit back-to-back and appear \~2px thick.
  Setting `border-spacing: 0` removes the _gap_ between cells, but it **doesn’t merge** borders.

- **Result in this demo**: with `separate` + `border-spacing: 0` + `th, td { border: 1px }`, the grid lines look thicker than expected.

- **Crisp 1px grid while keeping `separate`**:
  Put a **single outer border** on the table; on cells, draw only **`border-right`** and **`border-bottom`** (omit left/top). The table’s outer border provides the left/top edges, avoiding the doubled look.

## How to run

Open `index.html` in your browser.
You’ll see a table using **`border-collapse: separate; border-spacing: 0;`** with 1px borders on cells, exhibiting the “thick” grid effect.

## Notes

- Use **`collapse`** for classic grid tables where merged, single-pixel lines are desired with minimal CSS.
- Use **`separate`** when you need features like intrinsic width behavior or **`border-spacing`** gaps—but draw **one-sided** borders on cells (plus an outer table border) to avoid the doubled look.
- If borders still feel heavy, reduce contrast (e.g., `#666` or `rgba(0,0,0,.4)`) or try `border-width: .5px` on HiDPI screens.
