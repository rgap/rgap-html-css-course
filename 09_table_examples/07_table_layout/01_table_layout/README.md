# Table Layout Fixed

This lesson demonstrates the difference between `auto` (default) and `fixed` table layouts, and shows why simply adding `width` on table cells does not always produce the exact pixel values you expect.

## What you'll learn

- How browsers size columns with `auto` vs. `fixed` layout.
- Why adding `width` on `<th>/<td>` is not always enough for precise control.
- How **padding, collapsed borders, and rounding** affect the _visible_ column size.
- Why `fixed` can still be useful for performance and predictability.
- How to get **truly consistent** column tracks with `<colgroup>`.

## Explanation

### Auto (default)

- The browser looks at the content in all rows to decide column widths.
- A long or unbreakable word will stretch the column.
- Good when you want columns to adapt naturally to the data.

### Fixed (with widths on cells)

- Applying `width` to `th`/`td` **suggests** a target size, but:

  - On table cells, `width` sets the **content box**. Padding and borders add on top of that content width (increasing the visible border-box width).
  - With `border-collapse: collapse`, vertical borders are **shared** between columns and may be painted on either side.
  - When widths are set on **cells** (not on `<colgroup>`), the fixed-layout algorithm reconciles hints across rows; final tracks can differ slightly from your numbers.
  - Rounding to **integer CSS pixels** at the current zoom can nudge where a shared 1px border lands.

Despite these limits, `table-layout: fixed` makes layout calculation **fast and predictable**, especially for large tables.

---

## Why you may see **175px / 375px** at 100% zoom

Suppose you declare:

- Table width: **500px**
- Column widths (on cells): **150px** and **350px**
- Cell styles: `padding: 8px 12px` (so **24px** horizontally) and `border: 1px`
- `border-collapse: collapse`

What you often _measure_ (via DevTools or `getBoundingClientRect()` on a cell) are the **border-box** sizes, not the pure track widths. Per column, the observed \~25px extra comes from **padding (24px)** plus \~**1px** from the **collapsed border** after rounding:

- **Col 1 (painted cell width) ≈** `150 (content)` + `12 + 12 (padding)` + `~1 (collapsed vertical border / rounding)` → **≈ 175px**
- **Col 2 (painted cell width) ≈** `350 (content)` + `24 (padding)` + `~1 (collapsed vertical border / rounding)` → **≈ 375px**

> Note: 175/375 are the **painted cell boxes** you inspect. They do **not** prove the underlying tracks changed; they reflect padding and the shared collapsed border. Also, the _visual_ width of the whole table can exceed the declared `width: 500px` once padding and collapsed borders are included—see the 551px calculation below.

---

## Why the whole table can read **\~551px** (not 500px)

When you measure the _visual_ width of the table (e.g., in DevTools, looking at the painted border box in the collapsed-border model), the total includes:

- Sum of **content widths** you declared (150 + 350 = **500px**)
- **Horizontal padding** for each column (12px left + 12px right = **24px** per column → **48px** for 2 columns)
- **Collapsed internal border(s)**: 1px between columns → **+1px**
- **Outer left/right collapsed borders**: typically 1px each → **+2px**

**Total visual width ≈ 500 + 48 + 1 + 2 = 551px.**

That’s why you may see the table itself reported around **551px** wide while each column’s painted cell boxes read **≈175px** and **≈375px**.

---

## How to get _exact_ tracks

If you need columns that are **mathematically exact** (e.g., exactly 150px / 350px as tracks), do this:

1. **Declare tracks on `<colgroup>`** (authoritative for the fixed algorithm):

   ```html
   <table class="fixed">
     <colgroup>
       <col style="width:150px" />
       <col style="width:350px" />
     </colgroup>
     …
   </table>
   ```

2. Keep `table-layout: fixed; border-collapse: collapse;`.
3. Allow wrapping so content doesn’t force changes:

   ```css
   .fixed td,
   .fixed th {
     overflow-wrap: break-word;
   }
   ```

### If you want the _content box_ to be exactly 150px / 350px

Add the horizontal padding to your track sizes. For `padding: 8px 12px`:

- Content 150px ⇒ Track ≈ **174px** (150 + 24)
- Content 350px ⇒ Track ≈ **374px** (350 + 24)

So set:

```html
<colgroup>
  <col style="width:174px" />
  <col style="width:374px" />
</colgroup>
```

This makes the **content area** inside each cell \~150px / \~350px, while the **visible** border-box width will read \~175 / \~375 (depending on which side receives the shared collapsed border after rounding).

---

## How to run

Open `index.html` in your browser. You’ll see two tables:

1. **Default auto layout** → columns expand to fit their longest content.
2. **Fixed layout (with widths on cells)** → columns are closer to the declared sizes; the painted cell widths include padding and the collapsed borders, so you may observe **\~175px / \~375px** per column and a **total visual table width \~551px**.

---

## Notes & tips

- For **truly consistent** column tracks, use `<colgroup>` with `table-layout: fixed`.
- Cell `width` targets the **content box**; padding and borders make the **visible** cell wider.
- Enable wrapping with `overflow-wrap: break-word` to prevent long tokens from blowing up a column.
- `border-collapse: collapse` removes double borders, but the **shared** inner border is a real painted pixel that can land on either column after rounding.
- When inspecting sizes, DevTools often shows the **painted border box**. In collapsed mode that can be **content tracks + padding + internal 1px + outer 2px**, which explains totals like **551px** for a 2‑column `500px` table.
- **Verify the math quickly:**

  - Set `td, th { padding: 0 }` → total visual width drops by 48px (from \~551px → \~503px due to borders).
  - Then set `td, th { border: 0 }` (still collapsed) → total becomes \~**500px**.
  - Or keep styling but move track widths to `<colgroup>` for authoritative tracks.
