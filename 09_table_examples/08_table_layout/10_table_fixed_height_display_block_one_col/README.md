# Fixed Row Height — 1×2 (ALL cells display\:block)

**What this demo is**

A one‑column, two‑row table where we deliberately set **every `<th>` and `<td>` to `display:block`**. This is an **error demo** to show why changing table cells into block elements breaks real table layout.

**What you will see**

* Each cell looks about **42px** tall: **40px** content height **+ 1px top border + 1px bottom border** (because borders no longer collapse on block elements).
* “Rows” render one after another, but **true table behavior is gone**: column alignment, header/body alignment, and collapsed borders **don’t work**.
* Long text is **clipped** at the 40px content box because we use `overflow: hidden`.

**Why it behaves like this**

* Setting `display:block` on `<th>/<td>` removes table‑cell semantics. The browser can’t use table layout rules (no column grid, no collapsed borders).
* With non‑collapsing borders, the **visible height** becomes `content height + top border + bottom border` → **40px + 2px = 42px**.

**When (not) to use this**

* **Do not** use this pattern in production tables. It’s for learning/debugging only.
* If you just want strict height and clipping, use an **inner wrapper** while keeping real table cells (see later demos).

**Limitations**

* Breaks: column alignment, `<colgroup>` widths, intrinsic table sizing, assistive tech expectations for tables.
* Border math changes (no collapse), so your row height will **not** match normal table rows.

**Key CSS used**

```css
th, td {
  display: block;          /* breaks table semantics on purpose */
  border: 1px solid #444;  /* not collapsed anymore */
  padding: 0;
  height: 40px;            /* content box height */
  overflow: hidden;        /* clip extra content */
  white-space: normal;     /* allow wrapping */
}
```

**Takeaway**

Changing table cells to block elements **forces** a specific height but at the cost of **losing real table layout**. Prefer solutions that keep `<th>/<td>` as table cells and apply clipping inside.
