[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# OnlyFans クローン Full Stack アプリ

![Expo](https://img.shields.io/badge/Expo-48-000000?logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61DAFB?logo=react&logoColor=black)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-FF9900?logo=amazonaws&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android%20%7C%20Web-blue)
![Status](https://img.shields.io/badge/Status-Active%20Prototype-2ea44f)

### OnlyFans クローンアプリは、モバイル向けに同等の機能と体験を再現したフルスタック（フロントエンド + バックエンド）アプリです。

このリポジトリには、AWS Amplify バックエンド（Cognito、AppSync、DataStore、S3）を備えた Expo + React Native アプリが含まれており、クリエイタープラットフォームの主要フローを実装しています。
- Amplify Authenticator を使った認証
- クリエイター一覧・プロフィール閲覧
- サブスク UI 状態の切り替え（現実装ではクライアント側のみ）
- 任意の画像アップロード付き投稿作成
- 投稿フィード表示（投稿者情報・メディア取得を含む）

## 🧭 概要

アプリは `app/` 配下で `expo-router` によるファイルベースルーティングを使用し、Amplify バックエンドリソースは `amplify/` 配下で管理されています。ユーザーサインイン時には Amplify Hub の auth イベントを監視し、対応する `User` レコードを AppSync に作成しようとします。

| 領域 | 現在の実装 |
|---|---|
| Frontend | Expo + React Native + Expo Router |
| Auth | Amplify Authenticator 経由の Amazon Cognito |
| API | AWS AppSync GraphQL |
| Data sync | Amplify DataStore |
| Media | Amplify Storage 経由の S3 |
| Platforms | iOS, Android, Web |

## ✨ 機能

- `@aws-amplify/ui-react-native` 経由の Cognito 認証フロー
- `User` と `Post` の AppSync GraphQL モデル
- Amplify DataStore によるデータ永続化と同期
- Amplify Storage による S3 メディアのアップロードと取得
- Expo Router 画面:
  - `app/index.js` クリエイター一覧/ホーム
  - `app/user/[id].js` クリエイタープロフィール + 投稿
  - `app/newPost.js` 投稿作成

## 🛠️ 使用技術

（元のスタック一覧を保持し、分かりやすさのために拡張しています。）

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

`package.json` に含まれる追加依存関係:
- `expo-router`
- `@react-native-async-storage/async-storage`
- `@react-native-community/netinfo`
- `core-js`

## 🗂️ プロジェクト構成

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

## ✅ 前提条件

- Node.js 18+ 推奨
- npm
- `npx expo ...` による Expo CLI 利用
- バックエンドのプロビジョニング/取得（pull）のための AWS アカウントと Amplify CLI
- アプリが `src/aws-exports` として読み込む、生成済み Amplify クライアント設定ファイル

## 📥 リポジトリをクローン 🔧

```bash
https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app
```

同等のコマンド:

```bash
git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ インストール 🔧

（元のインストールコマンドを保持しています。）

```bash
npm install

npx expo start or npm start
```

リポジトリのスクリプト:

```bash
npm start
npm run android
npm run ios
npm run web
```

## 🔐 設定

### Amplify バックエンド

アプリは `app/_layout.js` で `../src/aws-exports` をインポートします。このファイルはコミットされておらず、ローカルで生成する必要があります。

一般的なセットアップフロー（コミット済みの `amplify/` フォルダと `.gitignore` に基づく想定）:

```bash
npm install -g @aws-amplify/cli
amplify pull
```

プロンプトが表示された場合は、AWS アカウント内の既存 Amplify プロジェクト/環境を使用してください。コミット済みバックエンド設定から次が確認できます。
- Auth: Cognito（email username、signup attributes に `NAME` と `NICKNAME` を含む）
- API: AppSync + 設定上で API key auth が有効
- Storage: S3 バケットリソースを設定済み

### Expo / Babel / Router

- `babel.config.js` には以下を含みます:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`
- `index.js` は `core-js/full/symbol/async-iterator` と `expo-router/entry` を初期化します

## ▶️ 使い方

1. アプリを起動:
   ```bash
   npm start
   ```
2. Expo Go / エミュレーター / Web で開きます。
3. Amplify Authenticator UI からサインアップ/サインインします。
4. ホーム画面でクリエイターを閲覧します。
5. クリエイタープロフィール（`/user/[id]`）を開きます。
6. UI 上でサブスク状態を切り替えます。
7. `New post` から新規投稿を作成し、必要に応じてメディアライブラリから画像を添付します。

## 🧱 データモデル

`amplify/backend/api/OnlyFansCloneApp/schema.graphql` より:

- `User`: `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`, 投稿とのリレーション
- `Post`: `id`, `text`, `image`, `likes`, `userID`

現在のスキーマでは、どちらのモデルも public auth rules を使用しています。

| モデル | 主要フィールド |
|---|---|
| `User` | `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` |
| `Post` | `id`, `text`, `image`, `likes`, `userID` |

## 📱 アプリ例

### アプリ利用には無料アカウントの作成が必要です

![Screenshot_20230424-200925](https://user-images.githubusercontent.com/64506662/234364566-863bc1e1-e289-4b9b-9658-a11e737bebd8.png)
![Screenshot_20230424-200957](https://user-images.githubusercontent.com/64506662/234364579-8e32708f-cb69-4c1c-82e3-eefd7cb5f161.png)
![Screenshot_20230424-201003](https://user-images.githubusercontent.com/64506662/234364622-e9cc5d14-77f2-415f-9027-1d3ffe3e7c17.png)
![Screenshot_20230424-201006](https://user-images.githubusercontent.com/64506662/234364653-73de6b92-b7a6-4ef7-a3a6-c26411bfd46a.png)
![Screenshot_20230424-201031](https://user-images.githubusercontent.com/64506662/234364754-f5ce7da1-1ad1-4e90-bf85-40add436ad23.png)

## 🧪 開発ノート

- `app/_layout.js` は Amplify Hub `auth` の sign-in イベントを監視し、`createUser` GraphQL mutation を実行します。
- 新規投稿は DataStore に保存され、任意画像は `Storage.put` でアップロードされます。
- プロフィールのサブスク挙動は現在ローカル UI 状態のみで、バックエンドのサブスクモデルとしては永続化されていません。
- 現在このリポジトリには明示的な自動テストスイートや CI ワークフローファイルはありません。

## 🩺 トラブルシューティング

- `Cannot find module '../src/aws-exports'`:
  - ローカル設定を生成するために `amplify pull`（または同等の Amplify 初期化フロー）を実行してください。
- 認証は動作するがデータ操作に失敗する:
  - Amplify 環境の AppSync/API key/auth mode 設定が、ローカル生成設定と一致していることを確認してください。
- 画像アップロードの問題:
  - Amplify storage の S3 権限を確認し、デバイスにメディアライブラリアクセス許可があることを確認してください。
- フィード/プロフィールデータが空:
  - `User`/`Post` レコードが投入済みであり、現在の auth rules で読み取り可能であることを確認してください。

## 🗺️ ロードマップ

- 永続化されたサブスクリプション関係と権限チェックの追加
- 投稿作成/アップロードフローのバリデーションとエラーハンドリング強化
- テスト（unit/integration/e2e）と CI パイプラインの追加
- 多言語 README バリアント追加と `i18n/` リソースの整備
- 認証/アクセスルールの強化（必要に応じて広範な public rules を置き換え）

## 🤝 コントリビュート

コントリビューションを歓迎します。

推奨フロー:

```bash
git checkout -b feat/your-change
# implement change
git commit -m "feat: describe change"
git push origin feat/your-change
```

続いて Pull Request を作成し、以下を記載してください:
- 何を変更したか
- なぜ変更したか
- 実行/テスト方法

## 📄 ライセンス

現在、このリポジトリには `LICENSE` ファイルが存在しません。

想定: メンテナーが明示的なライセンスファイルを追加しない限り、デフォルトでは all rights reserved です。
