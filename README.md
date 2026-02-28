[English](README.md) · [العربية](i18n/README.ar.md) · [Español](i18n/README.es.md) · [Français](i18n/README.fr.md) · [日本語](i18n/README.ja.md) · [한국어](i18n/README.ko.md) · [Tiếng Việt](i18n/README.vi.md) · [中文 (简体)](i18n/README.zh-Hans.md) · [中文（繁體）](i18n/README.zh-Hant.md) · [Deutsch](i18n/README.de.md) · [Русский](i18n/README.ru.md)

Language options: **English (current draft)**. i18n status: `/i18n` directory exists and is currently empty; multilingual README variants are not yet added in this repository.

# OnlyFans clone Full Stack App

![Expo](https://img.shields.io/badge/Expo-48-000000?logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61DAFB?logo=react&logoColor=black)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-FF9900?logo=amazonaws&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android%20%7C%20Web-blue)
![Status](https://img.shields.io/badge/Status-Active%20Prototype-2ea44f)

### OnlyFans clone app is a full stack app, front end and back end for mobile,replicates the features and functionality to the same.

This repository contains an Expo + React Native app with an AWS Amplify backend (Cognito, AppSync, DataStore, S3) that implements core creator-platform flows:
- Authentication with Amplify Authenticator
- Creator list and profile browsing
- Subscription UI state toggle (client-side in current implementation)
- Post creation with optional image upload
- Post feed rendering with author and media retrieval

## 🧭 Overview

The app uses file-based routing with `expo-router` under `app/`, while Amplify backend resources are tracked under `amplify/`. On user sign-in, the app listens to Amplify Hub auth events and attempts to create a corresponding `User` record in AppSync.

| Area | Current implementation |
|---|---|
| Frontend | Expo + React Native + Expo Router |
| Auth | Amazon Cognito via Amplify Authenticator |
| API | AWS AppSync GraphQL |
| Data sync | Amplify DataStore |
| Media | S3 via Amplify Storage |
| Platforms | iOS, Android, Web |

## ✨ Features

- Auth flow powered by Cognito via `@aws-amplify/ui-react-native`
- AppSync GraphQL models for `User` and `Post`
- Data persistence and sync through Amplify DataStore
- S3 media upload and retrieval via Amplify Storage
- Expo Router screens:
  - `app/index.js` creator list/home
  - `app/user/[id].js` creator profile + posts
  - `app/newPost.js` post composer

## 🛠️ Built With

(Original stack list preserved and expanded for clarity.)

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

Additional repository dependencies in `package.json` include:
- `expo-router`
- `@react-native-async-storage/async-storage`
- `@react-native-community/netinfo`
- `core-js`

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

## ✅ Prerequisites

- Node.js 18+ recommended
- npm
- Expo CLI usage via `npx expo ...`
- AWS account and Amplify CLI for backend provisioning/pull
- A generated Amplify client config file imported by the app as `src/aws-exports`

## 📥 Clone repo 🔧

```bash
https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app
```

Equivalent command:

```bash
git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ Installation 🔧

(Original install commands preserved.)

```bash
npm install

npx expo start or npm start
```

Repository scripts:

```bash
npm start
npm run android
npm run ios
npm run web
```

## 🔐 Configuration

### Amplify backend

The app imports `../src/aws-exports` in `app/_layout.js`. That file is not committed and must be generated locally.

Typical setup flow (assumption based on committed `amplify/` folder and `.gitignore`):

```bash
npm install -g @aws-amplify/cli
amplify pull
```

If prompted, use the existing Amplify project/environment from your AWS account. The committed backend config indicates:
- Auth: Cognito (email username, signup attributes include `NAME` and `NICKNAME`)
- API: AppSync + API key auth enabled in config
- Storage: S3 bucket resource configured

### Expo / Babel / Router

- `babel.config.js` includes:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`
- `index.js` initializes `core-js/full/symbol/async-iterator` and `expo-router/entry`

## ▶️ Usage

1. Start the app:
   ```bash
   npm start
   ```
2. Open in Expo Go/emulator/web.
3. Sign up/sign in through the Amplify Authenticator UI.
4. Browse creators on the home screen.
5. Open a creator profile (`/user/[id]`).
6. Toggle subscription state in UI.
7. Create a new post from `New post`, optionally attaching an image from the media library.

## 🧱 Data Model

From `amplify/backend/api/OnlyFansCloneApp/schema.graphql`:

- `User`: `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`, relation to posts
- `Post`: `id`, `text`, `image`, `likes`, `userID`

Both models use public auth rules in the current schema.

| Model | Key fields |
|---|---|
| `User` | `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` |
| `Post` | `id`, `text`, `image`, `likes`, `userID` |

## 📱 Examples App

### You need create a free account to use the app

![Screenshot_20230424-200925](https://user-images.githubusercontent.com/64506662/234364566-863bc1e1-e289-4b9b-9658-a11e737bebd8.png)
![Screenshot_20230424-200957](https://user-images.githubusercontent.com/64506662/234364579-8e32708f-cb69-4c1c-82e3-eefd7cb5f161.png)
![Screenshot_20230424-201003](https://user-images.githubusercontent.com/64506662/234364622-e9cc5d14-77f2-415f-9027-1d3ffe3e7c17.png)
![Screenshot_20230424-201006](https://user-images.githubusercontent.com/64506662/234364653-73de6b92-b7a6-4ef7-a3a6-c26411bfd46a.png)
![Screenshot_20230424-201031](https://user-images.githubusercontent.com/64506662/234364754-f5ce7da1-1ad1-4e90-bf85-40add436ad23.png)

## 🧪 Development Notes

- `app/_layout.js` listens to Amplify Hub `auth` sign-in events and executes a `createUser` GraphQL mutation.
- New posts are saved with DataStore and optional images are uploaded with `Storage.put`.
- Profile subscription behavior is currently local UI state and not persisted as a backend subscription model.
- Repository currently has no explicit automated test suite or CI workflow files.

## 🩺 Troubleshooting

- `Cannot find module '../src/aws-exports'`:
  - Run `amplify pull` (or equivalent Amplify init workflow) to generate local config.
- Auth works but data operations fail:
  - Confirm AppSync/API key/auth mode configuration in your Amplify environment matches local generated config.
- Image upload issues:
  - Verify S3 permissions in Amplify storage and ensure device has media-library access.
- Empty feed/profile data:
  - Ensure seeded `User`/`Post` records exist and that current auth rules allow read operations.

## 🗺️ Roadmap

- Add persisted subscription relationships and entitlement checks
- Add validations and richer error handling for post creation/upload flows
- Add testing (unit/integration/e2e) and CI pipeline
- Add multilingual README variants and populate `i18n/` resources
- Harden auth/access rules (replace broad public rules where needed)

## 🤝 Contributing

Contributions are welcome.

Suggested flow:

```bash
git checkout -b feat/your-change
# implement change
git commit -m "feat: describe change"
git push origin feat/your-change
```

Then open a Pull Request with:
- What changed
- Why it changed
- How to run/test it

## 📄 License

No `LICENSE` file is currently present in this repository.

Assumption: all rights are reserved by default unless the maintainer adds an explicit license file.
