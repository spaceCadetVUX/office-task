# Schema.org Audit Report — knxstore.vn

**Date:** 2026-06-01
**Site:** https://knxstore.vn
**Scope:** Homepage, Product pages, Blog posts, Category pages
**Standard:** schema.org + Google Rich Results guidelines (as of Feb 2026)

---

## 1. Validation Summary

| Page Type | Schema Types Detected | Status | Critical Issues |
|-----------|----------------------|--------|-----------------|
| Homepage | Organization, LocalBusiness, WebSite, BreadcrumbList, WebPage, ImageObject, FAQPage | ⚠️ Partial | FAQPage restricted; missing `sameAs`, `openingHours` |
| Product pages | Product, Offer, ShippingDeliveryTime, MerchantReturnPolicy, PropertyValue, OfferShippingDetails, QuantitativeValue | ⚠️ Partial | Missing `AggregateRating` opportunity |
| Blog posts | BlogPosting, BreadcrumbList, ImageObject, WebPage | ✅ Good | No critical issues |
| Category pages | — | ❌ Missing | No schema at all — highest priority gap |

---

## 2. Issue Details

### 2.1 Homepage — Organization

| Property | Status | Detail |
|----------|--------|--------|
| `@type` | ✅ | Organization + LocalBusiness (dual-type acceptable) |
| `name` | ✅ | Present |
| `url` | ✅ | Present |
| `logo` | ✅ | Present |
| `address` (PostalAddress) | ✅ | Present |
| `geo` (GeoCoordinates) | ✅ | Present |
| `contactPoint` | ✅ | Present |
| `sameAs` | ❌ Missing | No social profiles linked — Google uses `sameAs` for Knowledge Panel entity disambiguation |
| `openingHours` | ❌ Missing | Required for LocalBusiness rich results; without it Google cannot display hours |
| `legalName` | ⚠️ Check | Confirm value matches business registration exactly |
| `priceRange` | ⚠️ Optional | Recommend adding for LocalBusiness (`"priceRange": "$$"`) |

**Risk:** Without `sameAs`, Google Knowledge Panel will not reliably surface the correct entity for branded searches.

---

### 2.2 Homepage — FAQPage

**Verdict: REMOVE from production (non-compliant for commercial sites)**

Google restricted FAQPage rich results in August 2023 to **government and healthcare authority sites only**. A B2B/B2C distributor does not qualify. Keeping this markup:
- Will not generate rich results
- Creates noise in Google Search Console (no errors, but zero SERP benefit)
- May trigger a manual quality flag for schema misuse over time

**Exception — AI citation value:** FAQPage markup is parsed by LLM-based AI systems (Perplexity, ChatGPT Browse, Gemini) for structured Q&A extraction. If the 11 Q&A blocks contain genuinely informative KNX/DALI-2/Casambi technical content (not marketing copy), retention solely for AI citability is defensible. Evaluate per-question quality before removing.

**Recommendation:** Audit the 11 Q&A entries. Keep if ≥7 are substantive technical FAQs. Remove if primarily sales/promotional content.

---

### 2.3 Product Pages — AggregateRating

**Verdict: DO NOT ADD until a live review system is in place**

Adding `AggregateRating` without a functioning review collection and display system is a **Google policy violation** (rating data must be directly accessible on-page to users). This results in a manual action penalty.

**Precondition checklist before adding:**
- [ ] Review submission form live on product pages
- [ ] Individual reviews displayed to users (not just aggregate)
- [ ] `reviewCount` reflects real submitted reviews (not imported/fake)
- [ ] Reviews are **not** filtered/gated behind login

Do not add placeholder `"ratingValue": "5.0", "reviewCount": "1"` — this is a known penalty trigger.

---

### 2.4 Category Pages — CollectionPage / ItemList

**Verdict: HIGHEST PRIORITY — add immediately**

Category pages (e.g., `/casambi-gateway`, `/dali-gateway`, `/bo-dieu-khien-knx-gateway`) have zero schema markup. These pages aggregate products for technical B2B buyers who search brand/protocol terms. A `CollectionPage` + `ItemList` block:
- Enables breadcrumb rich results in SERPs
- Signals product inventory depth to Google's product understanding system
- Improves AI overview citations for "best KNX gateway Vietnam" type queries

---

### 2.5 Blog Posts — BlogPosting

| Property | Status | Detail |
|----------|--------|--------|
| `headline` | ✅ | Present |
| `datePublished` | ✅ | Present |
| `dateModified` | ✅ | Present |
| `author` | ⚠️ Check | Verify `author.@type` is `Person` (not `Organization`) and `author.url` links to an author bio page |
| `publisher` | ✅ | Present |
| `image` | ✅ | Present |
| `BreadcrumbList` | ✅ | Present |
| Person schema on author bio pages | ❌ Missing | If author bio pages exist, they need `Person` schema |

---

## 3. Priority Action Plan

| Priority | Action | Impact | Effort |
|----------|--------|--------|--------|
| P1 | Add `CollectionPage` + `ItemList` to all category pages | High — fills largest schema gap | Medium |
| P2 | Add `sameAs` array to Organization (social profiles) | High — entity disambiguation | Low |
| P3 | Add `openingHours` to LocalBusiness | Medium — rich result eligibility | Low |
| P4 | Audit FAQPage Q&A quality, decide keep/remove | Medium — compliance + AI citation | Low |
| P5 | Add `Person` schema to author bio pages | Low–Medium — E-E-A-T signals | Low |
| P6 | Add `AggregateRating` — only after review system live | High long-term | High (infra) |

---

## 4. Generated Schema

See `generated-schema.json` for ready-to-use JSON-LD blocks. The file contains:

1. `organization_updated` — Organization + LocalBusiness with `sameAs` and `openingHours`
2. `category_page_template` — CollectionPage + ItemList + BreadcrumbList (parameterized)
3. `person_author_template` — Person schema for author bio pages
4. `category_examples` — 3 concrete examples for the sample URLs provided

---

## 5. Implementation Notes

### JSON-LD placement
- All schema blocks must be in `<script type="application/ld+json">` in `<head>` or early `<body>`
- Per Google December 2025 guidance: do **not** inject via JavaScript only — include in server-rendered HTML, especially for `Product` and `Offer` types

### Validation tools
1. [Google Rich Results Test](https://search.google.com/test/rich-results) — official validator
2. [Schema.org Validator](https://validator.schema.org/) — spec compliance
3. Google Search Console → Enhancements → check for errors after deployment

### Locale
All schema uses `"inLanguage": "vi"` and `"addressCountry": "VN"` to match `vi_VN` locale.
