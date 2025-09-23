# Fixed Row Height — 2×2

**What this demo is**

A very simple table (2 columns × 2 rows) that sets `height: 40px` on every `<th>` and `<td>`. It keeps normal table behavior (columns align, borders collapse).

**What you will see**

* Short cells look about **41px** tall (≈ 40px content height + \~1px from collapsed borders).
* If a cell has **long text**, the **row grows taller** to fit the content. There is **no clipping** and **no ellipsis**.

**Why it behaves like this**

* In tables with `border-collapse: collapse`, the CSS `height` on a cell is a **minimum** for the **content box**.
* The **visible** row height is the content height **plus** the shared collapsed borders (≈ +1px).
* Because there is **no overflow control**, content is allowed to make the row taller.

**When to use this pattern**

* When you want a clean, default table where **all text is visible**.
* When exact, fixed row heights are **not required**.

**Limitations**

* You **cannot guarantee** a fixed visual row height. Long text will **expand** rows.
* No truncation or ellipsis—rows grow instead of hiding text.

**Key CSS used**

```css
table {
  border-collapse: collapse;
  table-layout: fixed;
}
th, td {
  border: 1px solid #444;
  padding: 0;
  height: 40px; /* minimum content height; row can grow */
}
```

**Takeaway**

This file is the **baseline**: it shows that setting `height` on table cells **does not** hard‑lock the row height. For strict heights you’ll need clipping, clamping, or an inner wrapper in later demos.
