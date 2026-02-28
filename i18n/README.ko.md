[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# OnlyFans clone Full Stack App

![Expo](https://img.shields.io/badge/Expo-48-000000?logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61DAFB?logo=react&logoColor=black)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-FF9900?logo=amazonaws&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android%20%7C%20Web-blue)
![Status](https://img.shields.io/badge/Status-Active%20Prototype-2ea44f)

### OnlyFans 클론 앱은 프론트엔드와 백엔드를 포함한 풀스택 앱이며, 동일한 기능과 동작을 재현합니다.

이 저장소는 핵심 크리에이터 플랫폼 플로우를 구현한 Expo + React Native 앱과 AWS Amplify 백엔드(Cognito, AppSync, DataStore, S3)를 포함합니다.
- Amplify Authenticator를 통한 인증
- 크리에이터 목록 및 프로필 탐색
- 구독 UI 상태 토글(현재 구현에서는 클라이언트 사이드)
- 선택적 이미지 업로드를 포함한 게시물 작성
- 작성자 및 미디어 조회를 포함한 게시물 피드 렌더링

## 🧭 개요

앱은 `app/` 아래에서 `expo-router` 기반 파일 라우팅을 사용하며, Amplify 백엔드 리소스는 `amplify/` 아래에서 관리됩니다. 사용자가 로그인하면 앱은 Amplify Hub 인증 이벤트를 수신하고 AppSync에 해당 `User` 레코드를 생성하려고 시도합니다.

| 영역 | 현재 구현 |
|---|---|
| Frontend | Expo + React Native + Expo Router |
| Auth | Amplify Authenticator를 통한 Amazon Cognito |
| API | AWS AppSync GraphQL |
| Data sync | Amplify DataStore |
| Media | Amplify Storage를 통한 S3 |
| Platforms | iOS, Android, Web |

## ✨ 기능

- `@aws-amplify/ui-react-native`를 통한 Cognito 인증 플로우
- `User`, `Post`를 위한 AppSync GraphQL 모델
- Amplify DataStore를 통한 데이터 저장 및 동기화
- Amplify Storage를 통한 S3 미디어 업로드 및 조회
- Expo Router 화면:
  - `app/index.js` 크리에이터 목록/홈
  - `app/user/[id].js` 크리에이터 프로필 + 게시물
  - `app/newPost.js` 게시물 작성기

## 🛠️ 사용 기술

(원본 스택 목록은 보존하고, 가독성을 위해 확장했습니다.)

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

`package.json`에 포함된 추가 저장소 의존성:
- `expo-router`
- `@react-native-async-storage/async-storage`
- `@react-native-community/netinfo`
- `core-js`

## 🗂️ 프로젝트 구조

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

## ✅ 사전 요구사항

- Node.js 18+ 권장
- npm
- `npx expo ...`를 통한 Expo CLI 사용
- 백엔드 프로비저닝/동기화를 위한 AWS 계정 및 Amplify CLI
- 앱에서 `src/aws-exports`로 import하는 생성된 Amplify 클라이언트 설정 파일

## 📥 저장소 클론 🔧

```bash
https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app
```

동일한 명령:

```bash
git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ 설치 🔧

(원본 설치 명령을 보존했습니다.)

```bash
npm install

npx expo start or npm start
```

저장소 스크립트:

```bash
npm start
npm run android
npm run ios
npm run web
```

## 🔐 설정

### Amplify 백엔드

앱은 `app/_layout.js`에서 `../src/aws-exports`를 import합니다. 이 파일은 커밋되지 않으며 로컬에서 생성해야 합니다.

일반적인 설정 흐름(`amplify/` 폴더와 `.gitignore` 기준 추정):

```bash
npm install -g @aws-amplify/cli
amplify pull
```

프롬프트가 표시되면 AWS 계정의 기존 Amplify 프로젝트/환경을 사용하세요. 커밋된 백엔드 설정 기준:
- Auth: Cognito(이메일 사용자명, 가입 속성에 `NAME`, `NICKNAME` 포함)
- API: AppSync + 설정에서 API key 인증 활성화
- Storage: S3 버킷 리소스 구성됨

### Expo / Babel / Router

- `babel.config.js` 포함 항목:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`
- `index.js`는 `core-js/full/symbol/async-iterator` 및 `expo-router/entry`를 초기화합니다.

## ▶️ 사용 방법

1. 앱 시작:
   ```bash
   npm start
   ```
2. Expo Go/에뮬레이터/웹에서 실행합니다.
3. Amplify Authenticator UI에서 회원가입/로그인합니다.
4. 홈 화면에서 크리에이터를 탐색합니다.
5. 크리에이터 프로필(`/user/[id]`)을 엽니다.
6. UI에서 구독 상태를 토글합니다.
7. `New post`에서 새 게시물을 작성하고, 필요하면 미디어 라이브러리에서 이미지를 첨부합니다.

## 🧱 데이터 모델

`amplify/backend/api/OnlyFansCloneApp/schema.graphql` 기준:

- `User`: `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`, 게시물 관계
- `Post`: `id`, `text`, `image`, `likes`, `userID`

현재 스키마에서 두 모델 모두 public auth 규칙을 사용합니다.

| 모델 | 핵심 필드 |
|---|---|
| `User` | `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` |
| `Post` | `id`, `text`, `image`, `likes`, `userID` |

## 📱 앱 예시

### 앱을 사용하려면 무료 계정을 생성해야 합니다

![Screenshot_20230424-200925](https://user-images.githubusercontent.com/64506662/234364566-863bc1e1-e289-4b9b-9658-a11e737bebd8.png)
![Screenshot_20230424-200957](https://user-images.githubusercontent.com/64506662/234364579-8e32708f-cb69-4c1c-82e3-eefd7cb5f161.png)
![Screenshot_20230424-201003](https://user-images.githubusercontent.com/64506662/234364622-e9cc5d14-77f2-415f-9027-1d3ffe3e7c17.png)
![Screenshot_20230424-201006](https://user-images.githubusercontent.com/64506662/234364653-73de6b92-b7a6-4ef7-a3a6-c26411bfd46a.png)
![Screenshot_20230424-201031](https://user-images.githubusercontent.com/64506662/234364754-f5ce7da1-1ad1-4e90-bf85-40add436ad23.png)

## 🧪 개발 노트

- `app/_layout.js`는 Amplify Hub `auth` 로그인 이벤트를 수신하고 `createUser` GraphQL mutation을 실행합니다.
- 새 게시물은 DataStore에 저장되며, 선택적 이미지는 `Storage.put`으로 업로드됩니다.
- 프로필 구독 동작은 현재 로컬 UI 상태이며 백엔드 구독 모델로는 저장되지 않습니다.
- 현재 저장소에는 명시적인 자동 테스트 스위트 또는 CI 워크플로 파일이 없습니다.

## 🩺 문제 해결

- `Cannot find module '../src/aws-exports'`:
  - 로컬 설정 생성을 위해 `amplify pull`(또는 동등한 Amplify init 플로우)을 실행하세요.
- 인증은 되지만 데이터 작업이 실패하는 경우:
  - Amplify 환경의 AppSync/API key/auth mode 설정이 로컬 생성 설정과 일치하는지 확인하세요.
- 이미지 업로드 이슈:
  - Amplify storage의 S3 권한과 디바이스 미디어 라이브러리 접근 권한을 확인하세요.
- 피드/프로필 데이터가 비어 있는 경우:
  - 시드된 `User`/`Post` 레코드가 존재하고 현재 auth 규칙이 읽기를 허용하는지 확인하세요.

## 🗺️ 로드맵

- 영속 구독 관계 및 권한(entitlement) 검증 추가
- 게시물 작성/업로드 플로우에 검증 및 향상된 오류 처리 추가
- 테스트(단위/통합/e2e) 및 CI 파이프라인 추가
- 다국어 README 변형 추가 및 `i18n/` 리소스 채우기
- 인증/접근 규칙 강화(필요 시 광범위한 public 규칙 대체)

## 🤝 기여

기여를 환영합니다.

권장 흐름:

```bash
git checkout -b feat/your-change
# implement change
git commit -m "feat: describe change"
git push origin feat/your-change
```

그다음 아래 내용을 포함해 Pull Request를 열어주세요:
- 변경된 내용
- 변경 이유
- 실행/테스트 방법

## 📄 라이선스

현재 이 저장소에는 `LICENSE` 파일이 없습니다.

가정: 관리자가 명시적 라이선스 파일을 추가하지 않는 한 기본적으로 모든 권리는 보유됩니다.
