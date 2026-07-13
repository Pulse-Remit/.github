# 📱 Frontend: Improve mobile responsiveness on dashboard and send pages

**Labels**: `frontend`, `good first issue`, `enhancement`, `help wanted`
**Complexity**: 🟢 Beginner-to-Medium — HTML/CSS/Tailwind knowledge only

## Summary
The dashboard (`/dashboard`) and send remittance (`/send`) pages were designed primarily for desktop. On mobile (375–430px viewport width), the employee table overflows horizontally and the corridor selector dropdown is too small to tap accurately.

## Issues to fix

### 1. Employee table on `/dashboard`
- Table overflows horizontally on screens < 480px
- Suggested fix: on mobile, collapse table into card-style rows (one employee per card, vertical layout)
- Or use `overflow-x-auto` on the table wrapper with sticky first column

### 2. Corridor selector on `/send`
- Dropdown text is too small on mobile (currently 14px, needs 16px minimum to prevent iOS auto-zoom)
- Add `font-size: 16px` to the select element

### 3. Navbar on mobile
- Nav links overflow on narrow screens
- Add a hamburger menu or horizontal scroll on the nav for screens < 640px

## Acceptance criteria
- [ ] Dashboard employee table readable on 375px viewport without horizontal scroll
- [ ] Corridor dropdown does not trigger iOS auto-zoom
- [ ] Navbar usable at 375px width
- [ ] Tested in Chrome DevTools mobile emulation (iPhone SE + Pixel 5)
- [ ] No visual regressions on desktop (1280px+)
- [ ] Screenshots of before/after attached to PR

## Notes
Tailwind breakpoint prefixes: `sm:` = 640px, `md:` = 768px. Use `xs:` or bare classes for < 640px styles.

## Stellar Wave
Points: 100 | Complexity: 🟢 Beginner — frontend devs with Tailwind experience
