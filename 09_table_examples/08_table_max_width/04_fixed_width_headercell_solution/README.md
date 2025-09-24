# Table — 500px Total + Header Width Hints (150px / 350px)

**What this demo is**

A 2‑column table with an explicit **total table width of 500px** and width **hints on the headers**:

```css
/* Total table width */
table { border-collapse: collapse; width: 500px; }

/* Column hints via <th> classes */
th.col-1 { width: 150px; }
th.col-2 { width: 350px; }
```

This aims for a **150px `Code`** column and a **350px `Description`** column within the fixed overall width.

**What you will see**

* The table renders at **\~500px total width** (plus the single collapsed outer border).
* Columns generally align near **150px / 350px**.
* The long description text **wraps inside the 350px track** and does not stretch the table beyond 500px.

**Why it behaves like this**

* With `table-layout: auto` (the default), the browser determines column tracks from the content **and** any width declarations it finds. Widths on the **header cells** act as **strong hints** for the column tracks.
* Setting `width: 500px` on `<table>` caps the **overall layout width**, so wrapping occurs rather than horizontal growth.
* Because content is wrappable text, the engine can satisfy both the **total width** and **per‑column hints** simultaneously.

**When to use this pattern**

* You want a **fixed total table width** and **reasonable per‑column proportions** without introducing `<colgroup>` yet.
* Your cells contain **wrappable content** (plain text) and not lots of unbreakable tokens.

**Limitations**

* **Not a hard guarantee**: Unbreakable content (e.g., large images, long URLs without breakpoints, `SuperLongIdentifierWithoutBreaks`) can force a column wider than its hint.
* Complex col/row spans may reduce predictability under the auto layout algorithm.
* Width hints on headers couple presentation to markup (repeated across tables unless abstracted).

**Gotchas & tips**

* Improve robustness against long tokens with a breaker:

  ```css
  th, td { overflow-wrap: anywhere; /* or: word-break: break-word; */ }
  ```
* For **authoritative** (hard) column tracks, switch to:

  * `table-layout: fixed` **and** `<colgroup><col style="width:…">…` for stable column sizing, OR
  * Explicit widths on `<col>` elements rather than only on headers.

**Key CSS used**

```css
table {
  border-collapse: collapse;
  width: 500px;              /* fixed overall width */
}
th, td {
  border: 1px solid #444;    /* collapsed borders */
}
/* Column width hints on headers */
th.col-1 { width: 150px; }
th.col-2 { width: 350px; }
```

**Takeaway**

Combining a **fixed total width** with **header‑based width hints** yields predictable, proportional columns for simple, text‑heavy tables. When content may resist wrapping or you need strict guarantees, graduate to **`table-layout: fixed` + `<colgroup>`** so column tracks become authoritative rather than heuristic.
