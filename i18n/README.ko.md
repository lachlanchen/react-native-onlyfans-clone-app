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

### 현재 원문은 **영어(진행 중 초안)**입니다. 번역본은 `i18n/` 경로에서 확인할 수 있습니다.

### OnlyFans 클론 앱은 모바일과 웹에서 크리에이터 플랫폼 스타일의 기능과 흐름을 재현하는 풀스택 앱입니다.

이 저장소에는 AWS Amplify 백엔드(`Cognito`, `AppSync`, `DataStore`, `S3`)와 함께 동작하는 Expo + React Native 앱이 포함되어 있으며, 크리에이터 플랫폼 클론을 구현합니다. 인증, 크리에이터 탐색, 게시물 생성, 미디어 업로드, 구독 UI 상태 흐름이 포함되어 있습니다.

## 🧭 개요

이 앱은 `app/`에서 Expo Router를 사용해 빌드되었고, `amplify/`에 커밋된 백엔드 리소스와 연결된 로컬 Amplify 데이터 계층을 사용합니다.

| Area | Current implementation |
|---|---|
| Frontend | Expo + React Native + Expo Router |
| Routing | File-based routing in `app/` |
| Auth | Amazon Cognito via `@aws-amplify/ui-react-native` |
| API | AWS AppSync GraphQL |
| Data sync | Amplify DataStore |
| Media | S3 via Amplify Storage |
| Platforms | iOS, Android, Web |

로그인 시 `app/_layout.js`가 Amplify Hub 인증 이벤트를 수신하고 AppSync에서 `User` 레코드를 생성하려고 시도합니다. 이 로직은 앱 부트스트랩 과정에서 처리됩니다.

## ✨ 기능

- Amplify Authenticator를 이용한 Cognito 인증 흐름
- `User` 및 `Post`에 대한 AppSync GraphQL 모델
- Amplify DataStore를 통한 데이터 영속성 및 동기화
- Amplify Storage를 통한 S3 이미지 업로드 및 조회
- Expo Router의 파일 기반 라우팅:
  - `app/index.js`: 크리에이터 목록 및 홈 피드
  - `app/user/[id].js`: 크리에이터 프로필 및 게시물
  - `app/newPost.js`: 게시물 작성기
- 재사용 가능한 프레젠테이션 컴포넌트:
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

`package.json`의 추가 의존성:
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

- Node.js 18+ (또는 최신 LTS)
- npm
- Expo CLI (`npx expo`로 실행 가능)
- AWS 계정과 Amplify CLI(필요 시 `src/aws-exports.js` 생성용)
- Expo Go가 설치된 iOS/Android 시뮬레이터 또는 실기기

## 📥 Clone repo 🔧

```bash

git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ Installation 🔧

```bash
npm install
```

`package.json`의 스크립트:

```bash
npm start
npm run android
npm run ios
npm run web
```

앱 실행:

```bash
npm start
```

## 🔐 Configuration

### Amplify backend

앱은 `app/_layout.js`에서 `../src/aws-exports`를 import합니다. 이 파일은 런타임에 필요하며 커밋되지 않도록 의도되어 있습니다.

일반적인 로컬 설정:

```bash
npm install -g @aws-amplify/cli
amplify pull
```

프롬프트가 표시되면, 이 저장소에 해당하는 기존 AWS Amplify 프로젝트/환경을 선택합니다.

### Data model assumptions from committed schema

- `User`: `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` 필드와 `Post`와의 관계가 포함됩니다.
- `Post`: `id`, `text`, `image`, `likes`, `userID` 필드를 포함합니다.
- 두 모델 모두 현재 커밋된 스키마/인증 설정에서 public read-level 가시성으로 구성되어 있습니다.

### Expo / routing / Babel

- `index.js`는 React Native 진입점과 `expo-router/entry`를 연결합니다.
- `babel.config.js`에는 `expo-router/babel`, `react-native-reanimated/plugin`, `@babel/plugin-proposal-export-namespace-from`가 포함됩니다.

## ▶️ Usage

1. 의존성을 설치하고 로컬 `src/aws-exports.js`를 생성/준비합니다.
2. Metro를 시작합니다.
   ```bash
   npm start
   ```
3. Expo Go, 시뮬레이터 또는 웹에서 앱을 엽니다.
4. Authenticator로 회원가입/로그인합니다.
5. `/`에서 크리에이터를 탐색합니다.
6. `/user/:id`에서 크리에이터 프로필을 엽니다.
7. UI에서 구독 상태를 토글합니다.
8. `/newPost`에서 새 게시물을 작성하고, 필요 시 미디어 첨부 파일을 추가합니다.

## 🧱 Data Model Notes

모델은 `amplify/backend/api/OnlyFansCloneApp/schema.graphql` 및 `src/models/schema.js`에서 정의됩니다.

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

- `app/_layout.js`는 `Amplify.configure`로 Amplify를 등록하고 Hub의 `auth` 이벤트를 구독합니다.
- 로그인 이벤트가 발생할 때마다 코드가 `createUser` mutation을 트리거해 백엔드 레코드를 초기화합니다.
- `app/newPost.js`는 선택적 이미지를 업로드하고 게시물 payload를 구성한 뒤 `DataStore.save`를 통해 저장합니다.
- `src/components/Post.js`는 피드 항목 렌더링 시 작성자와 이미지 URL을 동적으로 해석합니다.
- 백엔드와 시드 데이터는 현재 저장소에서 최소한 수준이며 자동화된 설정 스크립트가 없습니다.
- 저장소에는 전용 테스트 스위트나 CI 워크플로가 구성되어 있지 않습니다.

## 🩺 Troubleshooting

- `Cannot find module '../src/aws-exports'`
  - 로컬 설정 생성을 위해 저장소 루트에서 `amplify pull`(또는 일치하는 `amplify init` 흐름) 실행
- 인증은 되지만 쿼리/뮤테이션이 실패하는 경우
  - AppSync/API 키/인증 모드와 region이 생성된 설정과 일치하는지 확인
- 이미지 업로드 실패
  - `Storage` 권한이 존재하고 앱이 미디어 라이브러리 접근 권한을 갖고 있는지 확인
- 크리에이터/피드 데이터가 비어 있는 경우
  - 초기 `User`/`Post` 레코드가 DataStore/AppSync에 존재하고 public read 규칙이 사용 사례에 적합한지 확인
- 구독 상태가 저장되지 않음
  - 현재 구현은 UI-로컬 수준으로 동작하며, 백엔드 entitlement(권한) 모델은 아직 구현되지 않았습니다.

## 🗺️ Roadmap

- 백엔드 모델에서 구독 관계/권한(엔터타이틀먼트) 영속화
- 시드 데이터 추가와 마이그레이션 친화적 리셋 플로우 추가
- 게시물 유효성 검사와 에러 상태 개선
- 자동화 테스트(단위/통합/e2e) 추가
- CI/CD 및 lint/type 검사 추가
- 다국어 문서 확장 및 i18n README 동기화 유지
- 필요 시 인증/데이터 접근 규칙 강화

## 🤝 Contributing

기여를 환영합니다.

권장 진행 방식:

```bash
git checkout -b feat/your-change
# implement change
git commit -m "feat: describe change"
git push origin feat/your-change
```

그다음 Pull Request에 다음 항목을 포함해 주세요:
- 변경 내용
- 변경 이유
- 실행 및 테스트 방법

## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## 📄 License

이 저장소에는 현재 `LICENSE` 파일이 없습니다.

관리자가 명시적인 라이선스 파일을 추가하지 않는 한 기본적으로 모든 권한은 보유됩니다.
