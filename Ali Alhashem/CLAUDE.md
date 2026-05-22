# Ali Alhashem Studio — Project Reference

## What This Is
A static, self-contained Arabic/RTL photography studio website for **Ali Alhashem Studio** (استيديو علي الهاشم), based in Saudi Arabia. No build tools, no frameworks — pure HTML + inline CSS + vanilla JS.

## Pages
| File | Purpose |
|---|---|
| `index.html` | Main homepage — hero, about, services, portfolio, testimonials, clients, process, contact, social follow |
| `wedding.html` | Wedding photography/videography sub-page |
| `organizations.html` | Corporate & government events sub-page |
| `real-estate.html` | Real estate photography sub-page |

All CSS and JS are **inline** inside each HTML file's `<style>` and `<script>` tags. No external CSS/JS files exist.

## Assets
```
Assets/
  Studio Logo/        ← PNG logos (white/transparent background)
  Weddings/           ← JPG wedding photos
  Organizations/      ← JPG corporate event photos
  Real State/         ← JPG real estate / drone photos (DJI_*.JPG)
  entities worked with.jpeg
```
Primary logo used everywhere: `Assets/Studio Logo/شعار الهاشم-50.png`
All logo images use `filter: brightness(0) invert(1)` to render white on dark backgrounds.

## Design System (CSS Variables)
```css
--navy:       #1B2B6E   /* primary brand blue */
--navy-dark:  #0F1A4A   /* darkest bg (hero, footer, cards) */
--navy-mid:   #2D3F8F
--navy-light: #3D5296
--beige:      #C9B99A   /* primary accent / gold */
--beige-light:#E8DDD0
--beige-pale: #F4F0EA   /* light section backgrounds */
--white:      #FFFFFF
--off-white:  #F6F4F0
--gray:       #8A8A8A
--text-dark:  #1A1A2E
--font-ar:    'Cairo', 'Tajawal', sans-serif
--font-en:    'Inter', sans-serif
```

## Layout Direction
- `<html lang="ar" dir="rtl">` — all pages are RTL Arabic-primary
- English labels/values use `dir="ltr"` inline where needed
- Use **logical CSS properties** (`border-inline-end`, `margin-inline-start`) rather than physical left/right where direction matters

## Navigation Structure
Fixed sticky navbar (z-index: 1100) with:
- **Logo** (image, right side in RTL)
- **Nav links** — currently: `أعمالنا ▾` (dropdown) + `تواصل معنا` CTA button
  - `أعمالنا` dropdown items: الأعراس → `wedding.html`, المؤسسات → `organizations.html`, العقارات → `real-estate.html`
- **Mobile**: Nav links show inline (no hamburger overlay). Dropdown hidden on mobile. Logo scales to 62px height.
- Nav becomes dark (`nav.scrolled`) after scrolling 80px via JS

## Footer (All Pages)
Compact contact-only strip — **no logo, no copyright bar**:
```html
<footer>
  <div class="footer-simple">
    <div class="footer-contacts">
      <a class="footer-contact-item"> WhatsApp </a>
      <a class="footer-contact-item"> Email </a>
      <a class="footer-contact-item"> Phone </a>
    </div>
  </div>
</footer>
```
Contact details:
- WhatsApp: https://wa.me/message/M55JPOQYOR6RF1
- Email: alihashem@alhashem.sa
- Phone: +966 050 891 1564 (050 891 1564)

Footer CSS uses `border-inline-end` for RTL-correct separators between contact items.
Mobile (<640px): items stack vertically with `border-bottom` separators.

## Key JS Patterns (inline in each page)
1. **Navbar scroll** — adds `.scrolled` class when `scrollY > 80`
2. **IntersectionObserver** — adds `.visible` to `.reveal` elements as they enter viewport
3. **Lightbox** — gallery image viewer (only on sub-pages with galleries)
4. **Loader** (index.html only) — fades out after 2200ms

## Responsive Breakpoints
| Breakpoint | Notes |
|---|---|
| max-width: 1024px | Tablet: grid adjustments |
| max-width: 768px | Mobile: nav items inline (no hamburger), section padding reduces |
| max-width: 640px | Footer contacts stack vertically |
| max-width: 480px | Gallery goes single column |

## Sub-page Hero
Sub-pages (wedding/organizations/real-estate) use `.page-hero` with `min-height: 68vh`, floating diamond animations, and breadcrumb navigation. Hero has `padding-top: 80px` to clear the fixed navbar.

## What Has Been Done (recent session)
- **Footer redesigned**: removed large logo image and copyright/CR bar from all 4 pages; only compact contact strip remains
- **Mobile nav redesigned**: removed hamburger overlay; removed "من نحن" and "شركاؤنا" nav items; nav links now show inline on all screen sizes
- **Nav z-index**: fixed to 1100 consistently across all pages (was 1000 on sub-pages)
- **Footer CSS**: switched `border-right` → `border-inline-end` for proper RTL separator direction; added mobile stacking media query
- **Dead CSS removed**: `.footer-main`, `.footer-bottom`, `.footer-brand-logo`, `.footer-social`, `.footer-col`, `.fb-d` etc. cleaned up across all files

## Common Pitfalls
- CSS and JS are duplicated in each HTML file — any shared change must be made in **all 4 files**
- RTL flex order: in `flex-direction: row` with `dir="rtl"`, first HTML child appears on the **right** visually
- Avoid `border-right`/`border-left` for separators — use `border-inline-end` / `border-inline-start`
- The logo file path has Arabic characters — always URL-encode: `%D8%B4%D8%B9%D8%A7%D8%B1%20%D8%A7%D9%84%D9%87%D8%A7%D8%B4%D9%85-50.png`
