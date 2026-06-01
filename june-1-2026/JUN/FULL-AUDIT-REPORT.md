# SEO Audit Report — knxstore.vn
**Date:** 2026-06-01  
**Audited by:** Claude SEO v2.0.0  
**Scope:** Homepage + Category + Product + Blog pages, Sitemaps, Technical, Schema, GEO  
**Credentials:** Google API Key (PSI v5 + CrUX) | MCP GASC available

---

## SEO Health Score: 66 / 100

| Category | Weight | Score | Weighted |
|----------|--------|-------|---------|
| Technical SEO | 22% | 70 | 15.4 |
| Content Quality | 23% | 75 | 17.3 |
| On-Page SEO | 20% | 72 | 14.4 |
| Schema / Structured Data | 10% | 68 | 6.8 |
| Performance (CWV) | 10% | 72 | 7.2 |
| AI Search Readiness (GEO) | 10% | 30 | 3.0 |
| Images | 5% | 35 | 1.75 |

Performance score = field data CrUX (tất cả GOOD) weighted với lab mobile 66/100.

---

## Business Type Detected
**E-commerce B2B chuyên ngành + Local Business**
- Products, categories, cart → E-commerce
- Địa chỉ, số điện thoại, GeoCoordinates → Local Business
- Niche: KNX, DALI-2, Casambi, Matter, building automation (Việt Nam)
- Ngôn ngữ: `vi_VN`

---

## Executive Summary

KNXStore.vn có nền tảng kỹ thuật tốt (Cloudflare CDN, HTTPS, HSTS, sitemap index đầy đủ), schema product khá hoàn chỉnh (Product + ShippingDeliveryTime + MerchantReturnPolicy), và content blog có chiều sâu (~5.000 từ/bài). Điểm yếu tập trung ở 3 nhóm chính: (1) **Images thiếu alt text và dimensions** — ảnh hưởng CLS và image SEO; (2) **Không có llms.txt/ai.txt** — site gần như vô hình với AI search (ChatGPT, Perplexity, Google AI Overviews); (3) **FAQPage trên homepage sai target** — không còn trigger Google rich results cho commercial site (từ 08/2023).

**Top 5 critical issues:**
1. 9/92 ảnh homepage không có alt text (bao gồm toàn bộ banner)
2. Không có `llms.txt` — zero GEO readiness
3. FAQPage không generate rich results trên Google (thương mại, 08/2023)
4. 90/92 ảnh thiếu `width`/`height` → CLS (Layout Shift)
5. Robots.txt không khai báo Sitemap URL

**Top 5 quick wins:**
1. Thêm alt text vào 9 banner images (30 phút)
2. Tạo `/llms.txt` (1 giờ)
3. Thêm `Sitemap:` directive vào robots.txt (5 phút)
4. Thêm `loading="lazy"` và dimensions cho images (1 ngày)
5. Thêm Content-Security-Policy header (1 giờ, cần test)

---

## 1. Technical SEO — 70/100

### 1.1 HTTPS & Redirects
| Check | Status | Detail |
|-------|--------|--------|
| HTTPS | ✅ Pass | SSL active |
| HTTP → HTTPS redirect | ✅ Pass | 301 Permanent |
| HSTS | ✅ Pass | `max-age=31536000; includeSubDomains` |
| www redirect | ⚠️ Not checked | Verify www.knxstore.vn → knxstore.vn |

### 1.2 Security Headers
| Header | Status |
|--------|--------|
| `Strict-Transport-Security` | ✅ Present |
| `X-Content-Type-Options: nosniff` | ✅ Present |
| `X-Frame-Options: SAMEORIGIN` | ✅ Present |
| `Referrer-Policy: same-origin` | ✅ Present |
| `Content-Security-Policy` | ❌ **MISSING** |
| `Permissions-Policy` | ❌ MISSING |

**[MEDIUM]** Thiếu CSP — tăng nguy cơ XSS injection. Cloudflare có thể add CSP header-level mà không cần code deploy.

### 1.3 Robots.txt
```
User-agent: *
Disallow: /users/login
```

**Issues:**
- **[MEDIUM]** Không có `Sitemap: https://knxstore.vn/sitemap.xml` directive
- **[MEDIUM]** Không block `/search?` hoặc pagination parameters — có thể tạo duplicate content với crawl
- **[LOW]** Không có crawl delay — với 1.140 URLs Googlebot sẽ tự điều chỉnh

**Fix:**
```
User-agent: *
Disallow: /users/login
Disallow: /search?
Sitemap: https://knxstore.vn/sitemap.xml
```

### 1.4 Sitemap
| Sub-sitemap | URLs | Status |
|-------------|------|--------|
| sitemap-product.xml | 735 | ✅ |
| sitemap-category.xml | 89 | ✅ |
| sitemap-post.xml | 231 | ✅ |
| sitemap-solution.xml | 12 | ✅ |
| sitemap-brand.xml | 73 | ✅ |
| **Total** | **1,140** | ✅ |

- `lastmod` đồng bộ (2026-06-01) ✅
- Sitemap index ✅
- **[LOW]** `changefreq` và `priority` không có — không ảnh hưởng ranking nhưng là best practice

### 1.5 Crawlability
- CDN: Cloudflare ✅
- Blog URLs dùng `.html` extension — không có vấn đề kỹ thuật nhưng khác convention category/product

### 1.6 Core Web Vitals (Estimated)
- PSI API rate-limited — không có kết quả lab data trong audit này
- **[HIGH]** 90/92 ảnh thiếu `width`/`height` → CLS risk cao
- **[HIGH]** Không có `loading="lazy"` trên bất kỳ ảnh nào → LCP ảnh hưởng
- Cloudflare CDN ✅ giảm TTFB
- Nhiều vendor CSS/JS (nouislider, swiper, drift-zoom, simplebar, choices.js) — có thể defer

**Action:** Cài Google API key và chạy `/seo google pagespeed` để có field data thực tế.

---

## 2. Content Quality — 75/100

### 2.1 Homepage Content
- Tiêu đề H1 rõ ràng, có keyword thương hiệu: *"Thiết bị KNX, Casambi, Matter và DALI - Phân phối chính hãng tại Việt Nam"* ✅
- H2 structure: Casambi, KNX, An ninh, HVAC, Giá trị — tốt, theo product category ✅
- H3: 28 product names — đây là featured products, OK

### 2.2 Blog / Knowledge Base
- 231 bài viết có sitemap ✅
- Blog post mẫu (~5.000 từ): chiều sâu kỹ thuật tốt ✅
- BlogPosting schema đầy đủ ✅
- BreadcrumbList ✅
- Author signal: hiện diện ✅
- URLs blog: `.html` extension — consistent nhưng không phải best practice hiện đại

**[MEDIUM]** Cần audit thêm: bao nhiêu % trong 231 bài > 800 từ? Mục tiêu cho B2B technical niche: ≥ 1.000 từ/bài.

### 2.3 E-E-A-T Signals
- **Experience:** Có case study solution pages (12 URLs) ✅
- **Expertise:** Blog kỹ thuật sâu về KNX, DALI, firmware ✅
- **Authoritativeness:** DMCA protection, Bộ Công Thương badge ✅
- **Trust:** Địa chỉ, số điện thoại, schema LocalBusiness ✅

**[MEDIUM]** Thiếu author bio pages với credentials rõ ràng — cần cho E-E-A-T QRG compliance (đặc biệt với technical/B2B niche).

### 2.4 Thin Content Risk
- 735 product pages — risk thin content nếu nhiều trang chỉ có specs mà không có description
- 89 category pages — cần verify có unique intro text không hay chỉ là product grid

---

## 3. On-Page SEO — 72/100

### 3.1 Homepage
| Element | Value | Status |
|---------|-------|--------|
| Title | "KNXStore \| Thiết bị và giải pháp điều khiển cho mọi công trình" (62 chars) | ✅ |
| Meta Description | 117 chars — mô tả sản phẩm, có signal rõ | ✅ |
| H1 | "Thiết bị KNX, Casambi, Matter và DALI - Phân phối chính hãng tại Việt Nam" | ✅ |
| Canonical | `https://knxstore.vn/` | ✅ |
| OG Title | Có | ✅ |
| OG Description | Có | ✅ |
| OG Image | `https://knxstore.vn/assets/knxstore.png` | ✅ |
| Hreflang | Không có | ⚪ N/A (chỉ vi_VN) |
| meta keywords | "KNXStore" (1 từ) | ⚠️ Info |

### 3.2 Category Page (/casambi-gateway)
| Element | Value | Status |
|---------|-------|--------|
| Title | "Điều khiển Casambi chính hãng, cao cấp" | ✅ |
| Meta Desc | Có, mô tả sản phẩm Casambi Gateway | ✅ |
| H1 | "Điều khiển Casambi" | ⚠️ Quá ngắn |
| Schema | Không có CollectionPage/ItemList | ❌ |

**[MEDIUM]** H1 category pages quá ngắn và generic. Nên là: *"Bộ điều khiển Casambi Gateway chính hãng — Mua tại KNXStore"*

**[MEDIUM]** Category pages thiếu CollectionPage hoặc ItemList schema — bỏ lỡ opportunity structured data cho SERP.

### 3.3 Product Pages
| Element | Status |
|---------|--------|
| Product schema | ✅ |
| ShippingDeliveryTime | ✅ |
| MerchantReturnPolicy | ✅ |
| PropertyValue (specs) | ✅ |
| Price | ✅ |
| BreadcrumbList | ✅ |

Product pages schema rất tốt — phản ánh đầu tư thực sự.

### 3.4 Internal Linking
- Homepage có 258 internal links — đây là menu + featured products, bình thường cho e-commerce ✅
- Chỉ có 4 external links — tỉ lệ thấp, OK cho SEO nhưng có thể thiếu authority signals

---

## 4. Schema / Structured Data — 68/100

### Homepage Schema (1 JSON-LD block)
```
Organization + LocalBusiness
  └─ ImageObject, PostalAddress, GeoCoordinates, ContactPoint
WebSite + SearchAction (Sitelinks Searchbox)
BreadcrumbList
WebPage + ImageObject
FAQPage (11 questions)
```

| Schema | Status | Note |
|--------|--------|------|
| Organization / LocalBusiness | ✅ | Đầy đủ, có GeoCoordinates |
| WebSite + SearchAction | ✅ | Sitelinks Searchbox potential |
| BreadcrumbList | ✅ | |
| WebPage | ✅ | |
| FAQPage | ⚠️ Info | Không còn trigger Google rich results cho commercial site (Aug 2023). Giữ lại vì có giá trị cho AI citation (ChatGPT, Perplexity). **Không cần xóa.** |

### Thiếu Schema
| Schema Type | Page Type | Priority |
|-------------|-----------|----------|
| CollectionPage / ItemList | Category pages | **High** |
| Article / BlogPosting | Blog posts | ✅ Có rồi |
| Product | Product pages | ✅ Có rồi |
| LocalBusiness (store page) | /lien-he hoặc About | Medium |

---

## 5. Performance / Core Web Vitals — 72/100

**Nguồn:** PSI v5 + CrUX field data (period 2026-05-03 → 2026-05-30)

### Field Data — CrUX (Real Users, p75)

| Metric | Value | Rating | Good % |
|--------|-------|--------|--------|
| TTFB | 535ms | ✅ GOOD | 90.8% |
| FCP | 894ms | ✅ GOOD | 94.8% |
| LCP | 989ms | ✅ GOOD | 97.1% |
| INP | 34ms | ✅ GOOD | 98.8% |
| CLS | 0.000 | ✅ GOOD | 95.8% |

**Tất cả 5 Core Web Vitals ở mức GOOD** — đây là điểm mạnh bất ngờ của site. Cloudflare CDN và caching đang làm tốt công việc với real users.

### Lab Data — Lighthouse (Simulated)

| | Mobile | Desktop |
|--|--------|---------|
| Performance | 66/100 | 73/100 |
| Accessibility | 87/100 | 87/100 |
| Best Practices | 92/100 | 96/100 |
| SEO (Lighthouse) | 92/100 | 92/100 |

| Lab Metric | Mobile | Desktop |
|------------|--------|---------|
| FCP | 1.7s | 0.5s |
| LCP | **16.3s** ⚠️ | **7.3s** ⚠️ |
| TBT | 80ms ✅ | 90ms ✅ |
| CLS | 0 ✅ | 0 ✅ |
| Speed Index | 8.2s | 1.4s |

> **Lưu ý quan trọng:** Lab LCP (16.3s mobile) vs Field LCP (989ms) chênh lệch lớn vì lab không có Cloudflare cache và chạy với thiết bị mô phỏng chậm hơn. Google Rankings dùng **field data** — nên CWV hiện tại **không ảnh hưởng xấu đến ranking**.

### Top Opportunities (PSI)

| Issue | Savings | Priority |
|-------|---------|----------|
| Image delivery optimization | **8,707 KiB** | 🔴 Critical |
| Render-blocking requests | 940ms | 🟠 High |
| Unused JavaScript | 515 KiB / ~1,050ms | 🟠 High |
| Inefficient cache lifetimes | 8,038 KiB | 🟡 Medium |
| Unused CSS | 52 KiB / 300ms | 🟡 Medium |
| Network payload quá lớn | **13,022 KiB total** | 🟠 High |

### Other Issues
- **Browser console errors** detected — cần kiểm tra DevTools
- **LCP request discovery** — LCP element chưa được preload đúng cách
- **Images incorrect aspect ratio** — một số ảnh bị stretch/squish
- **Color contrast** — text/background không đủ contrast ratio (accessibility)

---

## 6. Images — 35/100

### Audit Summary (Homepage — 92 images)
| Check | Result | Pass? |
|-------|--------|-------|
| Images with alt text | 83/92 | ⚠️ |
| Images missing/empty alt | **9/92** | ❌ |
| Images with width + height | **2/92** | ❌ |
| Images with lazy loading | **0/92** | ❌ |
| Image payload | **8,707 KiB savings possible** | ❌ |
| Aspect ratio issues | Detected (PSI) | ❌ |

### Ảnh thiếu alt (banner slider — Critical)
Toàn bộ 9 banner ảnh không có alt text:
```
banner/1__knxstore-solution.jpg          → alt="" (EMPTY)
banner/2__Casambi-solution.jpg           → alt="" (EMPTY)
banner/3__eve-solution.jpg               → alt="" (EMPTY)
banner/4__knx-solution.jpg               → alt="" (EMPTY)
banner/5__BW_SATEL_ALARM_SYSTEM...jpg    → alt="" (EMPTY)
banner/6__MATTER_SOLUTION...jpg          → alt="" (EMPTY)
banner/7__MATTER_SOLUTION_SUNRICHER.jpg  → alt="" (EMPTY)
banner/8__AQARA-solution.jpg             → alt="" (EMPTY)
banner/9__PHILIPS-HUE-solution.jpg       → alt="" (EMPTY)
```

**Suggested alt text:**
- `alt="Giải pháp KNX tự động hóa tòa nhà - KNXStore"`
- `alt="Giải pháp chiếu sáng thông minh Casambi - KNXStore"`
- `alt="Giải pháp Matter Smarthome Sunricher - KNXStore"`
... (tương tự theo nội dung banner)

### Blog thumbnail generic alt
`assets/image/post/huong-dan-cap-nhat-firmware...jpg` → `alt="Image"` — thay bằng tiêu đề bài viết.

### Thiếu dimensions — CLS
90/92 ảnh không có `width` và `height`. Cần thêm vào HTML:
```html
<img src="..." alt="..." width="800" height="600" loading="lazy">
```

---

## 7. AI Search Readiness (GEO) — 30/100

### AI Crawler Access
| File | Status |
|------|--------|
| `/llms.txt` | ❌ **NOT FOUND** |
| `/ai.txt` | ❌ NOT FOUND |
| `/.well-known/llms.txt` | ❌ NOT FOUND |
| Robots.txt (AI bots) | ⚠️ Không block, không cho phép explicitly |

**[CRITICAL for GEO]** Không có `llms.txt` — ChatGPT, Perplexity, Claude, Gemini không biết cách cite knxstore.vn. Đây là cơ hội lớn trong niche KNX/DALI vì rất ít competitor Việt Nam có llms.txt.

### Citability Signals
| Signal | Status |
|--------|--------|
| FAQPage (11 Q&A) | ✅ — tốt cho AI extraction |
| GeoCoordinates + LocalBusiness | ✅ |
| SearchAction (Sitelinks) | ✅ |
| Structured specs (PropertyValue) | ✅ |
| Author credentials visible | ⚠️ Cần cải thiện |
| legalName trong schema | ✅ "Công ty TNHH Tích Hợp Hệ Thống Liên Minh" |

### Recommended llms.txt Template

Tạo file `/llms.txt` với nội dung:
```markdown
# KNXStore.vn — Phân phối thiết bị tự động hóa tòa nhà

KNXStore.vn là nhà phân phối chính hãng KNX, DALI-2, Casambi, Matter, DMX512,
BACnet, Modbus tại Việt Nam. Cung cấp thiết bị và tư vấn giải pháp cho
System Integrator, ME Contractor và chủ nhà.

## Sản phẩm chính
- KNX TP: bus controller, gateway, sensor, actuator
- DALI-2: driver, controller, sensor
- Casambi: mesh lighting control (Bluetooth)
- Matter: smart home devices
- An ninh: Satel alarm systems

## Tài nguyên
- Catalog sản phẩm: https://knxstore.vn/
- Kiến thức kỹ thuật: https://knxstore.vn/kien-thuc/
- Giải pháp: https://knxstore.vn/giai-phap/
- Liên hệ: https://knxstore.vn/lien-he
```

---

## 8. Local SEO — 65/100

### Schema LocalBusiness
```json
{
  "@type": ["Organization", "LocalBusiness"],
  "name": "KNXStore.vn",
  "legalName": "Công ty TNHH Tích Hợp Hệ Thống Liên Minh",
  "GeoCoordinates": ✅,
  "PostalAddress": ✅,
  "ContactPoint": ✅
}
```

- LocalBusiness schema ✅
- GeoCoordinates ✅
- NAP trong schema ✅

**[MEDIUM]** Không kiểm tra được Google Business Profile từ audit này (cần Google API). Verify GBP listing tại `business.google.com` với:
- Categories: "Electrical equipment supplier", "Automation company"
- Giờ làm việc
- Photos (tối thiểu 10 ảnh)

---

## Prioritized Action Plan

### 🔴 Critical — Fix ngay (< 1 tuần)

| # | Action | File/Page | Effort | Impact |
|---|--------|-----------|--------|--------|
| C1 | Thêm alt text cho 9 banner images | Homepage HTML | 30 min | Image SEO, Lighthouse SEO 92→100 |
| C2 | Tạo `/llms.txt` | Server root | 1 hr | GEO / AI search visibility |
| C3 | Thêm `Sitemap:` vào robots.txt + block `/search?` | robots.txt | 10 min | Crawl efficiency |

### 🟠 High — Fix trong 1 tuần

| # | Action | File/Page | Effort | Impact |
|---|--------|-----------|--------|--------|
| H1 | Optimize/compress images — **8,707 KiB savings** | CDN / assets | 1-2 ngày | Lab performance +10-15pts |
| H2 | Thêm `width`, `height`, `loading="lazy"` vào tất cả ảnh | Template/CMS | 1 ngày | Lab LCP, CLS insurance |
| H3 | Thêm `CollectionPage` + `ItemList` schema vào category pages | Template | 4 hrs | Category SERP features |
| H4 | Đổi alt text blog thumbnail `"Image"` → tiêu đề bài viết | CMS template | 2 hrs | Image SEO |
| H5 | Fix render-blocking CSS/JS (940ms savings mobile) | Frontend | 1-2 ngày | Lab performance |
| H6 | Reduce unused JS: 515 KiB (swiper, simplebar, choices) | Frontend | 2-3 ngày | TBT, lab score |
| H7 | Verify GBP listing + categories/photos | GBP | 2 hrs | Local SEO |

### 🟡 Medium — Fix trong 1 tháng

| # | Action | File/Page | Effort | Impact |
|---|--------|-----------|--------|--------|
| M1 | Content-Security-Policy header | Cloudflare | 2-4 hrs | Security |
| M2 | Nâng H1 category pages (quá ngắn) | CMS template | 1 ngày | On-page SEO |
| M3 | Author bio pages với credentials | New pages | 2 ngày | E-E-A-T |
| M4 | Fix browser console errors (detected by PSI) | DevTools audit | 2 hrs | Best Practices score |
| M5 | Fix color contrast issues (accessibility) | CSS | 4 hrs | Accessibility 87→95+ |
| M6 | Fix LCP preload — add `<link rel="preload">` cho LCP image | HTML template | 2 hrs | Lab LCP mobile |
| M7 | Audit 735 product pages: verify description ≥ 200 từ | Backlog | 1 tuần | Thin content |
| M8 | Thêm `Permissions-Policy` header | Cloudflare | 1 hr | Security |

### 🟢 Low — Backlog

| # | Action | Effort |
|---|--------|--------|
| L1 | Chuẩn hoá blog URL (bỏ `.html` extension) + 301 redirects | 1 tuần |
| L2 | LocalBusiness schema cho `/lien-he` page | 2 hrs |
| L3 | Thêm `changefreq`/`priority` vào sitemaps | 2 hrs |
| L4 | DMCA badge replace bằng trust badge có schema | 1 hr |

---

## Dependency Map

```
C3 (robots.txt sitemap) ─── standalone, do first
C1 (banner alt text) ──────── standalone
C2 (llms.txt) ─────────────── standalone

H1 (image dims) ────── unlocks: CLS fix → performance score
H2 (category schema) ── unlocks: category SERP features
H4 (product content) ── unlocks: thin content risk removal
M5 (Google API + PSI) ─ unlocks: real CWV data → informs M6

M6 (JS defer) ─────────── depends on: M5 data to prioritize
M3 (author bio) ────────── depends on: H4 audit complete (know which pages need authors)
```

---

## How Would We Know This Failed?

Per ACCEPT principle:
- **C1 done:** Google Search Console Image report → 0 images flagged missing alt
- **C2 done:** ChatGPT web search "KNXStore" → cites knxstore.vn với đúng context
- **H1 done:** CrUX CLS score < 0.1 (Good) — measure via `python3 scripts/crux_history.py`
- **H2 done:** Google Search Console rich results → category pages xuất hiện trong ItemList SERP features

---

## Leading Indicators (Monitor Without Re-Auditing)

| Metric | Tool | Cadence |
|--------|------|---------|
| Google impressions/clicks | GSC (sau khi cài API) | Weekly |
| CLS score | CrUX History API | Monthly |
| AI citation (ChatGPT, Perplexity) | Manual search "KNX DALI Việt Nam" | Monthly |
| Product rich results status | GSC → Enhancements | Weekly |
| GBP insights | business.google.com | Weekly |

---

## Notes

- **Google Search Console:** Chưa có API key. Ưu tiên cài để có data thực từ GSC (clicks, indexation, CWV field). Xem: `python3 scripts/google_auth.py --setup`
- **Backlinks:** Common Crawl tier (Tier 0) — không có domain authority data. Cân nhắc free Moz API (2.500 rows/tháng).
- **Drift baseline:** Chưa có baseline. Chạy `python3 scripts/drift_baseline.py https://knxstore.vn` để capture snapshot đầu tiên.

---

*Generated by Claude SEO v2.0.0 | audit date: 2026-06-01 | knxstore.vn*
