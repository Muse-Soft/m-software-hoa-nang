# DESIGN.md — Landing page tiệm hoa tươi Hoa Nắng

- Nguồn yêu cầu: MSR-21 (Linear TEC-167 → Epic TEC-168, task thiết kế TEC-169)
- Repo: Muse-Soft/m-software-hoa-nang
- Sản phẩm: landing page một trang cho tiệm hoa tươi "Hoa Nắng" ở TP.HCM, visual-first — ảnh hoa lớn là nội dung chính, ít chữ, nhiều khoảng trắng.
- Nguyên tắc xuyên suốt: mọi thông số dưới đây là quyết định dứt khoát để Dev (TEC-170) làm theo và QA (TEC-171) đối chiếu. Dữ liệu thật chưa có (địa chỉ, điện thoại) để đúng chuỗi `[CẦN BỔ SUNG]`, tuyệt đối không tự bịa.

## 1. Phong cách tham chiếu

**Tên phong cách: "Floral Editorial kiểu Kinfolk"** — bố cục tạp chí hoa tối giản: ảnh hoa khổ lớn chụp ánh sáng tự nhiên làm trung tâm, tiêu đề serif thanh lịch, nền trắng ấm, rất ít chi tiết trang trí, khoảng trắng rộng như trang tạp chí in.

Lấy đúng 4 đặc điểm này:
- Ảnh chiếm tối thiểu 60% diện tích thị giác của trang; chữ chỉ đóng vai trò chú thích cho ảnh.
- Mỗi mục (section) cách nhau một khoảng trắng lớn cố định (xem mục 5), không dùng đường kẻ/ngăn cách cứng giữa các mục trừ bảng giá.
- Tối đa 1 nút nhấn (CTA) chính trong mỗi khung nhìn; CTA phụ để dạng liên kết chữ có gạch chân.
- Không dùng: nền tối, gradient màu, bo góc quá lớn kiểu ứng dụng di động, icon hoạt hình, hiệu ứng parallax.

## 2. Bảng màu (hex + vai trò)

| Mã hex | Vai trò | Dùng ở đâu |
| --- | --- | --- |
| `#FDFBF7` | Nền chính (trắng ấm) | Nền toàn trang, nền mục 1/3/5 |
| `#F5EFE6` | Nền phụ (kem nhạt) | Nền xen kẽ mục 2/4/6, nền thẻ giá khi hover |
| `#FFFFFF` | Nền thẻ | Thẻ bộ sưu tập, thẻ nhận xét, ô nhập form |
| `#2B2622` | Chữ chính | Tiêu đề, nội dung, tên mẫu hoa |
| `#6E6259` | Chữ phụ (nâu xám ấm) | Chú thích ảnh, mô tả ngắn, nhãn form, ghi chú "giá tham khảo" |
| `#D97757` | Điểm nhấn chính (hồng đào) | Nút CTA "Đặt hoa ngay", giá tiền, sao đánh giá, liên kết khi hover |
| `#BC5836` | Điểm nhấn khi tương tác | Nền CTA khi hover/active (đậm hơn `#D97757` một bậc), viền ô nhập khi focus |
| `#68785D` | Điểm nhấn phụ (xanh lá xám) | Huy hiệu "Giao hoa tươi trong ngày", dấu tích cam kết — chỉ dùng điểm xuyết, không làm nền diện rộng |
| `#E7DED2` | Viền (be nhạt) | Viền thẻ, viền ô nhập, đường kẻ bảng giá |

Chữ trên nút CTA: trắng `#FFFFFF`, Be Vietnam Pro 600. Không đặt chữ màu nhấn lên nền kem cho đoạn văn dài (độ tương phản không đủ) — màu nhấn chỉ cho chữ ngắn, giá, nút và chi tiết nhỏ.

## 3. Font chữ

| Vai trò | Font | Cỡ / trọng lượng cụ thể |
| --- | --- | --- |
| Tiêu đề (H1, H2, tên tiệm) | **Playfair Display** | H1: 56px/1.15, weight 600 (mobile 36px); H2 đầu mục: 38px/1.2, weight 600 (mobile 28px); tên mẫu hoa trong thẻ: 24px, weight 500 |
| Nội dung | **Be Vietnam Pro** | Thân bài: 17px/1.65, weight 400 (mobile 16px); mô tả thẻ: 15px/1.6, weight 400; nhãn form + chú thích: 14px, weight 500 |
| Nút + giá | **Be Vietnam Pro** | Nút CTA: 16px, weight 600; giá tiền: 20px, weight 600, màu `#D97757` (trong bảng giá: 17px, weight 600, màu `#2B2622`) |

- Nạp qua Google Fonts với `display=swap`, bắt buộc gồm subset `vietnamese` (cả hai font đều hỗ trợ tiếng Việt; thiếu subset là lỗi khi QA đối chiếu dấu tiếng Việt).
- Font dự phòng: Playfair Display → `Georgia, 'Times New Roman', serif`; Be Vietnam Pro → `Arial, Helvetica, sans-serif`.
- Không dùng thêm font thứ ba; không dùng chữ nghiêng (italic) cho nội dung tiếng Việt ngoài trích dẫn nhận xét ở mục 5.

## 4. Quy tắc hình ảnh

- **Loại ảnh:** ảnh chụp hoa thật (bó hoa, lọ hoa, hoa tại tiệm) — không dùng hình minh họa vẽ/SVG hoa, không dùng ảnh có chữ/watermark.
- **Tông ảnh:** sáng, ấm, ánh sáng tự nhiên; hoa tươi màu rõ. Loại ảnh tông tối, ảnh mờ, ảnh lệch tông lạnh/xanh dương.
- **Tỉ lệ khung theo vùng** (CSS `aspect-ratio` + `object-fit: cover`, cắt giữa khung):
  - Ảnh mở đầu (hero): **16:9** toàn chiều ngang trên desktop; mobile cắt giữa thành **4:3**.
  - Ảnh thẻ bộ sưu tập: **4:3** cho cả 3 thẻ, đồng nhất.
  - Ảnh mục giới thiệu: **4:3**.
  - Ảnh đại diện người nhận xét: **1:1** tròn; nếu không có ảnh phù hợp thì dùng vòng tròn nền `#F5EFE6` chứa chữ cái đầu tên, không lấy ảnh người lạ.
- **Ảnh mẫu:** dùng ảnh chất lượng cao từ Unsplash (URL `images.unsplash.com`, đúng chủ đề hoa, đúng tỉ lệ sau cắt) và khai báo rõ là ảnh mẫu trong comment kết quả của Dev; mọi ảnh phải có `alt` tiếng Việt mô tả mẫu hoa kèm hậu tố "(ảnh mẫu)".
- Mỗi mục tối đa số ảnh theo bố cục mục 5 — không thêm dải ảnh trang trí ngoài bố cục.

## 5. Bố cục 6 mục (theo thứ tự trên trang)

Khung chung: container tối đa **1200px**, lề hai bên 24px (mobile 16px). Khoảng cách dọc giữa hai mục: **96px** desktop / **56px** mobile. Thẻ bo góc **16px**, bóng đổ nhẹ duy nhất một kiểu: `0 8px 24px rgba(43,38,34,0.08)`. Nút CTA bo tròn hoàn toàn (`border-radius: 999px`), đệm 14px × 28px.

Thanh đầu trang (header) dính trên cùng: nền `#FDFBF7`, gồm tên tiệm "Hoa Nắng" (Playfair Display 28px), các liên kết neo: Bộ sưu tập · Bảng giá · Giới thiệu · Nhận xét · Liên hệ, và 1 nút CTA "Đặt hoa ngay" cuộn tới form ở mục 6.

1. **Mở đầu (hero):** ảnh hoa 16:9 toàn chiều ngang; khối chữ đặt trên tấm nền `#FDFBF7` ở góc trái dưới ảnh (mobile: khối chữ nằm dưới ảnh). Nội dung tối đa: tên tiệm H1 "Hoa Nắng", 1 câu giới thiệu ngắn (tiệm hoa tươi tại TP.HCM, giao hoa trong ngày), nút CTA chính "Đặt hoa ngay" và huy hiệu xanh lá `#68785D` ghi "Giao hoa tươi trong ngày". Không thêm đoạn văn dài ở mục này.
2. **Bộ sưu tập theo dịp:** lưới 3 cột (mobile 1 cột), khoảng cách thẻ 32px. Đúng 3 thẻ theo dịp khách nêu: **Sinh nhật**, **Khai trương**, **Hoa cưới**. Mỗi thẻ: ảnh 4:3, tên dịp (Playfair Display 24px), 1 dòng mô tả ≤ 15 từ, dòng "Giá từ — tham khảo" (số cụ thể do Dev điền dạng giá mẫu, ghi rõ là tham khảo), liên kết chữ "Xem bảng giá" neo xuống mục 3.
3. **Bảng giá tham khảo:** bảng tối đa 6 dòng mẫu hoa: cột Tên mẫu · Dịp phù hợp · Kích cỡ · Giá tham khảo. Đầu bảng có tiêu đề H2 "Bảng giá tham khảo"; dưới bảng bắt buộc có dòng ghi chú chữ phụ 14px: "Giá chỉ mang tính tham khảo theo mẫu, giá chốt theo yêu cầu cụ thể khi đặt hoa." Đường kẻ hàng dùng màu viền `#E7DED2`; hàng hover đổi nền sang `#F5EFE6`.
4. **Giới thiệu + cam kết giao trong ngày:** bố cục 2 cột (ảnh 4:3 bên trái, chữ bên phải; mobile xếp dọc ảnh trên chữ dưới). Đoạn giới thiệu ≤ 120 từ. Dưới đoạn văn là đúng 3 gạch đầu dòng cam kết, mỗi dòng có dấu tích màu `#68785D`: giao hoa tươi trong ngày tại TP.HCM · hoa mới cắt mỗi sáng · gói hoa theo yêu cầu và ngân sách.
5. **Nhận xét của khách hàng:** lưới 3 thẻ (mobile 1 cột), nền thẻ `#FFFFFF`. Mỗi thẻ: hàng 5 sao ký tự ★ màu `#D97757`, trích dẫn ≤ 40 từ (được phép italic), tên người nhận xét + hậu tố "(nhận xét mẫu)" bằng chữ phụ 14px — bắt buộc có hậu tố này vì chưa có nhận xét thật.
6. **Liên hệ + form đặt hoa:** bố cục 2 cột (thông tin liên hệ bên trái, form bên phải; mobile xếp dọc). Thông tin liên hệ hiển thị đúng các dòng: Địa chỉ: `[CẦN BỔ SUNG]` · Điện thoại/Zalo: `[CẦN BỔ SUNG]` · Giờ mở cửa: `[CẦN BỔ SUNG]` — không thay bằng số/địa chỉ tự nghĩ. Form đặt hoa gồm đúng 5 trường: Họ tên (bắt buộc), Số điện thoại (bắt buộc), Mẫu hoa muốn đặt (ô chọn lấy từ 3 dịp ở mục 2 + "Khác"), Ngày giao hoa (ô chọn ngày), Ghi chú (không bắt buộc). Form chỉ chạy phía trước (frontend): bấm "Gửi yêu cầu đặt hoa" thì chặn gửi thật (`preventDefault`) và hiện dòng thông báo ngay dưới form: "Đã ghi nhận thông tin tại trang này. Đây là bản demo chưa gửi dữ liệu — vui lòng gọi [CẦN BỔ SUNG] để tiệm xác nhận đơn hoa." Không được hiện thông báo giả vờ đã gửi thành công về tiệm.

Chân trang (footer): nền `#F5EFE6`, gồm tên tiệm, lại địa chỉ + điện thoại dạng `[CẦN BỔ SUNG]`, và 1 dòng nhỏ chữ phụ: "Hoa Nắng — Landing page giới thiệu tiệm hoa tươi tại TP.HCM."

## 6. Đáp ứng (responsive) + đối chiếu QA

- Điểm gãy: 1024px (lưới 3 cột → 2 cột ở mục 2/5) và 640px (mọi lưới → 1 cột, H1 36px, H2 28px, nút CTA rộng 100%).
- QA đối chiếu theo tài liệu này ở mức thị giác (§16.4): đúng 9 mã hex ở mục 2, đúng 2 font ở mục 3, đúng tỉ lệ ảnh ở mục 4, đủ 6 mục theo thứ tự ở mục 5, và 3 chuỗi `[CẦN BỔ SUNG]` còn nguyên ở mục 6/footer — thiếu bất kỳ điểm nào là chưa đạt.
