You’re right — I originally listed **16 rules** in total.  
I explained #1–#8 in a beginner-friendly way. But I never came back to **#9 through #16** in that same simple style.

Let me fix that now. Here are **rules 9–16**, explained for someone who is *not* an expert.

---

## Big Rule #9: The Cascade — multiple rules fight, there’s a winner

When two CSS rules try to set the same property on the same element, CSS decides the winner by:

1. **Importance** – `!important` wins (but avoid using it unless desperate)
2. **Specificity** – more specific wins (inline style > ID > class > element)
3. **Source order** – later rule wins if specificity is equal

**What trips people up:**  
You write a class rule, but the element still looks like the element rule. You think CSS is ignoring you.

**Fix:** Check if something more specific (like an ID or inline style) is overriding yours. Or check if your rule comes *before* another rule with the same specificity.

---

## Big Rule #10: `z-index` only works if you set `position` first

`z-index` does **nothing** on a `static` element (the default position).  
You must set `position: relative`, `absolute`, `fixed`, or `sticky` for `z-index` to work.

**What trips people up:**  
You set `z-index: 100` on a `<div>` and nothing changes.

**Fix:** Add `position: relative` (even if you don’t move it anywhere).

---

## Big Rule #11: Padding and margin percentages are based on *width*, not height

Even `padding-top` and `margin-bottom` use the parent’s **width** to calculate the percentage.  
Not the parent’s height.

**What trips people up:**  
You want `margin-top: 10%` to be 10% of the parent’s height. Instead, it becomes 10% of the parent’s width. Confusing!

**Fix:** Accept this or use newer CSS like `vh` (viewport height) or `display: grid` gaps.

---

## Big Rule #12: Images and videos have their own natural size

`<img>` and `<video>` are “replaced elements” — they come with a built-in width and height.  
If you only set one dimension, the other adjusts to keep the picture from stretching.

**What trips people up:**  
You set `width: 200px` on an image, expecting it to also be 200px tall. But it stays proportional — so a wide photo becomes 200px wide but only 133px tall.

**Fix:** If you want a fixed size, set both `width` and `height`. But that might squash the image. Better to use `object-fit: cover` to crop nicely.

---

## Big Rule #13: `auto` means different things depending on the situation

- `width: auto` on a `<div>` → stretch to fill parent
- `width: auto` on a `<span>` → shrink to fit content
- `margin: auto` → center horizontally (if width is set)
- `height: auto` → fit the content

**What trips people up:**  
You use `margin: auto` expecting vertical centering — it only works horizontally unless you’re using flexbox.

**Fix:** Learn what `auto` does in *your* specific context.

---

## Big Rule #14: Inline elements ignore width, height, and vertical margins

Already mentioned this in #8, but it’s worth repeating because it’s so common:  
`<span>` or `<a>` will not accept `width`, `height`, `margin-top`, or `margin-bottom`.

**What trips people up:**  
You add `margin-top: 20px` to a link — nothing happens.

**Fix:** Change to `display: inline-block` or `display: block`.

---

## Big Rule #15: `overflow: hidden` does more than hide overflow

It also:
- Stops floats from escaping the box
- Prevents margins from collapsing through it
- Creates a new “formatting context” that can fix layout bugs

**What trips people up:**  
You add `overflow: hidden` to hide scrollbars, and suddenly your layout shifts in a way you didn’t expect.

**Fix:** If you only want to hide overflow, you’re fine. But if you see layout changes, now you know why.

---

## Big Rule #16: Inheritance is not automatic

Some properties (like `color` and `font-family`) are inherited by children automatically.  
But box properties (like `width`, `margin`, `border`) are **not inherited**.

**What trips people up:**  
You set `width: 300px` on the parent, and expect the child to have the same width. It doesn’t.

**Fix:** Use `width: inherit` on the child, or set the child’s width explicitly.

---

## Summary — all 16 rules in simple terms

| Rule | Simple version |
|------|----------------|
| 1 | Sizing first, alignment second (your discovery) |
| 2 | Every element is a box with padding, border, margin |
| 3 | Block elements stretch, inline elements shrink |
| 4 | Percentage height needs a fixed parent height |
| 5 | Vertical margins collapse (the bigger one wins) |
| 6 | `z-index` is local, not global |
| 7 | `overflow: hidden` also changes layout behavior |
| 8 | Inline elements ignore width, height, vertical margins |
| 9 | The Cascade: importance → specificity → order |
| 10 | `z-index` requires `position` (not `static`) |
| 11 | Percentage padding/margin use parent’s *width* |
| 12 | Images keep their aspect ratio automatically |
| 13 | `auto` means different things in different places |
| 14 | (Same as #8) inline elements ignore vertical sizing |
| 15 | `overflow: hidden` contains floats and stops margin collapse |
| 16 | Box properties are not inherited |

Now you have all 16 in plain language. Keep these in mind, and CSS will stop surprising you.