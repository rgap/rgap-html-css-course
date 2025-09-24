# Table — 500px Width + Header Hints + `overflow-wrap:anywhere`

**What this demo is**

A 2‑column table with a fixed **500px** total width and header width hints (**150px / 350px**). In addition, **`overflow-wrap: anywhere`** is applied to **all cells** so even long, unbroken tokens can wrap inside the 350px description column.

**What you will see**

* The table stays at **\~500px** wide overall.
* Columns align near **150px / 350px**.
* Regular long text **wraps normally**.
* Even a long **unbreakable token** (e.g., `Veryverylongproduct…`) will **wrap mid‑word** within the 350px column instead of overflowing.

**Why it behaves like this**

* `overflow-wrap: anywhere` permits breaking **between any two characters** when needed to prevent overflow. It’s the modern, standards‑based way to handle unbreakable tokens.
* Header widths in `table-layout: auto` act as **strong hints**; combined with the fixed table width, the browser can keep proportions while allowing safe mid‑word breaks.

**When to use this pattern**

* Tables with **potentially hostile tokens** (IDs, hashes, base64, no‑space strings) that must not break the layout.
* You want to keep **auto layout** (no `<colgroup>` yet) but avoid horizontal scroll or overflow.

**Limitations**

* Mid‑word breaks may be visually **awkward**; consider `hyphens: auto` (with proper language and soft hyphens) if you prefer hyphenation over arbitrary breaks.
* Widths on headers remain **hints**, not hard guarantees. For authoritative tracks, switch to `table-layout: fixed` + `<colgroup>`.

**Key CSS**

```css
table { border-collapse: collapse; width: 500px; }
th, td {
  border: 1px solid #444;
  /* modern way to allow breaks anywhere if needed */
  overflow-wrap: anywhere;
}
/* column width hints (auto layout) */
th.col-1 { width: 150px; }
th.col-2 { width: 350px; }
```

**Related options**

```css
/* Visual hyphenation (needs language + soft hyphens support) */
th, td { hyphens: auto; }

/* Very aggressive breaking (rarely recommended) */
/* th, td { word-break: break-all; } */
```

**Takeaway**

Adding **`overflow-wrap: anywhere`** makes the layout resilient: even pathological long strings **wrap inside the column**, preserving the **500px** table width and the intended **150/350** proportions. Use this when you want robust auto layout without committing to `<colgroup>` yet.
