# `inline-size: max-content` — Shrink‑Wrap Tables via Logical Sizes

**What this demo is**

A 2‑column table whose column tracks are defined via `<colgroup>` (**150px / 350px**). Instead of `width: 500px` or `display: inline-table`, it uses **logical sizing**:

```css
 table {
   border-collapse: collapse;
   inline-size: max-content; /* shrink-wrap to intrinsic width */
   table-layout: fixed;      /* honor <colgroup> track sizes */
 }
```

The focus is **`inline-size: max-content`** (the logical property for horizontal size in LTR/RTL writing modes).

---

## What `inline-size: max-content` does

* Sets the table’s **inline dimension** to its **max-content size** — i.e., the intrinsic width needed to lay out its contents **without soft wrapping**.
* With fixed tracks of **150px + 350px**, and `table-layout: fixed`, the intrinsic width is \~**500px** (plus borders). The table **shrink‑wraps** to that width **without** `width: 500px;` or `display: inline-table;`.
* Being a **logical** property, it respects writing modes. In vertical writing (`writing-mode: vertical-rl;`), this would apply along the column flow instead.

---

## Why pair it with `table-layout: fixed`

* `table-layout: fixed` makes `<colgroup>` track widths **authoritative** and avoids content re‑measurement, so the max‑content width is simply the **sum of tracks**.
* In contrast, with auto layout the max‑content width could be affected by very long unbreakable tokens that expand a column’s min/max content contributions.

---

## When to use `inline-size: max-content`

* You want a table to **size to its intrinsic tracks** and not stretch to fill its container.
* You prefer **logical properties** for better i18n / writing‑mode support.
* You need shrink‑wrap behavior but don’t want to change the element’s display type (keep it as a block‑level table, not `inline-table`).

---

## Differences vs other approaches

| Goal                           | Use                         | Notes                                       |
| ------------------------------ | --------------------------- | ------------------------------------------- |
| Hard code exact width          | `width: 500px;`             | Explicit; ignores content changes.          |
| Shrink‑wrap without width      | `display: inline-table;`    | Changes formatting context to inline‑level. |
| Shrink‑wrap via logical sizing | `inline-size: max-content;` | Keeps block formatting; writing‑mode aware. |

---

## Robustness & overflow

* Long unbreakable tokens can exceed fixed tracks. Keep a **break policy** to avoid overflow:

  ```css
  th, td { overflow-wrap: anywhere; } /* as used in this demo */
  /* optional: hyphens: auto; */
  ```
* Media inside cells (images/iframes) should be constrained:

  ```css
  td img { max-width: 100%; height: auto; }
  ```

---

## Centering & alignment

* Because the table keeps **block formatting**, center it with standard block techniques:

  ```css
  table { inline-size: max-content; margin-inline: auto; }
  ```
* Or align it like text within a container using logical text alignment:

  ```css
  .host { text-align: center; }
  ```

---

## Key CSS in this demo

```css
table {
  border-collapse: collapse;
  inline-size: max-content; /* shrink-wrap to tracks (~500px) */
  table-layout: fixed;      /* respect <colgroup> widths */
}
th, td { border: 1px solid #444; overflow-wrap: anywhere; }
.col-1 { width: 150px; }
.col-2 { width: 350px; }
```

**Takeaway**

Use **`inline-size: max-content`** when you want a table to **shrink‑wrap** to its intrinsic column tracks **without** switching to `inline-table` or hard‑coding a `width`. Pair it with **`table-layout: fixed` + `<colgroup>`** and a sensible **wrap policy** for resilient, predictable sizing.
