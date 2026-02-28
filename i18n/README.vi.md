[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# Ứng dụng Full Stack clone OnlyFans

![Expo](https://img.shields.io/badge/Expo-48-000000?logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61DAFB?logo=react&logoColor=black)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-FF9900?logo=amazonaws&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android%20%7C%20Web-blue)
![Status](https://img.shields.io/badge/Status-Active%20Prototype-2ea44f)
![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?logo=nodedotjs&logoColor=white)
![Repo%20Size](https://img.shields.io/github/repo-size/GonzaloVolonterio/react-native-onlyfans-clone-app?label=Repo%20Size&color=0f766e)

Ngôn ngữ: **English (bản nháp hiện tại)**. Bản dịch có sẵn trong thư mục `i18n/`.

### Ứng dụng clone OnlyFans là một ứng dụng full-stack cho di động và web mô phỏng các luồng và tính năng kiểu nền tảng creator.

Kho lưu trữ này chứa một ứng dụng Expo + React Native với backend AWS Amplify (`Cognito`, `AppSync`, `DataStore`, `S3`) triển khai bản sao nền tảng dành cho creator. Ứng dụng bao gồm xác thực, duyệt creator, tạo bài viết, tải lên media và các luồng UI cho đăng ký.

## 🧭 Tổng quan

Ứng dụng được xây dựng với Expo Router trong `app/` và một lớp dữ liệu Amplify local, liên kết với các tài nguyên backend đã commit trong `amplify/`.

| Khu vực | Triển khai hiện tại |
|---|---|
| Frontend | Expo + React Native + Expo Router |
| Định tuyến | Định tuyến theo file trong `app/` |
| Auth | Amazon Cognito qua `@aws-amplify/ui-react-native` |
| API | AWS AppSync GraphQL |
| Đồng bộ dữ liệu | Amplify DataStore |
| Media | S3 qua Amplify Storage |
| Nền tảng | iOS, Android, Web |

Khi đăng nhập, `app/_layout.js` lắng nghe sự kiện auth từ Amplify Hub và cố gắng tạo bản ghi `User` trong AppSync. Việc này diễn ra khi app khởi động.

## ✨ Tính năng

- Luồng xác thực dùng Cognito cùng với Amplify Authenticator
- Mô hình AppSync GraphQL cho `User` và `Post`
- Lưu trữ và đồng bộ dữ liệu qua Amplify DataStore
- Tải lên và lấy ảnh S3 qua Amplify Storage
- Định tuyến theo file trong Expo Router:
  - `app/index.js`: danh sách creator và bảng tin chính
  - `app/user/[id].js`: hồ sơ creator và bài viết
  - `app/newPost.js`: soạn bài viết mới
- Các component giao diện tái sử dụng:
  - `src/components/UserCard.js`
  - `src/components/UserProfileHeader.js`
  - `src/components/Post.js`

## 🛠️ Xây dựng với

```text
Expo 48
React 18.2.0
React Native 0.71.6
Expo Router
AWS Amplify (+ ui-react-native)
Amazon Cognito
AppSync
DataStore
S3
expo-image-picker
expo-crypto
expo-router
react-native-reanimated
react-native-gesture-handler
```

Các phụ thuộc bổ sung từ `package.json` bao gồm:
- `@react-native-async-storage/async-storage`
- `@react-native-community/netinfo`
- `core-js`
- `expo-constants`, `expo-linking`, `expo-updates`, và các công cụ icon/screen

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
│  │  ├─ index.js
│  │  ├─ schema.js
│  │  └─ schema.d.ts
│  └─ aws-exports.js (được tạo cục bộ; chưa được commit)
├─ amplify/
│  ├─ backend/
│  │  ├─ api/OnlyFansCloneApp/schema.graphql
│  │  ├─ auth/OnlyFansCloneApp/
│  │  └─ storage/s3onlyfanscloneappstorageb3e1fac4/
│  ├─ cli.json
│  └─ team-provider-info.json
├─ i18n/
│  ├─ README.ar.md
│  ├─ README.de.md
│  ├─ README.es.md
│  ├─ README.fr.md
│  ├─ README.ja.md
│  ├─ README.ko.md
│  ├─ README.ru.md
│  ├─ README.vi.md
│  ├─ README.zh-Hans.md
│  └─ README.zh-Hant.md
├─ app.json
├─ babel.config.js
├─ index.js
├─ package.json
└─ package-lock.json
```

## ✅ Điều kiện tiên quyết

- Node.js 18+ (hoặc bản LTS hiện đại)
- npm
- Expo CLI (có thể chạy qua `npx expo`)
- Tài khoản AWS và Amplify CLI nếu cần tạo `src/aws-exports.js`
- Máy giả lập Apple/Android hoặc thiết bị vật lý cài Expo Go để test app

## 📥 Clone repo 🔧

```bash
git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ Cài đặt 🔧

```bash
npm install
```

Scripts trong `package.json`:

```bash
npm start
npm run android
npm run ios
npm run web
```

Sau đó khởi chạy app:

```bash
npm start
```

## 🔐 Cấu hình

### Backend Amplify

Ứng dụng import `../src/aws-exports` trong `app/_layout.js`. File này bắt buộc phải có lúc chạy và được tạo ở local nên không được commit.

Thiết lập local điển hình:

```bash
npm install -g @aws-amplify/cli
amplify pull
```

Nếu được hỏi, hãy chọn dự án/môi trường AWS Amplify đã tồn tại cho kho này.

### Giả định mô hình dữ liệu từ schema đã commit

- `User`: bao gồm các trường `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`, và quan hệ tới `Post`
- `Post`: bao gồm các trường `id`, `text`, `image`, `likes`, `userID`
- Cả hai mô hình hiện đang được cấu hình để đọc công khai ở mức public trong schema/auth config đã commit

### Expo / routing / Babel

- `index.js` kết nối entry của React Native và `expo-router/entry`
- `babel.config.js` bao gồm `expo-router/babel`, `react-native-reanimated/plugin`, và plugin export namespace

## ▶️ Cách sử dụng

1. Cài dependencies và tạo/nhận `src/aws-exports.js` local
2. Khởi chạy Metro:
   ```bash
   npm start
   ```
3. Mở app trong Expo Go, trình giả lập, hoặc web
4. Đăng ký / đăng nhập qua Authenticator
5. Duyệt các creator tại `/`
6. Mở hồ sơ creator tại `/user/:id`
7. Chuyển trạng thái đăng ký trong UI
8. Tạo bài viết tại `/newPost`, có thể đính kèm media tùy chọn

## 🧱 Ghi chú mô hình dữ liệu

Các model được định nghĩa trong `amplify/backend/api/OnlyFansCloneApp/schema.graphql` và `src/models/schema.js`.

| Mô hình | Trường chính |
|---|---|
| `User` | `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` |
| `Post` | `id`, `text`, `image`, `likes`, `userID` |

## 📱 Ví dụ

### Ảnh chụp màn hình demo

![Screenshot_20230424-200925](https://user-images.githubusercontent.com/64506662/234364566-863bc1e1-e289-4b9b-9658-a11e737bebd8.png)
![Screenshot_20230424-200957](https://user-images.githubusercontent.com/64506662/234364579-8e32708f-cb69-4c1c-82e3-eefd7cb5f161.png)
![Screenshot_20230424-201003](https://user-images.githubusercontent.com/64506662/234364622-e9cc5d14-77f2-415f-9027-1d3ffe3e7c17.png)
![Screenshot_20230424-201006](https://user-images.githubusercontent.com/64506662/234364653-73de6b92-b7a6-4ef7-a3a6-c26411bfd46a.png)
![Screenshot_20230424-201031](https://user-images.githubusercontent.com/64506662/234364754-f5ce7da1-1ad1-4e90-bf85-40add436ad23.png)

## 🧪 Ghi chú phát triển

- `app/_layout.js` đăng ký Amplify bằng `Amplify.configure` và đăng ký lắng nghe sự kiện `auth` của Hub.
- Mỗi khi đăng nhập, mã sẽ kích hoạt mutation `createUser` để khởi tạo bản ghi backend.
- `app/newPost.js` tải lên ảnh tùy chọn, tạo payload bài viết, sau đó lưu qua `DataStore.save`.
- `src/components/Post.js` giải quyết tác giả và URL ảnh động khi render từng item trong feed.
- Dữ liệu backend và seed hiện đang tối thiểu/không có script thiết lập tự động trong repo.
- Repo hiện chưa có test suite hay workflow CI riêng.

## 🩺 Xử lý sự cố

- `Cannot find module '../src/aws-exports'`
  - Chạy `amplify pull` (hoặc luồng `amplify init` tương ứng) từ gốc repo để tạo cấu hình local.
- Xác thực thành công nhưng query/mutation lỗi
  - Kiểm tra lại AppSync/API key/chế độ auth và region có khớp với cấu hình đã import không.
- Tải ảnh lên thất bại
  - Kiểm tra quyền `Storage` đã có và app có quyền truy cập thư viện media.
- Dữ liệu creator/feed trống
  - Xác nhận có bản ghi khởi tạo `User`/`Post` trong DataStore/AppSync và quy tắc đọc công khai phù hợp với use case của bạn.
- Trạng thái subscription của bài viết không được lưu
  - Triển khai hiện tại dường như chỉ lưu state trong UI; mô hình entitlement backend chưa được triển khai.

## 🗺️ Lộ trình

- Lưu trữ quan hệ subscription/entitlement trong các model backend
- Thêm seed data và quy trình reset thân thiện với migration dữ liệu
- Cải thiện validation cho bài viết và trạng thái lỗi
- Thêm automated tests (unit/integration/e2e)
- Thêm CI/CD cùng lint/type checks
- Mở rộng tài liệu quốc tế hóa và giữ đồng bộ các README i18n
- Tăng cường quy tắc auth và truy cập dữ liệu khi cần

## 🤝 Đóng góp

Mọi đóng góp đều được chào đón.

Luồng đề xuất:

```bash
git checkout -b feat/your-change
# implement change
git commit -m "feat: describe your change"
git push origin feat/your-change
```

Sau đó mở Pull Request với:
- Nội dung thay đổi
- Lý do thay đổi
- Cách chạy/test

## 📄 Giấy phép

Hiện tại repository này chưa có file `LICENSE`.

Giả định: mặc định mọi quyền được bảo lưu trừ khi maintainer bổ sung file giấy phép rõ ràng.


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
