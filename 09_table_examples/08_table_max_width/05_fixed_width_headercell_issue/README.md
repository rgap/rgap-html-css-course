# Table — 500px Width + Header Hints with Unbreakable Token

**What this demo is**

Same as the previous example (fixed **500px** table, header width hints **150px/350px**) but the second row’s description contains an **unbreakable token**:

```
Veryverylongproductdescriptionthatwillwrapinsidethefixedcolumnwidthandwon’tstretchthelayout.
```

**What you will see**

* The table remains **\~500px** wide overall (because `table { width: 500px; }`).
* The first column stays near **150px**, second near **350px** for normal content.
* In the row with the unbreakable token, the **text won’t wrap**. It will typically **overflow the 350px cell** (spilling beyond the column/table) or appear to push the column visually—behavior varies by browser, but you should **expect overflow**, not reliable wrapping.

**Why it behaves like this**

* `table-layout: auto` honors header widths as **hints**, but layout is also constrained by the table’s fixed **500px** width.
* An **unbreakable token** has a very large **min-content width**; since the table can’t grow wider than 500px, the engine has no legal wrap point, so the content **overflows** instead of wrapping.
* Width hints on `<th>` do **not** force wrapping; they only guide **column track sizing**.

**When to use this pattern**

* When most content is **wrappable** and you can accept occasional overflow for rare pathological tokens.

**Limitations**

* Unbreakable strings (long IDs, URLs without hyphens, concatenated words, base64 blobs) will **overflow** or **distort** the intended proportions.
* Header hints are **not authoritative**; complex content can still upset the layout.

**How to make it robust**

Add an explicit breaker so long tokens can wrap inside the 350px cell:

```css
/* Prefer this for modern browsers */
th, td { overflow-wrap: anywhere; }

/* Older/alternate options (use with care) */
/* th, td { word-break: break-word; }    // legacy alias; now maps to overflow-wrap */
/* th, td { word-break: break-all; }     // more aggressive; can break in the middle of CJK/Latin */
/* th, td { hyphens: auto; }             // needs proper language + potential soft hyphens */
```

If you need **authoritative column tracks**, use:

```css
table { table-layout: fixed; width: 500px; }
colgroup {
  /* exact tracks: */
  /* <col style="width:150px"> <col style="width:350px"> */
}
```

…and keep a breaker like `overflow-wrap: anywhere;` so long tokens still wrap within the fixed track.

**Key CSS in this demo**

```css
table { border-collapse: collapse; width: 500px; }
th, td { border: 1px solid #444; }
th.col-1 { width: 150px; }
th.col-2 { width: 350px; }
```

**Takeaway**

Header width hints + fixed table width give nice proportions for **wrappable text**, but **unbreakable tokens** will break the illusion. Add a **wrap strategy** (e.g., `overflow-wrap: anywhere`) and consider **`table-layout: fixed` + `<colgroup>`** when you need hard, predictable tracks.
