# Fixed Row Height — 2×2 (ALL cells display\:block)

**What this demo is**

A two‑column, two‑row table where **every `<th>` and `<td>` is forced to `display:block`**. This intentionally breaks real table layout to show the consequences.

**What you will see**

* Each cell appears about **42px** tall: **40px** content + **1px** top border + **1px** bottom border (borders don’t collapse on blocks).
* **Columns won’t align.** Headers and body cells stack like normal block elements instead of forming a grid.
* Long text is **clipped** at 40px because of `overflow: hidden`; there’s no multi‑line ellipsis.

**Why it behaves like this**

* Changing `<th>/<td>` to `display:block` removes **table‑cell semantics**: no column grid, no intrinsic sizing, no `<colgroup>` tracks, and **no border collapsing**.
* Without border collapsing, visible height = content height + both borders → **40px + 2px = 42px**.

**When (not) to use this**

* **Do not** use this approach in production tables. It’s an **error demo**.
* If you need strict row heights, keep real table cells and clip inside with an **inner wrapper** (see later demos).

**Limitations**

* Breaks column alignment and header/body alignment.
* Ignores `<colgroup>` widths and intrinsic table sizing.
* Accessibility expectations for tables can be harmed.

**Key CSS used**

```css
th, td {
  display: block;          /* intentionally breaks table-cell behavior */
  border: 1px solid #444;  /* not collapsed when block */
  padding: 0;
  height: 40px;            /* content box height only */
  overflow: hidden;        /* hard clip beyond 40px */
  white-space: normal;     /* allow wrapping */
}
```

**Takeaway**

Forcing table cells to `display:block` can make height math look predictable, but you **lose the table**. Prefer solutions that **preserve table semantics** and control height with inner wrappers, clamping, or absolute inner spans.
