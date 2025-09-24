# White‑Space Handling in Tables

**What this demo is**

Two small tables that show how the CSS `white-space` property changes text flow *inside table cells*, using `table-layout: fixed` and explicit column tracks.

* **Table 1:** `white-space: normal` vs `white-space: nowrap`
* **Table 2:** `white-space: pre-wrap` vs `white-space: pre`

**Why this matters**

In data tables, the way text wraps (or doesn’t) controls row height, readability, and whether the layout overflows. `white-space` is the primary switch that controls wrapping and preservation of spaces/newlines.

---

## Table 1 — Normal vs NoWrap

**Normal** (`white-space: normal`)

* Default behavior: **collapses sequences of spaces** to one space.
* **Wraps** at soft wrap opportunities (spaces, hyphenation points).
* Good for prose and labels; keeps cells compact and readable.

**NoWrap** (`white-space: nowrap`)

* **Prevents wrapping**; the line stays single‑line.
* Spaces still collapse; newlines in the source are treated like spaces.
* Useful for short codes/IDs you don’t want broken; risky for long text (can overflow the cell or force horizontal scrolling).

**Gotcha**: With `nowrap`, long content can overflow a fixed‑width column. If you must use it, consider `text-overflow: ellipsis` with a constrained width and `overflow: hidden;` (works best on single‑line blocks).

---

## Table 2 — Pre‑Wrap vs Pre

**Pre‑Wrap** (`white-space: pre-wrap`)

* **Preserves** line breaks (`\n`) and **preserves** sequences of spaces.
* **Allows wrapping** when needed to avoid overflow.
* Great for multi‑line text (notes, code snippets) where you want author‑entered newlines and indentation preserved **but** still want soft wrapping on long lines.

**Pre** (`white-space: pre`)

* **Preserves** line breaks and **preserves** sequences of spaces.
* **No wrapping**; text only breaks at explicit newlines.
* Best for strict formatting (ASCII tables, code blocks). Expect horizontal overflow if lines exceed the column width.

**Tip**: If you need the visual look of `pre` but safer layout, try `pre-wrap` or combine `pre` with horizontal scrolling on an inner wrapper.

---

## Interactions & Practical Notes

* **`table-layout: fixed`**: Column widths come from tracks (e.g., `<col>` widths). Whether content wraps is determined by `white-space`. Fixed layout is faster and predictable; it won’t widen a column just because content is long.
* **Long unbreakable tokens** (URLs without hyphens, base64, hashes):

  * `normal`/`pre-wrap` may still fail to wrap unless you add a break policy like `overflow-wrap: anywhere;`.
  * `nowrap`/`pre` will *not* wrap regardless; use scroll or truncation.
* **Hyphenation**: `hyphens: auto;` can improve wrap quality for natural language (requires correct language settings). Use alongside `white-space: normal` or `pre-wrap`.

---

## Quick Reference

| Mode       | Collapses spaces | Preserves newlines   | Allows wrapping |
| ---------- | ---------------- | -------------------- | --------------- |
| `normal`   | ✅                | ❌ (treated as space) | ✅               |
| `nowrap`   | ✅                | ❌ (treated as space) | ❌ (single line) |
| `pre-wrap` | ❌                | ✅                    | ✅               |
| `pre`      | ❌                | ✅                    | ❌ (no wrap)     |

---

## Common Recipes

* **Readable prose**: `white-space: normal;` (+ `hyphens:auto;` if appropriate).
* **Single‑line labels with truncation**: `white-space: nowrap; overflow: hidden; text-overflow: ellipsis;` (constrain width).
* **Multiline notes with preserved indentation**: `white-space: pre-wrap;` (+ optional `overflow-wrap:anywhere;` for hostile tokens).
* **Code/ASCII that must not wrap**: `white-space: pre;` inside a scrollable inner wrapper.

**Example add‑ons**

```css
/* Improve robustness against long tokens */
th, td { overflow-wrap: anywhere; }

/* Optional hyphenation for natural language */
th, td { hyphens: auto; }

/* Single-line truncation pattern */
.cell-one-line {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

/* Scrollable inner wrapper for preformatted blocks */
.td-pre > .scroll {
  white-space: pre;
  display: block;
  overflow-x: auto;
}
```

**Takeaway**

Pick `white-space` based on how you want text to break:

* Use **`normal`** for most prose.
* Use **`pre-wrap`** when you need to **preserve** author newlines/indentation **and** avoid overflow.
* Use **`nowrap`** or **`pre`** only when you explicitly want **no soft wrapping**—and plan for overflow (ellipsis or scroll).
