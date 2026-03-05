# Folia Shoes CSS Fix + Polish Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Fix all missing/broken CSS in `css/style.css` and add tasteful visual polish without changing the leather/gold/parchment design direction.

**Architecture:** All changes are additive CSS appended to `css/style.css`. No HTML or JS changes needed. Tasks are ordered by section (top to bottom of page) to make visual verification easy.

**Tech Stack:** Vanilla CSS, Google Fonts (Playfair Display, Cormorant Garamond, Montserrat), Font Awesome icons.

---

### Task 1: Fix Hero Fade-In Animations

**Files:**
- Modify: `css/style.css` (append to end)

**Context:** The hero section uses `.fade-in`, `.delay-1`, `.delay-2`, `.delay-3` classes but no keyframes or animation rules exist. Hero content is invisible or appears instantly without animation.

**Step 1: Add the keyframe and fade-in rules**

Append to `css/style.css`:

```css
/* ── Hero Fade-In Animations ─────────────────────────────── */
@keyframes fadeInUp {
    from {
        opacity: 0;
        transform: translateY(25px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.fade-in {
    opacity: 0;
    animation: fadeInUp 0.9s cubic-bezier(0.4, 0, 0.2, 1) forwards;
}

.delay-1 { animation-delay: 0.25s; }
.delay-2 { animation-delay: 0.5s; }
.delay-3 { animation-delay: 0.75s; }
```

**Step 2: Verify visually**

Open `index.html` in browser. Reload the page. The hero subtitle ("Από το 1978"), h1, paragraph, and buttons should each fade in sequentially from bottom to top, staggered about 0.25s apart.

---

### Task 2: Fix Reveal Direction for Left/Right Elements

**Files:**
- Modify: `css/style.css` (find and update existing `.reveal-left`/`.reveal-right` rules at line ~682)

**Context:** `.reveal-left` and `.reveal-right` currently both use `translateY(30px)` — identical to `.reveal-up`. They should slide in from the correct horizontal direction.

**Step 1: Update the reveal rules**

Find the existing block:
```css
.reveal-up, .reveal-left, .reveal-right {
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.8s ease-out;
}
```

Replace with:
```css
.reveal-up, .reveal-left, .reveal-right {
    opacity: 0;
    transition: all 0.8s ease-out;
}

.reveal-up    { transform: translateY(30px); }
.reveal-left  { transform: translateX(-40px); }
.reveal-right { transform: translateX(40px); }

.reveal-up.active, .reveal-left.active, .reveal-right.active {
    opacity: 1;
    transform: translate(0, 0);
}
```

Also remove the existing `.reveal-up.active, .reveal-left.active, .reveal-right.active` block at line ~687 since it's now included above.

**Step 2: Verify visually**

Scroll to the "Η Ιστορία μας" section. The story image should slide in from the left, and the text should slide in from the right.

---

### Task 3: Story Image Accent Block

**Files:**
- Modify: `css/style.css` (append)

**Context:** The HTML has `<div class="img-accent"></div>` inside `.story-img` but no CSS. `.story-img` also needs `position: relative` to contain the absolute-positioned accent.

**Step 1: Add accent styles**

Append to `css/style.css`:

```css
/* ── Story Image Accent ───────────────────────────────────── */
.story-img {
    position: relative;
}

.img-accent {
    position: absolute;
    bottom: -20px;
    right: -20px;
    width: 120px;
    height: 120px;
    background-color: var(--accent-gold);
    z-index: -1;
}
```

**Step 2: Verify visually**

The story section image should now have a gold square peeking out from behind its bottom-right corner.

---

### Task 4: Review Cards — Internal Layout

**Files:**
- Modify: `css/style.css` (append)

**Context:** `.review-header`, `.reviewer-info`, `.card-stars`, `.badge`, `.quote` have no CSS. Cards show content but with no layout structure — name, badge, and stars are stacked with no visual hierarchy.

**Step 1: Add review card internal styles**

Append to `css/style.css`:

```css
/* ── Review Card Internals ───────────────────────────────── */
.review-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-bottom: 15px;
    gap: 10px;
}

.reviewer-info h4 {
    font-size: 1rem;
    font-weight: 700;
    color: var(--leather-dark);
    margin-bottom: 5px;
}

.badge {
    display: inline-block;
    font-size: 0.65rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 1px;
    color: var(--leather-mid);
    border: 1px solid var(--parchment-dark);
    padding: 2px 8px;
    border-radius: 20px;
}

.card-stars {
    display: flex;
    gap: 2px;
    flex-shrink: 0;
    padding-top: 2px;
}

.card-stars i {
    color: var(--accent-gold);
    font-size: 0.85rem;
}

.quote {
    font-style: italic;
    color: var(--text-muted);
    line-height: 1.85;
    font-size: 0.95rem;
    position: relative;
    padding-top: 10px;
}

.quote::before {
    content: "\201C";
    font-family: 'Playfair Display', serif;
    font-size: 3.5rem;
    color: var(--accent-gold);
    opacity: 0.35;
    position: absolute;
    top: -15px;
    left: -8px;
    line-height: 1;
    pointer-events: none;
}
```

**Step 2: Verify visually**

Scroll to the reviews section. Each card should show: reviewer name + local guide badge on the left, 5 gold stars on the right, then italic quote text with a faint decorative opening quote mark.

---

### Task 5: Rating Summary Block

**Files:**
- Modify: `css/style.css` (append)

**Context:** The rating block above the reviews (`.rating-summary`, `.rating-num`, `.stars`, `.reviews-count`) has no CSS. It renders as unstyled inline content.

**Step 1: Add rating summary styles**

Append to `css/style.css`:

```css
/* ── Rating Summary ──────────────────────────────────────── */
.rating-summary {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 15px;
    margin: 15px 0 50px;
    flex-wrap: wrap;
}

.rating-num {
    font-family: 'Playfair Display', serif;
    font-size: 3.5rem;
    font-weight: 700;
    color: var(--leather-dark);
    line-height: 1;
}

.stars {
    display: flex;
    gap: 4px;
}

.stars i {
    color: var(--accent-gold);
    font-size: 1.3rem;
}

.reviews-count {
    font-size: 0.85rem;
    color: var(--text-muted);
    font-style: italic;
}
```

**Step 2: Verify visually**

The section header of the reviews block should show "4.6" in large Playfair, followed by gold stars, followed by the small "Βασισμένο σε 49 κριτικές Google" text — all in a centered horizontal row.

---

### Task 6: Footer Text Styling

**Files:**
- Modify: `css/style.css` (append)

**Context:** `.footer-tagline` and `.copyright` have no CSS. They render as plain body-weight text with no visual distinction from each other.

**Step 1: Add footer text styles**

Append to `css/style.css`:

```css
/* ── Footer Text ─────────────────────────────────────────── */
.footer-tagline {
    font-style: italic;
    color: var(--parchment-dark);
    font-size: 1rem;
    margin-bottom: 30px;
    opacity: 0.8;
}

.copyright {
    font-size: 0.78rem;
    color: rgba(255, 255, 255, 0.35);
    margin-top: 20px;
    line-height: 1.8;
}
```

**Step 2: Verify visually**

Footer should show: "Folia Shoes" logo in gold, then italic tagline in muted parchment, then social icons, then very faint small copyright text at the bottom.

---

### Task 7: Mobile Nav Drawer

**Files:**
- Modify: `css/style.css` (append, inside or after the `@media (max-width: 992px)` block)

**Context:** The JS toggles `.mobile-active` on `.nav-links` and sets `display: flex` inline. There's no CSS transition, no proper mobile dropdown styling, and the menu appears abruptly.

**Step 1: Add mobile nav drawer styles**

Append to `css/style.css` (these rules go inside the existing media query or after — they need to be scoped to mobile):

```css
/* ── Mobile Nav Drawer ───────────────────────────────────── */
@media (max-width: 992px) {
    .nav-links.mobile-active {
        display: flex;
        position: absolute;
        top: 100%;
        left: 0;
        width: 100%;
        background: var(--leather-dark);
        flex-direction: column;
        gap: 0;
        padding: 20px 0;
        box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
    }

    .nav-links.mobile-active li {
        border-bottom: 1px solid rgba(255, 255, 255, 0.07);
    }

    .nav-links.mobile-active a {
        color: var(--parchment);
        padding: 15px 30px;
        display: block;
        font-size: 0.9rem;
    }

    .nav-links.mobile-active a:hover {
        color: var(--accent-gold);
        background: rgba(255, 255, 255, 0.04);
    }

    .mobile-menu-btn span {
        background: var(--leather-dark);
        transition: var(--transition);
    }

    header.scrolled .mobile-menu-btn span {
        background: var(--parchment);
    }
}
```

**Step 2: Verify visually**

Resize browser to < 992px. Click the hamburger menu. A dark drawer should appear below the header with stacked nav links in parchment text.

---

### Task 8: Collection Card + Feature Item Polish

**Files:**
- Modify: `css/style.css` (append)

**Context:** `.card-link` has no hover underline effect. `.feature-item h3` and `p` have no spacing or color rules — they render with inherited defaults.

**Step 1: Add collection card and feature item polish**

Append to `css/style.css`:

```css
/* ── Collection Card Polish ──────────────────────────────── */
.card-link {
    border-bottom: 1px solid transparent;
    transition: var(--transition);
    padding-bottom: 2px;
}

.card-link:hover {
    border-bottom-color: var(--accent-gold);
}

/* ── Feature Item Text ───────────────────────────────────── */
.feature-item h3 {
    font-size: 1.15rem;
    color: var(--leather-dark);
    margin-bottom: 12px;
}

.feature-item p {
    font-size: 0.92rem;
    color: var(--text-muted);
    line-height: 1.7;
}
```

**Step 2: Verify visually**

Hover over a "Δείτε περισσότερα" link — a gold underline should appear. The "Why Folia" feature cards should show properly sized, spaced, and colored heading + body text.

---

## Execution Order

1. Task 1 — Hero animations
2. Task 2 — Fix reveal directions
3. Task 3 — Story accent block
4. Task 4 — Review card internals
5. Task 5 — Rating summary
6. Task 6 — Footer text
7. Task 7 — Mobile nav
8. Task 8 — Card polish

All tasks are additive CSS changes to `css/style.css`. Task 2 is the only one that modifies an existing rule — all others append new rules. Safe to apply in any order, but the above order matches visual verification flow (top-to-bottom of page).
