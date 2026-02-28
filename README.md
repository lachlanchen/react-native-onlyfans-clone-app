[English](README.md) · [العربية](i18n/README.ar.md) · [Español](i18n/README.es.md) · [Français](i18n/README.fr.md) · [日本語](i18n/README.ja.md) · [한국어](i18n/README.ko.md) · [Tiếng Việt](i18n/README.vi.md) · [中文 (简体)](i18n/README.zh-Hans.md) · [中文（繁體）](i18n/README.zh-Hant.md) · [Deutsch](i18n/README.de.md) · [Русский](i18n/README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# OnlyFans clone Full Stack App

![Expo](https://img.shields.io/badge/Expo-48-000000?logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61DAFB?logo=react&logoColor=black)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-FF9900?logo=amazonaws&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android%20%7C%20Web-blue)
![Status](https://img.shields.io/badge/Status-Active%20Prototype-2ea44f)
![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?logo=nodedotjs&logoColor=white)
![Repo%20Size](https://img.shields.io/github/repo-size/GonzaloVolonterio/react-native-onlyfans-clone-app?label=Repo%20Size&color=0f766e)

Language options: **English (current draft)**. Translations are available under `i18n/`.

### OnlyFans clone app is a full-stack app for mobile and web that replicates creator-platform-style features and flows.

This repository contains an Expo + React Native app with an AWS Amplify backend (`Cognito`, `AppSync`, `DataStore`, `S3`) that implements a creator-platform clone. It includes authentication, creator browsing, post creation, media uploads, and subscription UI state flows.

## 🧭 Overview

The app is built with Expo Router in `app/` and a local Amplify data layer tied to committed backend resources in `amplify/`.

| Area | Current implementation |
|---|---|
| Frontend | Expo + React Native + Expo Router |
| Routing | File-based routing in `app/` |
| Auth | Amazon Cognito via `@aws-amplify/ui-react-native` |
| API | AWS AppSync GraphQL |
| Data sync | Amplify DataStore |
| Media | S3 via Amplify Storage |
| Platforms | iOS, Android, Web |

On sign-in, `app/_layout.js` listens to Amplify Hub auth events and attempts to create a `User` record in AppSync. This is handled at app bootstrap.

## ✨ Features

- Auth flow powered by Cognito with the Amplify Authenticator
- AppSync GraphQL models for `User` and `Post`
- Data persistence and sync through Amplify DataStore
- S3 image upload and retrieval via Amplify Storage
- File-based routing in Expo Router:
  - `app/index.js`: creator list and home feed
  - `app/user/[id].js`: creator profile and posts
  - `app/newPost.js`: post composer
- Reusable presentation components:
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

Additional dependencies from `package.json` include:
- `@react-native-async-storage/async-storage`
- `@react-native-community/netinfo`
- `core-js`
- `expo-constants`, `expo-linking`, `expo-updates`, and icon/screen tooling

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

- Node.js 18+ (or modern LTS)
- npm
- Expo CLI (can be run via `npx expo`)
- AWS account and Amplify CLI if you need to generate `src/aws-exports.js`
- Apple/Android simulators or a physical device with Expo Go for app testing

## 📥 Clone repo 🔧

```bash
git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ Installation 🔧

```bash
npm install
```

Repository scripts from `package.json`:

```bash
npm start
npm run android
npm run ios
npm run web
```

Then launch the app:

```bash
npm start
```

## 🔐 Configuration

### Amplify backend

The app imports `../src/aws-exports` in `app/_layout.js`. This file is required at runtime and is intentionally not committed.

Typical local setup:

```bash
npm install -g @aws-amplify/cli
amplify pull
```

If prompted, choose the existing AWS Amplify project/environment for this repository.

### Data model assumptions from committed schema

- `User`: fields include `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`, and relationship to `Post`
- `Post`: fields include `id`, `text`, `image`, `likes`, `userID`
- Both models are currently configured for public read-level visibility in committed schema/auth config

### Expo / routing / Babel

- `index.js` wires up React Native entry and `expo-router/entry`
- `babel.config.js` includes `expo-router/babel`, `react-native-reanimated/plugin`, and namespace export proposal plugin

## ▶️ Usage

1. Install dependencies and generate/obtain local `src/aws-exports.js`
2. Start Metro:
   ```bash
   npm start
   ```
3. Open the app in Expo Go, simulator, or web
4. Sign up / sign in via Authenticator
5. Browse creators on `/`
6. Open a creator profile at `/user/:id`
7. Toggle subscription state in UI
8. Create posts in `/newPost`, with optional media attachment

## 🧱 Data Model Notes

Models are defined in `amplify/backend/api/OnlyFansCloneApp/schema.graphql` and `src/models/schema.js`.

| Model | Key fields |
|---|---|
| `User` | `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` |
| `Post` | `id`, `text`, `image`, `likes`, `userID` |

## 📱 Examples

### Demo screenshots

![Screenshot_20230424-200925](https://user-images.githubusercontent.com/64506662/234364566-863bc1e1-e289-4b9b-9658-a11e737bebd8.png)
![Screenshot_20230424-200957](https://user-images.githubusercontent.com/64506662/234364579-8e32708f-cb69-4c1c-82e3-eefd7cb5f161.png)
![Screenshot_20230424-201003](https://user-images.githubusercontent.com/64506662/234364622-e9cc5d14-77f2-415f-9027-1d3ffe3e7c17.png)
![Screenshot_20230424-201006](https://user-images.githubusercontent.com/64506662/234364653-73de6b92-b7a6-4ef7-a3a6-c26411bfd46a.png)
![Screenshot_20230424-201031](https://user-images.githubusercontent.com/64506662/234364754-f5ce7da1-1ad1-4e90-bf85-40add436ad23.png)

## 🧪 Development Notes

- `app/_layout.js` registers Amplify with `Amplify.configure` and subscribes to Hub `auth` events.
- On each sign-in event, the code triggers a `createUser` mutation so a backend record is initialized.
- `app/newPost.js` uploads an optional image, composes post payload, then persists via `DataStore.save`.
- `src/components/Post.js` resolves post authors and image URLs dynamically when rendering feed items.
- Backend and seed data are currently minimal/no automated setup script in repo.
- There is no dedicated test suite or CI workflow configured in this repository.

## 🩺 Troubleshooting

- `Cannot find module '../src/aws-exports'`
  - Run `amplify pull` (or a matching `amplify init` flow) from the repository root to generate local config.
- Auth succeeds but queries/mutations fail
  - Verify your AppSync/API key/auth mode and region match the imported generated config.
- Image upload fails
  - Ensure `Storage` permissions are present and the app has media-library access.
- Empty creator/feed data
  - Confirm initial `User`/`Post` records exist in DataStore/AppSync and public read rules fit your use case.
- Post subscription state does not persist
  - Current implementation appears UI-local only; backend entitlement model is not yet implemented.

## 🗺️ Roadmap

- Persist subscription relationships/entitlements in backend models
- Add seed data and data-migration-friendly reset flow
- Improve post validation and error states
- Add automated tests (unit/integration/e2e)
- Add CI/CD and lint/type checks
- Expand international docs and keep i18n READMEs synchronized
- Harden authentication and data access rules where needed

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
