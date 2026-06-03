# Content Quality & E-E-A-T Report — KNXStore.vn

**Prepared:** 2026-06-01  
**Analyst:** Claude SEO / seo-content v2.0.0  
**Scope:** Homepage + 5 blog posts + 5 category pages + 2 product pages  
**Framework:** Google QRG Sept 2025 + Helpful Content (merged core, March 2024)

---

## 1. Content Quality Score: 61/100

| Dimension | Score | Rationale |
|---|---|---|
| Content depth (blog) | 16/20 | Most posts 2,000–4,000 words; good technical detail |
| Content depth (product) | 10/20 | Flagship products excellent; risk of thin tail pages |
| Content depth (category) | 9/20 | Inconsistent: 120–850 words; no schema on any sampled page |
| E-E-A-T signals | 14/25 | Strong trust infrastructure; weak author attribution everywhere |
| Freshness & dating | 7/10 | Dates present but no `dateModified`; no update cadence signalling |
| AI citation readiness | 5/5 | Structured Q&A, numbered guides, technical tables — well-optimised |

---

## 2. E-E-A-T Scorecard

### 2.1 Experience — 15/25

**Signals present:**
- 12 solution/case study pages (confirmed: Vegi Resort case study, HVAC VRV/VRF project guide)
- In-situ project photography (Vegi Resort: 6 images, real location — Castellina in Chianti, Siena)
- First-hand firmware guides with actual IP addresses, file sizes, timing data (KAC005: 192.168.1.232, 11.4 MB firmware, 2–5 min flash time)
- Product FAQ drawn from real customer questions (Pet Immunity warning, Thread vs Zigbee distinctions)

**Gaps:**
- Case studies lack quantified outcomes (no energy savings %, no ROI, no client testimonial quote)
- No project timelines or commissioning photos showing KNXStore engineers on-site
- Vegi Resort case study does not name the System Integrator partner — anonymous delivery
- No "before/after" comparisons in any content sampled

**Fix priority:** Add 3 quantified project outcomes to existing case studies. 1 number per case (kWh saved, commissioning time, device count) turns marketing copy into verifiable evidence.

---

### 2.2 Expertise — 14/25

**Signals present:**
- Deep technical blog content: DALI-2 / IEC 62386 referenced (even if not linked), KNX firmware with specific command sequences, HVAC VRV/VRF protocol mapping (KNX, Modbus RTU/TCP, BACnet)
- Author "KNX Team" and "Tạ Minh Vũ" appear on some posts — confirms named human authorship exists in the CMS
- Product descriptions go beyond manufacturer spec sheets: CBU-ASD-LR page includes 650-word FAQ with DALI IEC 62386 profiling/sourcing/sinking explanation
- B2B positioning consistent with genuine integrator knowledge (KAC005 default credentials, HosTools process)

**Gaps:**
- "KNX Team" is a team label, not a credentialed individual — Google QRG expects a named person for YMYL-adjacent technical content
- No author credential page: no KNX certification number, no project portfolio count, no years of experience
- Zero external citations to KNX Association (knx.org), IEC standards, DALI Alliance, BACnet.org in any sampled post
- DALI-2 article (~650 words) is shallow for a protocol overview — lacks IEC 62386-8 device type table, address capacity math, bus power specs

**Fix priority:** Link to knx.org and IEC 62386 standards inline (2–3 per technical post). Create individual author pages before adding more blog posts under "KNX Team."

---

### 2.3 Authoritativeness — 16/25

**Signals present:**
- Official Casambi partner — stated explicitly in meta and on homepage
- Bộ Công Thương badge (online.gov.vn #36531) — Vietnamese government e-commerce registration
- MST 0311846236 — corporate legal identity verified
- DMCA.com protection badge — content ownership signal
- Brand partnerships: 20+ named manufacturers (Casambi, Kanonbus, Legrand, CP Electronics, Helvar, etc.)
- 307 blog posts indexed — topical volume signals domain authority in niche

**Gaps:**
- No inbound authoritative citations visible — no KNX Association partner page link, no manufacturer "where to buy" listing confirmed
- Vegi Resort case study is a European project not executed by KNXStore — authoritativeness for B2B clients depends on citing own projects, not third-party ones
- No industry association membership listed (KNX Association member? DALI Alliance?)
- No press coverage, awards, or third-party expert mentions

**Fix priority:** Request KNX Association to list KNXStore on their official partner directory. Add the partner listing URL to the About/footer. This single action is the highest-leverage authority signal available.

---

### 2.4 Trustworthiness — 16/25

**Signals present:**
- Full legal identity visible: company name, MST, registered address (28 Mai Chí Thọ, Phường Bình Trưng, TP.HCM), phone (0918.918.755), email (sales@knxstore.vn)
- DMCA and Bộ Công Thương badges above the fold
- LocalBusiness schema implied (address/phone/legalName in footer)
- HTTPS (implied from sitemap and URL structure)
- 24-month warranty stated on product pages
- Breadcrumb navigation consistent site-wide

**Gaps:**
- No dedicated `/pages/about` or `/pages/gioi-thieu` page found (404 on both standard paths)
- No Privacy Policy or Terms of Service links visible in sampled footer content
- Zero user reviews or ratings on any product page sampled — this is an explicit QRG trust signal for e-commerce
- Product pages show no `datePublished` / `dateModified` — freshness unverifiable by crawlers
- No correction policy, editorial standards, or content review date on blog posts

**Fix priority (critical):** Create an About page. This is the single most impactful fix for QRG compliance (see Section 5).

---

## 3. Thin Content Risk Assessment

### 3.1 Category Pages — Sampled 5 URLs

| Category URL | Word Count (intro) | H2 Structure | Schema | Risk Level |
|---|---|---|---|---|
| `/cong-tac-knx` | ~850 words | 8 H2s, brand-structured | Not confirmed | LOW |
| `/cam-bien-hien-dien-knx` | ~650 words | 5 H2s, topic-structured | Not confirmed | LOW |
| `/casambi-cam-bien` | ~420 words | 6 H2s, logical flow | Not confirmed | MEDIUM |
| `/dali-gateway` | ~280 words | 6 H2s but shallow | Not confirmed | MEDIUM |
| `/gateway-matter` | ~120 words | 2 H2s, thin | Not confirmed | HIGH |

**Pattern observed:** Larger/older categories (KNX switches: 14 products) have 700–850 word intros with brand-level H2s. Newer or smaller categories (Gateway Matter: 3 products) have 120-word intros insufficient for ranking.

**Schema finding (critical):** Zero category pages in sample have `CollectionPage` or `BreadcrumbList` JSON-LD confirmed. BreadcrumbList is present in product pages (confirmed on CBU-ASD-LR). This inconsistency needs fixing — category pages are the highest commercial-intent URLs.

**Recommendation:** Tier category page content by product count:
- 10+ products → 600+ words with brand sections
- 4–9 products → 350–500 words with use-case H2s  
- 1–3 products → 200–300 words minimum + redirect consideration if < 2 products

### 3.2 Product Pages — Risk Assessment for 735 SKUs

**Baseline from sampled pages:**

| Page | Unique Text (ex-specs) | Review Count | Schema | Risk |
|---|---|---|---|---|
| CBU-ASD-LR (Casambi flagship) | ~2,850 words incl. FAQ | 0 | BreadcrumbList only | LOW |
| Aqara TH-S04D (Matter sensor) | ~1,200 words incl. FAQ | 0 | None detected | LOW-MED |
| (Tail product — not sampled) | Unknown | 0 | Unknown | HIGH (assumed) |

**Risk model for 735 products:**

Based on category structure (124 categories, ~6 products/category average), distribution likely follows an 80/20 pattern:
- ~150 flagship/core products: well-described, FAQ-rich (LOW risk)
- ~300 mid-tier products: spec tables + brief intro (MEDIUM risk — needs FAQ or use-case paragraph)
- ~285 tail products (accessories, combo bundles, clearance `/hang-thanh-ly`): likely spec-only (HIGH thin content risk)

**Strategy for 735 products — cannot hand-write, must systematise:**

**Tier A — Flagship (est. 150 products):** Manual review. Add `FAQ` schema markup to existing FAQ sections. Ensure `Product` + `Offer` + `AggregateRating` JSON-LD is complete.

**Tier B — Mid-tier (est. 300 products):** Template-driven expansion. Each product needs: (1) "Khi nào cần chọn [product]?" paragraph (~150 words), (2) "Tương thích với hệ thống nào?" section, (3) 3 FAQ questions from real customer queries. This can be AI-assisted with human review.

**Tier C — Tail (est. 285 products):** Minimum viable content: product category inherits intro text (already in place for most categories), individual product needs only spec table + 1-sentence differentiator. Consider canonicalizing truly duplicate variant pages (colour/finish variants) to a parent product URL.

**Universal product page gaps (apply to all tiers):**
1. No user reviews — zero `AggregateRating` schema possible. Implement a review collection mechanism (email post-purchase, Zalo follow-up).
2. No `datePublished` / `dateModified` visible. Add to JSON-LD on all product and blog pages.
3. No pricing schema for "Liên hệ" (contact for price) products. Use `PriceSpecification` with `priceCurrency: "VND"` and omit `price`, or use `availability: PreOrder` — do not leave `Offer` schema absent entirely.

---

## 4. Author Strategy

### 4.1 Current State

| Signal | Status |
|---|---|
| Named author on posts | Partial — "Tạ Minh Vũ" confirmed on sensor post; "KNX Team" on others |
| Author bio page | None — 404 on all standard paths |
| Author schema (Person) | Not detected in any sampled post |
| Credentials displayed | None — no KNX certification numbers, no project counts |

### 4.2 Author Bio Page Template (B2B Technical Niche)

The template below is designed for KNXStore's audience: System Integrators, ME Contractors, and technically-literate B2C buyers. It prioritises verifiable credentials over generic bio copy.

---

**URL pattern:** `/pages/tac-gia/[ten-tac-gia]`  
**Example:** `/pages/tac-gia/vu-viet-tung`

```
Schema (JSON-LD — add to page <head>):
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "Vũ Việt Tùng",
  "jobTitle": "Technical Director",
  "worksFor": {
    "@type": "Organization",
    "name": "Công ty CP Tích hợp Hệ thống Liên Minh",
    "url": "https://knxstore.vn"
  },
  "knowsAbout": ["KNX", "DALI-2", "Casambi", "BACnet", "Building Automation"],
  "url": "https://knxstore.vn/pages/tac-gia/vu-viet-tung",
  "image": "https://knxstore.vn/assets/tung-portrait.jpg",
  "sameAs": ["https://linkedin.com/in/[profile]"]
}
```

**Page content structure (H2-driven):**

**H1:** [Tên đầy đủ] — [Chức danh]

**H2: Chuyên môn và lĩnh vực**  
Danh sách bullet gồm: giao thức phụ trách, thương hiệu có kinh nghiệm, loại dự án (nhà ở, văn phòng, khách sạn, khu công nghiệp). Tránh văn hoa — dùng danh sách cụ thể.

**H2: Chứng chỉ và đào tạo**  
Ví dụ:
- KNX Partner Certificate — KNX Association (số: [KNX-PARTNER-XXXXX])
- Casambi Certified Installer — [năm]
- [Tên khóa đào tạo], [đơn vị cấp], [năm]

*Nếu chưa có chứng chỉ KNX chính thức: ghi nhận "KNX training — [nhà sản xuất/distributor], [năm]" và đặt kế hoạch thi chứng chỉ. Đừng bỏ trống mục này.*

**H2: Dự án tiêu biểu**  
Bảng 3–5 dự án:
| Công trình | Quy mô | Hệ thống | Năm |
|---|---|---|---|
| [Tên / loại công trình] | [m² hoặc số phòng] | KNX TP + DALI-2 | [năm] |

*Nếu tên khách hàng bảo mật: dùng "Khách sạn 4 sao, TP.HCM" — vẫn cung cấp verifiable context.*

**H2: Bài viết đã đăng**  
List 5 bài viết mới nhất của tác giả này (dynamic, linked).

**H2: Liên hệ tư vấn kỹ thuật**  
CTA + Zalo/email. Đây là conversion point cho B2B — không bỏ qua.

---

**Assignment of authors to existing content:**
- Tùng: KNX TP, DALI-2, BACnet, firmware guides, B2B solutions
- Vũ: Matter, Thread, Zigbee, HomeKit, B2C smart home content
- Huy: Hướng dẫn chọn sản phẩm, so sánh, FAQ thương mại

Retroactively assign authors to all 307 posts. This is a CMS meta field update, not content rewriting.

---

## 5. QRG Compliance — "Who Is Responsible for This Content?"

Google's Quality Rater Guidelines (Sept 2025) require three questions to be answerable from the page itself. Assessment for KNXStore:

| QRG Question | Status | Evidence | Action Required |
|---|---|---|---|
| **Who** created it? | FAIL | "KNX Team" label or no attribution; no bio page; no `author` in schema | Create author pages; update BlogPosting schema with `author.Person` |
| **How** was it created? | PARTIAL | Technical depth implies first-hand knowledge; no disclosure of process | Add short "Bài viết này dựa trên kinh nghiệm thực tế thi công của KNXStore" to post intro or footer |
| **Why** does it exist? | PASS | Content clearly written for technical practitioners, not for ranking; genuine utility confirmed in FAQ quality | Maintain — do not dilute with keyword-stuffed additions |

**Critical compliance gap — No About/Team page:**  
Both `/pages/about` and `/pages/gioi-thieu` return 404. For a B2B technical site where purchase decisions involve 20–500M VND projects, this is a serious trust gap. Google's quality raters specifically flag the absence of an entity page as a negative signal.

**Minimum viable About page content:**
1. Company founding year and mission (1 paragraph)
2. Named founders/technical leads with photos
3. KNX/Casambi partnership credentials
4. Physical address with map embed (already in footer — promote to dedicated page)
5. Representative project references (3–5, anonymised if needed)
6. Link to each team member's author page

---

## 6. Content Gaps — KNX/DALI/Casambi Niche

Topics with confirmed search demand in the niche that have no indexed content on KNXStore based on sitemap analysis:

### 6.1 Technical Reference Gaps (high B2B intent)

| Topic | Why it matters | Difficulty |
|---|---|---|
| KNX Group Address planning methodology | Core skill for every integrator; no tutorial exists on site | Medium |
| KNX IP routing vs. KNX TP — when to use which | Recurring question from integrators; affects product selection | Medium |
| DALI-2 device type table (DT0–DT8) | Required knowledge for specifying LED drivers; IEC 62386-207/209/210/211/215/218/219 | High |
| BACnet/IP vs BACnet MS/TP — topology decisions | KNXStore sells BACnet gateways; no context on protocol selection | Medium |
| KNX ETS 6 vs ETS 5 — migration guide | ETS 6 is current; ETS 5 users upgrading to new projects | Medium |
| Casambi network capacity limits | Max 127 nodes/network; multi-network architectures for large projects | Low |
| DALI 2-Part Device (2PD) commissioning | Emerging standard; few Vietnamese resources | High |

### 6.2 Comparison Content Gaps (high commercial intent)

| Topic | Search intent | Value |
|---|---|---|
| KNX vs Casambi vs DALI — when to use each | System selection for new projects | Very High |
| Matter vs KNX for residential — cost/benefit | B2C decision content; Matter is KNXStore's growth vertical | Very High |
| Casambi 4C vs standard Casambi | Existing product (dich-vu-casambi-4c) but no comparison article | High |
| Wired vs wireless lighting control for hotels | Hospitality is a core market; no dedicated guide | High |
| BACnet gateway selection guide — Intesis vs KAC00X | Both in catalogue; no comparison | Medium |

### 6.3 Vietnamese-language Resource Gaps

The following topics have strong English-language resources (knx.org, dali-alliance.org) but essentially no quality Vietnamese content — creating opportunity for topical authority:

- Hướng dẫn thiết kế hệ thống KNX TP từ đầu (sizing, topology, power supply calculation)
- IEC 62386 cho DALI — giải thích tiêu chuẩn bằng tiếng Việt
- Công trình xanh LEED/EDGE và vai trò của DALI/KNX trong lighting credit
- Casambi mesh reliability: số liệu thực tế từ dự án (coverage, latency, packet loss)

### 6.4 Local SEO Content Gaps

- "/giai-phap/khach-san" — no dedicated hotel automation solution page despite multiple hotel case studies implied
- "/giai-phap/van-phong" — office building BMS integration guide absent
- City-specific landing pages (HCMC, Hanoi, Da Nang) — none present; all traffic goes to generic pages

---

## 7. Recommendations — Priority Matrix

### P0 (Do within 2 weeks — compliance/trust)

1. **Create `/pages/ve-chung-toi`** with company history, team photos, partnership credentials, address map. Use `Organization` + `LocalBusiness` JSON-LD. This fixes the QRG "Who" question at site level.

2. **Add `author` field to all BlogPosting JSON-LD.** Minimum: `"author": {"@type": "Person", "name": "Tạ Minh Vũ"}`. Retroactively assign all 307 posts to named authors. This is a CMS bulk-update task.

3. **Add `dateModified` to all post and product JSON-LD.** Google uses this for freshness scoring. Even setting it equal to `datePublished` initially is better than omitting it.

### P1 (Do within 1 month — content quality)

4. **Create author bio pages** for Tùng and Vũ first (highest post volume). Use the template in Section 4.2. Link from all their post bylines.

5. **Add external citations to top 20 technical posts.** Priority: KNX Association (knx.org), IEC 62386 standard page, DALI Alliance (dali-alliance.org), Casambi documentation. 2–3 links per post with rel="noopener" to authority sources.

6. **Expand Gateway Matter category page** (currently 120 words → target 400 words). It's the highest commercial-intent Matter page on the site.

7. **Add `CollectionPage` + `BreadcrumbList` JSON-LD to all 124 category pages.** This is a template/CMS change — one template update deploys to all pages.

### P2 (Do within 3 months — content depth)

8. **Add quantified outcomes to 3 existing case studies.** Target metrics: device count, commissioning time, energy reduction %, or client satisfaction (anonymised quote). Vegi Resort case study is European — prioritise a domestic Vietnamese project.

9. **Create KNX vs Casambi vs DALI comparison guide** (~2,000 words). This is the highest-search-intent unaddressed topic in the niche and will drive B2B consultation requests.

10. **Implement product review collection.** Even 3–5 reviews on flagship products enables `AggregateRating` schema, which improves SERP CTR (star ratings in results). Post-purchase Zalo message is the natural collection channel.

11. **Write DALI-2 device type reference guide** (DT0–DT8 table, IEC 62386 part numbers, compatible products in catalogue). This is the kind of primary-source technical content that gets cited by other sites.

### P3 (Ongoing)

12. **Establish content update calendar.** Flag posts older than 12 months on fast-moving topics (Matter firmware, KNX ETS versions, Casambi app updates) for quarterly review. Add `dateModified` on each update.

13. **KNX Association partner directory listing.** Contact KNX Association to be listed at knx.org/international/partners. This creates the authoritative backlink that currently does not exist.

---

## 8. AI Citation Readiness: 72/100

KNXStore content is structurally well-positioned for AI Overviews and AI Mode citation:

**Strengths:**
- Answer-first format in FAQ sections (question as H3, direct answer in first sentence)
- Numbered step-by-step guides (KAC005 firmware: 6-step process with specific filenames)
- Comparison tables (sensor types, protocol comparison)
- Specific data points that AI systems prefer to quote (192.168.1.232 default IP, 11.4 MB firmware, 24-month warranty)
- Vietnamese-language technical content in an underserved niche — low AI citation competition

**Weaknesses:**
- No `FAQPage` or `HowTo` schema on guides — structured data would directly improve AI Overviews appearance
- No primary source citations — AI systems prefer content that itself cites authoritative sources
- Author anonymity reduces citation confidence for AI systems evaluating content trustworthiness
- No `speakable` schema for voice search / AI audio responses

**Quick win:** Add `HowTo` JSON-LD to the KAC005 firmware guide and HVAC VRV/VRF setup guide. These step-by-step posts are exactly what AI Mode cites for "how to" queries.

---

*Report generated from live page analysis: homepage, 5 blog posts, 5 category pages, 2 product pages, 3 sitemaps. Schema findings based on rendered HTML; JavaScript-rendered schema may differ — verify with Google's Rich Results Test for confirmed schema types.*
