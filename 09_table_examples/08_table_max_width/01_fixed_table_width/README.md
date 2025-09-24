# Table — Auto & Fixed

**What this demo is**

A simple 2‑column HTML table that is given a **fixed total width of 500px**. Each `<th>` and `<td>` has a 1px border, and the layout uses the default **auto table layout algorithm** (no `table-layout: fixed`).

**What you will see**

- The table always spans **500px wide** overall.
- Column widths are decided by the **content**:

  - The short `Code` column stays narrow.
  - The long `Description` column takes up the rest of the space.

- Long text in the description cells **wraps onto multiple lines** so it doesn’t force the table wider than 500px.

**Why it behaves like this**

- With **`table-layout: auto`** (the default), the browser looks at the **content of each column** to determine widths.
- Setting `width: 500px` on the table ensures the **total width is capped**.
- Since no explicit column widths are given, the first column shrinks to its minimum content size and the second column expands to fill the remaining width.

**When to use this pattern**

- When you want a **total fixed table width**, but you are fine letting the browser distribute space automatically.
- Good for cases where one column has predictable short codes/IDs and the other column holds variable text.

**Limitations**

- You cannot guarantee **exact pixel widths per column**. Column distribution depends on content.
- For stricter control, you’ll need **`table-layout: fixed`** with `<colgroup>` or explicit `width` settings.

**Key CSS**

```css
table {
  border-collapse: collapse;
  width: 500px; /* fixed total width */
}
th,
td {
  border: 1px solid #444;
}
```

**Takeaway**

This is the **default table algorithm** at work: you get a fixed overall width but **content-driven column widths**. For precise, predictable tracks, you’ll switch to a fixed layout in later demos.
