# Action Plan — knxstore.vn SEO
**Date:** 2026-06-01 | **Score:** 64/100 → Target: 78/100 in 90 days

## Sprint 1 — Tuần 1 (Quick Wins)

- [ ] **C3** `robots.txt` — thêm `Sitemap: https://knxstore.vn/sitemap.xml` và `Disallow: /search?` (5 phút)
- [ ] **C1** Thêm alt text 9 banner images trên homepage (30 phút)
- [ ] **C2** Tạo `/llms.txt` theo template trong FULL-AUDIT-REPORT.md (1 giờ)
- [ ] **H3** Sửa alt text `"Image"` trên blog thumbnails → tiêu đề bài viết (2 giờ)
- [ ] **H5** Verify + optimize Google Business Profile (2 giờ)

## Sprint 2 — Tuần 2–3 (Performance & Schema)

- [ ] **H1** Thêm `width`, `height`, `loading="lazy"` vào tất cả images trong template (1-2 ngày)
- [ ] **H2** Thêm `CollectionPage` + `ItemList` schema vào category page template (4 giờ)
- [ ] **M5** Cài Google API key → chạy PSI để đo CWV thực → `python3 scripts/google_auth.py --setup`
- [ ] **M1** Thêm Content-Security-Policy header qua Cloudflare

## Sprint 3 — Tháng 2 (Content & E-E-A-T)

- [ ] **H4** Audit 735 product pages: flag pages < 200 từ description → bổ sung nội dung
- [ ] **M2** Cập nhật H1 category pages (dài hơn, có keyword target)
- [ ] **M3** Tạo author bio pages với chứng chỉ KNX, kinh nghiệm
- [ ] **M6** Defer vendor JS (swiper, simplebar, choices.js) — sau khi có PSI data

## Baseline
```bash
python3 scripts/drift_baseline.py https://knxstore.vn
```
Chạy ngay để capture snapshot SEO hiện tại trước khi fix.
