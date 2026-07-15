<div align="center">

# TEdu ✳

### Tiệm quản lý dạy học · dành cho gia sư tận tâm

*Sổ quản lý toàn diện cho gia sư / giáo viên dạy một mình — học sinh, lớp, thời khoá biểu, điểm danh, học phí, phiếu thu, điểm kiểm tra, giáo án, thư viện tài liệu — gói gọn trong **một file HTML duy nhất**, khoác giao diện tiệm văn phòng phẩm Sài Gòn thập niên 60.*

**🌐 Dùng thử ngay: [tedu-app.netlify.app](https://tedu-app.netlify.app)** — bấm **"Xem thử bản demo"**, không cần tài khoản.

![Ngôn ngữ](https://img.shields.io/badge/ng%C3%B4n%20ng%E1%BB%AF-VI%20%C2%B7%20EN%20%C2%B7%20KO-93392C)
![Một file](https://img.shields.io/badge/to%C3%A0n%20b%E1%BB%99%20app-1%20file%20HTML-B08D3F)
![Không build](https://img.shields.io/badge/build-kh%C3%B4ng%20c%E1%BA%A7n-2F5D50)
![Firebase](https://img.shields.io/badge/%C4%91%E1%BB%93ng%20b%E1%BB%99-Firebase%20(t%C3%B9y%20ch%E1%BB%8Dn)-33506B)
![Giấy phép](https://img.shields.io/badge/gi%E1%BA%A5y%20ph%C3%A9p-MIT-2B2318)

<img src="docs/screenshots/01-landing.png" alt="Trang giới thiệu TEdu" width="850">

</div>

---

## Mục lục

- [Vì sao có TEdu](#vì-sao-có-tedu)
- [Tính năng](#tính-năng)
- [Bộ sưu tập màn hình](#bộ-sưu-tập-màn-hình)
- [Dùng ngay trong 30 giây](#dùng-ngay-trong-30-giây)
- [Tự triển khai bản của riêng bạn](#tự-triển-khai-bản-của-riêng-bạn)
- [Kiến trúc & công nghệ](#kiến-trúc--công-nghệ)
- [Bảo mật & dữ liệu](#bảo-mật--dữ-liệu)
- [Ngôn ngữ](#ngôn-ngữ)
- [Giấy phép](#giấy-phép)

---

## Vì sao có TEdu

Gia sư dạy một mình thường quản lý lớp bằng sổ tay + Zalo + Excel: điểm danh chỗ này, tính tiền chỗ kia, cuối tháng ngồi cộng tay từng buổi rồi soạn tin nhắn báo phụ huynh. TEdu gom toàn bộ quy trình đó về một trang web:

**Điểm danh xong là học phí tự cộng.** Mỗi buổi điểm danh được tính thẳng vào công nợ tháng của từng học sinh theo đơn giá mỗi buổi. Đến kỳ thu chỉ cần mở *Học phí*, mọi con số đã sẵn — kèm phiếu thu in được, mã VietQR tự điền số tiền, và tin nhắn soạn sẵn gửi phụ huynh.

Toàn bộ ứng dụng nằm trong **một file `index.html`** — không cần cài đặt, không cần server, mở bằng trình duyệt là chạy. Kết nối Firebase (tuỳ chọn) để đăng nhập Google và đồng bộ đám mây nhiều thiết bị.

## Tính năng

### 👩‍🏫 Lớp học
- **Học sinh** — hồ sơ đầy đủ (trường, lớp, môn, đơn giá/buổi, phụ huynh, SĐT); thêm/sửa/xoá từng em hoặc **thêm hàng loạt bằng bảng kiểu Excel** (dán trực tiếp từ Excel/Google Sheets, tab/enter di chuyển ô như spreadsheet).
- **Ca học có nhiệm kỳ** — mỗi ca có ngày bắt đầu/kết thúc, lịch tuần, màu riêng; ca hết hạn tự chuyển vào **thống kê lớp đã kết thúc** kèm tình trạng thu học phí từng em.
- **Sổ lớp** — nhật ký từng lớp đang dạy: danh sách học sinh, toàn bộ buổi đã dạy từ đầu, ai có mặt buổi nào, đã thu tiền hay chưa.
- **Thời khoá biểu dạng lịch thật** — xem theo tuần hoặc cả tháng, có thứ/ngày/tháng, hôm nay được đóng khung, bấm vào ô là điểm danh.
- **Điểm danh** — theo từng ca từng ngày: có mặt / vắng / muộn, ghi chú buổi học; sửa lại được các buổi cũ.

### 💰 Tài chính
- **Học phí tự tính** theo số buổi thực học × đơn giá; theo dõi đã thu / còn thiếu từng em từng tháng, thanh tiến độ thu cả tháng.
- **Phiếu học phí vintage** — biên lai kiểu thư tín xưa: số sê-ri, con dấu bưu điện ngày in, dòng kẻ chấm, số tiền bằng chữ viết tay, lưới ngày đi học như thẻ bấm lỗ, dấu son **"ĐÃ THU ĐỦ"** đóng xéo khi thu đủ. In từng phiếu hoặc **in cả tháng một lượt**.
- **VietQR tự điền số tiền** còn thiếu, hoặc **tải ảnh QR của riêng bạn** lên dùng cố định.
- **Tin nhắn phụ huynh soạn sẵn** — báo học phí, báo vắng, nhận xét — bấm là copy gửi Zalo/SMS.

### 📚 Học tập
- **Điểm kiểm tra** — lưu theo môn/loại bài, **biểu đồ tiến bộ có hover** xem chi tiết từng cột điểm, thang điểm tự co giãn.
- **Giáo án & thư viện tài liệu** — soạn giáo án theo buổi; kho tài liệu nhận **mọi định dạng file** (PDF, Word, Excel, ảnh, âm thanh, video…), lưu ngay trong trình duyệt (IndexedDB), xem trước, tải về, gắn vào từng giáo án.
- **Hướng dẫn A–Z trong app** — 10 chương có minh hoạ tương tác (demo điểm danh chạy được, lịch mẫu bấm được) ngay trong mục *Hướng dẫn*.

### ☁️ Tài khoản & vận hành (khi bật Firebase)
- **Đăng nhập Google** — lần đầu đăng nhập là tự tạo sổ; mỗi giáo viên một sổ dữ liệu riêng, đồng bộ tự động (đèn "Đã đồng bộ / Đang lưu" ở sidebar).
- **Chế độ demo cho khách** — dữ liệu mẫu đầy đủ, nghịch thoải mái, không ghi gì lên mây, thoát là tự dọn.
- **Trang Quản trị** — admin thấy toàn bộ tài khoản đã đăng ký (ngày tạo, hoạt động cuối, số học sinh), **khoá/mở khoá** tài khoản (chặn từ tầng máy chủ), bật **chế độ bảo trì**, **phát thông báo** đến mọi người dùng, thêm admin khác.
- **Không có Firebase vẫn chạy** — để `TEDU_FIREBASE_CONFIG = null` là app hoạt động offline một máy, dữ liệu trong localStorage.

### 🧰 Trải nghiệm
- Ba ngôn ngữ **Tiếng Việt · English · 한국어**, đổi ngay không tải lại trang.
- **Chống mất dữ liệu nhập dở**: lỡ bấm ra ngoài form đang gõ → hộp thoại *Tiếp tục / Lưu / Bỏ*.
- **Mọi nút đều có tooltip** giải thích khi rê chuột.
- Tối ưu **iPhone/Safari** (safe-area, thanh điều hướng dưới), in ấn, sao lưu/khôi phục toàn bộ dữ liệu ra file JSON (kèm cả tài liệu trong thư viện).

## Bộ sưu tập màn hình

*(Ảnh chụp từ bản demo với dữ liệu mẫu.)*

| | |
|:---:|:---:|
| **Bảng điều khiển** — số liệu tháng, ca hôm nay, ai chưa đóng đủ<br><img src="docs/screenshots/03-dashboard.png" width="420"> | **Học sinh** — sổ cái danh sách, tem trạng thái, thao tác nhanh<br><img src="docs/screenshots/04-students.png" width="420"> |
| **Thêm hàng loạt kiểu Excel** — dán từ bảng tính, sửa như spreadsheet<br><img src="docs/screenshots/05-bulk-excel.png" width="420"> | **Sổ lớp** — nhật ký từng lớp: buổi dạy, chuyên cần, học phí<br><img src="docs/screenshots/06-so-lop.png" width="420"> |
| **Thời khoá biểu** — lịch tháng thật, mỗi ca một màu<br><img src="docs/screenshots/07-tkb-month.png" width="420"> | **Điểm danh** — có mặt / vắng / muộn, ghi chú từng buổi<br><img src="docs/screenshots/08-attendance.png" width="420"> |
| **Học phí** — tự cộng theo buổi, tiến độ thu, nút thu nhanh<br><img src="docs/screenshots/09-fees.png" width="420"> | **Phiếu học phí vintage** — dấu "ĐÃ THU ĐỦ", tiền bằng chữ, VietQR<br><img src="docs/screenshots/10-receipt.png" width="420"> |
| **Thư viện tài liệu** — mọi định dạng, xem trước, gắn vào giáo án<br><img src="docs/screenshots/11-library.png" width="420"> | **Hướng dẫn trong app** — 10 chương, minh hoạ bấm được<br><img src="docs/screenshots/12-guide.png" width="420"> |
| **Màn đăng nhập** — Google / demo / cổng quản trị<br><img src="docs/screenshots/02-login.png" width="420"> | **Giao diện tiếng Anh** — đổi VI/EN/KO tức thì<br><img src="docs/screenshots/13-dashboard-en.png" width="420"> |

## Dùng ngay trong 30 giây

1. Mở **[tedu-app.netlify.app](https://tedu-app.netlify.app)**.
2. Bấm **"Xem thử bản demo"** — vào thẳng app với 12 học sinh, 6 lớp, điểm danh, học phí, tài liệu mẫu.
3. Ưng ý thì quay lại màn đăng nhập, bấm **"Đăng nhập bằng Google"** — sổ riêng của bạn được tạo ngay, trống tinh, đồng bộ đám mây.

Hoặc chạy hoàn toàn offline: tải file [`index.html`](index.html) về, mở bằng trình duyệt (file này gắn với Firebase của bản demo — muốn sổ offline riêng, sửa `window.TEDU_FIREBASE_CONFIG = null;` là xong).

## Tự triển khai bản của riêng bạn

Bạn có thể dựng một bản TEdu độc lập (Firebase + hosting riêng, bạn làm admin) trong **~15 phút, miễn phí 100%**. Toàn bộ các bước — tạo project Firebase, bật Google Sign-In, tạo Firestore, **bộ security rules đầy đủ**, lấy config, đưa lên Netlify/Firebase Hosting, phong admin — được viết chi tiết trong:

📘 **[HUONG-DAN-TRIEN-KHAI.md](HUONG-DAN-TRIEN-KHAI.md)**

Tóm tắt:

```text
1. console.firebase.google.com → Add project
2. Authentication → bật Google
3. Firestore → tạo DB → dán security rules (có sẵn trong hướng dẫn) → Publish
4. Project settings → tạo Web app → copy firebaseConfig
5. Dán config vào index.html (dòng window.TEDU_FIREBASE_CONFIG = ...)
6. Kéo thả index.html lên app.netlify.com/drop → có link ngay
7. Authentication → Authorized domains → thêm domain vừa nhận
8. Firestore → collection `admins` → tạo doc id = email của bạn (viết thường)
```

## Kiến trúc & công nghệ

```text
index.html  (~270 KB, tất cả trong một file)
├── CSS      thiết kế "tiệm văn phòng phẩm 1960": giấy ngả vàng, khung viền kép,
│            con dấu bưu điện xoay, hoa văn fleuron, nút letterpress, bảng sổ cái
├── HTML     landing page + app shell (sidebar, 12 trang, cổng đăng nhập)
└── JS       vanilla JavaScript, không framework, không bundler
    ├── Dữ liệu     localStorage (mỗi tài khoản một khoá riêng)
    ├── Tài liệu    IndexedDB — file nhị phân lưu tại máy, không tốn phí mây
    ├── Đồng bộ     Firebase Auth (Google) + Firestore, debounce 1.5s,
    │               fallback offline khi config = null
    ├── i18n        từ điển VI/EN/KO + MutationObserver dịch giao diện động
    └── In ấn       phiếu học phí render CSS thuần, mã VietQR (img.vietqr.io)
```

- **Phông chữ:** Playfair Display · Be Vietnam Pro · Dancing Script (Google Fonts, đủ dấu tiếng Việt).
- **Bảng màu:** giấy `#F1EAD8` · mực nâu đen `#2B2318` · đỏ gạch oxblood `#93392C` · xanh rêu `#2F5D50` · vàng đồng `#B08D3F` · nền espresso `#221B12`. Tuyệt đối không có màu tím 🙂.
- **Không có bước build** — sửa file, lưu, tải lại trang là thấy thay đổi. Cập nhật bản deploy = kéo thả đè file mới lên Netlify; dữ liệu người dùng không ảnh hưởng vì nằm ở Firestore.

## Bảo mật & dữ liệu

- Khoá `apiKey` Firebase trong `index.html` là **định danh công khai theo thiết kế của Firebase**, không phải bí mật — quyền truy cập thực sự do **Firestore Security Rules** + **Authorized domains** quyết định (xem rules đầy đủ trong [hướng dẫn triển khai](HUONG-DAN-TRIEN-KHAI.md)).
- Rules bảo đảm: mỗi giáo viên **chỉ đọc/ghi được sổ của chính mình**, và chỉ khi tài khoản còn `active`; người dùng **không thể tự đổi** trạng thái/quyền của mình; chỉ admin (doc trong collection `admins`) xem được danh sách tài khoản, khoá tài khoản, bật bảo trì, phát thông báo.
- Tài khoản bị admin khoá là bị chặn từ tầng máy chủ (không đọc/ghi được gì), không phải chỉ ẩn nút trên giao diện.
- File trong thư viện tài liệu nằm **trên máy người dùng** (IndexedDB), không đưa lên mây. Nên tải bản sao lưu JSON định kỳ trong *Cài đặt*.

## Ngôn ngữ

Nút chuyển **VI / EN / 한국어** đặt ở sidebar và góc landing page. Giao diện dịch tức thì kể cả nội dung sinh động (toast, modal, tooltip). Riêng **phiếu học phí và tin nhắn phụ huynh giữ nguyên tiếng Việt** — vì người nhận là phụ huynh Việt Nam.

## Giấy phép

Phát hành theo giấy phép [MIT](LICENSE) — dùng, sửa, chia sẻ tự do; chỉ cần giữ dòng ghi công.

---

<div align="center">

*Sổ ghi chép cẩn thận ❦ TEdu · EST. 2026*

Made with ☕ by **Tai Doan** — cùng Claude

</div>
