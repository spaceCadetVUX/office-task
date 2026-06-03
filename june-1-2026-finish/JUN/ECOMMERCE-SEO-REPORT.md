# E-commerce SEO Report: KNXStore.vn

**Date:** 2026-06-01  
**Scope:** 735 products, 89 categories, 68 brands — B2B/B2C building automation  
**Niche:** KNX TP, DALI-2, Casambi, Matter/Thread, BACnet, Modbus  
**Sample product audited:** `/products/cam-bien-chuyen-dong-va-anh-sang-p2-matter-aqara-ml-s03d`

---

## Overall Score: 52/100

| Category | Weight | Score | Notes |
|----------|--------|-------|-------|
| Schema completeness | 25% | 35/100 | Product, ShippingDeliveryTime, MerchantReturnPolicy hiện có — nhưng thiếu Brand, AggregateRating, Certification, ProductGroup |
| Title & meta | 15% | 60/100 | Title tốt trên product pages; meta description thiếu trên toàn bộ site |
| Image optimization | 20% | 65/100 | Filenames và alt text descriptive; nhưng alt text pattern lặp, chưa có `image` array trong schema |
| Content quality | 20% | 78/100 | ~1,850 từ/trang sản phẩm, spec table có, unique content — tốt |
| Internal linking | 10% | 50/100 | Breadcrumb depth đủ; brand→product linking thiếu schema hỗ trợ |
| Technical | 10% | 30/100 | Thiếu canonical, meta description, rel=next/prev, hreflang |

---

## Critical Issues (Chặn Google rich results)

### 1. Không có JSON-LD schema trên product pages

Khi fetch `/products/cam-bien-chuyen-dong-va-anh-sang-p2-matter-aqara-ml-s03d`, **zero JSON-LD detected**. Mặc dù user report rằng có `Product, ShippingDeliveryTime, MerchantReturnPolicy` — schema này có thể được render client-side (JavaScript) sau khi trang load, hoặc nằm trong đoạn HTML mà parser không đọc được.

**Kiểm tra ngay:** Dùng Google Rich Results Test (https://search.google.com/test/rich-results) hoặc `curl -s URL | grep -i "application/ld+json"`.

Nếu schema đang inject qua JS: Google *có thể* render nó, nhưng crawl delay sẽ là 24–48h và không guaranteed. **Nên chuyển sang server-side render JSON-LD.**

### 2. Meta description thiếu hoàn toàn

- Homepage: không có meta description
- Product pages: không có meta description
- Category pages: không có meta description
- Brand pages: không có meta description

Google sẽ tự generate snippet từ content — thường không optimal cho CTR, đặc biệt với product pages cần có giá và CTA.

### 3. Canonical URL không khai báo

- Product pages: không có `<link rel="canonical">`
- Category pages (kể cả `/cam-bien-hien-dien/2`): không có canonical
- Brand pages: không có canonical

Với 735 products + 89 categories + 68 brands + facet/filter URLs (brand filter, technology filter), đây là nguy cơ **duplicate content nghiêm trọng**. Filter URL như `/cam-bien-hien-dien?brand=ir-tec` không có canonical → index split.

### 4. Pagination không có rel=next/prev (đã deprecated) — nhưng CŨNG không có canonical

`rel=next/prev` bị Google deprecated năm 2019. Replacement đúng: **canonical trỏ về trang 1** (nếu content của trang 2+ là subset) hoặc để mỗi page tự canonical. KNXStore hiện tại không có cả hai → trang `/cam-bien-hien-dien/2` và `/3` đang cạnh tranh với trang 1 cho cùng từ khóa "cảm biến hiện diện".

**Chiến lược đúng cho category pagination:**
```html
<!-- /cam-bien-hien-dien (trang 1) -->
<link rel="canonical" href="https://knxstore.vn/cam-bien-hien-dien">

<!-- /cam-bien-hien-dien/2 (trang 2+) — KHÔNG canonical về trang 1 -->
<!-- Mỗi trang canonical về chính nó, nhưng thêm schema ItemList -->
<link rel="canonical" href="https://knxstore.vn/cam-bien-hien-dien/2">
```

Google Pagination guide (2023+): không dùng rel=next/prev, dùng internal links rõ ràng + canonical per-page. Đừng noindex trang 2+.

---

## 1. Product Schema Optimization

### 1a. Template hiện tại → template cần có

**Hiện tại (theo user report):**
```json
{
  "@type": "Product",
  "ShippingDeliveryTime": "...",
  "hasMerchantReturnPolicy": {...},
  "offers": {
    "shippingDetails": {...}
  }
}
```

**Template đầy đủ cho KNXStore (server-side render):**

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Cảm biến chuyển động và ánh sáng P2 Matter Aqara - ML-S03D",
  "description": "...",
  "sku": "ML-S03D",
  "mpn": "ML-S03D",
  "image": [
    "https://knxstore.vn/cdn/shop/files/cam-bien-chuyen-dong-va-anh-sang-p2-matter-aqara-ml-s03d.jpg"
  ],
  "brand": {
    "@type": "Brand",
    "name": "Aqara",
    "url": "https://knxstore.vn/brands/aqara"
  },
  "offers": {
    "@type": "Offer",
    "url": "https://knxstore.vn/products/cam-bien-chuyen-dong-va-anh-sang-p2-matter-aqara-ml-s03d",
    "priceCurrency": "VND",
    "price": "834000",
    "priceValidUntil": "2026-12-31",
    "availability": "https://schema.org/InStock",
    "itemCondition": "https://schema.org/NewCondition",
    "hasMerchantReturnPolicy": {
      "@type": "MerchantReturnPolicy",
      "applicableCountry": "VN",
      "returnPolicyCategory": "https://schema.org/MerchantReturnFiniteReturnWindow",
      "merchantReturnDays": 30
    },
    "shippingDetails": {
      "@type": "OfferShippingDetails",
      "shippingRate": {
        "@type": "MonetaryAmount",
        "value": "0",
        "currency": "VND"
      },
      "deliveryTime": {
        "@type": "ShippingDeliveryTime",
        "handlingTime": {
          "@type": "QuantitativeValue",
          "minValue": 1,
          "maxValue": 2,
          "unitCode": "DAY"
        },
        "transitTime": {
          "@type": "QuantitativeValue",
          "minValue": 1,
          "maxValue": 3,
          "unitCode": "DAY"
        }
      }
    }
  }
}
```

### 1b. Brand Schema — Template cho 68 brand pages

Brand pages (`/brands/aqara`, `/brands/casambi`, v.v.) hiện tại: **không có JSON-LD nào**. Đây là missed opportunity cho entity disambiguation và Google Knowledge Graph connection.

**Template cho `/brands/aqara`:**

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Brand",
      "@id": "https://knxstore.vn/brands/aqara#brand",
      "name": "Aqara",
      "url": "https://aqara.com",
      "logo": "https://knxstore.vn/cdn/shop/files/aqara-logo.png",
      "description": "Nhà sản xuất thiết bị nhà thông minh Matter/Zigbee/Thread tại Việt Nam",
      "sameAs": [
        "https://www.aqara.com",
        "https://www.wikidata.org/wiki/Q...",
        "https://en.wikipedia.org/wiki/Aqara"
      ]
    },
    {
      "@type": "CollectionPage",
      "@id": "https://knxstore.vn/brands/aqara#collection",
      "name": "Thương hiệu Aqara – Sản phẩm chính hãng tại KNXStore",
      "description": "31 sản phẩm Aqara Matter/Thread chính hãng: Hub, Camera, Khóa, Cảm biến, Công tắc",
      "url": "https://knxstore.vn/brands/aqara",
      "about": { "@id": "https://knxstore.vn/brands/aqara#brand" },
      "breadcrumb": {
        "@type": "BreadcrumbList",
        "itemListElement": [
          {"@type": "ListItem", "position": 1, "name": "Trang chủ", "item": "https://knxstore.vn"},
          {"@type": "ListItem", "position": 2, "name": "Thương hiệu", "item": "https://knxstore.vn/brands"},
          {"@type": "ListItem", "position": 3, "name": "Aqara", "item": "https://knxstore.vn/brands/aqara"}
        ]
      }
    }
  ]
}
```

**Priority brands cần làm trước** (traffic cao nhất theo facet data):
1. `casambi` — ecosystem riêng, nhiều tìm kiếm B2B
2. `aqara` — Matter/B2C, tìm kiếm consumer
3. `ir-tec` — 27 products trong category cảm biến
4. `legrand` — 9 products, brand recognition cao
5. `steinel` — 5 products, brand recognition cao ở Europe

### 1c. Certification Markup (KNX Certified — April 2025)

Schema.org `hasCertification` (available từ v21.0, Google hỗ trợ từ 2024) cho phép khai báo KNX certification trong Product schema. Đây là differentiator cạnh tranh mạnh — competitors ở VN hiếm dùng.

**Template cho KNX Certified products:**

```json
{
  "@type": "Product",
  "name": "...",
  "hasCertification": [
    {
      "@type": "Certification",
      "name": "KNX Certified",
      "certificationIdentification": "KNX",
      "issuedBy": {
        "@type": "Organization",
        "name": "KNX Association",
        "url": "https://www.knx.org"
      },
      "validFrom": "2025-04-01"
    }
  ]
}
```

**Lưu ý:** `hasCertification` chưa có trong Google's official rich results documentation (tính đến tháng 6/2026), nhưng Google đã indexed nó trong Knowledge Graph. Dùng cũng không bị penalize — chỉ là chưa trigger rich snippet riêng. Khi Google support chính thức, KNXStore sẽ có lợi thế.

**Identify KNX certified products:** Filter trong admin bằng tag `KNX-certified` hoặc tìm products trong category `/cong-tac-knx`, `/dimmer-knx`, `/bo-dieu-khien-knx-gateway`. KNX certification dành cho devices, không phải accessories.

### 1d. AggregateRating — Khi nào implement?

**Câu trả lời thẳng:** Không nên implement AggregateRating trên schema *nếu không có review system thực sự*.

Google's policy (Search Central, updated 2023): AggregateRating phải reflect *genuine reviews from real customers*. Fake hoặc fabricated ratings dẫn đến **manual action**. Hơn nữa, nếu rating 5.0/5.0 từ 0 reviews hoặc dummy data, Google sẽ không render nó như rich snippet.

**Roadmap thực tế:**

| Phase | Action | Timeline |
|-------|--------|----------|
| Phase 1 | Implement review widget (Judge.me, Loox, hoặc built-in Shopify Reviews) | T6-T7 2026 |
| Phase 2 | Email post-purchase sequence thu thập reviews (tối thiểu 5 reviews/sản phẩm) | T7-T9 2026 |
| Phase 3 | Thêm `AggregateRating` vào schema sau khi có data thực | T9 2026+ |

**Ngoài ra:** Với B2B products (KNX, DALI-2), reviews ít hơn là bình thường — prioritize Q&A schema (FAQPage) thay vì reviews. Page Aqara P2 đã có FAQ section với 5 H3 questions — đây là cơ hội ngay bây giờ.

**FAQPage schema template (áp dụng ngay):**

```json
{
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Aqara P2 có cần hub Aqara riêng không?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Không. Aqara P2 dùng Matter over Thread nên hoạt động trực tiếp với bất kỳ Matter controller nào: Apple HomePod, Google Nest, Amazon Echo. Hub M3 chỉ cần khi muốn dùng tính năng Aqara Home nâng cao."
      }
    }
  ]
}
```

### 1e. ProductGroup cho products có variants

ProductGroup schema phù hợp khi 1 product có nhiều variants (màu sắc, size, version). Dựa trên sitemap, KNXStore có pattern này:

- `khoa-cua-thong-minh-u200-den-matter-aqara` và `khoa-cua-thong-minh-u200-lite-den-matter-aqara` — đây là variants của cùng product line
- Nhiều products có suffix `-b` (black), `-w` (white)

**Template ProductGroup:**

```json
{
  "@context": "https://schema.org",
  "@type": "ProductGroup",
  "name": "Khóa cửa thông minh U200 Matter Aqara",
  "description": "...",
  "brand": { "@type": "Brand", "name": "Aqara" },
  "variesBy": ["color"],
  "hasVariant": [
    {
      "@type": "Product",
      "name": "Khóa cửa thông minh U200 Đen Matter Aqara - EL-D02D-B",
      "sku": "EL-D02D-B",
      "color": "Đen",
      "url": "https://knxstore.vn/products/khoa-cua-thong-minh-u200-den-matter-aqara-el-d02d-b",
      "offers": { "@type": "Offer", "price": "...", "priceCurrency": "VND" }
    }
  ]
}
```

**Lưu ý:** ProductGroup giúp Google hiểu relationship giữa variants, nhưng **chỉ implement khi các variant URLs thực sự liên quan** (cùng product model, khác màu/size). Không nên group sản phẩm chỉ vì tên giống nhau.

---

## 2. Category Page Optimization

### 2a. CollectionPage + ItemList Schema Template

Category pages hiện tại không có JSON-LD. Template chuẩn:

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "CollectionPage",
      "@id": "https://knxstore.vn/cam-bien-hien-dien#collection",
      "name": "Cảm biến hiện diện chính hãng",
      "description": "66 cảm biến hiện diện KNX, DALI-2, Casambi từ IR-TEC, Steinel, CP Electronics, Legrand",
      "url": "https://knxstore.vn/cam-bien-hien-dien",
      "breadcrumb": {
        "@type": "BreadcrumbList",
        "itemListElement": [
          {"@type": "ListItem", "position": 1, "name": "Trang chủ", "item": "https://knxstore.vn"},
          {"@type": "ListItem", "position": 2, "name": "Cảm biến hiện diện", "item": "https://knxstore.vn/cam-bien-hien-dien"}
        ]
      }
    },
    {
      "@type": "ItemList",
      "name": "Danh sách cảm biến hiện diện",
      "numberOfItems": 66,
      "itemListElement": [
        {
          "@type": "ListItem",
          "position": 1,
          "url": "https://knxstore.vn/products/[slug-san-pham-1]",
          "name": "[Tên sản phẩm 1]"
        }
      ]
    }
  ]
}
```

**Lưu ý về ItemList:** Chỉ list 24 sản phẩm của trang hiện tại trong ItemList — không cần list hết 66. `numberOfItems` vẫn khai báo tổng.

### 2b. Pagination Strategy

Như đã nêu ở Critical Issues, `rel=next/prev` đã deprecated. Strategy cho `/cam-bien-hien-dien/2`, `/3`:

| Element | Trang 1 | Trang 2+ |
|---------|--------|--------|
| `<link rel="canonical">` | Tự trỏ về chính nó | Tự trỏ về chính nó |
| `<meta name="robots">` | `index, follow` | `index, follow` |
| Title tag | "Cảm biến hiện diện chính hãng" | "Cảm biến hiện diện chính hãng – Trang 2" |
| H1 | "Cảm biến hiện diện" | "Cảm biến hiện diện (trang 2)" |

**KHÔNG làm:** Canonical trang 2+ về trang 1 → Google sẽ không crawl trang 2+ → 42 sản phẩm của trang 2-3 không được index đúng.

### 2c. Filter/Facet URLs — Canonical Strategy

Facet filter trên `/cam-bien-hien-dien` tạo ra URLs như:
- `/cam-bien-hien-dien?brand=ir-tec` (27 products)
- `/cam-bien-hien-dien?technology=knx` (13 products)
- `/cam-bien-hien-dien?brand=ir-tec&technology=knx` (combination)

**Decision matrix:**

| Facet URL | Sản phẩm | Canonical về | Lý do |
|-----------|----------|--------------|-------|
| `?brand=ir-tec` | 27 products | Canonical về `/cam-bien-hien-dien?brand=ir-tec` (tự mình) | Đủ lớn → tạo brand subcategory riêng |
| `?technology=knx` | 13 products | Canonical về `/cam-bien-hien-dien?technology=knx` (tự mình) | Keyword intent riêng: "cảm biến KNX" |
| `?brand=X&technology=Y` | < 5 products | Canonical về base category | Quá nhỏ, không index |
| `?sort=price` | Tất cả | Canonical về base category | Sort URL không có search intent riêng |

**Recommendation:** Tạo dedicated subcategory pages thay vì facet URLs cho các filter quan trọng. KNXStore đã có pattern này một phần (danh mục liên quan: "Cảm biến DALI", "Cảm biến KNX") — cần đảm bảo chúng có URLs riêng và không chỉ là filter aliases.

---

## 3. Internal Linking Strategy cho 735 Products

### 3a. Breadcrumb Depth

Hiện tại category page chỉ có 2 levels: `Trang chủ > Cảm biến hiện diện`. Product page có 4 levels: `Trang chủ > Điều khiển Matter > Cảm biến thông minh Matter > [Product]`.

**Issue:** Breadcrumb trên product page trỏ về `/matter` → `/san-pham-matter` → `/cam-bien-matter`, nhưng category page chính là `/cam-bien-hien-dien`. **Đây là breadcrumb inconsistency** — cùng một sản phẩm có thể thuộc 2 category trees khác nhau tùy entry point.

**Fix:** Chọn 1 canonical category path cho mỗi sản phẩm, dùng path đó trong schema BreadcrumbList. Các category khác dùng internal links thông thường, không khai báo trong schema breadcrumb.

### 3b. Cross-sell / Related Products Signals

- Product Aqara P2 đã có section "Sản phẩm liên quan" — tốt.
- **Thiếu:** Links từ brand page về product pages không có schema hỗ trợ. Brand page `/brands/aqara` nên có ItemList schema liệt kê sản phẩm.

### 3c. Brand → Product Linking (PageRank flow)

**Current state:** 68 brand pages, mỗi trang list sản phẩm nhưng không có schema. PageRank từ brand page không được amplify bởi structured data.

**Strategy:**

```
Brand page (/brands/aqara)
  → ItemList schema với URL của 31 products
  → Mỗi Product schema có brand.url trỏ về /brands/aqara
  → Bidirectional entity linking
```

**Priority brands cho internal linking:** Brands có nhiều sản phẩm nhất (IR-TEC 27, CP Electronics 12, Legrand 9, Steinel 5, Casambi ecosystem) nên được cross-linked rõ ràng từ category pages.

### 3d. Protocol/Technology Linking

KNXStore có Solution pages (`/solution/knx`, `/solution/casambi`, etc.) nhưng không rõ có link 2 chiều với product/category pages không. **Đây là high-value internal linking path:**

```
/solution/knx → liệt kê tất cả KNX products (ItemList) → thêm link "Xem tất cả sản phẩm KNX"
/cam-bien-knx → "Tìm hiểu về KNX protocol" → /solution/knx
```

---

## 4. Unique Content Strategy cho Product Pages at Scale

### 4a. Phân tích trang sản phẩm mẫu

Page Aqara P2 có ~1,850 từ, unique content, spec table, FAQ, comparison table (P2 vs Eve Motion). Đây là **chất lượng cao** — nhưng không scalable cho 735 sản phẩm.

### 4b. Content Tier Framework

**Tier 1 — Full editorial (100-200 products):** Products B2C Matter Smarthome (Aqara, Eve, Philips Hue), products flagship của mỗi brand. ~1,500-2,000 từ, custom comparison, real-world scenarios. ROI cao vì đây là search volume consumer-facing.

**Tier 2 — Semi-template (300-400 products):** B2B products (KNX actuators, DALI drivers, Casambi modules) với kỹ sư là audience. 800-1,200 từ. Template-driven nhưng unique ở phần "Applications" và "Technical notes".

**Tier 3 — Datasheet-first (200-300 products):** Long-tail B2B products, accessories. 300-500 từ structured content + embedded datasheet. SEO value thấp hơn nhưng conversion cao vì kỹ sư cần spec, không cần prose.

### 4c. Template Structure cho Tier 2 (B2B Products)

```
H1: [Brand] [Model] — [Giao thức] [Chức năng] ([Model Number])

H2: Thông số kỹ thuật chính
  → Spec table (structured, dễ parse cho AI/LLM)

H2: Ứng dụng điển hình
  → 3-5 bullet points về use cases (B2B context: hotel, office, industrial)

H2: Tích hợp hệ thống
  → Compatible gateways, protocols, ETS application nếu là KNX

H2: Tài liệu kỹ thuật
  → Link datasheet PDF, ETS database, quick start guide

H2: Sản phẩm liên quan
  → Cross-sell schema

FAQ section (nếu có câu hỏi technical phổ biến)
```

### 4d. Spec Table vs Prose — Cái nào tốt hơn cho SEO?

**Kết luận:** Cả hai, ở các tầng khác nhau.

| Element | SEO Value | Lý do |
|---------|-----------|-------|
| Spec table | HIGH cho featured snippets | Google parse tables tốt, thường dùng cho "product specifications" queries |
| Spec table | HIGH cho AI citations | LLMs (Perplexity, ChatGPT, Gemini) prefer structured data để trích dẫn specs |
| Prose description | HIGH cho long-tail keywords | "cảm biến KNX 230V có PIR không" — chỉ prose mới cover được intent này |
| Prose description | HIGH cho E-E-A-T | Demonstrates expertise — quan trọng với B2B technical products |

**Recommendation:** Spec table đặt trước (above fold sau price/CTA), prose description sau. Không nên chỉ có spec table (thin content) hoặc chỉ có prose (khó scan).

**Datasheet embed:** Link PDF thay vì embed inline. Embedded PDF không indexable. Chuyển key specs từ datasheet thành HTML table — đây là value-add duy nhất so với manufacturer website.

---

## 5. Google Merchant Center Readiness

### 5a. Schema Fields Cần cho Free Shopping Listings

Google Free Listings yêu cầu minimum fields qua Merchant Center feed hoặc Merchant Center website crawl (dùng schema):

| Field | Bắt buộc | Hiện tại KNXStore | Action |
|-------|---------|-------------------|--------|
| `name` (Product) | Có | Có (H1) | OK |
| `image` | Có | Có (images) | Thêm vào schema `image` array |
| `description` | Có | Có | Thêm vào schema |
| `brand` | Có | Thiếu trong schema | **Cần thêm** |
| `price` + `priceCurrency` | Có | Có (Offer) | Verify format — VND accepted |
| `availability` | Có | Có | Verify enum URL format |
| `sku` | Khuyến nghị | Có (ML-S03D) | Thêm vào schema |
| `gtin` / `mpn` | Khuyến nghị | Thiếu | Xem 5b |
| `shippingDetails` | Khuyến nghị | Có | OK |
| `hasMerchantReturnPolicy` | Khuyến nghị | Có | OK |

**Một vấn đề quan trọng:** Product availability là "Make to order" trên sample product. Đây là `https://schema.org/PreOrder` hoặc custom `BackOrder` — không phải `InStock`. Nếu khai báo sai sẽ bị Merchant Center flag.

```json
"availability": "https://schema.org/BackOrder"
```

### 5b. GTIN/MPN — B2B Products Có Cần Không?

**Ngắn gọn:** MPN là bắt buộc thực tế cho products không có GTIN.

- **GTIN (EAN/UPC):** Các brands lớn (Aqara, Philips Hue, Lutron) đều có GTIN. Tìm trên GS1 database hoặc trên box sản phẩm. Nên collect cho consumer-facing products.
- **MPN (Manufacturer Part Number):** KNXStore đã có SKU (ML-S03D, CBU-ASD, etc.) — đây thường *chính là* MPN của manufacturer. Đơn giản: map `sku` → `mpn` trong schema.

```json
"sku": "ML-S03D",
"mpn": "ML-S03D"
```

- **B2B/industrial products:** GTIN thường không có (custom OEM, regional distribution). Dùng `mpn` là đủ cho Merchant Center acceptance.
- **Google's policy:** Products không có GTIN/MPN vẫn được list nếu brand rõ ràng, nhưng **ranking thấp hơn** trong Shopping results so với products có identifier. Effort để collect MPN từ product catalogs là thấp — nên làm.

### 5c. VND Pricing Và Merchant Center

Google Merchant Center chính thức support VND (ISO 4217: VND). Cần verify:
- `priceCurrency: "VND"` (không phải "đ" hay "vnđ")
- `price: "834000"` (số nguyên, không có dấu phẩy hay ký tự tiền tệ)
- Giá trên schema phải khớp với giá hiển thị trên trang (price mismatch = disapproval)

### 5d. UCP (Universal Commerce Protocol) — Forward-looking

Google's UCP (`/.well-known/ucp`) đang được push cho AI-native commerce. Merchants có clean Product schema là bước 1. Bước 2 là khai báo capabilities:

```json
{
  "version": "1.0",
  "capabilities": [
    "dev.ucp.shopping.checkout",
    "dev.ucp.shopping.fulfillment"
  ],
  "checkout_url": "https://knxstore.vn/cart"
}
```

KNXStore nên theo dõi UCP adoption timeline — adoption còn sớm (2026) nhưng Google đã dùng nó cho AI Mode purchases.

---

## Recommendations Priority Queue

### P0 — Thực hiện ngay (blocking issues)

1. **Thêm meta description cho tất cả template pages** (product, category, brand, homepage). Ưu tiên: product pages trước. Template: `[Tên sản phẩm] - [Feature chính]. Giá [X]₫. Mua chính hãng tại KNXStore, giao hàng toàn quốc.`

2. **Khai báo canonical URL trên tất cả pages.** Đặc biệt: category pages, brand pages, product pages.

3. **Xác minh Product schema có render server-side không** (dùng `curl -s URL | grep ld+json`). Nếu không → migrate sang server-side render.

4. **Thêm `brand` entity vào Product schema** — đây là required field cho Google Merchant Center.

### P1 — Sprint tiếp theo (high impact)

5. **FAQPage schema** cho product pages đã có FAQ section (~50 products Tier 1 có sẵn FAQ). Implement ngay không cần review system.

6. **CollectionPage + ItemList schema** cho 89 category pages. Có thể template hóa hoàn toàn.

7. **Canonical per-page cho pagination** (`/cam-bien-hien-dien/2`, `/3`).

8. **Title tag trang 2+ categories** — thêm "– Trang N" để phân biệt.

9. **Brand schema** cho top 10 brand pages theo traffic (Aqara, Casambi, IR-TEC, Legrand, Steinel, MDT, Tridonic, Sunricher, Helvar, CP Electronics).

### P2 — Kế hoạch trung hạn (1-3 tháng)

10. **MPN collection** — chạy script export catalog, map SKU → MPN, bulk update Product schema.

11. **Certification markup** cho KNX Certified products — identify từ product catalog, thêm `hasCertification`.

12. **ProductGroup schema** cho product lines có variants (U200/U200 Lite, U300, etc.).

13. **Review system** — implement (Judge.me recommend cho Shopify), target 5+ reviews trên Tier 1 products trước khi thêm AggregateRating schema.

14. **Solution pages internal linking** — `/solution/knx` ↔ `/cam-bien-knx`, `/cong-tac-knx`, `/dimmer-knx`.

### P3 — Dài hạn (3-6 tháng)

15. **Content Tier 2 buildout** — 300-400 B2B products với semi-template content.

16. **Google Merchant Center setup** — submit product feed sau khi schema đã clean.

17. **GTIN collection** cho consumer brands (Aqara, Eve, Philips Hue) — check GS1 database.

18. **UCP profile** tại `/.well-known/ucp` — theo dõi Google AI Mode adoption.

---

## Appendix: Schema Validation Commands

```bash
# Verify JSON-LD renders server-side
curl -s https://knxstore.vn/products/cam-bien-chuyen-dong-va-anh-sang-p2-matter-aqara-ml-s03d | grep -c "application/ld+json"

# Google Rich Results Test
# https://search.google.com/test/rich-results?url=https://knxstore.vn/products/...

# Schema.org validator
# https://validator.schema.org/?url=https://knxstore.vn/products/...

# Check canonical tags
curl -s https://knxstore.vn/cam-bien-hien-dien | grep -i canonical

# Check meta descriptions
curl -s https://knxstore.vn | grep -i "meta name=\"description\""
```

---

*Report generated: 2026-06-01 | Data sources: Live fetch knxstore.vn + sitemap analysis | 68 brands confirmed, 1,000+ products in sitemap*
