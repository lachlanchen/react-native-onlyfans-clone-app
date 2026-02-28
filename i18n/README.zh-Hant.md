[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# OnlyFans clone Full Stack App

![Expo](https://img.shields.io/badge/Expo-48-000000?logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61DAFB?logo=react&logoColor=black)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-FF9900?logo=amazonaws&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android%20%7C%20Web-blue)
![Status](https://img.shields.io/badge/Status-Active%20Prototype-2ea44f)
![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?logo=nodedotjs&logoColor=white)
![Repo%20Size](https://img.shields.io/github/repo-size/GonzaloVolonterio/react-native-onlyfans-clone-app?label=Repo%20Size&color=0f766e)

### 語言選項：**英文（目前草案）**。繁體中文譯本可在 `i18n/` 目錄找到。

### OnlyFans clone app 是一個面向行動裝置與網頁的全端應用，重現了創作者平台風格的功能與流程。

本專案是一個使用 AWS Amplify 後端（`Cognito`、`AppSync`、`DataStore`、`S3`）的 Expo + React Native 應用，實作了創作者平台的複製版。它包含身分驗證、創作者瀏覽、貼文建立、媒體上傳，以及訂閱 UI 狀態流程。

## 🧭 概覽

本應用使用 Expo Router 建構在 `app/`，並透過本機 Amplify 資料層關聯到 `amplify/` 中已提交的後端資源。

| 區域 | 目前實作 |
|---|---|
| 前端 | Expo + React Native + Expo Router |
| 路由 | `app/` 中的檔案式路由 |
| 身份驗證 | 透過 `@aws-amplify/ui-react-native` 使用 Amazon Cognito |
| API | AWS AppSync GraphQL |
| 資料同步 | Amplify DataStore |
| 媒體 | 透過 Amplify Storage 使用 S3 |
| 平台 | iOS、Android、Web |

在登入時，`app/_layout.js` 會監聽 Amplify Hub 的 auth 事件，並在 AppSync 中嘗試建立 `User` 記錄，這是應用啟動時的流程。

## ✨ 功能

- 使用 Cognito 與 Amplify Authenticator 的驗證流程
- `User` 與 `Post` 的 AppSync GraphQL 模型
- 透過 Amplify DataStore 進行資料持久化與同步
- 透過 Amplify Storage 上傳與取得 S3 圖片
- Expo Router 的檔案式路由：
  - `app/index.js`：創作者清單與首頁訊息流
  - `app/user/[id].js`：創作者個人檔案與貼文
  - `app/newPost.js`：貼文撰寫頁面
- 可重複使用的展示元件：
  - `src/components/UserCard.js`
  - `src/components/UserProfileHeader.js`
  - `src/components/Post.js`

## 🛠️ 使用技術

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

`package.json` 內的其他相依套件包含：
- `@react-native-async-storage/async-storage`
- `@react-native-community/netinfo`
- `core-js`
- `expo-constants`、`expo-linking`、`expo-updates`，以及圖示與畫面工具相關套件

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
│  │  ├─ index.js
│  │  ├─ schema.js
│  │  └─ schema.d.ts
│  └─ aws-exports.js (generated locally; not committed)
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

## ✅ 先決條件

- Node.js 18+（或現代 LTS）
- npm
- Expo CLI（可透過 `npx expo` 執行）
- AWS 帳號與 Amplify CLI（如果你需要產生 `src/aws-exports.js`）
- 可進行測試的 Apple/Android 模擬器，或已安裝 Expo Go 的實機

## 📥 複製儲存庫 🔧

```bash
git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ 安裝 🔧

```bash
npm install
```

來自 `package.json` 的腳本：

```bash
npm start
npm run android
npm run ios
npm run web
```

接著啟動應用：

```bash
npm start
```

## 🔐 設定

### Amplify 後端

應用在 `app/_layout.js` 中引入 `../src/aws-exports`。此檔案於執行時必填，且有意不會提交到版本庫。

一般本機設定：

```bash
npm install -g @aws-amplify/cli
amplify pull
```

若系統要求，請選擇本專案對應的既有 AWS Amplify 專案／環境。

### 由提交的 schema 推斷的資料模型

- `User`：欄位包含 `id`、`name`、`handle`、`bio`、`avatar`、`coverImage`、`subscriptionPrice`，並與 `Post` 有關聯
- `Post`：欄位包含 `id`、`text`、`image`、`likes`、`userID`
- 目前兩個模型在提交的 schema 與權限設定中，皆設定為「公開讀取」可見性

### Expo / 路由 / Babel

- `index.js` 載入 React Native 入口與 `expo-router/entry`
- `babel.config.js` 含 `expo-router/babel`、`react-native-reanimated/plugin` 與 namespace export proposal 外掛

## ▶️ 使用方式

1. 安裝相依套件並產生 / 取得本機的 `src/aws-exports.js`
2. 啟動 Metro：
   ```bash
   npm start
   ```
3. 在 Expo Go、模擬器或網頁中開啟應用
4. 透過 Authenticator 註冊 / 登入
5. 在 `/` 瀏覽創作者清單
6. 在 `/user/:id` 開啟創作者個人資料
7. 在 UI 中切換訂閱狀態
8. 在 `/newPost` 建立貼文，可選擇附加媒體

## 🧱 資料模型說明

模型定義位於 `amplify/backend/api/OnlyFansCloneApp/schema.graphql` 與 `src/models/schema.js`。

| 模型 | 主要欄位 |
|---|---|
| `User` | `id`、`name`、`handle`、`bio`、`avatar`、`coverImage`、`subscriptionPrice` |
| `Post` | `id`、`text`、`image`、`likes`、`userID` |

## 📱 範例

### 示範截圖

![Screenshot_20230424-200925](https://user-images.githubusercontent.com/64506662/234364566-863bc1e1-e289-4b9b-9658-a11e737bebd8.png)
![Screenshot_20230424-200957](https://user-images.githubusercontent.com/64506662/234364579-8e32708f-cb69-4c1c-82e3-eefd7cb5f161.png)
![Screenshot_20230424-201003](https://user-images.githubusercontent.com/64506662/234364622-e9cc5d14-77f2-415f-9027-1d3ffe3e7c17.png)
![Screenshot_20230424-201006](https://user-images.githubusercontent.com/64506662/234364653-73de6b92-b7a6-4ef7-a3a6-c26411bfd46a.png)
![Screenshot_20230424-201031](https://user-images.githubusercontent.com/64506662/234364754-f5ce7da1-1ad1-4e90-bf85-40add436ad23.png)

## 🧪 開發備註

- `app/_layout.js` 在啟動時使用 `Amplify.configure` 設定 Amplify，並訂閱 Hub 的 `auth` 事件。
- 每次登入事件發生時，程式會觸發 `createUser` mutation 以初始化後端紀錄。
- `app/newPost.js` 可選擇性上傳圖片，組合貼文 payload，接著透過 `DataStore.save` 持久化。
- `src/components/Post.js` 在渲染訊息流時，會動態解析貼文作者與圖片網址。
- 後端與種子資料目前僅有最小配置，儲存庫中尚無自動化初始化腳本。
- 專案目前未配置完整測試套件或 CI 工作流程。

## 🩺 疑難排解

- `Cannot find module '../src/aws-exports'`
  - 在專案根目錄執行 `amplify pull`（或對應的 `amplify init` 流程）以產生本機設定。
- 驗證成功但查詢/變更失敗
  - 請確認 AppSync/API key/auth 模式與地區與匯入的生成設定一致。
- 圖片上傳失敗
  - 確認已配置 `Storage` 權限，且應用已取得媒體庫存取權。
- 創作者／訊息流資料為空
  - 確認 `DataStore/AppSync` 中存在初始 `User`／`Post` 記錄，且公開讀取規則符合你的使用情境。
- 訂閱狀態未持久化
  - 目前實作似乎僅維持 UI 本地狀態；後端權益模型尚未建立。

## 🗺️ 路線圖

- 在後端模型中持久化訂閱關係／權益
- 新增種子資料，並建立可支援資料遷移的重置流程
- 改善貼文驗證與錯誤狀態
- 加入自動化測試（unit/integration/e2e）
- 加入 CI/CD 與 lint/type 檢查
- 擴充多語言文件並持續同步 i18n README
- 在需要時加強驗證與資料存取規則

## 🤝 貢獻

歡迎任何形式的貢獻。

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
- 如何執行與測試

## 📄 授權

本儲存庫目前未包含 `LICENSE` 檔案。

推測上，除非維護者新增明確授權檔案，否則預設保留所有權利。


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
