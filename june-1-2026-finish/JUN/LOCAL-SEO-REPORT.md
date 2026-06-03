# Local SEO Report — KNXStore.vn

**Generated:** 2026-06-01  
**Domain:** https://knxstore.vn  
**Business:** Công Ty Cổ Phần Tích Hợp Hệ Thống Liên Minh (KNXStore)  
**Analyst:** Claude SEO v2.0 / seo-local skill  

---

## Local SEO Score: 28/100

| Dimension | Weight | Score | Notes |
|-----------|--------|-------|-------|
| GBP Signals | 25% | 3/25 | Không có embed, không có GBP reference trên website |
| Reviews & Reputation | 20% | 2/20 | Không có review widget, không có aggregateRating schema |
| Local On-Page SEO | 20% | 10/20 | NAP visible trong footer, title tag thiếu địa danh |
| NAP Consistency & Citations | 15% | 7/15 | NAP nhất quán trên page, nhưng thiếu citation coverage |
| Local Schema Markup | 10% | 2/10 | Không có JSON-LD LocalBusiness phát hiện được trên homepage |
| Local Link & Authority | 10% | 4/10 | Không phát hiện local authority signals rõ ràng |

> **Lưu ý về schema:** User cung cấp thông tin rằng schema LocalBusiness/Organization đã có trong codebase. WebFetch không extract được JSON-LD — có thể do schema inject qua JavaScript (client-side rendered). Điểm schema (2/10) phản ánh khả năng Google crawler parse được, không phải sự tồn tại của schema. Cần verify bằng Google Rich Results Test.

---

## Business Type: Hybrid

**Tín hiệu phát hiện:**
- Có địa chỉ vật lý cố định: Văn phòng SAV5-01.02, Lầu 1, Tháp 5, The Sun Avenue, 28 Mai Chí Thọ, Phường Bình Trưng, TP.HCM
- Có ngôn ngữ service area: "hỗ trợ kỹ thuật, báo giá dự án và tư vấn thiết kế hệ thống cho System Integrator và ME Contractor **toàn quốc**"

**Khuyến nghị loại GBP:** Service Area Business (SAB) — xem Section 6.

---

## Industry Vertical: B2B Automation Supplier / Electrical Equipment Distributor

Không match với bất kỳ vertical chuẩn nào (restaurant, healthcare, legal, home services, real estate, automotive). Áp dụng path: **Generic LocalBusiness + B2B-specific overlay**.

---

## 1. LocalBusiness Schema — Completeness Audit

### Trạng thái hiện tại (theo thông tin được cung cấp)

| Property | Hiện có | Giá trị hiện tại | Đánh giá |
|----------|---------|-----------------|---------|
| `@type` | Có | `["Organization", "LocalBusiness"]` | Chấp nhận được — xem ghi chú |
| `name` | Có | "KNXStore.vn" | OK |
| `legalName` | Có | "Công ty TNHH Tích Hợp Hệ Thống Liên Minh" | **Lưu ý: mismatch** (xem NAP section) |
| `geo` / `GeoCoordinates` | Có | — | Cần verify 5+ decimal places |
| `address` / `PostalAddress` | Có | — | Cần verify sub-properties |
| `ContactPoint` | Có | — | OK |
| `openingHours` | **Thiếu** | — | Critical |
| `sameAs` | **Thiếu** | — | High |
| `priceRange` | **Thiếu** | — | Medium |
| `areaServed` | **Thiếu** | — | High (SAB/Hybrid) |
| `hasMap` | **Thiếu** | — | Medium |
| `foundingDate` | **Thiếu** | — | Low |
| `aggregateRating` | **Thiếu** | — | High |
| `image` | **Không rõ** | — | Medium |
| `url` | **Không rõ** | — | Nên có |

### Updated JSON-LD — Sẵn sàng implement

```json
{
  "@context": "https://schema.org",
  "@type": ["Organization", "LocalBusiness"],
  "@id": "https://knxstore.vn/#organization",
  "name": "KNXStore.vn",
  "legalName": "Công ty Cổ Phần Tích Hợp Hệ Thống Liên Minh",
  "alternateName": "KNXStore",
  "description": "Phân phối và tư vấn giải pháp tự động hóa tòa nhà tại Việt Nam: KNX, DALI-2, Casambi, Matter, BACnet, Modbus, DMX512.",
  "url": "https://knxstore.vn",
  "logo": {
    "@type": "ImageObject",
    "url": "https://knxstore.vn/[LOGO-URL]",
    "width": 300,
    "height": 60
  },
  "image": "https://knxstore.vn/[STOREFRONT-OR-OFFICE-IMAGE-URL]",
  "telephone": "+84918918755",
  "email": "sales@knxstore.vn",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "Văn phòng SAV5-01.02, Lầu 1, Tháp 5, The Sun Avenue, 28 Mai Chí Thọ",
    "addressLocality": "Thành phố Hồ Chí Minh",
    "addressRegion": "TP.HCM",
    "postalCode": "700000",
    "addressCountry": "VN"
  },
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": "[LAT_MIN_5_DECIMAL_PLACES]",
    "longitude": "[LNG_MIN_5_DECIMAL_PLACES]"
  },
  "hasMap": "https://maps.google.com/?q=[GOOGLE_MAPS_PLACE_ID_OR_CID]",
  "openingHoursSpecification": [
    {
      "@type": "OpeningHoursSpecification",
      "dayOfWeek": ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"],
      "opens": "08:30",
      "closes": "17:30"
    },
    {
      "@type": "OpeningHoursSpecification",
      "dayOfWeek": "Saturday",
      "opens": "08:30",
      "closes": "12:00"
    }
  ],
  "areaServed": [
    {
      "@type": "Country",
      "name": "Vietnam"
    },
    {
      "@type": "City",
      "name": "Thành phố Hồ Chí Minh"
    },
    {
      "@type": "City",
      "name": "Hà Nội"
    },
    {
      "@type": "City",
      "name": "Đà Nẵng"
    }
  ],
  "priceRange": "$$",
  "currenciesAccepted": "VND",
  "paymentAccepted": "Cash, Bank Transfer",
  "foundingDate": "[YYYY-MM-DD — điền năm thành lập thực tế]",
  "taxID": "0311846236",
  "sameAs": [
    "https://www.facebook.com/knxstore.vn",
    "https://www.youtube.com/@KNXStore",
    "https://zalo.me/0918918755",
    "[LINKEDIN_URL nếu có]",
    "[BING_PLACES_URL sau khi claim]",
    "[APPLE_MAPS_URL sau khi claim Apple Business Connect]"
  ],
  "knowsAbout": [
    "KNX Building Automation",
    "DALI-2 Lighting Control",
    "Casambi Wireless Lighting",
    "Matter Smart Home",
    "BACnet Protocol",
    "Modbus Protocol",
    "DMX512 Lighting"
  ]
}
```

**Ghi chú thực tế:**
- `legalName`: Homepage hiển thị "Công Ty **Cổ Phần**" nhưng user cung cấp "Công ty **TNHH**" — cần xác minh loại hình doanh nghiệp chính xác trên Giấy ĐKKD. Mã số thuế 0311846236 là nguồn truth.
- `@type` dual: `["Organization", "LocalBusiness"]` hợp lệ theo Schema.org. Tuy nhiên, nếu muốn tối ưu hơn có thể dùng `"ProfessionalService"` hoặc `"Store"` làm type phụ thay cho generic `"LocalBusiness"`.
- `geo` coordinates: Đã có trong schema hiện tại — đảm bảo dùng tối thiểu 5 chữ số thập phân (yêu cầu confirmed của Schema.org).
- `openingHoursSpecification`: Dùng structured format thay vì string `"Mo-Fr 08:30-17:30"` — tương thích tốt hơn với Google.

---

## 2. GBP (Google Business Profile) Optimization Checklist

### 2.1 Business Type cho GBP

**Khuyến nghị: Service Area Business (SAB)**

Lý do:
- Khách hàng chính (System Integrators, ME Contractors) không đến văn phòng — họ được phục vụ tại dự án
- Business model là phân phối + tư vấn kỹ thuật, không phải walk-in retail
- Địa chỉ hiện tại là văn phòng trong tòa nhà chung (The Sun Avenue) — không tạo được visual impression như showroom

**Cấu hình GBP đề xuất:**
- Ẩn địa chỉ street address trên GBP listing (tùy chọn trong SAB mode)
- Set service area: TP.HCM + Hà Nội + Đà Nẵng + "Toàn quốc" (all provinces)
- Giữ địa chỉ trong schema website (vẫn cần cho NAP consistency)

> Nếu muốn giữ chân showroom/walk-in visitors, có thể giữ Brick-and-mortar — nhưng cần đầu tư vào photos thực tế và signage rõ ràng.

### 2.2 GBP Primary & Secondary Categories

**Primary Category (quan trọng nhất — #1 ranking factor):**

| Option | Lý do |
|--------|-------|
| `Automation Company` | Gần nhất với core business |
| `Electronics Store` | Nếu muốn nhắm B2C Matter/Smarthome |
| `Electrical Equipment Supplier` | Phù hợp B2B, nhưng ít search volume hơn |

**Khuyến nghị Primary:** `Automation Company`

**Secondary Categories (tối đa 9, khuyến nghị 4):**
1. `Electrical Equipment Supplier`
2. `Electronics Store`
3. `Building Materials Store` (liên quan đến MEP contractors)
4. `Industrial Equipment Supplier`

> Lưu ý: GBP tại Việt Nam có thể không có đầy đủ category tiếng Việt. Dùng tiếng Anh nếu cần — Google Maps VN dùng cùng category set.

### 2.3 Photos Strategy

Businesses with photos nhận 45% more direction requests (Agency Jet). KNXStore là B2B nên photos cần thể hiện **expertise và trust**, không cần đẹp như retail.

| Photo Type | Số lượng khuyến nghị | Nội dung cụ thể |
|-----------|---------------------|-----------------|
| **Cover photo** | 1 | Logo + tagline "Tự động hóa tòa nhà — KNX, DALI, Casambi, Matter" |
| **Logo** | 1 | Logo đúng tỷ lệ GBP (1:1, min 250x250) |
| **Office/Showroom** | 3-5 | Văn phòng The Sun Avenue, display nếu có thiết bị trưng bày |
| **Products** | 10-20 | KNX actuators, Casambi drivers, DALI gateways, Matter hubs — real product photos |
| **Case study / Installation** | 10-15 | Dự án thực tế: Vegi Resort, Blum Experience Center, Magnolia Park (đã có blog posts) |
| **Team photos** | 3-5 | Kỹ sư tư vấn, team giao nhận, hỗ trợ kỹ thuật |
| **Video (GBP)** | 1-2 | Walkthrough sản phẩm, unboxing KNX panel, demo Casambi app |

### 2.4 GBP Posts Strategy

GBP Posts không có direct ranking impact (WebFX confirmed) nhưng kích hoạt **Post Justifications** — snippet xuất hiện trong local pack kết quả, tăng CTR.

**Lịch đăng posts khuyến nghị:**

| Tần suất | Loại post | Ví dụ nội dung |
|----------|-----------|---------------|
| 2x/tháng | **What's New** | "Firmware mới Casambi 4.x — những thay đổi cho SI cần biết" |
| 1x/tháng | **Product** | "MDT KNX Push Button Interface — pricing & specs" |
| Theo dự án | **Event/Case Study** | "Case study: DALI-2 cho Magnolia Park — 200 luminaires, 1 gateway" |
| Khi có offer | **Offer** | "Demo kit KNX miễn phí cho SI đăng ký trước [ngày]" |

**Tần suất tối thiểu:** 1 post/2 tuần — tuân thủ **18-day rule** (Sterling Sky: rankings cliff nếu không có hoạt động sau 3 tuần).

### 2.5 Q&A Strategy (GBP Q&A bị deprecated Dec 2025)

Google đã remove GBP Q&A feature (Dec 2025) — không export được nội dung cũ. Thay thế:

**FAQ sections trên website** — mục tiêu AI Overviews + ChatGPT citations:

Câu hỏi nên seeding vào FAQ pages:
- "KNXStore có bán lẻ thiết bị KNX không hay chỉ bán B2B?"
- "Tôi cần tư vấn thiết kế hệ thống KNX cho dự án — KNXStore có hỗ trợ không?"
- "Thiết bị Casambi có bảo hành không? Thời gian bảo hành bao lâu?"
- "KNXStore có kho hàng tại Hà Nội không?"
- "Tôi có thể mua lẻ 1-2 thiết bị KNX để test không?"
- "Giá thiết bị KNX tại VN cao hơn EU bao nhiêu? Tại sao?"

Implement dưới dạng `FAQPage` JSON-LD schema để kích hoạt FAQ rich results.

---

## 3. NAP Consistency Audit

### 3.1 NAP Sources Comparison

| Source | Name | Address | Phone |
|--------|------|---------|-------|
| **Homepage (visible)** | Công Ty Cổ Phần Tích Hợp Hệ Thống Liên Minh (KNXStore) | Văn phòng SAV5-01.02, Lầu 1, Tháp 5, The Sun Avenue, 28 Mai Chí Thọ, Phường Bình Trưng, TP.HCM | 0918.918.755 |
| **Schema (user-provided)** | KNXStore.vn | Có (chi tiết không rõ) | Có |
| **legalName trong schema** | Công ty **TNHH** Tích Hợp Hệ Thống Liên Minh | — | — |
| **GBP listing** | Chưa verify — cần kiểm tra thủ công | — | — |

### 3.2 Vấn đề phát hiện

**CRITICAL — Legal name inconsistency:**
- Homepage: "Cổ Phần" (Joint Stock Company)
- Schema legalName: "TNHH" (Limited Liability Company)
- Mã số thuế 0311846236 cấp bởi Sở KH&ĐT TP.HCM ngày 29/12/2025

**Hành động cần thiết:** Xác minh loại hình doanh nghiệp chính xác từ Giấy ĐKKD hiện tại. Đảm bảo `legalName` trong schema, GBP, và mọi citation đều nhất quán.

**MEDIUM — Phone number format:**
- Homepage: `0918.918.755` (format dấu chấm)
- `tel:` link: `0918918755` (liền)
- GBP và citations: Cần dùng E.164 format `+84918918755` cho schema, giữ `0918.918.755` hoặc `0918 918 755` cho display text

**Khuyến nghị format chuẩn:**
```
Display: 0918 918 755
Schema telephone: "+84918918755"
tel: link: tel:+84918918755
```

**LOW — Ward name:**
- Homepage: "Phường Bình Trưng" — cần verify đúng tên (có thể là "Phường Bình Trưng Đông" hoặc "Phường Bình Trưng Tây" — The Sun Avenue thuộc Quận 2, Phường An Phú theo địa chính hiện tại sau sáp nhập 2021)

> Sau khi TP.HCM sáp nhập Quận 2, 9, Thủ Đức thành TP.Thủ Đức (2021), địa chỉ cần update: "Phường An Phú, TP.Thủ Đức, TP.HCM" hoặc theo format mới nhất của Bưu điện VN.

---

## 4. Citation Strategy cho Ngành Automation / Electrical Equipment tại Việt Nam

### 4.1 Tier 1 — Core Citations (Ưu tiên cao nhất)

| Platform | URL | Lý do ưu tiên | Trạng thái |
|----------|-----|--------------|-----------|
| **Google Business Profile** | business.google.com | #1 local ranking factor | Cần verify |
| **Bing Places for Business** | bingplaces.com | Powers ChatGPT, Copilot, Alexa | **Chưa claim** |
| **Apple Business Connect** | register.apple.com/business-connect | Usage tăng 2x lên 27% (BrightLocal 2026) | **Chưa claim** |
| **Facebook Business Page** | facebook.com/knxstore.vn | Đã có — cần verify completeness | Có — cần audit |
| **YouTube Channel** | youtube.com/@KNXStore | Đã có | Có |

### 4.2 Tier 2 — Vietnam B2B Directories

| Platform | URL | Ghi chú |
|----------|-----|---------|
| **Vietmap Business** | maps.vietmap.vn | Vietnam maps alternative — cần claim |
| **Trang Vàng (Yellow Pages VN)** | trangvang.vn | Directory truyền thống VN, vẫn có traffic |
| **Doanh Nghiep VN** | doanhnghiep.com.vn | B2B directory, indexed tốt |
| **VietnamBiz** | vietnambiz.vn | B2B news + directory — potential PR placement |
| **Masothue.com.vn** | masothue.com.vn | Tra cứu MST — citation tự động khi MST đăng ký |
| **Thongtincongty.com** | thongtincongty.com | Thông tin công ty từ ĐKKD |
| **Congty.vn** | congty.vn | Company directory |

### 4.3 Tier 3 — Industry-Specific (Ngành Automation / Electrical)

| Platform | URL | Relevance |
|----------|-----|-----------|
| **KNX Association Member Directory** | knx.org/members | Nếu là KNX Partner — citation authority cao |
| **Casambi Partner Map** | casambi.com/partner-map | Nếu là Casambi Partner chính thức |
| **VINPA** (Vietnam Industrial Park Assoc.) | — | B2B networking |
| **Vietnam Electrical Equipment Association** | — | Industry association citation |
| **Alibaba/Made-in-China** | — | Không phù hợp — tránh, sẽ harm brand positioning |
| **Clutch.co** | clutch.co | Cho tech/integration services — có search volume từ SI |
| **ThomasNet / GlobalSpec** | — | International B2B — nếu target export/international SI |

### 4.4 Data Aggregators (Upstream distribution)

Submit vào 3 aggregator này để tự động lan truyền xuống hàng trăm directories con:

1. **Foursquare** (foursquare.com/business) — feeds Apple Maps, nhiều apps
2. **Data Axle** (businesslistings.cloud.data-axle.com) — feeds 70+ directories Mỹ (ít relevant nhưng feeds international databases)
3. **Neustar/TransUnion** (localeze.com) — feeds Bing, Siri, navigation systems

> Với business VN focus, Foursquare là ưu tiên nhất trong 3 aggregators này.

### 4.5 Platforms để TRÁNH

| Platform | Lý do tránh |
|----------|-------------|
| Foody / Shopeefood | Restaurant-focused — irrelevant, gây nhầm category |
| Yelp (VN) | Không có presence mạnh tại VN |
| TripAdvisor | Tourism-focused — không phù hợp |
| Sendo / Shopee | Marketplace, sẽ dilute brand positioning |

---

## 5. Review Strategy cho B2B Niche

### 5.1 B2B vs B2C Local Review — Khác biệt căn bản

| Dimension | B2C Local Business | KNXStore B2B |
|-----------|-------------------|-------------|
| Review volume target | 50-200+ reviews | 10-30 reviews chất lượng cao là đủ |
| Review velocity | Weekly new reviews | 1-2 reviews/tháng từ closed projects |
| Reviewer identity | Anonymous consumers | Named professionals (SI, contractor) với title |
| Review content | "Great food, fast service" | Technical competence, delivery reliability, support quality |
| Star rating threshold | 4.5+ (31% consumers require) | 4.7+ — B2B buyers do more due diligence |
| Platforms | Google, Yelp, TripAdvisor | Google, Facebook, LinkedIn, Clutch |
| Review trigger | Post-purchase immediate | Post-project completion (3-6 months cycle) |
| CRITICAL risk | Fake reviews từ competitors | Negative reviews từ 1 bad B2B relationship — high impact |

### 5.2 Review Generation Strategy cho KNXStore

**The 18-day rule:** Phải duy trì ít nhất 1 review mới trong mỗi 18 ngày để tránh ranking cliff (Sterling Sky research).

**Quy trình thu thập reviews:**

```
1. Sau khi dự án hoàn thành (1-2 tuần sau delivery/commissioning):
   → Huy (Sales B2B) hoặc Vũ (Sales B2C) gửi follow-up email/Zalo
   → Template: "Dự án [tên] đã hoàn thành. Anh/chị có hài lòng với 
     thiết bị và hỗ trợ kỹ thuật không? Nếu có, feedback của anh/chị 
     trên Google rất có ý nghĩa với team chúng tôi: [LINK]"

2. KHÔNG pre-screen satisfaction trước khi gửi link Google Review
   → Vi phạm Google Fake Engagement Policy + FTC ($53,088/violation)

3. Respond 100% reviews trong 48h
   → B2B buyers xem response rate như indicator của business reliability

4. Negative reviews: Respond professionally, acknowledge, offer offline resolution
   → KHÔNG xóa hoặc flag trừ khi rõ ràng spam/fake
```

**Platform priorities:**
1. **Google Business Profile** — primary, ảnh hưởng local pack
2. **Facebook** (facebook.com/knxstore.vn) — đã có, cần kích hoạt reviews tab
3. **LinkedIn** — dành riêng cho SI/Contractor testimonials dạng long-form
4. **Clutch.co** — platform cho B2B tech services, audience là decision makers

### 5.3 Review Content Guidance (cho khách hàng)

Hướng dẫn khách hàng đề cập những điểm này trong review để tối đa SEO value:
- Loại thiết bị sử dụng (KNX, Casambi, DALI...)
- Loại dự án (biệt thự, văn phòng, khách sạn...)
- Thành phố / khu vực
- Mức độ hỗ trợ kỹ thuật

Ví dụ review tốt: *"Mua thiết bị KNX MDT cho dự án văn phòng 10 tầng tại Hà Nội. KNXStore hỗ trợ kỹ thuật rất nhanh, giao hàng đúng tiến độ, firmware update guide rõ ràng."*

---

## 6. GBP Type Recommendation: SAB vs Brick-and-Mortar

### Phân tích

| Criteria | Brick-and-Mortar | Service Area Business (SAB) |
|----------|----------------|-----------------------------|
| Khách hàng đến văn phòng | Hiếm — không phải mô hình | Không cần |
| Serve location | TP.HCM + toàn quốc | Toàn quốc |
| Địa chỉ hiện tại | Office trong chung cư thương mại (The Sun Avenue) | Không cần hiển thị |
| Local pack appearance | Chỉ rank tốt cho "HCM" queries | Rank cho queries theo service area |
| Photo requirement | Cần storefront, exterior photos | Không cần exterior |
| Risk | GBP bị suspend nếu không có rõ signage/storefront | Thấp hơn |

### Khuyến nghị: **Service Area Business (SAB)**

**Lý do chính:**
1. Business model hoàn toàn không phụ thuộc walk-in traffic
2. Revenue đến từ dự án khắp cả nước — không giới hạn địa lý HCM
3. Địa chỉ The Sun Avenue là văn phòng làm việc, không phải showroom — không có lợi thế khi hiển thị trên Maps
4. SAB cho phép set service area theo tỉnh/thành phố, ranking tốt hơn cho B2B queries từ Hà Nội, Đà Nẵng

**Cấu hình SAB trên GBP:**
- Ẩn địa chỉ street (optional nhưng recommended)
- Set service areas: TP.Hồ Chí Minh, Hà Nội, Đà Nẵng, Bình Dương, Đồng Nai + "Whole Vietnam"
- Primary category: `Automation Company`
- Business description (750 chars): Tập trung vào expertise và brands phân phối

**Trường hợp giữ Brick-and-Mortar:** Nếu có kế hoạch mở showroom thực sự để khách SI/contractor đến xem sản phẩm thực tế và tư vấn trực tiếp — đây là investment đáng cân nhắc về dài hạn.

---

## 7. Local On-Page SEO Assessment

### Title Tag

**Hiện tại:** "Thiết bị KNX, Casambi, Matter và DALI - Phân phối chính hãng tại Việt Nam"

**Đánh giá:** Thiếu location keyword. Tốt cho national SEO nhưng không signal local intent.

**Khuyến nghị cho local:**
```
Thiết bị KNX, DALI, Casambi tại TP.HCM — Phân phối chính hãng | KNXStore
```
Hoặc giữ national focus (phù hợp hơn nếu SAB toàn quốc):
```
Phân phối KNX, DALI-2, Casambi tại Việt Nam — Tư vấn tự động hóa tòa nhà
```

### H1 Assessment

**Hiện tại:** "Thiết bị KNX, Casambi, Matter và DALI - Phân phối chính hãng tại Việt Nam"  
H1 = Title tag — không nên trùng hoàn toàn. H1 có thể variation tập trung vào value prop hơn.

### Click-to-Call

**Status:** Có `tel:0918918755` — tốt. Nên upgrade sang `tel:+84918918755` (E.164 format) để compatibility tốt hơn với quốc tế và schema.

### Google Maps Embed

**Status:** Không có Maps embed phát hiện được trên homepage.  
**Khuyến nghị:** Thêm Maps embed trên trang contact/footer với lazy-load attribute để không ảnh hưởng Core Web Vitals.

```html
<iframe
  src="https://www.google.com/maps/embed?pb=[EMBED_CODE]"
  loading="lazy"
  width="100%"
  height="400"
  style="border:0;"
  allowfullscreen=""
  referrerpolicy="no-referrer-when-downgrade">
</iframe>
```

---

## 8. AI Search / Local AI Impact

> Phần này là local-specific context. Chạy `/seo geo https://knxstore.vn` để phân tích đầy đủ GEO/AI citability.

**Key facts relevant với KNXStore:**
- ChatGPT **không** access GBP trực tiếp — source từ Bing index, Yelp, BBB, Reddit
- **Bing Places** là critical vì powers ChatGPT + Copilot + Alexa
- Với B2B niche: AI Overviews xuất hiện cho ~68% local searches nhưng B2B queries ít local intent hơn
- ChatGPT converts at **15.9%** vs Google organic **1.76%** — B2B decision makers ngày càng dùng AI để research vendors

**Action items cho AI visibility:**
1. Claim Bing Places ngay — data sync vào ChatGPT ecosystem
2. Tạo presence trên Reddit (r/homeautomation, r/smarthome) với genuine expert contributions — ChatGPT source này
3. "Best KNX distributor Vietnam" type queries — cần có presence trên industry forums và review platforms mà AI index

---

## 9. Top 10 Prioritized Actions

### CRITICAL (làm ngay — tác động cao, cost thấp)

| # | Action | Effort | Impact | Owner |
|---|--------|--------|--------|-------|
| 1 | **Xác minh + nhất quán hóa legalName** — "Cổ Phần" vs "TNHH" trên schema, GBP, tất cả citations | 1h | High | Thảo (kế toán — có ĐKKD) |
| 2 | **Claim và optimize Bing Places** — tạo listing đầy đủ, upload photos | 2h | High | Vũ (Dev Web) |
| 3 | **Add openingHoursSpecification vào LocalBusiness schema** — dùng template Section 1 | 1h | High | Vũ (Dev Web) |
| 4 | **Xác minh JSON-LD render server-side** — test bằng Google Rich Results Test (search.google.com/test/rich-results) và Google Search Console URL Inspection | 30min | Critical | Vũ (Dev Web) |
| 5 | **Fix địa chỉ ward** — verify "Phường Bình Trưng" vs "Phường An Phú, TP.Thủ Đức" sau sáp nhập 2021 | 1h | Medium-High | Thảo |

### HIGH (tháng 1-2)

| # | Action | Effort | Impact | Owner |
|---|--------|--------|--------|-------|
| 6 | **Claim Apple Business Connect** — upload photos, set service area | 2h | High | Vũ |
| 7 | **Add sameAs array vào schema** — Facebook, YouTube, Zalo, Bing Places (sau khi claim) | 30min | Medium | Vũ |
| 8 | **GBP review generation** — implement quy trình thu thập reviews sau mỗi dự án (dùng template Section 5.2) | 2h setup | High long-term | Huy (B2B Sales) |
| 9 | **Submit to Tier 2 VN directories** — Trang Vàng, Doanhnghiep.com.vn, Thongtincongty.com | 3h | Medium | Thảo/Vũ |
| 10 | **Thêm Google Maps embed** trên footer hoặc trang contact với lazy-load | 1h | Medium | Vũ |

---

## 10. Limitations — Những gì không thể đánh giá được

| Limitation | Lý do | Tool thay thế |
|-----------|-------|--------------|
| **Geo-grid ranking position** | Cần live SERP data theo tọa độ GPS | DataForSEO Local Pack API, BrightLocal Rank Tracker |
| **GBP Insights data** | Không accessible công khai (views, searches, calls, direction requests) | GBP dashboard trực tiếp |
| **Actual local pack position** | Kết quả khác nhau theo location của searcher | Local Falcon, BrightLocal |
| **Citation coverage breadth** | Không crawl toàn bộ internet để check citations | Moz Local, BrightLocal Citation Audit |
| **Competitor GBP analysis** | Không có access GBP data của competitors | DataForSEO, BrightLocal |
| **Schema rendering verification** | WebFetch không execute JavaScript — JSON-LD inject qua JS không visible | Google Rich Results Test, GSC URL Inspection |
| **Domain Authority** | Cần Moz/Ahrefs API | `/seo backlinks https://knxstore.vn` |

---

## Appendix — Verification Checklist

```
[ ] Xác minh loại hình DN: "Cổ Phần" hay "TNHH" — từ Giấy ĐKKD 2025-12-29
[ ] Verify Google Rich Results Test: search.google.com/test/rich-results
[ ] Verify JSON-LD server-side render (View Source — không phải DevTools)
[ ] Verify địa chỉ ward sau sáp nhập 2021: Phường An Phú, TP.Thủ Đức, TP.HCM
[ ] Claim Bing Places: bingplaces.com
[ ] Claim Apple Business Connect: register.apple.com/business-connect  
[ ] Kiểm tra GBP listing hiện có: maps.google.com → search "KNXStore Liên Minh"
[ ] Set up GBP review link shortcut cho Huy/Vũ để gửi khách hàng
[ ] Add Maps embed vào footer/contact page với loading="lazy"
[ ] Test click-to-call trên mobile: tel:+84918918755
```

---

*Report generated by Claude SEO / seo-local skill v2.0.0*  
*Data sources: WebFetch homepage scrape 2026-06-01, sitemap analysis, user-provided schema context*  
*For AI search visibility analysis: run `/seo geo https://knxstore.vn`*  
*For backlink profile: run `/seo backlinks https://knxstore.vn`*
