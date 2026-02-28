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

语言选项：**English（当前草案）**。翻译版本位于 `i18n/` 下。

### OnlyFans 克隆应用是一个面向移动端和网页的全栈应用，复现了创作者平台风格的功能与流程。

该仓库包含一个使用 AWS Amplify 后端（`Cognito`、`AppSync`、`DataStore`、`S3`）的 Expo + React Native 应用，实现了创作者平台的克隆版本。它包含身份验证、创作者浏览、帖子创建、媒体上传和订阅 UI 状态流程。

## 🧭 概览

该应用在 `app/` 中使用 Expo Router 构建，并通过本地 Amplify 数据层与 `amplify/` 中提交的后端资源关联。

| 区域 | 当前实现 |
|---|---|
| 前端 | Expo + React Native + Expo Router |
| 路由 | `app/` 中的文件式路由 |
| 身份验证 | 通过 `@aws-amplify/ui-react-native` 使用 Amazon Cognito |
| API | AWS AppSync GraphQL |
| 数据同步 | Amplify DataStore |
| 媒体 | 通过 Amplify Storage 使用 S3 |
| 平台 | iOS、Android、Web |

在登录时，`app/_layout.js` 会监听 Amplify Hub 的 auth 事件，并尝试在 AppSync 中创建 `User` 记录；这在应用启动阶段完成。

## ✨ 特性

- Cognito 驱动的认证流程，使用 Amplify Authenticator
- `User` 与 `Post` 的 AppSync GraphQL 模型
- 通过 Amplify DataStore 持久化与同步数据
- 通过 Amplify Storage 上传与读取 S3 图片
- Expo Router 的文件式路由：
  - `app/index.js`：创作者列表与首页信息流
  - `app/user/[id].js`：创作者资料页与帖子
  - `app/newPost.js`：发帖编辑页
- 可复用展示组件：
  - `src/components/UserCard.js`
  - `src/components/UserProfileHeader.js`
  - `src/components/Post.js`

## 🛠️ 技术栈

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

`package.json` 中的其他依赖包括：
- `@react-native-async-storage/async-storage`
- `@react-native-community/netinfo`
- `core-js`
- `expo-constants`、`expo-linking`、`expo-updates` 及图标/界面工具链相关依赖

## 🗂️ 项目结构

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

## ✅ 先决条件

- Node.js 18+（或现代 LTS 版本）
- npm
- Expo CLI（可通过 `npx expo` 运行）
- AWS 账户与 Amplify CLI（若需要生成 `src/aws-exports.js`）
- 可用于测试的 Apple/Android 模拟器，或安装了 Expo Go 的真机

## 📥 克隆仓库 🔧

```bash
git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ 安装 🔧

```bash
npm install
```

`package.json` 中的仓库脚本：

```bash
npm start
npm run android
npm run ios
npm run web
```

然后启动应用：

```bash
npm start
```

## 🔐 配置

### Amplify 后端

应用在 `app/_layout.js` 中导入 `../src/aws-exports`。该文件在运行时是必需的，并且特意不提交到仓库。

本地设置示例：

```bash
npm install -g @aws-amplify/cli
amplify pull
```

若出现提示，请选择此仓库对应的现有 AWS Amplify 项目/环境。

### 来源于提交 schema 的数据模型约定

- `User`：字段包含 `id`、`name`、`handle`、`bio`、`avatar`、`coverImage`、`subscriptionPrice`，并与 `Post` 存在关联
- `Post`：字段包含 `id`、`text`、`image`、`likes`、`userID`
- 两个模型当前均在已提交的 schema 与权限配置中设置为公共读取可见

### Expo / 路由 / Babel

- `index.js` 挂载了 React Native 入口与 `expo-router/entry`
- `babel.config.js` 包含 `expo-router/babel`、`react-native-reanimated/plugin` 和 `@babel/plugin-proposal-export-namespace-from`

## ▶️ 使用方法

1. 安装依赖并生成/获取本地 `src/aws-exports.js`
2. 启动 Metro：
   ```bash
   npm start
   ```
3. 在 Expo Go、模拟器或 Web 中打开应用
4. 通过 Authenticator 注册或登录
5. 在 `/` 浏览创作者列表
6. 在 `/user/:id` 打开创作者详情页
7. 在 UI 中切换订阅状态
8. 在 `/newPost` 创建帖子，可选附加媒体文件

## 🧱 数据模型说明

模型定义位于 `amplify/backend/api/OnlyFansCloneApp/schema.graphql` 和 `src/models/schema.js`。

| 模型 | 关键字段 |
|---|---|
| `User` | `id`、`name`、`handle`、`bio`、`avatar`、`coverImage`、`subscriptionPrice` |
| `Post` | `id`、`text`、`image`、`likes`、`userID` |

## 📱 示例

### 截图演示

![Screenshot_20230424-200925](https://user-images.githubusercontent.com/64506662/234364566-863bc1e1-e289-4b9b-9658-a11e737bebd8.png)
![Screenshot_20230424-200957](https://user-images.githubusercontent.com/64506662/234364579-8e32708f-cb69-4c1c-82e3-eefd7cb5f161.png)
![Screenshot_20230424-201003](https://user-images.githubusercontent.com/64506662/234364622-e9cc5d14-77f2-415f-9027-1d3ffe3e7c17.png)
![Screenshot_20230424-201006](https://user-images.githubusercontent.com/64506662/234364653-73de6b92-b7a6-4ef7-a3a6-c26411bfd46a.png)
![Screenshot_20230424-201031](https://user-images.githubusercontent.com/64506662/234364754-f5ce7da1-1ad1-4e90-bf85-40add436ad23.png)

## 🧪 开发说明

- `app/_layout.js` 在启动时通过 `Amplify.configure` 注册 Amplify，并订阅 Hub 的 `auth` 事件。
- 每次登录事件触发时，代码会执行 `createUser` mutation，以初始化后端记录。
- `app/newPost.js` 可选上传图片，拼装帖子 payload，并通过 `DataStore.save` 持久化。
- `src/components/Post.js` 在渲染动态流时动态解析作者与图片链接。
- 后端和种子数据当前是最小化的，仓库中尚无自动化初始化脚本。
- 仓库中尚未配置专门的测试套件或 CI 工作流。

## 🩺 故障排查

- `Cannot find module '../src/aws-exports'`
  - 从仓库根目录运行 `amplify pull`（或匹配的 `amplify init` 流程）以生成本地配置。
- 认证成功但查询/变更失败
  - 确认 AppSync/API key/auth 模式和区域与导入的生成配置一致。
- 图片上传失败
  - 确认存在 `Storage` 权限，并且应用已获得媒体库访问权限。
- 创作者/动态数据为空
  - 确认 DataStore/AppSync 中存在初始 `User`/`Post` 记录，并且公开读取规则符合你的使用场景。
- 订阅状态未持久化
  - 当前实现似乎仅是 UI 本地状态；后端权利关系模型尚未实现。

## 🗺️ 路线图

- 在后端模型中持久化订阅关系与权利
- 增加种子数据，并提供友好的数据迁移重置流程
- 改进帖子校验与错误状态处理
- 增加自动化测试（单元/集成/e2e）
- 增加 CI/CD 与 lint/type 检查
- 扩展多语言文档并保持 i18n README 同步
- 按需加固认证与数据访问权限规则

## 🤝 贡献

欢迎提交贡献。

建议流程：

```bash
git checkout -b feat/your-change
# implement change
git commit -m "feat: describe your change"
git push origin feat/your-change
```

然后建立 Pull Request，并说明：
- 变更内容
- 为何修改
- 如何运行/测试

## 📄 许可证

当前仓库中暂无 `LICENSE` 文件。

假设：除非维护者添加明确的许可文件，否则默认保留所有权利。


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
