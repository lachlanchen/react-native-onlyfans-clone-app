[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# OnlyFans 克隆全栈应用

![Expo](https://img.shields.io/badge/Expo-48-000000?logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61DAFB?logo=react&logoColor=black)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-FF9900?logo=amazonaws&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android%20%7C%20Web-blue)
![Status](https://img.shields.io/badge/Status-Active%20Prototype-2ea44f)

### OnlyFans 克隆应用是一个全栈应用，包含移动端前端与后端，复刻了相同的特性与功能。

本仓库包含一个 Expo + React Native 应用，并配套 AWS Amplify 后端（Cognito、AppSync、DataStore、S3），实现了创作者平台的核心流程：
- 使用 Amplify Authenticator 进行身份认证
- 创作者列表与个人主页浏览
- 订阅 UI 状态切换（当前实现为客户端侧）
- 支持可选图片上传的发帖
- 带作者与媒体资源读取的动态流渲染

## 🧭 概览

应用在 `app/` 下使用 `expo-router` 的基于文件路由；Amplify 后端资源在 `amplify/` 下追踪。用户登录后，应用会监听 Amplify Hub 的 auth 事件，并尝试在 AppSync 中创建对应的 `User` 记录。

| 区域 | 当前实现 |
|---|---|
| 前端 | Expo + React Native + Expo Router |
| 认证 | 通过 Amplify Authenticator 接入 Amazon Cognito |
| API | AWS AppSync GraphQL |
| 数据同步 | Amplify DataStore |
| 媒体 | 通过 Amplify Storage 使用 S3 |
| 平台 | iOS、Android、Web |

## ✨ 功能

- 通过 `@aws-amplify/ui-react-native` 使用 Cognito 驱动的认证流程
- 面向 `User` 与 `Post` 的 AppSync GraphQL 模型
- 通过 Amplify DataStore 进行数据持久化与同步
- 通过 Amplify Storage 完成 S3 媒体上传与读取
- Expo Router 页面：
  - `app/index.js` 创作者列表/首页
  - `app/user/[id].js` 创作者主页 + 帖子
  - `app/newPost.js` 发帖页面

## 🛠️ 技术栈

（保留原始技术栈列表，并为清晰性做了扩展。）

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

`package.json` 中还包含以下仓库依赖：
- `expo-router`
- `@react-native-async-storage/async-storage`
- `@react-native-community/netinfo`
- `core-js`

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

## ✅ 前置要求

- 推荐 Node.js 18+
- npm
- 通过 `npx expo ...` 使用 Expo CLI
- 用于后端创建/拉取的 AWS 账号与 Amplify CLI
- 应用以 `src/aws-exports` 导入的 Amplify 客户端配置文件（需本地生成）

## 📥 克隆仓库 🔧

```bash
https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app
```

等价命令：

```bash
git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ 安装 🔧

（保留原始安装命令。）

```bash
npm install

npx expo start or npm start
```

仓库脚本：

```bash
npm start
npm run android
npm run ios
npm run web
```

## 🔐 配置

### Amplify 后端

应用在 `app/_layout.js` 中导入 `../src/aws-exports`。该文件未提交，需要在本地生成。

典型初始化流程（根据已提交的 `amplify/` 文件夹与 `.gitignore` 推断）：

```bash
npm install -g @aws-amplify/cli
amplify pull
```

若有提示，请使用你 AWS 账号中已存在的 Amplify 项目/环境。已提交的后端配置显示：
- 认证：Cognito（email 作为用户名，注册属性包含 `NAME` 与 `NICKNAME`）
- API：AppSync + 配置中启用了 API key 认证
- 存储：已配置 S3 bucket 资源

### Expo / Babel / Router

- `babel.config.js` 包含：
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`
- `index.js` 初始化了 `core-js/full/symbol/async-iterator` 与 `expo-router/entry`

## ▶️ 使用方式

1. 启动应用：
   ```bash
   npm start
   ```
2. 在 Expo Go / 模拟器 / Web 中打开。
3. 通过 Amplify Authenticator UI 完成注册/登录。
4. 在首页浏览创作者。
5. 打开创作者主页（`/user/[id]`）。
6. 在 UI 中切换订阅状态。
7. 从 `New post` 创建新帖子，并可选附加媒体库图片。

## 🧱 数据模型

来自 `amplify/backend/api/OnlyFansCloneApp/schema.graphql`：

- `User`：`id`、`name`、`handle`、`bio`、`avatar`、`coverImage`、`subscriptionPrice`、与帖子关系
- `Post`：`id`、`text`、`image`、`likes`、`userID`

当前 schema 中两个模型都使用了 public auth 规则。

| 模型 | 关键字段 |
|---|---|
| `User` | `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` |
| `Post` | `id`, `text`, `image`, `likes`, `userID` |

## 📱 示例应用

### 你需要创建一个免费账号才能使用该应用

![Screenshot_20230424-200925](https://user-images.githubusercontent.com/64506662/234364566-863bc1e1-e289-4b9b-9658-a11e737bebd8.png)
![Screenshot_20230424-200957](https://user-images.githubusercontent.com/64506662/234364579-8e32708f-cb69-4c1c-82e3-eefd7cb5f161.png)
![Screenshot_20230424-201003](https://user-images.githubusercontent.com/64506662/234364622-e9cc5d14-77f2-415f-9027-1d3ffe3e7c17.png)
![Screenshot_20230424-201006](https://user-images.githubusercontent.com/64506662/234364653-73de6b92-b7a6-4ef7-a3a6-c26411bfd46a.png)
![Screenshot_20230424-201031](https://user-images.githubusercontent.com/64506662/234364754-f5ce7da1-1ad1-4e90-bf85-40add436ad23.png)

## 🧪 开发说明

- `app/_layout.js` 监听 Amplify Hub 的 `auth` 登录事件，并执行 `createUser` GraphQL mutation。
- 新帖子通过 DataStore 保存，可选图片通过 `Storage.put` 上传。
- 主页订阅行为目前仅为本地 UI 状态，未持久化为后端订阅模型。
- 当前仓库没有明确的自动化测试套件或 CI 工作流文件。

## 🩺 故障排查

- `Cannot find module '../src/aws-exports'`：
  - 运行 `amplify pull`（或等价的 Amplify 初始化流程）以生成本地配置。
- 认证正常但数据操作失败：
  - 确认 Amplify 环境中的 AppSync/API key/认证模式配置与本地生成配置一致。
- 图片上传问题：
  - 检查 Amplify storage 中的 S3 权限，并确保设备已授权媒体库访问。
- 动态流/主页数据为空：
  - 确保已存在初始化的 `User`/`Post` 记录，且当前认证规则允许读取。

## 🗺️ 路线图

- 添加可持久化的订阅关系与权限校验
- 为发帖/上传流程增加校验与更完善的错误处理
- 增加测试（unit/integration/e2e）与 CI 流水线
- 增加多语言 README 变体并完善 `i18n/` 资源
- 加固认证/访问规则（在必要处替换过宽的 public 规则）

## 🤝 贡献

欢迎贡献。

建议流程：

```bash
git checkout -b feat/your-change
# implement change
git commit -m "feat: describe change"
git push origin feat/your-change
```

然后提交 Pull Request，包含：
- 改了什么
- 为什么改
- 如何运行/测试

## 📄 许可证

当前仓库中不存在 `LICENSE` 文件。

推断：除非维护者添加明确的许可证文件，否则默认保留所有权利。
