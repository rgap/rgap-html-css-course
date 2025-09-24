# Table — Column Widths via Header Classes (150px / 350px)

**What this demo is**

A 2‑column table where only the **header cells** (`<th>`) carry width classes:

```css
th.col-1 {
  width: 150px;
}
th.col-2 {
  width: 350px;
}
```

This suggests a **150px** column for `Code` and **350px** for `Description`. Body cells (`<td>`) inherit the column tracks chosen by the browser’s **auto table layout**.

**What you will see**

- The table typically renders close to **150px / 350px** columns.
- Long description text **wraps within the second column** (≈350px) instead of stretching the table.
- Overall width approximates **500px** (plus borders), provided content can wrap.

**Why it behaves like this**

- In `table-layout: auto` (default), the browser computes column widths from **all cells in the column**. A declared width on a `<th>` is a **strong hint** that influences the chosen track size.
- Since both headers carry concrete widths, the layout tends to honor **150 / 350** as long as the content **can** fit by wrapping.

**When to use this pattern**

- You want quick, readable widths without adding `<colgroup>` yet.
- The table is small/simple and content is mostly **wrappable text**.

**Limitations**

- **Not a hard guarantee**: Certain content can override the hint and **force the column wider** (e.g., large images, long unbreakable strings like `SuperLongWordWithoutBreaks`, long URLs without hyphens).
- **Maintenance**: Width classes on headers couple presentation to markup; duplicating in multiple tables can get repetitive.
- **Col/row spans**: Complex spanning can reduce predictability.

**Gotchas & tips**

- To handle long unbreakable tokens, add a breaker:

  ```css
  td,
  th {
    overflow-wrap: anywhere;
  }
  /* or break-word */
  ```

- If you need **strict control**, prefer:

  - `table-layout: fixed` **plus** `<colgroup><col style="width:…">…` for authoritative tracks, or
  - Explicit widths on `<col>` elements rather than headers.

**Key CSS used**

```css
table {
  border-collapse: collapse;
}
th,
td {
  border: 1px solid #444;
}

/* Header widths act as column hints in auto layout */
th.col-1 {
  width: 150px;
}
th.col-2 {
  width: 350px;
}
```

**Takeaway**

Header‑only width classes are a **convenient hint** that usually yields 150/350 tracks for simple, text‑heavy tables. For **robust, exact** column widths—especially with images, long tokens, or complex spans—use **`table-layout: fixed` + `<colgroup>`** so the column tracks are authoritative rather than heuristic.
