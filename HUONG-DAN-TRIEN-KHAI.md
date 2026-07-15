# Đưa TEdu vào hoạt động — hướng dẫn từ A đến Z

Tổng thời gian: ~15 phút. Miễn phí 100% (gói Spark của Firebase).
Kết quả: web chạy online, đăng nhập bằng Google, mỗi giáo viên một sổ dữ liệu riêng đồng bộ đám mây, bạn là quản trị viên có quyền khoá tài khoản, bật bảo trì, phát thông báo.

---

## Bước 1 — Tạo dự án Firebase (3 phút)

1. Mở https://console.firebase.google.com → đăng nhập Google → **Add project**.
2. Đặt tên, ví dụ `tedu-app` → Continue. Google Analytics: chọn **Disable** cho gọn → Create project.

## Bước 2 — Bật đăng nhập Google (1 phút)

1. Menu trái: **Build → Authentication** → Get started.
2. Tab **Sign-in method** → chọn **Google** → gạt **Enable** → chọn support email → Save.

## Bước 3 — Tạo cơ sở dữ liệu Firestore (2 phút)

1. Menu trái: **Build → Firestore Database** → Create database.
2. Location: chọn `asia-southeast1 (Singapore)` → Next.
3. Chọn **Start in production mode** → Create.
4. Vào tab **Rules**, XOÁ hết nội dung cũ, dán nguyên khối dưới đây → **Publish**:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{db}/documents {

    function signedIn() { return request.auth != null; }
    function isAdmin() {
      return signedIn()
        && exists(/databases/$(db)/documents/admins/$(request.auth.token.email.lower()));
    }
    function ownerActive(uid) {
      return signedIn() && request.auth.uid == uid
        && get(/databases/$(db)/documents/users/$(uid)).data.status == 'active';
    }

    // Hồ sơ tài khoản
    match /users/{uid} {
      allow get: if signedIn() && (request.auth.uid == uid || isAdmin());
      allow list: if isAdmin();
      allow create: if signedIn() && request.auth.uid == uid
        && request.resource.data.status == 'active'
        && request.resource.data.role == 'user';
      // Người dùng tự cập nhật hồ sơ nhưng KHÔNG được tự đổi status/role
      allow update: if isAdmin()
        || ( signedIn() && request.auth.uid == uid
             && !request.resource.data.diff(resource.data).affectedKeys().hasAny(['status','role']) );
      allow delete: if isAdmin();

      // Sổ dữ liệu của từng giáo viên — chỉ chủ tài khoản ĐANG HOẠT ĐỘNG đọc/ghi được
      match /data/{doc} {
        allow read, write: if ownerActive(uid);
      }
    }

    // Danh sách quản trị viên (doc id = email viết thường)
    match /admins/{email} {
      allow get: if signedIn() && (request.auth.token.email.lower() == email || isAdmin());
      allow list: if isAdmin();
      allow create, delete: if isAdmin();
      allow update: if false;
    }

    // Cấu hình hệ thống: bảo trì + thông báo
    match /system/{doc} {
      allow read: if signedIn();
      allow write: if isAdmin();
    }
  }
}
```

## Bước 4 — Lấy config và dán vào file web (2 phút)

1. Bấm biểu tượng **⚙ → Project settings** → kéo xuống **Your apps** → bấm biểu tượng **`</>`** (Web).
2. Đặt nickname `tedu-web` → Register app (KHÔNG cần tick Hosting ở bước này).
3. Firebase hiện đoạn `const firebaseConfig = {...}` — copy phần trong `{...}`.
4. Mở file `TEdu-quan-ly-hoc-sinh.html` bằng trình soạn thảo bất kỳ (TextEdit/Notepad/VS Code), tìm dòng:
   `window.TEDU_FIREBASE_CONFIG = null;`
   đổi thành (dán config của bạn):
   ```js
   window.TEDU_FIREBASE_CONFIG = {
     apiKey: "AIza....",
     authDomain: "tedu-app.firebaseapp.com",
     projectId: "tedu-app",
     appId: "1:1234567890:web:abc123"
   };
   ```
   Lưu file. (Để `null` thì web chạy chế độ offline một máy như cũ.)

## Bước 5 — Đưa web lên mạng (2 phút)

Cách dễ nhất — **Netlify Drop** (không cần cài gì):
1. Đổi tên file thành `index.html`.
2. Mở https://app.netlify.com/drop → kéo thả file vào → nhận link dạng `https://ten-gi-do.netlify.app`.
3. (Tuỳ chọn) Đổi tên miền phụ trong Site settings, hoặc gắn tên miền riêng.

Cách chính chủ — **Firebase Hosting** (cần Node.js):
```bash
npm i -g firebase-tools
firebase login
mkdir tedu && cd tedu && mkdir public
# chép file index.html vào thư mục public/
firebase init hosting   # chọn project tedu-app, public dir = public, single-page: No
firebase deploy
```
→ nhận link `https://tedu-app.web.app`.

## Bước 6 — Cho phép tên miền đăng nhập (1 phút)

Firebase Console → **Authentication → Settings → Authorized domains** → **Add domain** → dán domain vừa có (vd `ten-gi-do.netlify.app`). Thiếu bước này sẽ báo lỗi `auth/unauthorized-domain` khi đăng nhập.

## Bước 7 — Phong mình làm quản trị viên (1 phút)

1. Firestore Database → **Start collection** → Collection ID: `admins` → Next.
2. **Document ID**: gõ đúng email Google của bạn, VIẾT THƯỜNG toàn bộ (vd `xuantai.net@gmail.com`).
3. Thêm field: `at` (string) = ngày hôm nay. → Save.
4. Mở web → đăng nhập bằng email đó → sidebar hiện mục **Quản trị**.

---

## Ba lối vào ở màn đăng nhập

1. **Đăng nhập bằng Google** — dành cho giáo viên. Lần đầu = đăng ký, tự tạo sổ riêng.
2. **Xem thử bản demo** — khách bấm vào là dùng ngay, không cần tài khoản: dữ liệu mẫu đầy đủ (12 học sinh, lớp, điểm danh, học phí, tài liệu), thao tác thoải mái, không ghi gì lên đám mây, thoát demo là dữ liệu tự xoá.
3. **Đăng nhập quản trị →** (góc phải dưới) — cổng riêng cho admin: đăng nhập Google xong đáp thẳng vào trang Quản trị. Email không nằm trong danh sách `admins` thì được báo "không có quyền quản trị" và vào chế độ giáo viên bình thường.

## Dùng hàng ngày

- Ai mở link cũng thấy trang giới thiệu → bấm vào là màn **Đăng nhập bằng Google** — lần đầu đăng nhập tức là đăng ký, tự tạo sổ riêng.
- Dữ liệu của mỗi tài khoản tách biệt hoàn toàn, đồng bộ tự động (góc sidebar có đèn "Đã đồng bộ / Đang lưu").
- **Trang Quản trị** (chỉ admin thấy): danh sách toàn bộ tài khoản (ngày đăng ký, hoạt động cuối, số học sinh), nút **Khoá / Mở khoá** từng tài khoản (khoá là chặn từ tầng máy chủ, không đọc/ghi được gì), bật **Chế độ bảo trì** (chặn tất cả trừ admin), **phát thông báo** hiện ở Tổng quan của mọi người, thêm quản trị viên khác bằng email.
- **Cập nhật phiên bản web**: sửa file `index.html` → kéo thả đè lên Netlify (hoặc `firebase deploy` lại) → người dùng tải lại trang là dùng bản mới. Dữ liệu không bị ảnh hưởng vì nằm ở Firestore.

## Lưu ý

- **Thư viện tài liệu** (file PDF/ảnh...) lưu trên máy từng người (IndexedDB), KHÔNG đồng bộ đám mây — tránh phát sinh phí lưu trữ. Sổ liệu (học sinh, điểm danh, học phí, điểm, giáo án chữ) đồng bộ đầy đủ.
- Gói miễn phí Spark: 50.000 lượt đọc + 20.000 lượt ghi Firestore mỗi NGÀY — vài trăm giáo viên dùng thoải mái.
- Sao lưu JSON trong Cài đặt vẫn hoạt động — nên tải định kỳ cho chắc.
- Muốn xoá quyền admin của ai: vào Firestore → collection `admins` → xoá document email đó.
