# `overflow-wrap` in Tables — `normal` vs `break-word` vs `anywhere`

**What this demo is**

A compact set of table cells (fixed 200px width) that shows how `overflow-wrap` controls breaking long, unspaced tokens when `white-space: normal` is in effect.

* **Table 1:** `overflow-wrap: normal` (no forced breaks)
* **Table 2:** `overflow-wrap: break-word` (allow mid‑word breaks at safe opportunities)
* **Table 3:** `overflow-wrap: anywhere` (allow breaks between *any* two characters)

`table-layout: fixed` is used so column width is predictable and the effect of wrapping is easy to see.

---

## How each mode behaves

### 1) `overflow-wrap: normal`

* **Default** behavior.
* **Does not** break long, unspaced tokens.
* Result: a long string can **overflow** the cell or cause horizontal scroll.
* Use when your content is natural language with spaces and you **do not** expect hostile tokens.

### 2) `overflow-wrap: break-word`

* Permits breaking **within words** when needed to avoid overflow, but prefers breaking at allowed opportunities first (spaces/hyphenation points).
* Result: long tokens will **wrap** if necessary, typically creating cleaner breaks than `anywhere`.
* Good default for UI text where occasional long tokens appear (IDs, URLs) but you want aesthetically nicer wraps.

### 3) `overflow-wrap: anywhere`

* Allows a break **between any characters** when needed.
* Result: guarantees wrapping, even for pathological strings (base64, hashes, unbroken identifiers).
* Most robust for grids that must never overflow, at the cost of potentially **awkward** break points.

---

## Interactions & related properties

* **`white-space`**: This demo keeps `white-space: normal`. If you set `nowrap` or `pre`, wrapping is disabled regardless of `overflow-wrap`.
* **`hyphens: auto`**: Improves quality of breaks for natural language (requires proper language and hyphenation support). Use with `normal` or `break-word`.
* **`word-break`**: Legacy/alternate behavior. `word-break: break-word` is now treated as an alias of `overflow-wrap: anywhere` in modern engines. `word-break: break-all` is more aggressive than `anywhere` and can affect CJK/Latin; use **sparingly**.
* **Fixed vs auto table layout**: With `table-layout: fixed`, columns won’t expand to fit content—wrapping (or overflow) is your only relief. With auto layout, browsers *may* widen columns if space is available.

---

## Quick decision guide

* **Mostly prose, occasional long words** → `overflow-wrap: break-word;` (+ `hyphens: auto;` if available).
* **Must never overflow, arbitrary tokens appear** → `overflow-wrap: anywhere;`.
* **Strict single‑line truncation** → keep `white-space: nowrap;` and use `text-overflow: ellipsis; overflow: hidden;` (this pattern ignores `overflow-wrap`).

---

## Key CSS in this demo

```css
table {
  border-collapse: collapse;
  width: 200px;
  table-layout: fixed; /* predictable column width */
}
th, td { border: 1px solid #444; padding: 8px; }

/* 1) Default wrapping — tokens won’t break */
td.normal {
  white-space: normal;
  overflow-wrap: normal;
}

/* 2) Prefer safe mid-word breaks */
td.breakword {
  white-space: normal;
  overflow-wrap: break-word;
}

/* 3) Break anywhere if needed */
td.anywhere {
  white-space: normal;
  overflow-wrap: anywhere;
}
```

**Optional enhancements**

```css
/* Better looking natural-language wraps */
th, td { hyphens: auto; }

/* Guard rails for unexpected media */
th img, td img { max-width: 100%; height: auto; }
```

**Takeaway**

Pick the weakest tool that prevents overflow:

* Start with **`break-word`** for decent aesthetics.
* Escalate to **`anywhere`** when you must guarantee wrapping for arbitrary tokens.
* Remember: `white-space` can *disable* wrapping entirely; keep it `normal` if you want these rules to work.
