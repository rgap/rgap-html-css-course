# Table — Equal Column Widths (250px each)

**What this demo is**

A 2-column table where both `<th>` and `<td>` cells are given a **fixed width of 250px**. With two columns, the table effectively becomes **500px wide total**. Borders are 1px, and text wraps naturally.

**What you will see**

- Each column is locked to **250px width** regardless of content.
- Long text inside the `Description` column **wraps onto multiple lines** within the fixed 250px width.
- The table doesn’t expand beyond 500px because every cell has the same set width.

**Why it behaves like this**

- Assigning `width: 250px` to both `<th>` and `<td>` ensures all cells in that column obey this size.
- The browser respects these explicit widths even with `table-layout: auto`, because the widths are concrete.
- Content that doesn’t fit in a single line simply **wraps** instead of forcing the table wider.

**When to use this pattern**

- When you want **equal-sized columns** in a simple table.
- Good for layouts where consistency matters more than dynamic distribution.

**Limitations**

- This hard-codes column widths. If you change the number of columns, you need to manually recalc widths.
- Less flexible than `colgroup` or `table-layout: fixed` for larger/more complex tables.
- Can cause horizontal overflow if the table has more columns and the fixed widths don’t fit the container.

**Key CSS**

```css
table {
  border-collapse: collapse;
}
th,
td {
  border: 1px solid #444;
  width: 250px; /* every cell 250px wide */
}
```

**Takeaway**

This demo shows a **forced equal-width table**: all columns are exactly the same width (250px here). It’s simple and predictable, but less flexible than using `<colgroup>` or a fixed layout for scalable designs.
