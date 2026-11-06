# Market research: tool vận hành đa sàn Shopee + TikTok Shop VN

Ngày đọc nguồn: 2026-11-06. Dựa trên PRD "Tool vận hành Shopee và TikTok Shop" v1.0 (05/11/2026, 16 trang).
Nhãn: `confirmed` = đã mở trang gốc; `secondary` = báo/tổng hợp; `vendor` = hãng tự nói; `giả định` = của mình.
Tỷ giá dùng để quy đổi: **1 USD = 26.000 VND** (giả định, sai số khoảng 1%).

> **Cập nhật lần 2 (2026-11-06, theo bản skill `market-research` mới):** thêm đọc G2/Capterra/Trustpilot/Reddit/HN bằng `read-blocked`, giá vốn và biên gộp, kênh phân phối và CAC/LTV, độ giữ chân thật, rủi ro nền tảng upstream/downstream, và độ sâu JTBD so với độ rộng tính năng (mục 4, 5, 8–12). Kết luận và đề xuất đã sửa theo (mục 1, 15).

## Mục tiêu (Bước 0)

Tôi cần biết đối thủ, giá, nỗi đau seller và kích thước thị trường về tool vận hành đa sàn Shopee/TikTok Shop VN, để quyết định **build hay không / giá bao nhiêu / vào bằng đường nào**.

## 1. Kết luận (đọc phần này nếu chỉ có 2 phút)

1. **Không nên build nguyên PRD như một sản phẩm "tất cả trong một".** Phần vận hành thuần (đồng bộ đơn, tồn, in tem) đã có 9+ hãng, nhiều hãng có vốn lớn (KiotViet được KKR rót $45M, BigSeller $210M năm 2022). Đua ở đó là đua với đối thủ có nhiều tiền hơn.
2. **Khoảng trống hẹp hơn mình nghĩ lúc đầu.** Shopee VN đã có "Quản lý Kế toán" hiển thị doanh thu, giá vốn, phí và lợi nhuận từng đơn (bài 15/05/2024), nên phần "lãi theo đơn" riêng cho Shopee đang bị sàn tự làm. TikTok Shop US cũng đã có Earnings Analytics (05/2026); bản VN chưa xác nhận. Phần còn lại sàn khó làm vì bất lợi cạnh tranh giữa hai sàn:
    - **một sổ lãi thật cho cả Shopee và TikTok**, có quảng cáo (GMV Max, Shopee Ads) quy về lãi theo SKU;
    - **giải thích từng đơn "vì sao tiền về thấp hơn giá bán"** và đối soát có hồ sơ khiếu nại kèm bằng chứng;
    - **duyệt và audit log** cho các thao tác ảnh hưởng tiền.
   Không hãng nào trong 15 hãng đã chấm gộp đủ cả ba. Renda gần nhất nhưng không có tầng vận hành; BigSeller thiếu KOC theo lợi nhuận, duyệt và audit; Kixmon chỉ TikTok Shop và không thấy tiếng Việt.

3. **Thị trường cho thuê bao thuần là nhỏ.** TAM/SAM/SOM (mục 7) ra SAM nền ≈ $2,1M/năm (khoảng $0,13–13M) và SOM 12 tháng nền ≈ $41 nghìn. Con số phụ thuộc mạnh vào 3 giả định chưa có nguồn công khai.
4. **Rủi ro API và đường vào ISV lớn hơn PRD thừa nhận (mục 5, 11).** TikTok có Finance API chi tiết và GMV Max API hỗ trợ VN, nhưng đổi API hàng chục lần mỗi tháng, chat bị chặn nếu chưa có ≥1.000 seller, và thông tin người mua bị che theo App Category từ 12/10/2026. Shopee bắt ISV nộp pentest từ 13/07/2026 (hạn 16/10/2026 đã qua; nguồn là trang Singapore, chưa xác nhận cho VN), và tiêu chí nhận ISV đòi sản phẩm đã chạy và đã tích hợp sàn khác.
5. **Độ giữ chân: đối soát và lãi thật là "hệ thống ghi nhận định kỳ", chưa chứng minh dùng hàng ngày (mục 10).** Ví dụ xác minh duy nhất về công cụ lợi nhuận TikTok Shop có doanh thu giảm khoảng 7% mỗi tháng trong 10 tháng. Nên bán gói năm, không bán thuần theo tháng.
6. **Biên gộp phụ thuộc vào việc giới hạn AI (mục 8).** Với giả định chi phí in rõ, người dùng trung bình ở $25/tháng có biên gộp ≈ 51%, người dùng nặng với AI không giới hạn bị âm (≈ −21%). Cần trần token và hạn mức đơn; không nên bán gói "Unlimited".
7. **Kênh vào: content/SEO cộng affiliate định kỳ, không xây đội sales (mục 9).** Sales-led là kênh dễ không hoàn vốn nhất khi churn cao. Hai từ khoá còn trống trong kết quả WebSearch (proxy, chưa phải Google VN): "tính lãi lỗ shopee tiktok shop" và đối soát tiền về.
8. **Đề xuất vào bằng đường nào (mục 15):** build một lát cắt hẹp về đối soát và lãi thật đa sàn kèm duyệt/audit, không build kho/in tem/đăng video/chat. Bán cho shop ≥100 triệu/tháng, gói năm, có trần AI. Có thể bắt đầu bằng nhập file báo cáo (suy luận của mình, chưa kiểm điều khoản) để chưa phải qua cổng ISV. Xác thực bằng bán trước và 5 cuộc phỏng vấn.

## 2. Đối thủ và bảng giá thật

Giá VND, vùng VN, đọc 2026-11-06. Gói nhỏ nhất đủ nối Shopee + TikTok Shop.

| Hãng | Gói | Giá | Quy năm (USD) | Ghi chú | Nhãn |
|---|---|---|---|---|---|
| Sapo | Pro | 249.000đ/tháng | ≈ $115 | 5 gian hàng sàn, 10.000 đơn/tháng. Trang không ghi kỳ tính và VAT. Phí cài đặt 1–3 triệu, miễn nếu ký ≥2 năm | confirmed |
| Nhanh.vn | POS Basic + Nhanh.Ecom | 250.000 + 50.000đ/tháng | ≈ $138 | Giá list. Mua 2 năm: 150.000 + 50.000 | confirmed |
| KiotViet | Gói hỗ trợ | 270.000đ | ≈ $125 | Chỉ nối Shopee và TikTok Shop. Kỳ tính không ghi. Banner "8.000đ/ngày" không khớp (xem mục 13) | confirmed |
| Haravan | Standard | 300.000đ/tháng | ≈ $138 | Đã gồm VAT, trả theo năm, 3 gian hàng sàn | confirmed |
| MISA eShop | Starter | 199.000đ/tháng | ≈ $92 | Từ PDF báo giá 04/2025, trang web lệch ở gói cao hơn | confirmed (PDF) |
| Pancake POS | Free | 0đ | $0 | Miễn phí. Không có đối soát tiền về từ sàn | confirmed |
| Renda | PRO | 600.000đ | ≈ $277 nếu là /tháng | 3 shop. **Kỳ tính không ghi**, giả định tháng. Gói Free: 1 shop, làm mới 1 lần/ngày | confirmed (trang), kỳ = giả định |
| BigSeller | vip1 | 7.753.000đ/năm | ≈ $298 | 10.000 đơn, 12 shop, 5 user. Gói free: 1.500 đơn, 3 shop. Giá gạch 8,4 triệu, giảm thật 7,7% | confirmed (API giá site VN) |
| Ginee | Pro | Không công bố | n/a | Chỉ có hạn mức, giá phải liên hệ | confirmed |
| Kixmon | Startup | $190/năm | $190 | Chỉ TikTok Shop, 500 đơn/tháng. Không ghi mã tiền tệ | confirmed |

Công cụ dữ liệu thị trường TikTok (mảng khác, bổ trợ chứ không cạnh tranh trực tiếp): FastMoss Basic 342.000đ/tháng (≈ $13), Kalodata Starter $21,9/tháng, EchoTik $13,9/tháng. Đều không phải công cụ vận hành shop.

**Giá thật so với giá quảng cáo:**

- BigSeller: giá năm = 12 × tháng × 0,923 → giảm 7,7% (không phải mức "giảm sâu"). Giá 6 tháng = đúng 6 × giá tháng.
- Nhanh.vn: mua 2 năm giảm 26,7–40% tùy gói (tự tính từ giá list và giá 2 năm).
- Giá gia hạn: **không hãng nào công bố.** Chỉ Haravan ghi rõ VAT.
- Chưa đọc được giá: Salework, Abit, Pancake chat. Các trang render bằng JS hoặc không có bản VN.

### Bộ tiêu chí 15 hạng mục và điểm

Hạng mục (lấy từ PRD): 1 đồng bộ đơn · 2 tồn kho trung tâm · 3 SLA/cảnh báo quá hạn · 4 in tem/quét/đóng gói · 5 đối soát tiền thực nhận · 6 lãi lỗ theo đơn/SKU · 7 ads + lãi sau ads · 8 KOC theo lợi nhuận · 9 listing/giá hàng loạt · 10 khuyến mãi có mô phỏng lãi · 11 CSKH chat gộp · 12 lịch nội dung/đăng video · 13 livestream · 14 phân quyền + duyệt + audit · 15 AI đề xuất kèm bằng chứng.

Cách chấm: ✓ = 1, một phần = 0,5, "không thấy" = 0. **"Không thấy" nghĩa là không có trên các trang đã đọc, không chắc hãng không có tính năng.** Ô "chưa kiểm được" tính 0, nên điểm của Ginee là cận dưới.

| Hãng | Điểm /15 | Thấy mạnh | Thiếu |
|---|---|---|---|
| BigSeller | 8,5 | Đơn, tồn, in tem, lãi lỗ, listing | KOC, chat, livestream TikTok, ma trận duyệt, audit |
| Sapo | 7,0 | Đơn, tồn, in tem | SLA, KOC, khuyến mãi mô phỏng, lịch nội dung |
| Haravan | 7,0 | Đơn, tồn, listing, chat | SLA, KOC, khuyến mãi mô phỏng |
| Renda | 7,0 | SLA, đối soát, lãi thật, ROAS theo lợi nhuận | Tồn, in tem, listing, chat |
| Pancake POS | 5,5 | Đơn, tồn | SLA, KOC |
| Ginee | 5,5 (cận dưới) | Đơn, tồn, listing, chat | Ads, lãi, KOC |
| Nhanh.vn / MISA / Salework / Kixmon | 5,0 | | |
| Shop Manager | 4,0 | | |
| KiotViet | 3,5 | | |

**Ô trống toàn thị trường:** khuyến mãi có mô phỏng lợi nhuận (10) và lịch nội dung/đăng video (12): không hãng nào. KOC theo lợi nhuận (8): chỉ Kixmon (gói Max, TikTok) và Renda (một phần). SLA (3): chỉ Renda rõ ràng.

### Biểu đồ định vị

![Giá trị × Tính năng](chart.svg)

- Trục X: số hạng mục phủ (/15). Trục Y: điểm tính năng trên mỗi $100/năm. (Đã đổi từ $10 sang $100 so với script gốc, vì giá VN cao hơn nên điểm dồn sát đáy.)
- Giá quy năm: gói nhỏ nhất, giá list vì không hãng nào công bố giá gia hạn, tỷ giá 26.000đ/$.
- Ô thoi hồng là **giả thuyết** cho sản phẩm của mình (điểm tính năng 8,5 là MVP theo PRD, 11,5 là sau giai đoạn 2 trừ các module không có API, xem mục 5). **Lát cắt đối soát + lãi thật** (5,5/15) = đồng bộ đơn 1 + đối soát 1 + lãi lỗ 1 + ads 0,5 (GMV Max có API, Shopee Ads chưa xác nhận) + KOC 0,5 + phân quyền/duyệt/audit 1 + AI đề xuất 0,5. Điểm thấp hơn, nhưng đó là cố ý: xem mục 12 về độ sâu so với độ rộng.
- Vùng "trống" (≥9 hạng mục, ≥3 điểm/$100): chưa hãng nào đứng. Điểm MVP + giai đoạn 2 ở $300/năm lọt vào đó, **nhưng đó là điều mình hứa chưa làm, không phải bằng chứng.**
- Bảng xếp hạng đầy đủ: `ranking.md`. Dữ liệu đầu vào: `data.json`.

## 3. Hồ sơ công ty (tiền chảy theo đường nào)

| Hãng | Thành lập | Chủ sở hữu | Vốn / thương vụ | Quy mô tự công bố | Nhãn |
|---|---|---|---|---|---|
| Sapo | 2008 (trang công ty) hoặc 2009 (registry) | Founder Trần Trọng Tuyến, VC thiểu số | Series A "7 chữ số USD" 05/2020 (Smilegate, Teko). Tin đàm phán $20M 05/2023, chưa thấy đã đóng | >230.000 khách; nhân sự 1.000+ (Tracxn: 375) | confirmed / vendor |
| KiotViet | 2010 (pháp nhân), sản phẩm 2014 | Founder-led, KKR dẫn Series B | $6M (08/2019) + $45M (09/2021) = $51M | ~300.000 khách (banner không ngày) | confirmed / vendor |
| Nhanh.vn | 2014 (pháp nhân 2019) | Founder + MoMo (tỷ lệ không công bố) | MoMo đầu tư 01/2022, giá trị không công bố | >80.000 doanh nghiệp (2022) | confirmed |
| Haravan | 2014 | Founder-led | Chỉ thấy $50K accelerator (secondary) | 60.000+ khách | vendor |
| iPOS.vn | 2010 | **MoMo nắm 68,1%** (05/2024) | Không có vòng VC công khai | 100.000+ khách F&B | confirmed |
| BigSeller | 2014 | Shenzhen Meiyunji, VC/growth | C $100M (03/2022), D $110M (08/2022: SoftBank VF2, Sequoia China) | Không có số VN riêng | confirmed |
| Ginee | 2021 (đổi tên) | **Advance Intelligence Group** (Singapore), không phải "Ecosoft" | Tập đoàn: Series D >$400M, định giá >$2 tỷ (09/2021); $80M (05/2023) | Merchant tập đoàn 100.000 (2021) → 75.000 (2023) | confirmed |
| Kalodata, FastMoss | | Không xác định | Không công bố | Số người dùng không so sánh được | UNVERIFIED |
| Renda | | **Chưa tra hồ sơ** | | | chưa tra |

**Một dòng:** VC/PE dẫn đầu chỉ ở vài tên lớn (KiotViet, BigSeller, OnPoint), tập đoàn chiến lược mua kiểm soát (MoMo giữ 68,1% iPOS và một phần Nhanh.vn), phần còn lại tự thân; vòng lớn gần nhất đều từ 2022 trở về trước. MoMo đang cân nhắc bán tới 50% ở tầng mẹ (định giá tới $3 tỷ), chưa chốt.

Giới hạn: không qua được cổng đăng ký kinh doanh quốc gia (captcha). Nguồn registry là bản gương chogia.vn/tratencongty.com (secondary). Không có dữ liệu registry Trung Quốc.

## 4. Seller đang khen/chê gì

Nguồn: gần 8.000 review 1–2★ trên App Store và Google Play (đọc thẳng từ endpoint store) cho Sapo, KiotViet, Nhanh, Haravan, BigSeller, Kalodata, cộng app Shopee Seller Center và TikTok Shop Seller Center làm đại diện nỗi đau seller. Số theo nhóm là regex tự đếm, quote thì đã đọc từng cái.

Nhóm than phiền nhiều nhất (trên review của chính app sàn, 1–2★ từ 2024): phí cao ăn hết lãi (Shopee 18%, TikTok 6%), hoàn/trả hàng mất hàng mất tiền (10% và 9%), tiền về chậm và phí không minh bạch (khoảng 1–4%).

Khoảng trống theo độ mạnh bằng chứng:

1. **Giải thích từng đơn "tại sao tiền về thấp hơn giá bán"** (affiliate, voucher shop tài trợ, ads, hoàn). Ví dụ: đơn 858k, phí 160k + trợ giá 50k + ads 50k + thuế 12k = 272k, tức 31,7% giá bán (mình tự tính). Độ tin: trung bình–cao.
2. **Quản lý hoàn/trả hàng, khiếu nại có bằng chứng.** Review Sapo: tính năng "chờ nhận hàng hoàn" không tự cập nhật khi hàng về kho. Review TikTok: nút hoàn tiền không có bước xác nhận, bấm nhầm mất quyền khiếu nại tiếp. Độ tin: trung bình–cao.
3. **Lệch tồn khi sale:** nhiều người than, nhưng nhiều đối thủ đã có, nên khó khác biệt.
4. **Lãi thật sau GMV Max/KOC:** **review chưa chứng minh.** Không review nào nhắc "GMV Max" hay "KOC". Bằng chứng còn lại là blog của vendor. Độ tin: thấp.
5. **Ma trận duyệt:** chỉ vài review gián tiếp. Cần phỏng vấn.

**Điều chưa biết:** 0/790 review 1–2★ của Sapo, KiotViet, Nhanh, Haravan nhắc "đối soát". Có thể tính năng ít người dùng, hoặc họ dùng web và không viết review app. Dữ liệu không tách được hai khả năng, nên **không kết luận được "chưa ai làm tốt đối soát"**.

**Nguồn thiếu và phần đã bổ sung (cập nhật 2026-11-06):**

- **Reddit:** thử qua proxy ở hai IP thoát khác nhau (Malaysia, Canada), cả hai đều gặp trang CAPTCHA "Prove your humanity", không đọc được. Kho lưu trữ chỉ trả được bài không liên quan (về Shopify). Bài này không dùng số liệu Reddit nào.
- **G2 và Capterra:** đã đọc được G2 (qua trình duyệt từ xa). Ginee có trang với 5/5 từ 3 review, hồ sơ chưa được claim. Tìm kiếm không ra trang riêng của BigSeller trên G2 hay Capterra (kết quả "BE BIG SELLER" là một công ty khác). Hai nguồn này gần như trống cho thị trường này, nên không bổ sung được nỗi đau seller.
- **Facebook group** (nguồn quan trọng nhất cho than phiền seller VN, cần đăng nhập), **Voz, Tinhte:** vẫn chưa đọc.
- Hacker News không có tín hiệu về thị trường này.

### Bổ sung 2026-11-06: đọc G2, Capterra, Trustpilot, Reddit, HN bằng `read-blocked`

Đọc bằng `read.sh` (rung `brightdata(scraping browser)`) và `scroll-read.mjs`. Trang đã mở đều có URL và ngày trong dữ liệu thô; số dưới đây lấy từ trang gốc, không từ đoạn trích tìm kiếm.

| Hãng | G2 | Capterra | Trustpilot |
|---|---|---|---|
| KiotViet | **4,5/5, 2 review** (4★ và 5★, không có review 1–3★) | không thấy | không có hồ sơ |
| Sapo | có hồ sơ "Sapo POS", **0 review** | không thấy | không có hồ sơ |
| Haravan | có "Haraweb" (website builder), 3,5/5, 1 review (2023) | không thấy | không có hồ sơ |
| Ginee | 5/5, 3 review, chưa claim | không thấy | không có hồ sơ |
| BigSeller | không có hồ sơ ("BE BIG SELLER" là công ty khác) | không thấy | có hồ sơ "FairCloud Technology", **0 review** |
| Kalodata | 3,5/5, 1 review | 4,0/5, 1 review | 3,3/5, 14 review |
| FastMoss | 5,0/5, 7 review | có hồ sơ, 0 review | 3,8/5, 2 review |
| Kixmon | 5,0/5, 6 review | có hồ sơ, 0 review | có hồ sơ, 0 review |
| EchoTik, HiveHQ | không tìm thấy | có hồ sơ, 0 review | EchoTik không có; HiveHQ có hồ sơ, 0 review |

- **Khoảng trống bằng chứng là kết quả chính.** Không có review G2/Capterra/Trustpilot nào nói về việc bán Shopee + TikTok Shop ở VN bằng tool nội địa.
- **Than phiền có nhiều bằng chứng thật nhất:** billing/hủy gói/paywall của Kalodata (Trustpilot: 3 trong 7 review 1–2★ nói không hủy được hoặc bị trừ tiền sau khi hủy, 2 nói gói rẻ bị giới hạn rồi bị đẩy lên gói đắt), và CSKH chậm ở tool OMS đa sàn (Anchanto 5 trong 11 review Capterra, bản chụp Wayback 11/2024).
- **Đáng chú ý cho phần lãi lỗ:** một review 1★ trên Capterra của SiteGiant (ERP đa sàn Shopee/Lazada/TikTok Shop, Malaysia, 07/2023) chê báo cáo lãi gộp: nhập sai hoặc bỏ trống giá vốn thì phải tự truy từng SKU từ mã đơn và sửa tay từng đơn. Đây là một review, nhưng đúng loại nỗi đau mà lát cắt lãi thật nhắm vào.
- **Reddit** (bản lưu trữ Arctic Shift, không phải Reddit trực tiếp, vì Reddit trực tiếp bị CAPTCHA): ba thread r/TikTokshop (09–10/2026, hướng Mỹ) hỏi cách tính lãi thật vì phí chỉ có trong báo cáo settlement. Người bán tự làm bảng tính: "I enter them by hand", mất khoảng một giờ. Một người nêu cụ thể: chỉ đơn đã settle mới có trong báo cáo, nên tuần gần nhất luôn trông nhẹ. **Tín hiệu bị nhiễu:** ít nhất 3 trong khoảng 9 người bình luận là người xây công cụ hoặc agency tự khai, và một người đăng 3 bài gần giống nhau trong 7 phút. Không có thread nào về BigSeller, Ginee hay công cụ Việt Nam.
- **Hacker News:** không có thảo luận độc lập nào. Một comment Show HN (02/2026) nói TikTok Shop có "45+ loại phí" khiến khó biết lãi từng đơn; tác giả là người xây công cụ.
- **Review Kixmon trên G2 (6 review 5★):** 3 review đọc được đều đề ngày 08–15/11/2025, một cụm 8 ngày liền ngay sau khi hồ sơ từ 0 review. Mình coi độ tin thấp.

## 5. Khả thi kỹ thuật và pháp lý (theo từng module PRD)

Tài liệu gốc của Shopee Open Platform và TikTok Partner Center đều là SPA, agent chỉ đọc được qua đoạn trích tìm kiếm. Mọi dòng dưới đây cần kiểm lại trên trang gốc trước khi cam kết.

| Nhu cầu PRD | TikTok Shop | Shopee |
|---|---|---|
| Đơn, tồn | Có | Có (suy từ SDK cộng đồng) |
| Tài chính/đối soát | **Có, rất chi tiết** (statements, giao dịch theo đơn/SKU, payments) | Có `get_escrow_detail` (nguồn SDK cộng đồng, chưa xác nhận VN) |
| Quảng cáo / GMV Max | **Có**, GMV Max API v1.3 liệt kê VN, nhưng ở cổng TikTok API for Business (khác Partner Center). 1 shop chỉ ủy quyền 1 tài khoản quảng cáo | ERP/ISV có Ads API hay không: hai nguồn mâu thuẫn |
| Affiliate/KOC | Có nhóm Affiliate Seller API, VN chưa xác nhận | API affiliate riêng cho người làm affiliate, không phải cho ISV |
| Chat/CSKH | **Chặn:** cần ≥1.000 seller ủy quyền hoặc 1 triệu lệnh gọi/ngày | Chỉ whitelist (chưa xác nhận) |
| Đăng video | **Không tìm thấy API** | Có `media_space` qua SDK cộng đồng, chưa xác nhận |
| Livestream | Chỉ analytics, không điều khiển | Không tìm thấy |

Hệ quả cho PRD:

- Module 07/08 (nội dung, đăng video) và 10 (chat CSKH) có thể không làm được bằng API chính thức. PRD cho phép "giao việc đăng thủ công", nên đó là lối thoát.
- **PRD §4.2, §8.2, §8.3** cho phép thao tác Seller Center bằng trình duyệt/user phụ khi chưa có API, trong khi §7.3 cấm "khai thác API không chính thức". Hai ý này dễ mâu thuẫn trong thực tế. Cần đọc điều khoản Open Platform và Partner Center trước khi giữ phần này.
- ISV TikTok cần email khác email seller; compliance review từ 2 đến 3 tuần trở lên. Shopee: hồ sơ ISV duyệt ~3 ngày làm việc, **pentest bắt buộc từ 13/07/2026** (trang Singapore, chưa xác nhận cho VN). Trường hợp một công ty VN bị từ chối ISV 3 lần vì "sản phẩm phải đang chạy, đã tích hợp sàn khác, có tài khoản trial": một người kể, không phải quy định. Có thể là rào chặn thật với người mới.
- Dữ liệu khách: Shopee giới hạn lưu dữ liệu cá nhân tối đa 90 ngày (secondary, từ Zetpy 2024). Module chăm sóc khách và xuất dữ liệu khách của PRD phải theo giới hạn này.
- Phí sàn đổi liên tục trong 2026 (Shopee 24/04, 01/05, 23/05, 01/06; TikTok 09/05, 03/07, 03/08): logic tính lãi phải cập nhật bảng phí liên tục. Đây là chi phí bảo trì, và cũng là lý do seller muốn tool.

### Bổ sung 2026-11-06 (đọc changelog TikTok Partner Center bằng trình duyệt từ xa)

- **Sửa lại:** "Finance API 202309 → 202605" thực ra chỉ là **Get Payments** và chỉ mất trường `reserve_amount`. Hai endpoint sao kê (Statement Transactions) đi theo đường 202309 → 202501, bản cũ hết hạn 31/12/2025.
- **Thông tin người mua bị che theo App Category** từ 12/10/2026 (Get Order Detail/List, Package Detail). Category ERP, Multi-Channel Management, OMS/WMS, Connectors nhận dữ liệu đầy đủ; category khác nhận dữ liệu đã che theo mặc định. Tool chỉ làm tài chính và quảng cáo không cần thông tin người mua nhưng phải chọn đúng category.
- **Shopee, ISV:** từ 13/07/2026 phải nộp báo cáo pentest; ISV không tuân thủ trước 16/10/2026 có thể bị hạn chế quyền xem thông tin người mua. Cả hai mốc đã qua. Nguồn gốc duy nhất là trang Seller Education Singapore; Wizlynx (secondary) ghi ngày và thị trường khác (Thái Lan, 01/03/2026). Chưa xác nhận cho VN.
- **Ủy quyền chính thức qua TikTok Shop Partner (TSP):** seller ủy quyền cho đối tác với thời hạn và phạm vi do seller chọn, thu hồi được bất cứ lúc nào. Phần "user phụ hoặc trình duyệt" của PRD (§4.2, §8.2, §8.3) nằm ngoài đường này. Không tìm được điều khoản nguyên văn của sàn nào cấm hay cho phép tự động hóa Seller Center.
- **Sandbox TikTok:** hai trang chính thức nêu ngưỡng khác nhau (100 và 1.000 yêu cầu/giờ). Chưa rõ cái nào đang áp dụng.

## 6. Kích thước thị trường (số của hãng phân tích, mỗi con số một định nghĩa)

| Nguồn | Phân khúc | Năm 2025 | Nhãn |
|---|---|---|---|
| Metric | Doanh số 4 sàn (Shopee, TikTok Shop, Lazada, Tiki) | 429,7 nghìn tỷ VND ≈ $16,4 tỷ; +34,75% | confirmed |
| YouNet ECI | GMV 4 sàn | 458.160 tỷ VND | secondary (tỷ lệ thị phần cộng ra 103,8%) |
| Momentum Works | GMV gồm cả đơn hủy/trả | $20,4 tỷ | confirmed (phụ lục press kit) |
| e-Conomy SEA 2026 | TMĐT VN (2025 suy ra ≈ $26 tỷ, 2026: $32 tỷ) | ≈ $26 tỷ | secondary |
| Cục TMĐT, Bộ Công Thương | Bán lẻ TMĐT toàn quốc | ≈ $31 tỷ | confirmed |

Thị phần 2025 (Metric): Shopee 56,04%, TikTok Shop 41,31%, Lazada + Tiki ≈ 2,65%. TikTok Shop vượt Shopee ở một số kỳ ngắn (Tết 2026: 51–52%). Metric cảnh báo đó là hiệu ứng ngắn hạn.

**Số shop có đơn:** 601.780 trên 4 sàn năm 2025, giảm 7,43% (so với ≈ 650.100 năm 2024, mình tự tính ngược). Shopee ≈ 209.000 và TikTok Shop >266.000 nhà bán có doanh thu (YouNet, nửa đầu 2025, secondary, định nghĩa "có doanh thu" không rõ). Cộng lại không trừ trùng được.

**Phân bố rất lệch (mình tự tính từ số Metric):**

- Doanh số TB mỗi shop có đơn: 429,7 nghìn tỷ ÷ 601.780 ≈ **714 triệu/năm ≈ 59 triệu/tháng**.
- Shop Mall (2,12% số shop, 32,6% doanh số): ≈ 12.800 shop × ≈ 10,7 tỷ/năm. Con số 12.800 là ước (tử số của 2,12% gồm cả Lazada/Tiki).
- Shop không-Mall: ≈ 479 triệu/năm ≈ **40 triệu/tháng** trung bình. Trung vị chắc chắn thấp hơn.
- Hệ quả: shop ≥100 triệu/tháng là thiểu số. Số lượng cụ thể **không có nguồn công khai**.

**Phí sàn hiện hành VN (đọc qua đoạn trích tìm kiếm, kiểm lại trên Seller Center):**

| | Shopee | TikTok Shop |
|---|---|---|
| Phí giao dịch | 6% (từ 01/05/2026) | 6% (từ 09/05/2026); giảm 1% nếu chi GMV Max ≥4% GMV |
| Phí cố định/hoa hồng | Theo ngành, bảng không đọc được | 14% Marketplace mặc định từ 03/07/2026; Mall 15,5% (trang seller-vn) hoặc 16% (báo chí), chưa chốt |
| Tuỳ chọn | Voucher Xtra 2%, Content Xtra 3% | Voucher Xtra 5%, affiliate 10–20% |

## 7. TAM / SAM / SOM

Sản phẩm: SaaS thuê bao cho seller đa sàn Shopee + TikTok Shop VN, tập trung vào shop doanh số ≥100 triệu/tháng.

```
TAM = số shop đa sàn × giá/năm
    = 570.000 shop có đơn trên Shopee+TikTok × 35% bán cả hai sàn = 199.500 shop
      × 5.388.000đ/năm (Sapo Omni 449.000đ × 12)
    = 1.075 tỷ VND ≈ $41,3M

SAM = TAM × % đúng phân khúc
    = 1.075 tỷ × (10% shop ≥100 triệu/tháng × 50% vẫn vận hành/đối soát thủ công)
    = 1.075 tỷ × 5%  = 53,7 tỷ VND ≈ $2,07M   (≈ 9.975 shop)

SOM (12 tháng) = SAM × 2%
    = 53,7 tỷ × 2% = 1,07 tỷ VND ≈ $41,3 nghìn ARR  (≈ 199 shop trả tiền)
```

| | Thấp | Nền | Cao |
|---|---|---|---|
| Shop đa sàn | 112.500 | 199.500 | 270.000 |
| Giá/năm (VND) | 2.040.000 (Sapo StartUp) | 5.388.000 | 11.988.000 (Sapo Growth) |
| TAM | 229,5 tỷ ≈ $8,8M | 1.075 tỷ ≈ $41,3M | 3.237 tỷ ≈ $124,5M |
| % đúng phân khúc | 1,5% | 5% | 10,5% |
| SAM | 3,4 tỷ ≈ $0,13M | 53,7 tỷ ≈ $2,07M | 339,9 tỷ ≈ $13,1M |
| % chiếm trong 12 tháng | 0,5% | 2% | 5% |
| SOM | ≈ 17 triệu ≈ $0,7 nghìn | 1,07 tỷ ≈ $41,3 nghìn | 17,0 tỷ ≈ $654 nghìn |

**Giả định phải cãi được (không có nguồn công khai):**

- 35% shop bán cả hai sàn (thấp 25%, cao 45%): biến quyết định TAM.
- 10% shop có doanh số ≥100 triệu/tháng (thấp 5%, cao 15%).
- 50% trong nhóm đó đang làm thủ công (thấp 30%, cao 70%).
- 2% chiếm trong 12 tháng: sanity check ≈ 199 shop với đội nhỏ.
- Có nguồn: 601.780 shop (Metric), giá Sapo (trang giá). 570.000 là giả định neo vào 475.000 (YouNet nửa đầu, không trừ trùng) và 601.780.

**Cách tính khác: theo giá trị thu hồi** (giả định r = 0,3% GMV thu hồi được từ đối soát, thấp 0,1%, cao 0,6%, **chưa có nguồn nào công bố tỷ lệ này**):

- GMV của shop ≥100 triệu/tháng ≈ 80% × 418,3 nghìn tỷ (Shopee + TikTok = 97,35% của 429,7 nghìn tỷ) = 334,6 nghìn tỷ VND.
- Thu hồi 0,3% = 1.004 tỷ VND/năm ≈ $38,6M. Lấy 20% phí = $7,7M/năm cho **toàn bộ 57.000 shop ≥100 triệu/tháng** (biến nền), không chỉ đa sàn.
- Ngưỡng hòa vốn (GMV hòa vốn = giá tool/tháng ÷ r): với tool 449.000đ/tháng, r = 0,3% thì shop cần GMV ≥150 triệu/tháng; r = 0,1% thì 450 triệu; r = 0,6% thì 75 triệu.
- Hàm ý: giá trị thu hồi chỉ vượt giá tool với shop khoảng ≥100 triệu/tháng. Shop không-Mall trung bình (40 triệu/tháng) không với tới.

**Đọc kết quả:** SAM $2–13M/năm là thị trường của một doanh nghiệp nhỏ–vừa, không phải của một venture. Hướng mở rộng: tăng giá/khách (lên theo giá trị thu hồi), thêm Mall/brand (12.800 shop, ACV giả định 30 triệu/năm → ≈ 384 tỷ ≈ $14,8M, chưa có nguồn cho ACV), hoặc thêm sàn. Mỗi hướng cần kiểm riêng.

## 8. Giá vốn (COGS) và kiểm tra biên lợi nhuận gộp

Phạm vi: lát cắt đề xuất (đồng bộ, đối soát, lãi thật, cảnh báo) không tạo ảnh hay video; chỉ phần "AI giải thích chênh lệch và đề xuất" tính theo lượt dùng. **Hệ số tạo hỏng (reroll) và "chi phí trên mỗi kết quả dùng được" chỉ áp dụng cho giai đoạn 3 (tạo ảnh/video), chưa có số đo nào nên không tính ở đây.**

**Giả định (tất cả là giả định của mình, không có nguồn; phải đo trên bản chạy thử):**

- Giá $25/tháng (≈ 650.000đ, $300/năm), quota 10.000 đơn/tháng, 12 shop (cùng cỡ BigSeller vip1).
- Hạ tầng theo đơn $0,0005/đơn (≈ 13đ); theo kết nối shop $0,30/shop/tháng.
- LLM $4 mỗi 1 triệu token (giá trộn, giả định; kiểm lại bảng giá model đang dùng).
- Thanh toán 3% doanh thu = $0,75. Hỗ trợ $1 / $2 / $5 mỗi tài khoản cho Light / Average / Power.

| Kịch bản | Hạ tầng theo đơn | Hạ tầng theo shop | LLM | Thanh toán | Hỗ trợ | Tổng chi phí | Biên gộp |
|---|---|---|---|---|---|---|---|
| Light (20% quota) | 1,00 | 1,20 | 0,80 | 0,75 | 1,00 | 4,75 | 81,0% |
| Average (70%) | 3,50 | 2,70 | 3,20 | 0,75 | 2,00 | 12,15 | 51,4% |
| Power (100% quota, AI không giới hạn) | 5,00 | 3,60 | 16,00 | 0,75 | 5,00 | 30,35 | -21,4% |
| Power, AI giới hạn 1 triệu token | 5,00 | 3,60 | 4,00 | 0,75 | 5,00 | 18,35 | 26,6% |
| Abuse / "Unlimited" (30,000 đơn, 20 triệu token) | 15,00 | 3,60 | 80,00 | 0,75 | 5,00 | 104,35 | -317,4% |

Số đơn, số shop và token cho từng kịch bản: Light 2.000 đơn, 4 shop, 0,2 triệu token; Average 7.000 đơn, 9 shop, 0,8 triệu token; Power 10.000 đơn, 12 shop, 4 triệu token (hoặc 1 triệu khi có trần); Abuse 30.000 đơn, 12 shop, 20 triệu token.

- **Ngưỡng cắt lỗ:** ở Power, chi phí ngoài LLM là $14,35, nên hòa vốn ở (25 − 14,35) ÷ 4 = **2,66 triệu token/tháng**. Trần AI 1 triệu token đưa Power lên ≈ 26,6%.
- **Pha trộn 50% Light / 40% Average / 10% Power có trần AI:** chi phí trung bình $9,07, **biên gộp ≈ 63,7%**.
- **Độ nhạy:** nếu giá token gấp đôi ($8 mỗi triệu), biên của Average giảm từ 51,4% xuống 38,6%. Chi phí LLM và hỗ trợ là hai biến lớn nhất.
- **Gói "Unlimited": không đề xuất.** Nếu buộc phải có thì phải kèm hạn mức đơn và trần token. Gói đơn bổ sung nên dựa vào benchmark BigSeller: 10.000 đơn = 702.000đ (≈ 70đ/đơn), 100 đơn = 11.700đ (117đ/đơn), so với chi phí hạ tầng giả định ≈ 13đ/đơn.
- **Điều này ảnh hưởng mục 9:** biên 80% mà agent 5 dùng cho CAC payback cao hơn biên pha trộn ở đây (≈ 60–64%), nên mình tính lại ở 60%.

## 9. Kênh phân phối gốc và CAC so với LTV

**Đối thủ lấy khách từ đâu (đọc 2026-11-06):**

- **SEO/blog:** Sapo 3.654 URL blog (109 có "tiktok", 111 có "shopee"); BigSeller 4.789 URL nhiều ngôn ngữ, ít nhất 113 slug tiếng Việt khớp từ khoá, trong đó ≥12 bài cùng cụm "phần mềm quản lý bán hàng đa kênh Shopee TikTok"; Nhanh.vn 2.400 URL; Ginee VN 999 URL; Haravan 356 URL. Mình đếm từ sitemap; số của BigSeller là cận dưới vì chưa tách theo ngôn ngữ, và ngày `lastmod` của Sapo bị làm mới hàng loạt nên không suy ra tần suất đăng.
- **Quảng cáo trả tiền (Meta Ad Library VN, mẫu 50–59 quảng cáo mỗi truy vấn, "không thấy" không có nghĩa là không chạy):** BigSeller đang chạy ít nhất 4 mẫu với wedge là "Miễn phí vĩnh viễn", sao chép sản phẩm đối thủ và đăng hàng loạt, không phải lãi lỗ hay đối soát. Sapo có một quảng cáo máy bán hàng cầm tay. Google Ads không đọc được (CAPTCHA).
- **Đội sales:** KiotViet tuyển sales với lương cứng đến 12 triệu và hoa hồng đến 40% doanh thu tháng (tin tuyển dụng). Số "~1.200 sales" từ Forbes VN 03/2023 không còn nguồn 2026; KiotViet tự nói hơn 1.700 nhân sự (05/2026) mà không nêu số sales.
- **Affiliate/đại lý:** BigSeller trả hoa hồng **định kỳ trong 24 tháng, bậc 10% / 15% / 20%** theo số người trả tiền (rút lần đầu cần ≥3 tài khoản mới đã mua VIP). Sapo (chính sách đại lý 2018, chưa kiểm còn hiện hành): chiết khấu lần đầu 35–50%, từ lần hai 15% nếu tỷ lệ giữ khách <50% và 20% nếu ≥50%. KiotViet, Haravan, Nhanh, Ginee, Renda, Kixmon, Pancake không công bố tỷ lệ.
- **Chợ ứng dụng:** BigSeller có tên trong danh sách Premium Service Partner của Shopee (Q4/2026, trang Singapore). Sapo tự nói đạt Premium ở Shopee VN đến Q2/2026. Danh mục TikTok Shop App & Service Store cần đăng nhập, không đọc được.
- **Gói miễn phí làm wedge:** BigSeller (1.500 đơn/tháng, 3 shop), Pancake POS, Renda Free (1 shop, làm mới 1 lần/ngày).

**CAC payback (tự tính, giả định in rõ).** Giá 650.000đ/tháng, **biên gộp 60%** (từ mục 8; agent 5 dùng 80%), thu tháng đầu ngay, churn tháng 3% / 5% / 8%, 26.000đ = $1. Công thức: n thỏa CAC = m·(1 − (1−c)ⁿ)/c, với m = giá × biên gộp.

| Kênh | CAC | Hoàn vốn, churn 3% (tháng) | 5% | 8% | LTV:CAC (3% / 5% / 8%) |
|---|---|---|---|---|---|
| Affiliate, thưởng một lần 20% × 12 tháng giá | 1,56 tr ≈ $60 | 4,2 | 4,4 | 4,6 | 8,3 / 5,0 / 3,1 |
| Affiliate, thưởng một lần 30% × 12 tháng giá | 2,34 tr ≈ $90 | 6,5 | 7,0 | 7,8 | 5,6 / 3,3 / 2,1 |
| Sales-led, 6 hợp đồng/tháng (CAC 3 triệu) | 3,00 tr ≈ $115 | 8,6 | 9,5 | 11,5 | 4,3 / 2,6 / 1,6 |
| Sales-led, 3 hợp đồng/tháng (CAC 6 triệu) | 6,00 tr ≈ $231 | 20,3 | 28,6 | không bao giờ | 2,2 / 1,3 / 0,8 |
| Sales-led, 2 hợp đồng/tháng (CAC 9 triệu) | 9,00 tr ≈ $346 | 38,7 | không bao giờ | không bao giờ | 1,4 / 0,9 / 0,5 |
| Content/SEO, 15 khách/tháng (CAC 2 triệu) | 2,00 tr ≈ $77 | 5,5 | 5,8 | 6,3 | 6,5 / 3,9 / 2,4 |
| Content/SEO, 5 khách/tháng (CAC 6 triệu) | 6,00 tr ≈ $231 | 20,3 | 28,6 | không bao giờ | 2,2 / 1,3 / 0,8 |

CAC của affiliate là thưởng một lần; CAC sales-led và content là giả định của mình (lương gộp 18 triệu/tháng chia số hợp đồng; 30 triệu/tháng chi phí nội dung chia số khách), chưa có số đo từ hãng nào. Chưa tính chi phí lead, hỗ trợ và độ trễ 6–9 tháng của SEO.

- **Sales-led** là kênh duy nhất không hoàn vốn ở churn 8% với CAC từ 6 triệu, và chỉ hoàn vốn sau hơn 28 tháng ở churn 5%, dài hơn vòng đời (20 tháng). Hãng lớn sống bằng đội sales đã có sẵn; một đội nhỏ không cạnh tranh được ở đó.
- **Affiliate thưởng một lần dưới 30%** hoàn vốn trong 4–8 tháng ở mọi mức churn. Affiliate định kỳ kiểu BigSeller không tốn tiền trước; chi phí là LTV giảm.
- **Content/SEO** ngang affiliate nếu được 15 khách/tháng và ngang sales-led nếu chỉ 5 khách/tháng. Số khách/tháng ở đây là giả định.
- **Wedge đề xuất:** gói miễn phí cho 1 shop nhập báo cáo thanh toán của cả hai sàn và hiện lãi thật cộng đối soát từng khoản chênh lệch (tiền chưa về, phí sai, đơn hoàn). Renda Free đã có lãi lỗ báo cáo nhưng làm mới 1 lần/ngày; khác biệt phải nằm ở đối soát từng khoản, không chỉ hiển thị lãi.
- **Từ khoá còn trống** (WebSearch chỉ trả kết quả Mỹ, Google VN bị CAPTCHA nên đây chỉ là proxy): "tính lãi lỗ shopee tiktok shop" không có hãng phần mềm nào đứng đầu (Sapo và Nhanh chỉ có bài blog); "đối soát shopee" nghiêng về thuế và kế toán.

## 10. Độ giữ chân thật (Tourist Churn so với Daily Habit)

- **Không có hồ sơ doanh thu xác minh (TrustMRR/Stripe) cho Kalodata, FastMoss, EchoTik, Tabcut, Kixmon, HiveHQ, BigSeller.** "Không tìm thấy" không chứng minh là không có (trang tìm kiếm của TrustMRR chạy ở phía client).
- **Doanh thu tự công bố hoặc ước tính, chưa xác minh:** FastMoss ≈ $3,7 triệu/năm là ước tính của GetLatka, trang này tự ghi "FastMoss chưa công bố doanh thu"; HiveHQ $550 nghìn cũng là ước tính GetLatka; Kixmon nói "5.000+ seller đã theo dõi $50M lợi nhuận" (hãng tự nói, không phải số người trả tiền).
- **Ví dụ xác minh duy nhất:** một công cụ lãi và doanh số TikTok Shop ở UK ("Stealth Company", hồ sơ TrustMRR có Stripe, đọc 2026-11-06): MRR $426 từ 7 người đăng ký; doanh thu 30 ngày thực $330 (77% MRR); doanh thu theo tháng giảm từ $657 (12/2025) xuống $315 (10/2026), tức **−52%, khoảng −7,1% mỗi tháng** (mình tính lại, khớp). Một mẫu, một quốc gia, nên là phản ví dụ cho giả thuyết "công cụ lợi nhuận thì dính khách", không phải kết luận cho cả nhóm. Một công cụ quản lý cửa hàng Etsy cũng có 7 người đăng ký và doanh thu tháng 5 tụt 85% sang tháng 6.
- **Số trong đoạn trích tìm kiếm sai:** một đoạn trích nói "Stealth Company" có $94 nghìn doanh thu 30 ngày; trang thật chỉ có $330. Chỉ trang hồ sơ mới đáng tin.
- **Dấu hiệu churn qua review:** Kalodata trên Trustpilot (14 review): 3 trong 7 review 1–2★ nói không hủy được hoặc bị trừ tiền sau khi hủy. Phân bổ sao đọc từ ảnh chụp (7 review 5★, 2 review 2★, 5 review 1★) khớp với số trên trang.
- **Tham chiếu:** ChartMogul 2023 (SaaS, giữ khách theo năm): ngay cả nhóm tốt nhất ở ARPA dưới $10/tháng giữ khách 12 tháng chỉ khoảng 63%. Churn tháng 3–7% của SMB đến từ blog thứ cấp, chưa kiểm được gốc. Quy đổi (mình tính): 3% tháng = 30,6% năm, vòng đời 33 tháng; 5% = 46%, 20 tháng; 7% = 58%, 14 tháng.
- **Phân loại.** Nhóm nghiên cứu sản phẩm/creator (Kalodata, FastMoss, EchoTik, Tabcut) nghiêng về **Tourist Tool** (dùng theo đợt). Nhóm đối soát/lãi thật là **hệ thống ghi nhận định kỳ**: dùng theo tuần hoặc tháng chốt sổ vì tiền về chậm và nhu cầu thuế; chưa chứng minh dùng hàng ngày. Độ dính nếu có sẽ đến từ dữ liệu lưu lại (giá vốn, ánh xạ phí, gói xuất cho kế toán), không phải tần suất dùng. Tần suất hằng ngày thuộc về ERP/OMS (đơn, tồn, in tem).
- **Hệ quả cho cách bán (suy luận của mình):** mặc định gói năm (đối thủ đã làm: Kixmon "2 tháng miễn phí" khi trả năm); không trông vào gói tháng thuần; thêm tính năng khóa dữ liệu (gói xuất cho kế toán) và đo cohort thật trước khi tin "đối soát thì dính".

## 11. Rủi ro phụ thuộc nền tảng (Upstream và Downstream)

| Rủi ro | Mức | Bằng chứng |
|---|---|---|
| Đổi version, gỡ field, thu hẹp cửa sổ query (TikTok) | **Cao**, chắc chắn xảy ra | Changelog đọc nguyên văn: Get Payments 202309 ngừng 15/08/2026; Analytics gỡ endpoint 28/12/2026 và hạ cửa sổ query từ 11/06/2026; hàng chục thay đổi mỗi tháng 07–11/2026 |
| Shopee bắt pentest và hạn chế thông tin người mua với ISV không đạt | **Cao với đường vào ISV** | Trang Seller Education Singapore: từ 13/07/2026, hạn 16/10/2026 (đã qua). Chưa xác nhận cho VN |
| Rào cản nhận ISV Shopee | **Cao với tool mới** | Tiêu chí: công ty hợp pháp, sản phẩm đang chạy và đã tích hợp sàn khác, cấp tài khoản test; một người kể bị từ chối 3 lần |
| Sàn tự làm lãi theo đơn | **Cao cho từng sàn riêng; trung bình cho đa sàn** | Shopee VN "Quản lý Kế toán" (15/05/2024) và báo cáo Doanh thu 5 trang; TikTok US Earnings Analytics (05/2026), Seller Assistant, Shop Diagnostics. Bản VN của TikTok chưa xác nhận |
| Che thông tin người mua theo App Category (TikTok) | Trung bình; thấp nếu chỉ làm tài chính/ads | Từ 12/10/2026, category ngoài danh sách nhận dữ liệu đã che |
| Mất ủy quyền (seller hủy, hết hạn, shop inactive bị chặn 401) | **Cao, nhỏ lẻ nhưng liên tục** | Shopee: huỷ liên kết thì đối tác "không còn quyền truy cập dữ liệu"; TikTok: chặn shop inactive từ 20/07/2026 |
| Sàn tắt cả cổng API, buộc di cư | Trung bình, đã có tiền lệ | Tokopedia Open API tắt hẳn 30/09/2025, mọi ISV phải sang TikTok Shop Partner Center |
| Nội dung AI đưa lên TikTok bị xử phạt | Trung bình, kiểm soát được | Chính sách AIGC VN (cập nhật 21/10/2026, đọc nguyên văn): cho phép nếu không sai lệch sản phẩm, không làm giả kết quả, và bật nhãn AI; vi phạm lặp lại bị phạt nặng hơn |
| Giới hạn giỏ hàng cho video AI hàng loạt | Trung bình cho module nội dung | 7 video có giỏ hàng/7 ngày từ 24/08/2026 áp cả video AI: chỉ qua Rentracks (secondary), chưa có trang gốc |
| Tự động hóa trình duyệt hoặc user phụ bị coi là vi phạm | Không định lượng được, coi là cao | TikTok có đường TSP chính thức; không tìm được điều khoản cấm hay cho phép nguyên văn |
| Phí sàn đổi liên tục, có can thiệp pháp lý | Cao với module lãi | Shopee hoãn một loại phí mới sau khi Ủy ban Cạnh tranh can thiệp (secondary) |
| ISV bị gỡ vì vi phạm | Không đánh giá được | Không tìm thấy tiền lệ ở VN/SEA; đây là kết quả âm, không phải bằng chứng là chưa từng xảy ra |

- **Hệ quả:** logic tính lãi phải coi bảng phí và phiên bản API là dữ liệu cấu hình, không hard-code. Chi phí bảo trì tích hợp TikTok là đều đặn và cao.
- **Chưa đọc được:** `open.shopee.com` (changelog và điều khoản đối tác), Điều khoản dịch vụ Shopee VN, bản gốc chính sách "giới hạn đăng nội dung" của TikTok Shop.

## 12. Độ sâu kết quả (Core JTBD) so với độ rộng tính năng

Trục X của biểu đồ đếm số tính năng, nên dễ tạo ảo giác rằng "siêu chợ tất cả trong một" luôn thắng. Lát cắt đề xuất chỉ được 5,5/15 và nằm thấp hơn BigSeller (8,5) trên biểu đồ. Điều đó là cố ý: tiêu chí cần chấm là mức xuống tiền cho một bài toán tạo ra tiền trực tiếp, không phải số ô được tích.

**Ba công việc cốt lõi (JTBD) mình đề xuất, kèm bằng chứng:**

1. **Biết tiền thật của từng đơn/SKU sau mọi khoản trừ, trên cả hai sàn, có quảng cáo.** Bằng chứng: review seller không hiểu vì sao tiền về thấp hơn giá bán (mục 4); ba thread Reddit hướng Mỹ hỏi đúng bài toán này; review SiteGiant về báo cáo lãi gộp. Khoảng trống còn lại sau khi trừ công cụ gốc của Shopee: đa sàn và quảng cáo (mục 11).
2. **Thu hồi tiền thất thoát: đối soát chênh lệch và hồ sơ khiếu nại có bằng chứng.** Bằng chứng: review hoàn/trả hàng mất hàng mất tiền (mục 4). Không hãng nào trong dữ liệu có đủ "khiếu nại kèm bằng chứng"; Sapo có đánh dấu "quá hạn thanh toán" nhưng phí sàn do người dùng tự nhập (31/03/2025), BigSeller có cảnh báo chênh lệch thanh toán, Renda có theo dõi tiền về ví.
3. **Thao tác ảnh hưởng tiền có người duyệt và có nhật ký.** Bằng chứng yếu: hai review TikTok về nút hoàn tiền không có bước xác nhận. Cần phỏng vấn để xác thực.

Không đưa vào lõi: đồng bộ tồn, in tem, đăng video, chat. Đây là chỗ đã đông (mục 2) hoặc không có API (mục 5).

**Mức phủ ba JTBD theo trang hãng (✓ rõ, ◐ một phần, ✗ không thấy; lời hãng, chưa dùng thử):**

| Hãng | 1. Lãi thật đa sàn + ads | 2. Đối soát + khiếu nại có bằng chứng | 3. Duyệt + audit |
|---|---|---|---|
| Renda | ✓ (cả hai sàn, ROAS theo lợi nhuận) | ◐ (tiền về ví, phí bất thường) | ◐ |
| BigSeller | ◐ (lãi lỗ đơn; ads Shopee ✓, TikTok chưa xác nhận) | ◐ (cảnh báo chênh lệch thanh toán) | ◐ (role, không thấy duyệt/audit) |
| Kixmon | ✓ nhưng chỉ TikTok Shop | ◐ (tìm khoản bồi hoàn FBT, Mỹ) | ◐ |
| Sapo | ◐ (phí sàn nhập tay) | ◐ (cờ quá hạn thanh toán) | ◐ |
| Shopee (công cụ gốc) | ◐ (chỉ Shopee, lãi từng đơn) | ◐ (báo cáo Doanh thu) | ✗ |

Không hãng nào có ✓ ở cả ba cột. Đó là chỗ đứng của lát cắt, và cũng là chỗ dễ bị sàn hoặc Renda đuổi kịp, nên phải xác thực nhanh.

## 13. Số bị từ chối in

1. **"600.000 shop chia tay TMĐT 2025"** (tiêu đề Báo Pháp Luật): gốc Metric là 601.780 shop *còn có đơn*, giảm khoảng 48.000.
2. **"80.000 shop không có đơn nào H1/2025"** (The Investor): thân bài nói 80.000 shop *hoạt động ít hơn*.
3. **KiotViet "GMV $3 tỷ/tháng":** tổng doanh số cửa hàng khách hàng, hãng tự nói, không phải doanh thu KiotViet. Banner "8.000đ/ngày" không khớp giá (270.000/30 = 9.000).
4. **Nhanh.vn "$200 triệu":** là vòng huy động của MoMo, không phải giá trị đầu tư vào Nhanh.vn.
5. **BigSeller "1,1 triệu seller":** số của 6 nước, không phải VN. Số khách của BigSeller (320k → 430k → 1,1 triệu → 3,9 triệu) và FastMoss (800k → 2M → 2,6M → 4,7M) không cùng định nghĩa.
6. **"TMĐT VN 39 tỷ USD 2025":** hai thứ khác nhau: dự báo cũ 2022 và tổng kinh tế số của e-Conomy 2025 (TMĐT chỉ ≈ $25 tỷ). "38,5 tỷ USD theo VECOM": không truy được.
7. **Chênh lệch GMV 2025:** Metric $16,4 tỷ, Momentum Works $20,4 tỷ, e-Conomy ≈ $26 tỷ, Cục TMĐT ≈ $31 tỷ. Không nguồn nào tự giải thích chênh lệch. Giữ nguyên, không chọn một số.
8. **YouNet:** thị phần cộng ra 103,8%.
9. **Ecomobi "GMV affiliate +105%, creator ×2,8, GMV/creator −11%":** phép tính 2,05/2,8 ra giảm ≈ 27%, không phải 11%. Chỉ thấy qua đoạn trích.
10. **"Phí sàn 30–40%":** chỉ là seller tự khai, không có sao kê.
11. **"Kalodata Starter $40, FastMoss Basic $60":** đến từ bài so sánh của Tabcut (đối thủ). Giá gốc Kalodata Starter là $21,9 (VN), $55 (SEA) hoặc $59,9 (Global).
12. **Giá "$348/năm" và "$297/năm" của Ginee** (Shopify App Store, pickyourapp): không khớp nhau, không truy được về Ginee. ChannelEngine "hỗ trợ TikTok Shop VN": trang gốc không nhắc VN.
13. **Giá gạch Haravan:** Standard và Omni Pro có giá gạch 1.000.000đ nằm trong thẻ bị ẩn. Chỉ mức giảm 20% của Omni Advanced hiển thị. Không dùng 70% hay 32%.
14. **Định giá "$200–300M" của KiotViet:** ước chừng của đại diện công ty, không rõ người nói.
15. **Chênh lệch chưa giải được:** hoa hồng Mall TikTok 15,5% hay 16%; giới hạn gói free BigSeller trên blog (1.500/3 shop và 3.000/5 shop); MISA Professional 399.000 hay 499.000đ; Sapo thành lập 2008 hay 2009; nhân sự Sapo 1.000+ hay 375.
16. **Đoạn trích tìm kiếm lệch với trang gốc (bổ sung 2026-11-06):** KiotViet trên G2 "21 ratings" (trang gốc: 2 review); Kixmon trên Trustpilot "4,5 từ 20 review" (trang gốc: 0 review); FastMoss trên G2 "2,5/5 từ 2 review" và "một review báo subscription ngừng hoạt động" (trang gốc: 5,0/5 từ 7 review, không có review 1–3★).
17. **Đoạn trích TrustMRR sai:** "Stealth Company" $94 nghìn doanh thu 30 ngày và StreamWrapped $67 nghìn (trang gốc: $330 và $0). Nguyên nhân khả dĩ là thẻ "startup khác" ở thanh bên; chỉ trang hồ sơ mới đáng tin.
18. **"90% seller TikTok Shop thất bại" và "55% shop không hoạt động":** không truy được; trang thống kê của Dashboardly, nguồn mà một bài tổng hợp gán, không có số này.
19. **Doanh thu chưa xác minh:** FastMoss ≈ $3,7 triệu/năm và HiveHQ $550 nghìn là ước tính của GetLatka; Kixmon "5.000+ seller đã theo dõi $50M lợi nhuận" là số hãng tự nói, không phải người trả tiền. Hồ sơ TrustMRR của "Mergoio" ($458/30 ngày, rao bán $15 nghìn) trả 404; việc nó trùng với "Stealth Company" chỉ dựa vào giá giống hệt.
20. **BigSeller "113 bài tiếng Việt":** cận dưới từ sitemap nhiều ngôn ngữ (4.789 URL). **KiotViet "~1.200 sales":** từ Forbes VN 03/2023, không có nguồn 2026.
21. **Ngày pentest Shopee:** trang Singapore ghi 13/07/2026 và 16/10/2026; Wizlynx ghi 01/03/2026 và nói về Thái Lan. Chưa giải được. **Sandbox TikTok:** 100 hay 1.000 yêu cầu/giờ, hai trang chính thức mâu thuẫn.
22. **Chỉ có nguồn thứ cấp:** giới hạn 7 video có giỏ hàng/7 ngày từ 24/08/2026 (Rentracks); Shopee hoãn một loại phí mới sau khi Ủy ban Cạnh tranh can thiệp (theinvestor.vn).

## 14. Chỗ đã sửa của agent (checklist yêu cầu có ít nhất một)

1. **Agent 1b nói giá VND của Kalodata "đắt hơn giá USD khoảng 20%" cho cùng gói.** Tính lại ở 26.000đ/$: Starter 549.000đ = $21,1 vs $21,9 (**rẻ hơn 3,6%**), Professional $53,8 vs $43,9 (đắt hơn 22,6%), Enterprise $328,8 vs $300 (đắt hơn 9,6%). Chỉ gói Professional khớp.
2. **Giới hạn gói free của BigSeller:** agent 1a và agent 3 thấy hai blog nói khác nhau (1.500 đơn/3 shop vs 3.000/5 shop). Giá đọc từ API của chính trang (agent 1b) ra 1.500 đơn, 3 shop, 2 user, nên mình dùng số này.
3. **Agent 3 viết Sapo liệt kê đa sàn ở "tất cả gói bán lẻ";** agent 1a đọc kỹ hơn: Sapo StartUp chỉ có 1 kênh bán. Mình dùng Sapo Pro làm mốc.
4. **Lỗi của mình trong brief:** mình giao agent 4 tìm "Ginee thuộc Ecosoft". Agent 4 kiểm ra là sai: Ginee thuộc Advance Intelligence Group.
5. **Cách lấy giá của agent 1b:** để thấy giá các nước khác của BigSeller, agent gửi header `X-Forwarded-For` giả. Không dùng làm nguồn chính; giá VN đọc từ IP Việt Nam.
6. **Lỗi của mình trong lúc báo cáo:** mình từng nói "Sapo và KiotViet cũng không thấy trên G2/Capterra". Sai: KiotViet có trang G2 (4,5/5, 2 review) và Sapo POS có hồ sơ G2 với 0 review. Agent đọc lại bằng `read-blocked` mới phát hiện ra.
7. **Agent 7 sửa lại giả định rộng:** "Finance API 202309 → 202605" thực ra chỉ là Get Payments và chỉ mất trường `reserve_amount`; hai endpoint sao kê đi theo đường khác (202309 → 202501).
8. **Agent 5 dùng biên gộp 80% cho CAC payback,** mâu thuẫn với phép kiểm tra biên gộp ở mục 8 (51–64%). Mình tính lại ở 60% và giá 650.000đ: affiliate thưởng 20% hoàn vốn 4,2–4,6 tháng thay vì 3,1–3,3 (agent, giá 700.000đ, biên 80%).
9. **Agent 5 nhận xét bảng giá Nhanh "có thể là bản cũ"** so với 250.000đ + 50.000đ. Thực ra khớp nhau: POS Basic 250.000đ cộng add-on Nhanh.Ecom 50.000đ.
10. **Đối chiếu chéo cho kết quả tốt:** agent 6 ước phân bổ sao của Kalodata trên Trustpilot từ độ rộng thanh trong ảnh (7 / 2 / 5); agent 2 đọc nguyên văn từng review ra đúng 7 review 5★, 2 review 2★, 5 review 1★. Phép tính hoàn vốn của agent 5 và các phép tính tỷ lệ suy giảm của agent 6 mình đều tính lại và khớp.
11. **Chi phí Scraping Browser:** agent 7 dùng khoảng 14 lượt (trần 12), agent 2 khoảng 17 lượt (trần 20, 13 lượt đọc được), agent 6 có 7 lượt thất bại, agent 5 có 2 lượt thất bại.

## 15. Đề xuất

**Build hay không:** có, nhưng như một sản phẩm hẹp, không phải toàn bộ PRD. Nếu mục tiêu là venture lớn thì thị trường này (SAM $0,13–13M) chưa đủ ở giá hiện tại; nếu là doanh nghiệp nhỏ–vừa hoặc công cụ cho chính mình thì hợp lý. Khoảng trống hẹp hơn lúc đầu vì Shopee đã có lãi từng đơn riêng cho Shopee (mục 1, 11).

**Vào bằng đường nào:**

1. **Lát cắt theo ba JTBD (mục 12):** lãi thật đa sàn có GMV Max, đối soát từng khoản chênh lệch kèm hồ sơ khiếu nại, và duyệt/audit cho thao tác ảnh hưởng tiền. Bỏ khỏi bản đầu: kho, in tem, đăng video, chat, livestream, tạo ảnh/video.
2. **Cách nối dữ liệu:** bắt đầu bằng nhập file báo cáo thanh toán xuất từ Seller Center để chưa phải qua cổng ISV. Đây là suy luận của mình, chưa kiểm điều khoản và chưa kiểm định dạng file VN. Làm API sau, qua đường ủy quyền chính thức (Partner Center, TSP). Không dùng user phụ hay trình duyệt tự động.
3. **Khách hàng:** shop ≥100 triệu/tháng bán cả hai sàn, cộng kế toán và agency vận hành shop làm kênh. Thông điệp: "tiền về thấp hơn giá bán vì sao".
4. **Giá thử:** 650.000đ/tháng (≈ $25), mặc định bán gói năm (≈ 7,8 triệu/năm), hạn mức 10.000 đơn/tháng và trần AI 1 triệu token/tháng. Đơn vượt hạn mức tính theo gói (benchmark BigSeller: 70–117đ/đơn). Không bán gói Unlimited. Biên gộp pha trộn ≈ 64% theo giả định ở mục 8. Không dưới Sapo Omni 449.000đ: thấp hơn là đua giá với POS rẻ và miễn phí. Đây là giả thuyết để kiểm bằng bán trước, không phải kết luận.
5. **Kênh:** content/SEO vào hai cụm "tính lãi lỗ shopee tiktok shop" và "đối soát tiền về", cộng affiliate định kỳ 15–20% trong 24 tháng (mẫu BigSeller) cho kế toán và agency. Không xây đội sales.
6. **Wedge:** gói miễn phí 1 shop nhập báo cáo hai sàn, hiện lãi thật và đối soát từng khoản chênh lệch. Khác Renda Free (làm mới 1 lần/ngày, chỉ báo cáo mẫu) ở chỗ đối soát từng khoản, không chỉ hiển thị lãi.

**Xác thực trước khi viết dòng code nào (rẻ nhất đến đắt nhất):**

1. **Kiểm tra trên tài khoản seller VN thật** xem công cụ gốc làm được gì: Shopee "Quản lý Kế toán" và báo cáo Doanh thu; TikTok Shop VN đã có Earnings Analytics/Seller Assistant chưa. Nếu chúng đã giải quyết JTBD 1 và 2 cho từng sàn thì lát cắt chỉ còn giá trị ở phần đa sàn và quảng cáo.
2. **Xin 3–5 sao kê đối soát thật** của seller (đã ẩn thông tin) để đo r, tỷ lệ thất thoát thu hồi được. Đây là biến lớn nhất không có nguồn nào.
3. **Phỏng vấn 5 seller ≥100 triệu/tháng:** đang đối soát bằng gì, Excel hay tool nào, trả bao nhiêu, có muốn thấy phí affiliate theo từng đơn không, có dùng "Quản lý Kế toán" của Shopee không.
4. **Hỏi trực tiếp Shopee VN và TikTok Shop VN** về ISV: còn mở cho đơn vị mới không, pentest có áp dụng ở VN không, điều kiện, thời gian, Ads API và API tài chính cho ISV VN. Đây là cổng chặn có thể làm hỏng cả kế hoạch.
5. **Landing + waitlist, hoặc bán trước** cho vài shop đã biết mình, kèm một câu hỏi về gói năm.
6. **Đo cohort thật** khi có khách đầu tiên: giữ chân theo tháng, vì không có dữ liệu giữ chân nào cho nhóm công cụ này.

## 16. Giới hạn của bản research này

- Không đọc được tài liệu gốc của Shopee Open Platform và TikTok Partner Center (SPA); mọi dòng API là đoạn trích tìm kiếm hoặc nguồn thứ cấp.
- Không có Facebook group, Voz, Tinhte; Reddit bị CAPTCHA; G2 và Capterra gần như trống cho thị trường này (xem mục 4). Không có dữ liệu Metric/YouNet trả phí (số shop theo dải doanh thu, mức chồng lấn Shopee ∩ TikTok).
- Chưa dùng thử bất kỳ tool nào: mọi "✓" là từ trang hãng (vendor), chưa kiểm bằng sản phẩm thật.
- Renda (đối thủ gần PRD nhất): chưa có hồ sơ công ty, chưa mở demo, chưa biết số khách.
- "Không thấy" trong ma trận không đồng nghĩa với "hãng không có".
- Kỳ tính giá của Sapo, KiotViet, Renda không được trang ghi rõ; mình giả định theo tháng.
- Số liệu thị trường 2026 (phí sàn, e-Conomy) mới trong vài tuần: kiểm lại trước khi trích.
- **Bổ sung 2026-11-06:**
    - Reddit trực tiếp bị CAPTCHA ở hai IP thoát; chỉ có bản lưu trữ Arctic Shift (hay báo "Too many requests") và PullPush (lỗi 526). Các lần trả rỗng không phải bằng chứng "không có thread".
    - Google VN không đọc được (CAPTCHA), nên các nhận định về từ khoá chỉ là proxy từ WebSearch kết quả Mỹ.
    - Meta Ad Library chỉ nạp một mẫu 50–59 quảng cáo mỗi truy vấn.
    - Capterra: chỉ có tìm kiếm nội bộ mờ cho Sapo, KiotViet, Nhanh, Haravan, Ginee, BigSeller; "không thấy" chưa phải "không có". Nhanh.vn chưa tìm được trên G2.
    - TrustMRR: không tìm thấy hồ sơ cho các hãng lớn; trang tìm kiếm chạy ở phía client.
    - Giá vốn (mục 8) và CAC (mục 9) dùng giả định của mình, chưa có số đo từ hãng nào hay từ bản chạy thử.
    - Không đọc được `open.shopee.com`, Điều khoản dịch vụ Shopee VN, danh mục TikTok Shop App & Service Store, và bản gốc chính sách giới hạn đăng nội dung của TikTok Shop.

## Tự chấm theo checklist của skill

- [x] Mọi số có nhãn, có nguồn, có ngày đọc (một số dòng ở mục 5 và 6 là đoạn trích tìm kiếm, đã ghi rõ).
- [x] TAM SAM SOM với giả định in ra (mục 7).
- [x] Cột giá từng đối thủ, ghi vùng/tiền tệ (mục 2).
- [x] Biểu đồ Giá trị × Tính năng, bảng, bộ tiêu chí và nhận định Core JTBD so với độ rộng (mục 2, 12; `chart.svg`, `ranking.md`).
- [x] Giá vốn, biên gộp ở 3 kịch bản, ngưỡng cắt lỗ cho gói Unlimited (mục 8). Hệ số tạo hỏng và chi phí trên mỗi kết quả dùng được: không áp dụng cho lát cắt đề xuất, đã ghi rõ.
- [x] Kênh phân phối gốc, CAC/LTV (mục 9), độ giữ chân thật (mục 10), rủi ro nền tảng upstream/downstream (mục 11).
- [x] Bảng hồ sơ công ty (mục 3).
- [x] Số bị từ chối in (mục 13).
- [x] Sửa ít nhất một chỗ agent sai (mục 14).
- [x] Đọc G2, Capterra, Reddit, Trustpilot, HN bằng `read-blocked` (mục 4). Reddit chỉ qua bản lưu trữ vì trực tiếp bị CAPTCHA.
- Đề xuất sửa skill `market-research`:
    - **Chuỗi bị hỏng trong SKILL.md:** "lỗ −mới.15M" (ví dụ MacPaw), "Bổ–$3k", "trục Y: điểm tính năng trên mỗi theo giá quy về một năm" (thiếu đơn vị), "(vận–theo/tháng)". Trông như hậu quả của một lần thay thế hàng loạt.
    - **Tên công cụ không khớp môi trường:** skill ghi `search_web` và "subagent `self`"; môi trường này có `WebSearch` và agent `general-purpose`.
    - **`positioning_chart.py` cố định trục Y tối thiểu 5 và đơn vị "$10/năm":** với thị trường có giá cao hơn thì điểm dồn sát đáy. Nên thêm tham số đơn vị giá.
    - Chưa sửa file nào của skill.
