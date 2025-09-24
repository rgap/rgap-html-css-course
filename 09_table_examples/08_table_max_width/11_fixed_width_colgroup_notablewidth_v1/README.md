# `display: inline-table` — Shrink‑Wrap Tables

**What this demo is**

A 2‑column table whose column tracks are defined via `<colgroup>` (**150px / 350px**). The table uses:

```css
 table {
   border-collapse: collapse;
   display: inline-table;   /* shrink-wrap to intrinsic width */
   table-layout: fixed;     /* honor <colgroup> track sizes */
 }
```

The focus here is **`display: inline-table`**.

---

## What `inline-table` does

* **Shrink‑wraps** the table’s box to its **intrinsic width** (≈ sum of column tracks + borders), instead of stretching to the container like a block.
* Makes the table behave like an **inline-level replaced element** (similar to an image) for layout/flow purposes:

  * It can sit inline with text or other inline/inline‑block elements.
  * It respects **vertical‑align** in inline formatting contexts.

With fixed tracks of **150px + 350px**, the intrinsic width is \~**500px** (plus borders), so the table naturally sizes to \~500px **without** setting `width: 500px;`.

---

## Why pair it with `table-layout: fixed`

* `table-layout: fixed` makes `<colgroup>` widths **authoritative** and avoids content re‑measurement.
* Together with `inline-table`, you get a table that is **exactly as wide as its tracks** and **won’t stretch** just because the container is wider.

---

## When to use `inline-table`

* You want a table to **size to its tracks** (or content) rather than **fill the container**.
* You’re laying out multiple small tables side‑by‑side or inline within prose.
* You need **precise width** without hard‑coding `width: …` (useful for reusable components).

---

## Differences vs `display: table` (block default)

| Aspect             | `table` (block)                    | `inline-table`                                     |
| ------------------ | ---------------------------------- | -------------------------------------------------- |
| Width behavior     | Expands to container (width: auto) | **Shrink‑wraps** to intrinsic width                |
| Flow               | Starts on new line                 | Flows inline with text/inline elements             |
| Vertical alignment | N/A                                | Respects `vertical-align`                          |
| Centering          | Use margin auto on a fixed width   | Use text alignment on parent: `text-align:center;` |

---

## Practical tips

* **Center an inline-table**:

  ```css
  .host { text-align: center; }
  table { display: inline-table; }
  ```
* **Line‑height gaps**: As with inline elements, whitespace in HTML can introduce tiny gaps between adjacent inline‑tables. Control with `font-size:0` on the parent or remove whitespace in markup.
* **Wrapping long tokens**: Keep `overflow-wrap: anywhere;` (as in this demo) so unbroken strings don’t force overflow inside fixed tracks.
* **Responsive tracks**: Replace pixel tracks with percentages in `<col>` for shrink‑wrapped tables that scale within a known container.

---

## Key CSS in this demo

```css
table {
  border-collapse: collapse;
  display: inline-table; /* shrink-wrap to tracks (~500px) */
  table-layout: fixed;   /* respect <colgroup> widths */
}
th, td { border: 1px solid #444; overflow-wrap: anywhere; }
.col-1 { width: 150px; }
.col-2 { width: 350px; }
```

**Takeaway**

Use **`display: inline-table`** when you want a table to **shrink‑wrap** to its column tracks (or intrinsic content) rather than stretch to the container. Pair it with **`table-layout: fixed` + `<colgroup>`** for authoritative, predictable column widths without hard‑coding a `width`.
