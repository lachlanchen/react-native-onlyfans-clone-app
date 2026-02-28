[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# Ứng dụng Full Stack bản sao OnlyFans

![Expo](https://img.shields.io/badge/Expo-48-000000?logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61DAFB?logo=react&logoColor=black)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-FF9900?logo=amazonaws&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android%20%7C%20Web-blue)
![Status](https://img.shields.io/badge/Status-Active%20Prototype-2ea44f)

### Ứng dụng bản sao OnlyFans là một ứng dụng full stack, bao gồm front-end và back-end cho di động, tái tạo các tính năng và chức năng tương tự.

Repository này chứa ứng dụng Expo + React Native với backend AWS Amplify (Cognito, AppSync, DataStore, S3), triển khai các luồng cốt lõi của nền tảng creator:
- Xác thực bằng Amplify Authenticator
- Danh sách creator và duyệt hồ sơ
- Chuyển trạng thái đăng ký (subscription) trên UI (phía client trong triển khai hiện tại)
- Tạo bài viết kèm tùy chọn tải ảnh lên
- Hiển thị feed bài viết với thông tin tác giả và media

## 🧭 Tổng quan

Ứng dụng sử dụng định tuyến theo file với `expo-router` trong `app/`, trong khi tài nguyên backend Amplify được theo dõi trong `amplify/`. Khi người dùng đăng nhập, ứng dụng lắng nghe các sự kiện auth từ Amplify Hub và cố gắng tạo bản ghi `User` tương ứng trong AppSync.

| Khu vực | Triển khai hiện tại |
|---|---|
| Frontend | Expo + React Native + Expo Router |
| Auth | Amazon Cognito qua Amplify Authenticator |
| API | AWS AppSync GraphQL |
| Đồng bộ dữ liệu | Amplify DataStore |
| Media | S3 qua Amplify Storage |
| Nền tảng | iOS, Android, Web |

## ✨ Tính năng

- Luồng xác thực dùng Cognito qua `@aws-amplify/ui-react-native`
- Mô hình AppSync GraphQL cho `User` và `Post`
- Lưu trữ và đồng bộ dữ liệu qua Amplify DataStore
- Tải lên và truy xuất media S3 qua Amplify Storage
- Các màn hình Expo Router:
  - `app/index.js` danh sách creator/trang chủ
  - `app/user/[id].js` hồ sơ creator + bài viết
  - `app/newPost.js` màn hình soạn bài

## 🛠️ Xây dựng với

(Danh sách stack gốc được giữ nguyên và mở rộng để rõ ràng hơn.)

```text
Expo
React
React Native
Expo crypto
Expo image picker
Expo linking
Aws amplify/ ui-react-native
Amazon cognito identity-js
Aws-amplify
Javascript
StyleSheet
React Native gesture handler
React native reanimated
```

Các dependency bổ sung trong repository tại `package.json` bao gồm:
- `expo-router`
- `@react-native-async-storage/async-storage`
- `@react-native-community/netinfo`
- `core-js`

## 🗂️ Cấu trúc dự án

```text
.
├─ app/
│  ├─ _layout.js
│  ├─ index.js
│  ├─ newPost.js
│  └─ user/[id].js
├─ src/
│  ├─ components/
│  │  ├─ Post.js
│  │  ├─ UserCard.js
│  │  └─ UserProfileHeader.js
│  ├─ models/
│  └─ aws-exports.js (được tạo cục bộ; không commit)
├─ amplify/
│  └─ backend/
│     ├─ api/OnlyFansCloneApp/schema.graphql
│     ├─ auth/OnlyFansCloneApp/
│     └─ storage/s3onlyfanscloneappstorageb3e1fac4/
├─ i18n/
├─ app.json
├─ babel.config.js
├─ index.js
└─ package.json
```

## ✅ Điều kiện tiên quyết

- Khuyến nghị Node.js 18+
- npm
- Dùng Expo CLI qua `npx expo ...`
- Tài khoản AWS và Amplify CLI để cấp phát/kéo backend
- File cấu hình Amplify client đã tạo được app import dưới tên `src/aws-exports`

## 📥 Clone repo 🔧

```bash
https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app
```

Lệnh tương đương:

```bash
git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ Cài đặt 🔧

(Các lệnh cài đặt gốc được giữ nguyên.)

```bash
npm install

npx expo start or npm start
```

Các script trong repository:

```bash
npm start
npm run android
npm run ios
npm run web
```

## 🔐 Cấu hình

### Amplify backend

Ứng dụng import `../src/aws-exports` trong `app/_layout.js`. File đó không được commit và cần được tạo cục bộ.

Luồng thiết lập điển hình (giả định dựa trên thư mục `amplify/` đã commit và `.gitignore`):

```bash
npm install -g @aws-amplify/cli
amplify pull
```

Nếu được hỏi, hãy dùng dự án/môi trường Amplify hiện có từ tài khoản AWS của bạn. Cấu hình backend đã commit cho thấy:
- Auth: Cognito (username bằng email, thuộc tính đăng ký gồm `NAME` và `NICKNAME`)
- API: AppSync + bật API key auth trong cấu hình
- Storage: đã cấu hình tài nguyên S3 bucket

### Expo / Babel / Router

- `babel.config.js` bao gồm:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`
- `index.js` khởi tạo `core-js/full/symbol/async-iterator` và `expo-router/entry`

## ▶️ Cách sử dụng

1. Khởi động ứng dụng:
   ```bash
   npm start
   ```
2. Mở bằng Expo Go/emulator/web.
3. Đăng ký/đăng nhập qua giao diện Amplify Authenticator.
4. Duyệt creator ở màn hình trang chủ.
5. Mở hồ sơ creator (`/user/[id]`).
6. Chuyển trạng thái subscription trên UI.
7. Tạo bài viết mới từ `New post`, có thể đính kèm ảnh từ thư viện media.

## 🧱 Mô hình dữ liệu

Từ `amplify/backend/api/OnlyFansCloneApp/schema.graphql`:

- `User`: `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`, quan hệ tới bài viết
- `Post`: `id`, `text`, `image`, `likes`, `userID`

Cả hai mô hình đều đang dùng quy tắc auth public trong schema hiện tại.

| Model | Trường chính |
|---|---|
| `User` | `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` |
| `Post` | `id`, `text`, `image`, `likes`, `userID` |

## 📱 Ví dụ ứng dụng

### Bạn cần tạo tài khoản miễn phí để sử dụng ứng dụng

![Screenshot_20230424-200925](https://user-images.githubusercontent.com/64506662/234364566-863bc1e1-e289-4b9b-9658-a11e737bebd8.png)
![Screenshot_20230424-200957](https://user-images.githubusercontent.com/64506662/234364579-8e32708f-cb69-4c1c-82e3-eefd7cb5f161.png)
![Screenshot_20230424-201003](https://user-images.githubusercontent.com/64506662/234364622-e9cc5d14-77f2-415f-9027-1d3ffe3e7c17.png)
![Screenshot_20230424-201006](https://user-images.githubusercontent.com/64506662/234364653-73de6b92-b7a6-4ef7-a3a6-c26411bfd46a.png)
![Screenshot_20230424-201031](https://user-images.githubusercontent.com/64506662/234364754-f5ce7da1-1ad1-4e90-bf85-40add436ad23.png)

## 🧪 Ghi chú phát triển

- `app/_layout.js` lắng nghe sự kiện đăng nhập `auth` từ Amplify Hub và thực thi mutation GraphQL `createUser`.
- Bài viết mới được lưu bằng DataStore và ảnh tùy chọn được tải lên bằng `Storage.put`.
- Hành vi subscription trên profile hiện chỉ là trạng thái UI cục bộ và chưa được lưu như mô hình subscription ở backend.
- Repository hiện chưa có bộ test tự động hoặc file workflow CI rõ ràng.

## 🩺 Khắc phục sự cố

- `Cannot find module '../src/aws-exports'`:
  - Chạy `amplify pull` (hoặc luồng khởi tạo Amplify tương đương) để tạo cấu hình cục bộ.
- Auth hoạt động nhưng thao tác dữ liệu thất bại:
  - Xác nhận cấu hình AppSync/API key/chế độ auth trong môi trường Amplify khớp với cấu hình local đã tạo.
- Lỗi tải ảnh lên:
  - Kiểm tra quyền S3 trong Amplify storage và đảm bảo thiết bị có quyền truy cập thư viện media.
- Feed/profile trống dữ liệu:
  - Đảm bảo có bản ghi `User`/`Post` đã seed và quy tắc auth hiện tại cho phép thao tác đọc.

## 🗺️ Lộ trình

- Thêm quan hệ subscription được lưu bền vững và kiểm tra entitlement
- Thêm validate và xử lý lỗi đầy đủ hơn cho luồng tạo bài/tải ảnh lên
- Thêm test (unit/integration/e2e) và pipeline CI
- Thêm các biến thể README đa ngôn ngữ và bổ sung tài nguyên `i18n/`
- Siết chặt quy tắc auth/access (thay các quy tắc public quá rộng khi cần)

## 🤝 Đóng góp

Mọi đóng góp đều được chào đón.

Luồng đề xuất:

```bash
git checkout -b feat/your-change
# implement change
git commit -m "feat: describe change"
git push origin feat/your-change
```

Sau đó mở Pull Request với:
- Nội dung đã thay đổi
- Lý do thay đổi
- Cách chạy/test

## 📄 Giấy phép

Hiện tại repository này chưa có file `LICENSE`.

Giả định: mặc định mọi quyền được bảo lưu trừ khi maintainer bổ sung file giấy phép rõ ràng.
