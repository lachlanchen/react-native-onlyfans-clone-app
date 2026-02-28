[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# OnlyFans クローン フルスタックアプリ

![Expo](https://img.shields.io/badge/Expo-48-000000?logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61DAFB?logo=react&logoColor=black)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-FF9900?logo=amazonaws&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android%20%7C%20Web-blue)
![Status](https://img.shields.io/badge/Status-Active%20Prototype-2ea44f)
![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?logo=nodedotjs&logoColor=white)
![Repo%20Size](https://img.shields.io/github/repo-size/GonzaloVolonterio/react-native-onlyfans-clone-app?label=Repo%20Size&color=0f766e)

Language options: **English (current draft)**. Translations are available under `i18n/`.

### OnlyFans クローンアプリは、モバイルと Web の両方でクリエイタープラットフォーム風の機能とフローを再現するフルスタックアプリです。

このリポジトリには、AWS Amplify バックエンド（`Cognito`、`AppSync`、`DataStore`、`S3`）を利用した Expo + React Native アプリが含まれており、クリエイター向けプラットフォームのクローンを実装しています。認証、クリエイター閲覧、投稿作成、メディアアップロード、サブスクリプションの UI 状態管理を備えています。

## 🧭 Overview

アプリは `app/` 配下で Expo Router を使って構築されており、`amplify/` のコミット済みバックエンドリソースに紐づくローカル Amplify データレイヤーを持ちます。

| 領域 | 現在の実装 |
|---|---|
| Frontend | Expo + React Native + Expo Router |
| Routing | `app/` のファイルベースルーティング |
| Auth | `@aws-amplify/ui-react-native` 経由の Amazon Cognito |
| API | AWS AppSync GraphQL |
| Data sync | Amplify DataStore |
| Media | Amplify Storage 経由の S3 |
| Platforms | iOS, Android, Web |

サインイン時、`app/_layout.js` は Amplify Hub の auth イベントを監視し、AppSync の `User` レコードを作成しようとします。これはアプリ起動時に行われます。

## ✨ Features

- Amplify Authenticator で Cognito を用いた認証フロー
- `User` と `Post` の AppSync GraphQL モデル
- Amplify DataStore によるデータ永続化と同期
- Amplify Storage 経由の S3 画像アップロードと取得
- Expo Router のファイルベースルーティング:
  - `app/index.js`: クリエイター一覧・ホームフィード
  - `app/user/[id].js`: クリエイタープロフィールと投稿
  - `app/newPost.js`: 投稿作成画面
- 再利用可能な表示コンポーネント:
  - `src/components/UserCard.js`
  - `src/components/UserProfileHeader.js`
  - `src/components/Post.js`

## 🛠️ Built With

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

`package.json` の追加依存関係:
- `@react-native-async-storage/async-storage`
- `@react-native-community/netinfo`
- `core-js`
- `expo-constants`、`expo-linking`、`expo-updates`、および icon/screen tooling

## 🗂️ Project Structure

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

## ✅ Prerequisites

- Node.js 18+（または同等のモダン LTS）
- npm
- Expo CLI（`npx expo` で実行可）
- `src/aws-exports.js` を生成するための AWS アカウントと Amplify CLI
- Apple/Android エミュレーター、または実機の Expo Go

## 📥 Clone repo 🔧

```bash
git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ Installation 🔧

```bash
npm install
```

`package.json` のスクリプト:

```bash
npm start
npm run android
npm run ios
npm run web
```

アプリを起動します:

```bash
npm start
```

## 🔐 Configuration

### Amplify backend

アプリは `app/_layout.js` で `../src/aws-exports` をインポートします。このファイルは実行時に必要ですが、意図的にコミットされていません。

ローカル環境での基本セットアップ:

```bash
npm install -g @aws-amplify/cli
amplify pull
```

プロンプトが表示されたら、このリポジトリに対応する既存の AWS Amplify プロジェクト/環境を選択します。

### Data model assumptions from committed schema

- `User`: フィールドは `id`、`name`、`handle`、`bio`、`avatar`、`coverImage`、`subscriptionPrice`、`Post` とのリレーションを含む
- `Post`: フィールドは `id`、`text`、`image`、`likes`、`userID`
- どちらのモデルも現在はコミット済みのスキーマ／認証設定で public read レベルの可視性が有効

### Expo / routing / Babel

- `index.js` は React Native エントリーと `expo-router/entry` を接続
- `babel.config.js` には `expo-router/babel`、`react-native-reanimated/plugin`、`@babel/plugin-proposal-export-namespace-from` を含める

## ▶️ Usage

1. 依存関係をインストールし、ローカルの `src/aws-exports.js` を生成または取得する
2. Metro を起動:
   ```bash
   npm start
   ```
3. Expo Go、シミュレーター、または Web でアプリを開く
4. Authenticator でサインアップ / サインインする
5. `/` でクリエイターを閲覧する
6. `/user/:id` でクリエイタープロフィールを開く
7. UI 上でサブスク状態を切り替える
8. `/newPost` で投稿を作成し、必要に応じて画像を添付する

## 🧱 Data Model Notes

モデルは `amplify/backend/api/OnlyFansCloneApp/schema.graphql` と `src/models/schema.js` で定義されています。

| モデル | 主要フィールド |
|---|---|
| `User` | `id`、`name`、`handle`、`bio`、`avatar`、`coverImage`、`subscriptionPrice` |
| `Post` | `id`、`text`、`image`、`likes`、`userID` |

## 📱 Examples

### Demo screenshots

![Screenshot_20230424-200925](https://user-images.githubusercontent.com/64506662/234364566-863bc1e1-e289-4b9b-9658-a11e737bebd8.png)
![Screenshot_20230424-200957](https://user-images.githubusercontent.com/64506662/234364579-8e32708f-cb69-4c1c-82e3-eefd7cb5f161.png)
![Screenshot_20230424-201003](https://user-images.githubusercontent.com/64506662/234364622-e9cc5d14-77f2-415f-9027-1d3ffe3e7c17.png)
![Screenshot_20230424-201006](https://user-images.githubusercontent.com/64506662/234364653-73de6b92-b7a6-4ef7-a3a6-c26411bfd46a.png)
![Screenshot_20230424-201031](https://user-images.githubusercontent.com/64506662/234364754-f5ce7da1-1ad1-4e90-bf85-40add436ad23.png)

## 🧪 Development Notes

- `app/_layout.js` では `Amplify.configure` で Amplify を登録し、Hub の `auth` イベントを購読します。
- サインインイベントごとに `createUser` mutation を実行して、バックエンド側のレコードを初期化します。
- `app/newPost.js` は任意画像をアップロードして投稿内容を組み立て、`DataStore.save` で保存します。
- `src/components/Post.js` はフィード表示時に投稿者情報と画像 URL を動的に解決します。
- バックエンドとシードデータは現在最小限で、リポジトリ内の自動化されたセットアップスクリプトはありません。
- 本リポジトリには専用のテストスイートや CI ワークフローは設定されていません。

## 🩺 Troubleshooting

- `Cannot find module '../src/aws-exports'`
  - `amplify pull`（または一致する `amplify init` フロー）をリポジトリのルートから実行してローカル設定を生成してください。
- 認証は成功するがクエリ/ミューテーションが失敗する
  - AppSync/API キー・認証モード・リージョンがローカルの生成設定と一致しているか確認してください。
- 画像アップロードに失敗する
  - `Storage` の権限が付与されているか、アプリがメディアライブラリアクセスを持っているか確認してください。
- クリエイター/フィードデータが空
  - DataStore/AppSync に初期 `User` / `Post` レコードが存在し、公開読み取りルールが利用ケースに合っていることを確認してください。
- 投稿のサブスクリプション状態が永続化されない
  - 現在の実装では UI 側のみで、バックエンド側のエンタイトルメントモデルはまだ未実装です。

## 🗺️ Roadmap

- サブスクリプション関係／権利をバックエンドモデルに永続化する
- シードデータの追加とデータ移行しやすいリセットフローを追加する
- 投稿バリデーションとエラー状態の改善
- 自動テスト（unit/integration/e2e）を追加する
- CI/CD と lint/type チェックを追加する
- 国際化ドキュメントを拡張し、i18n README を同期させ続ける
- 必要に応じて認証とデータアクセスルールを強化する

## 🤝 Contributing

Contributions are welcome.

Suggested flow:

```bash
git checkout -b feat/your-change
# implement change
npm start
git commit -m "feat: describe your change"
git push origin feat/your-change
```

## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## 📄 License

No `LICENSE` file is currently present in this repository.

Assumption: all rights are reserved unless the maintainer adds an explicit license file.
