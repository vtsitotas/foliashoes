# Folia Shoes — CSS Fix + Polish Design

**Date:** 2026-03-03
**Scope:** Fix broken/missing CSS and add tasteful visual polish
**File to edit:** `css/style.css`

---

## Problems Being Fixed

### Broken / Missing CSS
1. `.fade-in`, `.delay-1/2/3` — hero animations do nothing (no keyframes defined)
2. `.reveal-left`, `.reveal-right` — both use `translateY` instead of `translateX`
3. `.img-accent` — decorative story section element, completely unstyled
4. `.review-header`, `.reviewer-info`, `.card-stars`, `.badge`, `.quote` — review cards have no internal layout
5. `.rating-summary`, `.rating-num`, `.stars`, `.reviews-count` — rating block unstyled
6. `.footer-tagline`, `.copyright` — footer text lacks any styling
7. Mobile nav — JS handles show/hide with inline styles only, no CSS transitions

### Visual Polish
- Collection `.card-link` hover effect
- `.feature-item` spacing and text color
- Mobile nav styled as a proper dropdown drawer

---

## Design Decisions

### Section 1: Animations
- Add `@keyframes fadeInUp` and apply to `.fade-in` with `opacity: 0 → 1`, `translateY(20px → 0)`
- `.delay-1` = `animation-delay: 0.3s`, `.delay-2` = `0.6s`, `.delay-3` = `0.9s`
- Fix `.reveal-left` to `translateX(-40px)` and `.reveal-right` to `translateX(40px)`

### Section 2: Story Image Accent
- `.story-img` gets `position: relative`
- `.img-accent` positioned absolute bottom-right: `60×60px` gold square, offset `-20px -20px` outside the image edge

### Section 3: Review Cards
- `.review-header`: `display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 15px`
- `.reviewer-info h4`: `1rem`, bold, small margin
- `.badge`: pill style — gold border, dark text, `0.65rem` uppercase, small padding
- `.card-stars`: gold color stars
- `.quote`: italic, muted color, `line-height: 1.8`, decorative `"` pseudo-element in large gold Playfair
- `.rating-summary`: centered flex row with gaps; `.rating-num` in large Playfair (3rem); `.stars` gold; `.reviews-count` small muted

### Section 4: Mobile Nav, Footer, Collection Cards
- `.nav-links.mobile-active`: absolute positioning below header, full-width, flex-column, white background, padding — replaces JS inline style with proper CSS
- `.footer-tagline`: italic, `var(--parchment-dark)`, `margin-bottom: 30px`
- `.copyright`: `0.8rem`, `rgba(255,255,255,0.4)`, `margin-top: 20px`
- `.card-link`: add `border-bottom: 1px solid transparent` + hover `border-color: var(--accent-gold)`
- `.feature-item h3`: `1.2rem`, `var(--leather-dark)`, `margin-bottom: 10px`
- `.feature-item p`: `var(--text-muted)`, `0.95rem`
