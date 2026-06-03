## SEO Agent – KNXStore

### 1. Executive summary
- Homepage đang định vị khá rõ cho các cụm **KNX / Casambi / Matter / DALI** và có độ phủ internal links lớn (quan sát được ~154 internal URLs từ homepage), nhưng **information architecture cho Matter đang bị tách đôi** giữa `/matter` và `/solution/matter`, tạo rủi ro cannibalization/confused canonical.
- Có ít nhất 2 vấn đề technical SEO impact cao: **404 page canonical về homepage** (`/this-page-should-not-exist-xyz-20260602` canonical = `/`) và **page `/matter` canonical sang `/matter-home`** thay vì chính URL đang crawl được.
- Nhiều trang category/blog quan trọng vẫn dùng **metadata khá generic hoặc chưa tối ưu theo search intent B2B**: ví dụ `/blogs` title = `Tin tức`, meta description = `Tin tức`; `/bo-dieu-khien-knx-gateway` title và description chưa phản ánh đúng use case; nhiều bài blog dùng meta description template rất chung chung.
- Cụm **HVAC control** có độ sâu hàng hóa tốt (`/dieu-khien-may-lanh` hiển thị 117 sản phẩm), nhưng page vẫn thiên e-commerce listing hơn là **commercial pillar page** cho các intent như KNX HVAC control, VRV/VRF integration, FCU control, Modbus/BACnet integration.
- Mức độ chắc chắn: **cao** với các phát hiện về title/meta/canonical/H1/404/internal linking dựa trên crawl trực tiếp bằng browser; **trung bình** với nhận định về duplicate/cannibalization toàn site vì audit lần này chỉ kiểm tra homepage + một nhóm URL điều hướng chính, chưa crawl toàn bộ sitemap.

### 2. Issues phát hiện

#### High
1. **404 page canonical về homepage**  
   - URL test: `https://knxstore.vn/this-page-should-not-exist-xyz-20260602`  
   - Quan sát: title = `404 - KNX Store`, H1 = `Không tìm thấy`, nhưng canonical = `https://knxstore.vn/`.  
   - Impact: dễ gửi tín hiệu sai cho Google về soft-404 / canonicalization, làm nhiễu indexation và crawl signals.

2. **Matter landing page có canonical bất thường và H1 không khớp intent**  
   - URL: `https://knxstore.vn/matter`  
   - Quan sát: title = `Thiết bị nhà thông minh Matter | Hệ sinh thái đa nền tảng`, meta description có intent tốt; nhưng canonical = `https://knxstore.vn/matter-home`, H1 lại là `Camera trong nhà` (nhiều khả năng bị lấy từ hero slider).  
   - Impact: Google có thể hiểu sai primary topic của trang Matter; giảm topical relevance cho keyword Matter / Matter smarthome / Matter devices.

3. **Trùng/chồng chéo topic Matter giữa `/matter` và `/solution/matter`**  
   - `/matter`: title mạnh nhưng H1/canonical lỗi.  
   - `/solution/matter`: title = `Thiết bị Matter chính hãng — Chuẩn nhà thông minh Apple, Google, Amazon | KNXStore`, H1 = `Matter`, content dài hơn (~2883 words quan sát được), canonical self-referencing chuẩn.  
   - Impact: rủi ro cannibalization giữa 2 URL cùng intent thương mại cao.

#### Medium
4. **Blogs hub chưa tối ưu metadata và brand/search intent**  
   - URL: `https://knxstore.vn/blogs`  
   - title = `Tin tức`, H1 = `Blogs`, meta description = `Tin tức`.  
   - Impact: khó rank cho các intent như `kiến thức KNX`, `blog Casambi`, `Matter smarthome guide`, `HVAC control blog`.

5. **Category metadata còn generic/không đúng use case kỹ thuật**  
   - `/bo-dieu-khien-knx-gateway`: title = `Bộ điều khiển KNX controller chính hãng, cao cấp`; meta description nói về chuyển đổi KNX sang DMX512 — quá hẹp và có thể không đúng toàn bộ category.  
   - `/casambi-gateway`: title = `Điều khiển Casambi chính hãng, cao cấp` — chưa có modifier B2B như gateway, bridge, integration, project support.  
   - Impact: CTR và keyword match thấp hơn tiềm năng.

6. **HVAC page có taxonomy/label lỗi chính tả**  
   - URL: `/dieu-khien-may-lanh`  
   - Quan sát filter technology hiển thị `Mobus` thay vì `Modbus`; `Homekit` viết chưa chuẩn capitalization.  
   - Impact: yếu trust signal, giảm semantic consistency cho entity/giao thức kỹ thuật.

7. **Meta description của bài blog sản phẩm/giải pháp còn mang template chung**  
   - Ví dụ bài `Casambi không kết nối HomeKit? MTB10 Matter Bridge là giải pháp` dùng description dạng `được cập nhật liên tục, tham khảo một số thông tin khác tại website chúng tôi`.  
   - Impact: lãng phí cơ hội tăng CTR cho long-tail commercial informational keywords.

#### Low
8. **robots.txt quá tối giản**  
   - Quan sát: chỉ có `User-agent: *` và `Disallow: /users/login`.  
   - Không thấy dòng `Sitemap:` trong robots.txt dù sitemap index tồn tại tại `/sitemap.xml`.  
   - Impact thấp vì sitemap vẫn truy cập được, nhưng có thể tối ưu tốt hơn cho discovery.

9. **Homepage có cảnh báo JS/UX ở slider**  
   - Browser console ghi nhận `Swiper Loop Warning: The number of slides is not enough for loop mode...` và nhiều JS exceptions không có message chi tiết.  
   - Impact SEO trực tiếp chưa chắc chắn, nhưng có thể ảnh hưởng rendering/UX/CWV nếu lặp lại trên nhiều template.

### 3. Top 5 actions tuần này
1. **Hợp nhất chiến lược Matter landing page**  
   - Chọn **1 URL chuẩn duy nhất** cho intent thương mại Matter: ưu tiên `/solution/matter` vì metadata + nội dung hiện đang tốt hơn.  
   - Nếu giữ `/matter`, cần sửa ngay: H1 chuẩn (`Thiết bị Matter` / `Giải pháp Matter Smarthome`), canonical self-reference hoặc 301 về URL chuẩn.  
   - Update internal links trong menu/home/blog về cùng 1 URL.

2. **Sửa template 404**  
   - 404 phải trả về canonical self-reference hoặc không đặt canonical về homepage.  
   - Thêm `noindex, follow` nếu template hiện không trả HTTP 404 chuẩn (điểm này cần dev xác minh server response).  
   - Re-test 3–5 URL giả sau khi fix.

3. **Rewrite metadata cho 5 trang tiền thương mại quan trọng**  
   Ưu tiên: homepage, `/blogs`, `/casambi-gateway`, `/bo-dieu-khien-knx-gateway`, `/dieu-khien-may-lanh`.  
   - Title nên thêm intent: `KNX`, `Casambi`, `DALI`, `HVAC`, `Matter`, `gateway`, `integration`, `giải pháp công trình`, `báo giá dự án`.  
   - Meta description nên nêu rõ use case + đối tượng B2B: system integrator, M&E contractor, tư vấn thiết kế, retrofit, tòa nhà/villa/hotel/office.

4. **Biến `/dieu-khien-may-lanh` thành pillar page cho HVAC control**  
   - Giữ listing sản phẩm nhưng thêm section nội dung rõ theo subtopic: VRV/VRF, FCU, fresh air, thermostat, KNX HVAC, Modbus gateway, BACnet integration, Home Assistant integration.  
   - Thêm jump links + FAQ schema + internal links xuống subcategories và bài blog liên quan.

5. **Chuẩn hóa taxonomy và anchor text kỹ thuật**  
   - Sửa `Mobus` -> `Modbus`, `Homekit` -> `HomeKit`.  
   - Rà soát tên category/filters/anchors cho các entity: KNX, DALI, Matter, BACnet, Modbus, HVAC, Home Assistant.  
   - Với blog/product cards, ưu tiên anchor text giàu intent hơn thay vì generic kiểu `Chi tiết`, `Xem thêm` ở các block giải pháp chính.

### 4. Keyword/content gaps quan trọng
- **BACnet**: chưa thấy landing page/anchor nổi bật từ homepage và navigation cho intent `BACnet gateway`, `KNX to BACnet`, `HVAC BACnet integration` (mức chắc chắn: trung bình, dựa trên kiểm tra homepage + nav chính). Đây là gap lớn cho lead B2B tòa nhà/BMS.
- **Modbus**: có dấu hiệu hiện diện trong content/taxonomy HVAC nhưng rất yếu; chưa thấy hub page mạnh cho `Modbus HVAC control`, `KNX Modbus gateway`, `Modbus lighting/HVAC integration`.
- **Home Assistant integration**: có bài news về Matter Server nhưng chưa thấy pillar/page mang intent triển khai thực tế như `KNX + Home Assistant`, `Casambi + Home Assistant`, `Matter bridge cho Home Assistant`. Đây là gap tốt để thu hút integrator/prosumer chất lượng cao.
- **DALI commercial intent**: homepage có nhắc DALI mạnh, nhưng lần kiểm tra này chưa thấy một content hub nổi bật kiểu `DALI lighting control`, `DALI vs Casambi`, `DALI gateway cho công trình`. Nên tăng content cluster cho lighting specifier/MEP audience.
- **Topic hierarchy**: blog hiện có nhiều bài kiến thức phổ thông (NFC, IC, Thread) nhưng số bài mang intent mua/triển khai B2B cho KNX/Casambi/HVAC/BMS còn ít hơn tiềm năng.

### 5. 2 URL hoặc 2 bài blog nên tạo/cập nhật tiếp theo
1. **Cập nhật URL hiện có:** `https://knxstore.vn/dieu-khien-may-lanh`  
   - Mục tiêu: biến thành landing page/pillar cho cụm **HVAC control / KNX HVAC / VRV-VRF / FCU / Modbus / BACnet**.  
   - Nên bổ sung các section: so sánh giao thức, sơ đồ kiến trúc, use case theo loại công trình, CTA báo giá/tư vấn tích hợp.

2. **Tạo bài blog mới:** `/knx-vs-bacnet-vs-modbus-cho-bms-hvac-nen-chon-giao-thuc-nao`  
   - Search intent: tư vấn lựa chọn giao thức cho công trình, MEP consultant, system integrator, chủ đầu tư.  
   - Outline đề xuất: khi nào dùng KNX, khi nào dùng BACnet, khi nào dùng Modbus; khác nhau về topology, interoperability, commissioning, chi phí retrofit; mapping sang giải pháp KNXStore.

---

### URL đã kiểm tra trực tiếp trong lần audit này
- `https://knxstore.vn/`
- `https://knxstore.vn/robots.txt`
- `https://knxstore.vn/sitemap.xml`
- `https://knxstore.vn/casambi-gateway`
- `https://knxstore.vn/bo-dieu-khien-knx-gateway`
- `https://knxstore.vn/dieu-khien-may-lanh`
- `https://knxstore.vn/blogs`
- `https://knxstore.vn/matter`
- `https://knxstore.vn/solution/matter`
- `https://knxstore.vn/casambi-khong-ket-noi-homekit-mtb10-matter-bridge-la-giai-phap.html`
- `https://knxstore.vn/this-page-should-not-exist-xyz-20260602`

### Dữ liệu crawl nổi bật
- Homepage: title `KNXStore | Thiết bị và giải pháp điều khiển cho mọi công trình`; meta description hiện tại khá ngắn; H1 đúng chủ đề; quan sát ~154 internal links.
- robots.txt: chỉ có `User-agent: *` và `Disallow: /users/login`.
- sitemap index: gồm `sitemap-product.xml`, `sitemap-category.xml`, `sitemap-post.xml`, `sitemap-solution.xml`, `sitemap-brand.xml`.
