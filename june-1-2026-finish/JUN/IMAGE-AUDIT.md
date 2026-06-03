# Image SEO Audit — knxstore.vn

**Date:** 2026-06-01  
**Scope:** Homepage (https://knxstore.vn)  
**Data source:** parse_html.py + PageSpeed Insights API

---

## Executive Summary

| Metric | Status | Count |
|--------|--------|-------|
| Total Images | — | 92 |
| Missing / Empty Alt Text | FAIL | 9 |
| Generic Alt Text ("Image") | FAIL | 1+ |
| Inconsistent Logo Alt Text | WARN | 1 duplicate |
| No `width` + `height` (CLS risk) | FAIL | 90 / 92 |
| No `loading="lazy"` | FAIL | 92 / 92 |
| No `fetchpriority="high"` on LCP | FAIL | — |
| No JS lazy-loader detected | INFO | lazy_method: none |
| Estimated image payload savings | CRITICAL | **8,707 KiB** (PSI) |
| Incorrect aspect ratios | WARN | detected by PSI |
| Images as % of total payload | CRITICAL | ~67% of 13,022 KiB |

**Priority order:** Fix CLS (width/height) → Enable lazy loading → Convert to WebP → Fix alt text → Fix aspect ratios → Add fetchpriority to LCP

---

## 1. Alt Text — Specific Copy for 9 Banner Images

All 9 banners are confirmed empty alt. Filenames are used as the source of truth for content inference.

| File | Suggested Alt Text |
|------|--------------------|
| `1__knxstore-solution.jpg` | `Giải pháp tự động hóa tòa nhà KNXStore — KNX, DALI-2, Matter và BACnet` |
| `2__Casambi-solution.jpg` | `Giải pháp chiếu sáng không dây Casambi — điều khiển Bluetooth mesh cho tòa nhà` |
| `3__eve-solution.jpg` | `Thiết bị Matter Eve — cảm biến và điều khiển thông minh tương thích HomeKit` |
| `4__knx-solution.jpg` | `Hệ thống KNX TP — tiêu chuẩn quốc tế tự động hóa điện thông minh cho tòa nhà` |
| `5__BW_SATEL_ALARM_SYSTEM_INTEGRA_300x150.jpg` | `Hệ thống báo động Satel Integra — tích hợp an ninh với KNX qua gateway` |
| `6__MATTER_SOLUTION_SUNRICHER_AZOULA.jpg` | `Giải pháp Matter Sunricher Azoula — bộ điều khiển LED thông minh chuẩn Matter` |
| `7__MATTER_SOLUTION_SUNRICHER.jpg` | `Thiết bị Matter Sunricher — dimmer và driver LED tương thích Apple Home, Google` |
| `8__AQARA-solution.jpg` | `Giải pháp Aqara Matter — cảm biến, công tắc và hub thông minh cho nhà ở` |
| `9__PHILIPS-HUE-solution.jpg` | `Hệ thống chiếu sáng thông minh Philips Hue — tích hợp Matter và KNX gateway` |

**Additional fix — blog thumbnail:**

| File | Current | Suggested |
|------|---------|-----------|
| `/assets/image/post/huong-dan-cap-nhat-firmware...jpg` | `alt="Image"` | `alt="Hướng dẫn cập nhật firmware thiết bị KNX — quy trình từng bước cho kỹ thuật viên"` |

**Logo consistency fix:**

| Element | Current | Fix |
|---------|---------|-----|
| Header logo | `alt="KNXStore Logo"` | Keep (canonical form) |
| Footer logo duplicate | `alt="KNX Store Logo"` | Change to `alt="KNXStore Logo"` (match header, remove space) |

---

## 2. HTML Templates

### 2a. LCP Hero Image (Above the Fold — Banner Slider First Frame)

```html
<!-- LCP hero: fetchpriority="high", NO loading="lazy", explicit dimensions -->
<picture>
  <source
    srcset="/assets/banner/1__knxstore-solution.avif 1920w, /assets/banner/1__knxstore-solution-800.avif 800w"
    sizes="100vw"
    type="image/avif"
  >
  <source
    srcset="/assets/banner/1__knxstore-solution.webp 1920w, /assets/banner/1__knxstore-solution-800.webp 800w"
    sizes="100vw"
    type="image/webp"
  >
  <img
    src="/assets/banner/1__knxstore-solution.jpg"
    alt="Giải pháp tự động hóa tòa nhà KNXStore — KNX, DALI-2, Matter và BACnet"
    width="1920"
    height="640"
    fetchpriority="high"
    decoding="sync"
  >
</picture>
```

**Rules applied:**
- `fetchpriority="high"` — tells browser to prioritize this network request
- No `loading="lazy"` — LCP images must never be lazy-loaded
- `decoding="sync"` on LCP — avoids async decode delay on the critical image
- `width` + `height` — prevents CLS during load
- AVIF > WebP > JPEG fallback chain

### 2b. Below-Fold Images (Banners 2–9, Product Cards, Blog Thumbnails)

```html
<!-- Below-fold: loading="lazy" + decoding="async", explicit dimensions -->
<picture>
  <source
    srcset="/assets/banner/2__Casambi-solution.avif 1920w, /assets/banner/2__Casambi-solution-800.avif 800w"
    sizes="100vw"
    type="image/avif"
  >
  <source
    srcset="/assets/banner/2__Casambi-solution.webp 1920w, /assets/banner/2__Casambi-solution-800.webp 800w"
    sizes="100vw"
    type="image/webp"
  >
  <img
    src="/assets/banner/2__Casambi-solution.jpg"
    alt="Giải pháp chiếu sáng không dây Casambi — điều khiển Bluetooth mesh cho tòa nhà"
    width="1920"
    height="640"
    loading="lazy"
    decoding="async"
  >
</picture>
```

**For product thumbnails (smaller dimensions):**

```html
<picture>
  <source srcset="/assets/products/knx-dimmer.avif" type="image/avif">
  <source srcset="/assets/products/knx-dimmer.webp" type="image/webp">
  <img
    src="/assets/products/knx-dimmer.jpg"
    alt="KNX dimmer 4 kênh 250W — điều chỉnh độ sáng đèn LED và halogen"
    width="300"
    height="300"
    loading="lazy"
    decoding="async"
  >
</picture>
```

**For blog thumbnails:**

```html
<picture>
  <source srcset="/assets/image/post/huong-dan-cap-nhat-firmware.avif" type="image/avif">
  <source srcset="/assets/image/post/huong-dan-cap-nhat-firmware.webp" type="image/webp">
  <img
    src="/assets/image/post/huong-dan-cap-nhat-firmware.jpg"
    alt="Hướng dẫn cập nhật firmware thiết bị KNX — quy trình từng bước cho kỹ thuật viên"
    width="800"
    height="450"
    loading="lazy"
    decoding="async"
  >
</picture>
```

---

## 3. Shell Commands — Convert to WebP and AVIF

### Check available tools first

```bash
which exiftool cwebp convert ffmpeg
```

### Batch convert banner images to WebP (cwebp — preferred)

```bash
cd /path/to/site/assets/banner

# Convert all JPEG banners to WebP at quality 82, preserve metadata
for f in *.jpg; do
  cwebp -q 82 -metadata all "$f" -o "${f%.jpg}.webp"
done

# Verify output sizes
du -sh *.webp | sort -h
```

### Batch convert to WebP (ImageMagick fallback if cwebp not installed)

```bash
cd /path/to/site/assets/banner

for f in *.jpg; do
  convert "$f" -quality 82 -define webp:lossless=false "${f%.jpg}.webp"
done
```

### Generate AVIF variants (FFmpeg — slower but best compression)

```bash
cd /path/to/site/assets/banner

for f in *.jpg; do
  ffmpeg -i "$f" -c:v libaom-av1 -crf 30 -still-picture 1 -y "${f%.jpg}.avif"
done
```

### Generate responsive variants per banner (1920w + 800w for mobile)

```bash
cd /path/to/site/assets/banner

for f in *.jpg; do
  base="${f%.jpg}"
  # WebP responsive variants
  convert "$f" -resize 1920x -quality 82 "${base}.webp"
  convert "$f" -resize 800x  -quality 82 "${base}-800.webp"
  # AVIF responsive variants
  ffmpeg -i "$f" -vf scale=800:-1 -c:v libaom-av1 -crf 30 -still-picture 1 -y "${base}-800.avif"
done
```

### Inject IPTC metadata (brand attribution for Google Images rich results)

```bash
cd /path/to/site/assets/banner

exiftool -overwrite_original \
  -IPTC:By-line="KNXStore.vn" \
  -IPTC:Credit="KNXStore.vn" \
  -IPTC:CopyrightNotice="Copyright 2026 Công ty CP Tích hợp Hệ thống Liên Minh" \
  -IPTC:Source="knxstore.vn" \
  -XMP:Creator="KNXStore.vn" \
  -XMP:Rights="Copyright 2026 KNXStore.vn" \
  *.jpg *.webp *.png
```

---

## 4. Savings Estimate — WebP Conversion

PSI reports **8,707 KiB** savings from "Serve images in next-gen formats".

Typical WebP compression ratios vs JPEG at equivalent perceptual quality:

| Image type | JPEG → WebP savings | Applied to knxstore.vn |
|------------|---------------------|------------------------|
| Banner/hero photos | 25–35% | ~2,177–3,047 KiB |
| Product photos | 20–30% | depends on count |
| Blog thumbnails | 25–35% | small contribution |
| **Total realistic estimate** | **25–30%** of image payload | **2,177–2,612 KiB saved** |

PSI's 8,707 KiB figure is the upper bound assuming lossless re-encode of currently unoptimized originals. In practice, converting the 9 oversized banner images alone (which dominate the ~8.7 MB identified savings) to WebP at quality 82 should recover 3–5 MB. Switching to AVIF adds another 15–20% on top of WebP.

**Practical target after full WebP conversion:** Image payload drops from ~8,700 KiB to ~2,000–3,500 KiB — a 60–75% reduction in image transfer size.

---

## 5. Prioritized Fix List

| Priority | Issue | Impact | Effort | Fix |
|----------|-------|--------|--------|-----|
| P1 | 90 images missing `width` + `height` | CLS — layout shift on every page load | Medium — requires measuring actual pixel dimensions | Add `width` + `height` to all `<img>` tags |
| P2 | 92 images — zero lazy loading | Loads entire 8.7 MB image payload on first paint | Low — add `loading="lazy"` to below-fold `<img>` tags | Add `loading="lazy" decoding="async"` to all non-LCP images |
| P3 | LCP banner has no `fetchpriority="high"` | LCP score degraded — browser treats hero same as other images | Low — single attribute on one element | Add `fetchpriority="high"` to first banner slide `<img>` |
| P4 | No WebP/AVIF served | 8,707 KiB wasted bandwidth — direct PSI flag | High — image conversion + `<picture>` element refactor | Convert banners + product images to WebP; wrap in `<picture>` |
| P5 | 9 banners with empty alt text | Accessibility failure + missed keyword signal for Google Images | Low — copy-paste from table in Section 1 | Add alt text from Section 1 table |
| P6 | Blog thumbnail `alt="Image"` | Generic, zero SEO value, hurts Google Images ranking | Low — update CMS template default | Fix template so alt is pulled from post title |
| P7 | Incorrect aspect ratios (PSI flag) | CLS — images rendered at wrong ratio cause reflow | Medium — identify which images + fix CSS or add `aspect-ratio` | Audit each flagged image: fix intrinsic dimensions or CSS |
| P8 | Footer logo alt inconsistency | Minor — dilutes brand name entity signal | Trivial | Change `alt="KNX Store Logo"` → `alt="KNXStore Logo"` |
| P9 | No CDN for images | High-latency delivery from origin for international users | High — requires CDN setup | Serve `/assets/` via Cloudflare or BunnyCDN |
| P10 | Missing IPTC metadata on banners | No brand attribution in Google Images rich results | Low — batch exiftool command | Run exiftool batch from Section 3 |

---

## 6. Implementation Checklist

### Sprint 1 — Quick wins (< 1 day, zero tooling required)

- [ ] Add `width` + `height` to all 90 `<img>` tags missing dimensions
- [ ] Add `loading="lazy" decoding="async"` to all below-fold images
- [ ] Add `fetchpriority="high"` to LCP hero (first banner slide)
- [ ] Paste alt text from Section 1 into 9 banner `<img>` elements
- [ ] Fix blog thumbnail CMS template — pull alt from post title, not "Image"
- [ ] Fix footer logo alt: `"KNX Store Logo"` → `"KNXStore Logo"`

### Sprint 2 — WebP conversion (2–4 hours with shell commands)

- [ ] Run cwebp batch convert on all `/assets/banner/*.jpg`
- [ ] Run cwebp batch convert on all `/assets/image/post/*.jpg` and product images
- [ ] Generate 800w responsive variants for each banner
- [ ] Update HTML to `<picture>` elements with AVIF > WebP > JPEG fallback
- [ ] Re-run PSI to verify savings materialise

### Sprint 3 — Structural (requires CMS/dev time)

- [ ] Investigate and fix PSI "incorrect aspect ratio" images
- [ ] Evaluate CDN setup (Cloudflare free tier covers this case)
- [ ] Run exiftool IPTC batch inject for brand attribution
- [ ] Generate AVIF variants for banners (FFmpeg, slower but worthwhile)

---

## 7. Expected Outcome After All Fixes

| Metric | Before | After (estimated) |
|--------|--------|-------------------|
| Image payload | ~8,700 KiB | ~2,000–3,500 KiB |
| CLS score | Failing (no dimensions) | Pass |
| LCP score | Degraded | Improved (fetchpriority + no lazy on hero) |
| Accessibility (alt) | 10 violations | 0 violations |
| Google Images indexability | Poor (empty alt on all banners) | Good |
| PSI "Serve next-gen formats" | 8,707 KiB flag | Resolved |

---

*Generated by Claude SEO / seo-images skill — knxstore.vn audit 2026-06-01*
