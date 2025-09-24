# Table — `<colgroup>` Tracks (150px / 350px) — with & without `table-layout: fixed`

**What this demo is**

A 2‑column table that defines **column tracks via `<colgroup>`**:

```html
<colgroup>
  <col class="col-1" />  <!-- 150px -->
  <col class="col-2" />  <!-- 350px -->
</colgroup>
```

and assigns widths in CSS (`.col-1 { width:150px }`, `.col-2 { width:350px }`). The lines for `table { width:500px; table-layout:fixed; }` are commented out so you can compare **auto** vs **fixed** layout behavior.

**What you will see (as‑is, auto layout)**

* Browsers often honor `<col>` widths as **strong preferences** when content is wrappable and the sum (150 + 350) fits comfortably.
* The table **expands to the container width** (block‑level default). If the container is wider than 500px, the columns may **receive extra space**, so they won’t look strictly 150/350.
* Long, normal text **wraps** within whatever width each column ends up with.

**What changes if you enable `table-layout: fixed`**

* `<col>` widths become **authoritative tracks**: the engine **does not re‑measure content** to adjust columns.
* You get **predictable, stable columns** at exactly **150px / 350px** (subject to min/max constraints).
* **Performance**: fixed layout is typically faster on large tables because it skips content measurement.

**What changes if you also set `width: 500px`**

* The table’s **box** becomes exactly **500px** wide (150 + 350). It **won’t stretch** to fill a wider container.
* Visually, you get a precise 150/350 split with no extra distribution.

**Alternative to `width:500px`**

* Use `display: inline-table;` to **shrink‑wrap** the table to its tracks (≈500px) while still using fixed layout. Helpful when you want the table to size to content/tracks rather than the container.

**When to use each option**

* **As‑is (auto + `<colgroup>`)**: quick setup; good when content is wrappable and exact pixel tracks are not mission‑critical.
* **`table-layout: fixed` + `<colgroup>`**: when you need **hard, predictable** column tracks and better performance on big datasets.
* **Add `width: 500px`** (or `inline-table`) when you want the **table box** to match your track sum exactly.

**Limitations & gotchas**

* **Unbreakable tokens** (long URLs, identifiers without spaces) can still cause overflow. Consider:

  ```css
  th, td { overflow-wrap: anywhere; }
  /* or: word-break: break-word;  (legacy alias) */
  /* optionally: hyphens: auto;   (needs language + soft hyphen support) */
  ```
* Min/max constraints still apply: images or very wide replaced elements can exceed the track and overflow.
* Complex `rowspan`/`colspan` patterns reduce predictability under auto layout.

**Key CSS knobs (recap)**

```css
/* Authoritative tracks */
/* table { table-layout: fixed; } */

/* Exact table box width (sum of tracks) */
/* table { width: 500px; } */

/* Shrink-wrap alternative */
/* table { display: inline-table; } */

/* Robust wrapping for scary tokens */
th, td { /* overflow-wrap: anywhere; */ }
```

**Takeaway**

`<colgroup>` is the **right place** to define column tracks. Add `table-layout: fixed` to make those tracks **authoritative**, and set either `width:500px` or `display:inline-table` if you don’t want the table to stretch with its container. For hostile strings, pair it with `overflow-wrap:anywhere` to keep the layout intact.
