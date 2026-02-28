[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# OnlyFans clone Full Stack App

![Expo](https://img.shields.io/badge/Expo-48-000000?logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61DAFB?logo=react&logoColor=black)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-FF9900?logo=amazonaws&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android%20%7C%20Web-blue)
![Status](https://img.shields.io/badge/Status-Active%20Prototype-2ea44f)

### OnlyFans clone app 是一個全端應用程式，包含前端與後端，重現其核心功能與操作流程。

此儲存庫包含一個 Expo + React Native 應用程式，搭配 AWS Amplify 後端（Cognito、AppSync、DataStore、S3），實作創作者平台的核心流程：
- 使用 Amplify Authenticator 的身分驗證
- 創作者列表與個人頁面瀏覽
- 訂閱 UI 狀態切換（目前為前端本地狀態）
- 建立貼文並可選擇上傳圖片
- 貼文串流渲染（含作者與媒體讀取）

## 🧭 概覽

此應用在 `app/` 下使用 `expo-router` 的檔案式路由，Amplify 後端資源則位於 `amplify/`。使用者登入後，應用會監聽 Amplify Hub 的 auth 事件，並嘗試在 AppSync 中建立對應的 `User` 紀錄。

| 區域 | 目前實作 |
|---|---|
| Frontend | Expo + React Native + Expo Router |
| Auth | Amazon Cognito via Amplify Authenticator |
| API | AWS AppSync GraphQL |
| Data sync | Amplify DataStore |
| Media | S3 via Amplify Storage |
| Platforms | iOS, Android, Web |

## ✨ 功能

- 透過 `@aws-amplify/ui-react-native` 以 Cognito 驅動驗證流程
- 使用 AppSync GraphQL 模型：`User` 與 `Post`
- 透過 Amplify DataStore 進行資料儲存與同步
- 透過 Amplify Storage 上傳與讀取 S3 媒體
- Expo Router 畫面：
  - `app/index.js` 創作者列表/首頁
  - `app/user/[id].js` 創作者個人頁 + 貼文
  - `app/newPost.js` 貼文編輯器

## 🛠️ 使用技術

（保留原始技術清單，並為清晰度擴充。）

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

`package.json` 中的其他相依套件包含：
- `expo-router`
- `@react-native-async-storage/async-storage`
- `@react-native-community/netinfo`
- `core-js`

## 🗂️ 專案結構

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
│  └─ aws-exports.js (generated locally; not committed)
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

## ✅ 先決條件

- 建議使用 Node.js 18+
- npm
- 透過 `npx expo ...` 使用 Expo CLI
- 用於佈建/拉取後端的 AWS 帳號與 Amplify CLI
- 應用程式會匯入的 Amplify 用戶端設定檔 `src/aws-exports`

## 📥 複製儲存庫 🔧

```bash
https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app
```

等效指令：

```bash
git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ 安裝 🔧

（保留原始安裝指令。）

```bash
npm install

npx expo start or npm start
```

儲存庫腳本：

```bash
npm start
npm run android
npm run ios
npm run web
```

## 🔐 設定

### Amplify 後端

應用在 `app/_layout.js` 中匯入 `../src/aws-exports`。該檔案未提交，需在本機產生。

典型設定流程（根據已提交的 `amplify/` 資料夾與 `.gitignore` 推定）：

```bash
npm install -g @aws-amplify/cli
amplify pull
```

若出現提示，請在你的 AWS 帳號中使用既有的 Amplify 專案/環境。已提交的後端設定顯示：
- Auth：Cognito（email username，註冊屬性包含 `NAME` 與 `NICKNAME`）
- API：AppSync + 設定中啟用 API key auth
- Storage：已設定 S3 bucket resource

### Expo / Babel / Router

- `babel.config.js` 包含：
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`
- `index.js` 初始化 `core-js/full/symbol/async-iterator` 與 `expo-router/entry`

## ▶️ 使用方式

1. 啟動應用程式：
   ```bash
   npm start
   ```
2. 在 Expo Go / 模擬器 / Web 開啟。
3. 透過 Amplify Authenticator UI 註冊/登入。
4. 在首頁瀏覽創作者。
5. 開啟創作者個人頁（`/user/[id]`）。
6. 在 UI 中切換訂閱狀態。
7. 從 `New post` 建立新貼文，並可選擇從媒體庫附加圖片。

## 🧱 資料模型

來自 `amplify/backend/api/OnlyFansCloneApp/schema.graphql`：

- `User`：`id`、`name`、`handle`、`bio`、`avatar`、`coverImage`、`subscriptionPrice`、與貼文關聯
- `Post`：`id`、`text`、`image`、`likes`、`userID`

目前 schema 中兩個模型都使用 public auth 規則。

| Model | Key fields |
|---|---|
| `User` | `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` |
| `Post` | `id`, `text`, `image`, `likes`, `userID` |

## 📱 應用程式範例

### 你需要建立免費帳號才能使用此應用程式

![Screenshot_20230424-200925](https://user-images.githubusercontent.com/64506662/234364566-863bc1e1-e289-4b9b-9658-a11e737bebd8.png)
![Screenshot_20230424-200957](https://user-images.githubusercontent.com/64506662/234364579-8e32708f-cb69-4c1c-82e3-eefd7cb5f161.png)
![Screenshot_20230424-201003](https://user-images.githubusercontent.com/64506662/234364622-e9cc5d14-77f2-415f-9027-1d3ffe3e7c17.png)
![Screenshot_20230424-201006](https://user-images.githubusercontent.com/64506662/234364653-73de6b92-b7a6-4ef7-a3a6-c26411bfd46a.png)
![Screenshot_20230424-201031](https://user-images.githubusercontent.com/64506662/234364754-f5ce7da1-1ad1-4e90-bf85-40add436ad23.png)

## 🧪 開發備註

- `app/_layout.js` 會監聽 Amplify Hub 的 `auth` 登入事件，並執行 `createUser` GraphQL mutation。
- 新貼文透過 DataStore 儲存，選用圖片則以 `Storage.put` 上傳。
- 個人頁的訂閱行為目前僅為本地 UI 狀態，尚未持久化為後端訂閱模型。
- 儲存庫目前沒有明確的自動化測試套件或 CI workflow 檔案。

## 🩺 疑難排解

- `Cannot find module '../src/aws-exports'`：
  - 執行 `amplify pull`（或等效 Amplify 初始化流程）以產生本機設定。
- Auth 正常但資料操作失敗：
  - 確認 Amplify 環境中的 AppSync/API key/auth mode 設定與本機產生設定一致。
- 圖片上傳問題：
  - 檢查 Amplify storage 的 S3 權限，並確認裝置已授予媒體庫存取權。
- 貼文串流/個人頁資料為空：
  - 確認已有 `User`/`Post` 種子資料，且目前 auth 規則允許讀取操作。

## 🗺️ 路線圖

- 新增可持久化的訂閱關係與授權檢查
- 為貼文建立/上傳流程加入驗證與更完整的錯誤處理
- 新增測試（unit/integration/e2e）與 CI pipeline
- 新增多語 README 版本並填充 `i18n/` 資源
- 強化 auth/access 規則（在需要處取代過寬的 public 規則）

## 🤝 貢獻

歡迎貢獻。

建議流程：

```bash
git checkout -b feat/your-change
# implement change
git commit -m "feat: describe change"
git push origin feat/your-change
```

接著建立 Pull Request，並說明：
- 變更內容
- 變更原因
- 如何執行/測試

## 📄 授權

此儲存庫目前沒有 `LICENSE` 檔案。

推定：除非維護者新增明確授權檔案，否則預設為保留所有權利。
