# v-exam

Bộ công cụ biên soạn bài tập, tài liệu ôn tập và trộn đề thi trắc nghiệm / tự luận chuẩn định dạng Bộ Giáo dục & Đào tạo Việt Nam dành cho mọi môn học (Toán, Vật lý, Hóa học, Sinh học, Lịch sử, Địa lý, GDKT&PL,...).

---

## 🚀 Tính năng nổi bật

- **Tự động trộn đề:** Trộn đảo phương án NLC, đảo ý $a, b, c, d$ của câu hỏi Đúng/Sai, hoán vị câu hỏi theo seed mã đề.
- **Tự động xuất bảng đáp án & mã QR:** Tạo bảng đáp án tổng hợp và mã QR cho phần mềm chấm thi tự động (như Untest,...).
- **Hỗ trợ câu hỏi chùm (Dữ kiện chung):** Tự động gom nhóm các câu hỏi con đi kèm đoạn văn cảnh/dữ kiện dùng chung mà không bị xáo rời rạc.
- **Biên soạn bài tập nối tiếp (`exercise` / `baitap_inline`):** Hỗ trợ biên soạn tài liệu giảng dạy, bài tập ôn tập chuyên đề có kèm lời giải chi tiết.

---

## 📦 Hướng dẫn sử dụng

### 1. Import thư viện

```typst
#import "@preview/v-exam:0.1.0": *
```

### 2. Định dạng ngân hàng câu hỏi

Ngân hàng câu hỏi được lưu dưới dạng mảng `array` các `dictionary`:

```typst
#let data = (
// Câu hỏi đơn trắc nghiệm nhiều lựa chọn.
(
    type: "NLC",
    hv:none,//none: không có hình vẽ; nếu có hình vẽ có thể dùng image("đường dẫn) dùng cho trường hợp import hình có sẳn hoặc canvas({}) để vẽ trực tiếp
    lv: 1, //lv: 1 - Nhận biết, lv: 2 - Thông hiểu, lv: 3 - Vận dụng
    nd: [Nội dung lời dẫn],
    pa: ([Phương án A], [Phương án B], [Phương án C], [Phương án]),
    cot: 4,//cot: 1 - bố trí 1 cột, cot: 2 - bố trí 2 cột, cot: 4 - bố trí 4 cột
    da: 0, //da: 0 - đáp án đúng A, da: 1 - đáp án đúng B, da: 2 - đáp án đúng C, da: 3 - đáp án đúng D
    lg: [Lời giải cho câu hỏi],
  ),
// Câu hỏi chùm trắc nghiệm nhiều lựa chọn.
(
    type: "NLC",
    hv:none,//none: không có hình vẽ; nếu có hình vẽ có thể dùng image("đường dẫn) dùng cho trường hợp import hình có sẳn hoặc canvas({}) để vẽ trực tiếp
    lv: 1, //lv: 1 - Nhận biết, lv: 2 - Thông hiểu, lv: 3 - Vận dụng
    is_chum:true,
    du_kien:[Nội dung dùng chung],
    cau_hoi_con:(
    // Câu hỏi con 1.
    (nd: [Nội dung lời dẫn câu hỏi 1],
    pa: ([Phương án A], [Phương án B], [Phương án C], [Phương án]),
    cot: 4,//cot: 1 - bố trí 1 cột, cot: 2 - bố trí 2 cột, cot: 4 - bố trí 4 cột
    da: 0, //da: 0 - đáp án đúng A, da: 1 - đáp án đúng B, da: 2 - đáp án đúng C, da: 3 - đáp án đúng D
    lg: [Lời giải cho câu hỏi 1],),
    // Câu hỏi con 2.
    (nd: [Nội dung lời dẫn câu hỏi 2],
    pa: ([Phương án A], [Phương án B], [Phương án C], [Phương án]),
    cot: 4,//cot: 1 - bố trí 1 cột, cot: 2 - bố trí 2 cột, cot: 4 - bố trí 4 cột
    da: 0, //da: 0 - đáp án đúng A, da: 1 - đáp án đúng B, da: 2 - đáp án đúng C, da: 3 - đáp án đúng D
    lg: [Lời giải cho câu hỏi 2],)
  ),
  // Câu hỏi đúng sai
  (
    type: "TF",
    hv:none,//none: không có hình vẽ; nếu có hình vẽ có thể dùng image("đường dẫn) dùng cho trường hợp import hình có sẳn hoặc canvas({}) để vẽ trực tiếp
    lv: 2, //lv: 1 - Nhận biết, lv: 2 - Thông hiểu, lv: 3 - Vận dụng
    nd: [Lời dẫn của của câu hỏi],
    ytf: (
      [nội dung ý a],
      [nội dung ý b],
      [nội dung ý c],
      [nội dung ý d],
    ),
    da: (1, 0, 1, 0), // 1 - đúng, 0 - sai
    lg: ([Lời giải cho ý a],
        [Lời giải cho ý b],
        [Lời giải cho ý c],
        [Lời giải cho ý d],
  ),
(
    type: "TLN",
    hv:none,//none: không có hình vẽ; nếu có hình vẽ có thể dùng image("đường dẫn) dùng cho trường hợp import hình có sẳn hoặc canvas({}) để vẽ trực tiếp
    lv: 2, //lv: 1 - Nhận biết, lv: 2 - Thông hiểu, lv: 3 - Vận dụng
    nd: [Lời dẫn của của câu hỏi],
    da:so,// Số nhập có thể là số thực chứa phần thập phân hoặc không (tối đa 4 kí tự) đối với thập phân thì viết dấu "." thay cho ","
    lg:[Lời giải cho bài toán],
    dong_ke: so_dong_ke,
)
(
    type: "TL",
    hv:none,//none: không có hình vẽ; nếu có hình vẽ có thể dùng image("đường dẫn) dùng cho trường hợp import hình có sẳn hoặc canvas({}) để vẽ trực tiếp
    lv: 2, //lv: 1 - Nhận biết, lv: 2 - Thông hiểu, lv: 3 - Vận dụng
    nd: [Lời dẫn của của câu hỏi],
    lg:[Lời giải cho bài toán],
    dong_ke: so_dong_ke,
)
)
```

### 3. Biên soạn bài tập / Tài liệu ôn tập (`exercise` / `baitap_inline`)
a) Import nguồn để tạo bài tập
```typst
#import "file.typ" as b
// code tạo bài tập.
#exercise(
  b.data,
  cm: 1,
  num_nlc: (1, 0, 0),
  num_tf: (0, 1, 0),
  num_tln: (0,1,2),
  show_lg: true,
  seed: 123,
  theo_lv:true,
  dong_ke:4
)
```

### 4. Trộn đề thi khác nhau(`make-exam-matrix` / `tron_de_bankLevel`)
+
```typst
Import ngân hàng
#import "file.typ" as b
#let info = (
  so_gd: [SỞ GD&ĐT QUẢNG NGÃI],
  truong: [TRƯỜNG THPT NGUYỄN CÔNG PHƯƠNG],
  ky_thi: [KIỂM TRA GIỮA KỲ I],
  mon: [VẬT LÝ 12],
  thoi_gian: [45 phút],
  ds_ma_de: ("101", "102", "103", "104"),
)

#let matrix = (
  (
    bank: b.data,
    NLC_dem: (1, 0, 0),
    tf_dem: (0, 1, 0),
    tln_dem: (0, 1, 0),
    tl_dem: (0, 1, 0),
  ),
)

#make-exam-matrix(matrix, info, show_lg: false, hienthi_bangdapan: true)
```

---

## 📜 Giấy phép

Phát hành theo giấy phép [MIT License](LICENSE).
