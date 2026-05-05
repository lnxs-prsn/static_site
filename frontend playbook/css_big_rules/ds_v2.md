Yes — there are more fundamental “big rules” that change how you think about CSS layout. Here are several **not yet covered** that will save you hours of debugging.

---

### 9. **The Cascade is not just specificity**  
CSS stands for **Cascading** Style Sheets. The final value for any property comes from:  
1. **Origin & importance** (user `!important` > author `!important` > author normal > user normal > user agent)  
2. **Specificity** (inline style > ID > class > element)  
3. **Source order** (later rules win)  
- **One‑step thinking:** “My class selector overrides the element selector.”  
  **Two steps:** ① Check if an `!important` from a higher origin exists ② Then compare specificity, then source order.

---

### 10. **Stacking context – z-index is local**  
`z-index` only works on positioned elements (`relative`, `absolute`, etc.) and creates a local stacking context.  
A child with `z-index: 999` cannot pop out of its parent if the parent has a lower `z-index` but creates its own stacking context (e.g., `opacity <1`, `transform`, `mix-blend-mode`).  
- **One‑step thinking:** “This absolute modal has z-index: 10000, so it will be on top of everything.”  
  **Two steps:** ① Check the parent chain – has any ancestor created a new stacking context? ② The modal’s z-index only matters *inside* that context.

---

### 11. **Percentage padding/margin is always relative to the *width* of the containing block**  
Even `padding-top` and `margin-bottom` (vertical directions) use the **width** of the parent, not height.  
This is what makes aspect‑ratio boxes (`padding-bottom: 56.25%` for 16:9) work.  
- **One‑step thinking:** “I want vertical margin to be 10% of the parent’s height.”  
  **Two steps:** ① Measure the parent’s *width* ② Apply 10% of that width, not height.

---

### 12. **Replaced elements have intrinsic dimensions**  
`<img>`, `<video>`, `<iframe>`, `<svg>` have their own natural size. Without explicit `width`/`height`, they keep their aspect ratio and shrink‑to‑fit (but max 100% of container by default).  
If you set only one dimension, the other auto‑scales to maintain aspect ratio.  
- **One‑step thinking:** “I set `width: 200px` on the image, and it will also be 200px tall.”  
  **Two steps:** ① The image preserves its aspect ratio (e.g., 4:3) ② Height becomes `200 × 3/4 = 150px`.

---

### 13. **The `auto` keyword means different things per property**  
- `width: auto` (block) → stretch to container width.  
- `width: auto` (inline) → shrink‑to‑fit.  
- `margin: auto` → absorb leftover space (centering).  
- `height: auto` → fit content.  
- `position: absolute; top: 0; bottom: 0; height: auto` → stretch to containing block (if both top/bottom set).  
- **One‑step thinking:** “`auto` just figures it out.”  
  **Two steps:** ① What is the element’s display / position / context? ② Apply the specific `auto` behavior for that property in that context.

---

### 14. **Inline elements ignore width, height, and vertical margin**  
Setting `width: 100px` on a `<span>` does nothing.  
`margin-top` / `margin-bottom` on inline elements also do nothing (only left/right work).  
- **One‑step thinking:** “I’ll give this link a margin-top: 10px.”  
  **Two steps:** ① Is it inline (default for `<a>`)? ② Then vertical margin is ignored – you must change to `display: inline-block` or `block`.

---

### 15. **Overflow: hidden does more than hide**  
It also establishes a new **block formatting context** (BFC) and **clips** children absolutely positioned inside the element (if the parent is positioned).  
It also prevents margin collapse across it.  
- **One‑step thinking:** “I just want to hide overflow.”  
  **Two steps:** ① The element becomes a BFC (floats inside are contained, margins stop collapsing) ② Now also hides overflowing content.

---

### 16. **Inheritance is not universal**  
Only certain properties inherit by default (e.g., `color`, `font-family`, `text-align`).  
Box model properties (`width`, `margin`, `border`) do **not** inherit.  
- **One‑step thinking:** “This child should have the same width as parent.”  
  **Two steps:** ① Check if `width` even inherits (it doesn’t). ② Explicitly set `width: inherit` or `width: 100%` if you want that.

---

Each of these is a “two‑step” rule in disguise. Once you internalize them, you stop guessing and start *knowing* how CSS will behave.