# Table Layout Fixed — Corrected

This version shows how to get predictable column tracks (**150px + 350px**) using `table-layout: fixed` with `<colgroup>`.

## Why this works

- **Authoritative widths on `<colgroup>`**  
  Set widths on `<col>` elements so the fixed-layout algorithm uses them as the column tracks.

- **Table width equals the sum of tracks**  
  `width: 500px` matches `150px + 350px`, avoiding redistribution of extra/deficit space.

- **Wrapping enabled**  
  `overflow-wrap: break-word` lets long tokens break instead of forcing track growth.

- **Collapsed borders**  
  `border-collapse: collapse` avoids extra gaps from separated borders.

## Content box vs. column track

- Declared column widths are **border-box** (include padding + borders).  
  With `padding: 8px 12px`, the text area inside a `150px` column is `~126px` wide.
- If you need the **content box** to be exactly `150px / 350px`, increase the tracks by the horizontal padding (24px):  
  set `--col1: calc(150px + 24px)` and `--col2: calc(350px + 24px)`.

## Why DevTools shows ~501px instead of 500px

- The `width: 500px` you set applies to the **content box** of the table.
- Each table still has **outer borders** (`1px` left and right). With `border-collapse: collapse`, the inner borders are merged, but the two outside edges remain.
- So the **rendered box** = `500px content + 1px left border + 1px right border = 502px`.
- Depending on zoom level and rounding, DevTools often reports this as **501px** instead of 502px.
- In short: the table really is 500px wide inside, but the _visual border-inclusive size_ is 501–502px.

## How to use

Open `index.html` and inspect the table with DevTools or a ruler:

- Column tracks stay at **150px** and **350px**.
- Long text wraps inside the second column instead of resizing it.
- The total table box may show ~501px because of the extra border pixels.
