[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# تطبيق Full Stack مستنسخ من OnlyFans

![Expo](https://img.shields.io/badge/Expo-48-000000?logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61DAFB?logo=react&logoColor=black)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-FF9900?logo=amazonaws&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android%20%7C%20Web-blue)
![Status](https://img.shields.io/badge/Status-Active%20Prototype-2ea44f)

### تطبيق OnlyFans clone هو تطبيق Full Stack (واجهة أمامية وخلفية) للهواتف المحمولة، ويكرر الميزات والوظائف الأساسية لنفس الفكرة.

يحتوي هذا المستودع على تطبيق Expo + React Native مع خلفية AWS Amplify (Cognito, AppSync, DataStore, S3) ينفّذ تدفقات منصة صُنّاع المحتوى الأساسية:
- المصادقة باستخدام Amplify Authenticator
- تصفح قائمة صنّاع المحتوى والملفات الشخصية
- تبديل حالة الاشتراك في واجهة المستخدم (على جهة العميل في التنفيذ الحالي)
- إنشاء منشورات مع إمكانية رفع صورة اختياريًا
- عرض موجز المنشورات مع جلب المؤلف والوسائط

## 🧭 نظرة عامة

يستخدم التطبيق توجيهًا قائمًا على الملفات عبر `expo-router` داخل `app/`، بينما يتم تتبع موارد Amplify الخلفية داخل `amplify/`. عند تسجيل دخول المستخدم، يستمع التطبيق إلى أحداث مصادقة Amplify Hub ويحاول إنشاء سجل `User` مقابل في AppSync.

| المجال | التنفيذ الحالي |
|---|---|
| الواجهة الأمامية | Expo + React Native + Expo Router |
| المصادقة | Amazon Cognito عبر Amplify Authenticator |
| API | AWS AppSync GraphQL |
| مزامنة البيانات | Amplify DataStore |
| الوسائط | S3 عبر Amplify Storage |
| المنصات | iOS, Android, Web |

## ✨ الميزات

- تدفق مصادقة مدعوم بواسطة Cognito عبر `@aws-amplify/ui-react-native`
- نماذج AppSync GraphQL لـ `User` و `Post`
- تخزين البيانات ومزامنتها عبر Amplify DataStore
- رفع واسترجاع الوسائط من S3 عبر Amplify Storage
- شاشات Expo Router:
  - `app/index.js` قائمة/الصفحة الرئيسية لصنّاع المحتوى
  - `app/user/[id].js` ملف صانع المحتوى + المنشورات
  - `app/newPost.js` شاشة إنشاء المنشور

## 🛠️ التقنيات المستخدمة

(تم الحفاظ على قائمة التقنيات الأصلية وتوسيعها لتحسين الوضوح.)

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

تعتمد الحزمة أيضًا في `package.json` على:
- `expo-router`
- `@react-native-async-storage/async-storage`
- `@react-native-community/netinfo`
- `core-js`

## 🗂️ هيكل المشروع

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

## ✅ المتطلبات المسبقة

- يوصى باستخدام Node.js 18+
- npm
- استخدام Expo CLI عبر `npx expo ...`
- حساب AWS و Amplify CLI لتجهيز/سحب الخلفية
- ملف إعداد Amplify client مولّد يتم استيراده في التطبيق باسم `src/aws-exports`

## 📥 استنساخ المستودع 🔧

```bash
https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app
```

الأمر المكافئ:

```bash
git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ التثبيت 🔧

(تم الحفاظ على أوامر التثبيت الأصلية.)

```bash
npm install

npx expo start or npm start
```

سكربتات المستودع:

```bash
npm start
npm run android
npm run ios
npm run web
```

## 🔐 الإعداد

### خلفية Amplify

يقوم التطبيق باستيراد `../src/aws-exports` في `app/_layout.js`. هذا الملف غير مُلتزم في المستودع ويجب توليده محليًا.

تدفق إعداد شائع (افتراضًا بناءً على مجلد `amplify/` الملتزم و `.gitignore`):

```bash
npm install -g @aws-amplify/cli
amplify pull
```

إذا ظهرت مطالبات، استخدم مشروع/بيئة Amplify الحالية من حساب AWS الخاص بك. يشير إعداد الخلفية الملتزم إلى:
- المصادقة: Cognito (اسم مستخدم عبر البريد الإلكتروني، وخصائص التسجيل تشمل `NAME` و `NICKNAME`)
- API: AppSync مع تفعيل مصادقة API key في الإعداد
- التخزين: مورد S3 bucket مُعد مسبقًا

### Expo / Babel / Router

- يتضمن `babel.config.js` ما يلي:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`
- يقوم `index.js` بتهيئة `core-js/full/symbol/async-iterator` و `expo-router/entry`

## ▶️ الاستخدام

1. شغّل التطبيق:
   ```bash
   npm start
   ```
2. افتح التطبيق في Expo Go أو المحاكي أو الويب.
3. أنشئ حسابًا/سجّل الدخول عبر واجهة Amplify Authenticator.
4. تصفح صنّاع المحتوى في الشاشة الرئيسية.
5. افتح ملف صانع محتوى (`/user/[id]`).
6. بدّل حالة الاشتراك في الواجهة.
7. أنشئ منشورًا جديدًا من `New post`، مع إمكانية إرفاق صورة من مكتبة الوسائط.

## 🧱 نموذج البيانات

من `amplify/backend/api/OnlyFansCloneApp/schema.graphql`:

- `User`: الحقول `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` مع علاقة بالمنشورات
- `Post`: الحقول `id`, `text`, `image`, `likes`, `userID`

يستخدم النموذجان قواعد مصادقة عامة في المخطط الحالي.

| النموذج | الحقول الأساسية |
|---|---|
| `User` | `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` |
| `Post` | `id`, `text`, `image`, `likes`, `userID` |

## 📱 أمثلة من التطبيق

### تحتاج إلى إنشاء حساب مجاني لاستخدام التطبيق

![Screenshot_20230424-200925](https://user-images.githubusercontent.com/64506662/234364566-863bc1e1-e289-4b9b-9658-a11e737bebd8.png)
![Screenshot_20230424-200957](https://user-images.githubusercontent.com/64506662/234364579-8e32708f-cb69-4c1c-82e3-eefd7cb5f161.png)
![Screenshot_20230424-201003](https://user-images.githubusercontent.com/64506662/234364622-e9cc5d14-77f2-415f-9027-1d3ffe3e7c17.png)
![Screenshot_20230424-201006](https://user-images.githubusercontent.com/64506662/234364653-73de6b92-b7a6-4ef7-a3a6-c26411bfd46a.png)
![Screenshot_20230424-201031](https://user-images.githubusercontent.com/64506662/234364754-f5ce7da1-1ad1-4e90-bf85-40add436ad23.png)

## 🧪 ملاحظات التطوير

- يستمع `app/_layout.js` إلى أحداث تسجيل الدخول `auth` من Amplify Hub وينفّذ طفرة GraphQL باسم `createUser`.
- يتم حفظ المنشورات الجديدة عبر DataStore، وتُرفع الصور الاختيارية عبر `Storage.put`.
- سلوك الاشتراك في الملف الشخصي هو حالة واجهة محلية حاليًا وغير محفوظ كنموذج اشتراك في الخلفية.
- لا يحتوي المستودع حاليًا على مجموعة اختبارات آلية صريحة أو ملفات سير عمل CI.

## 🩺 استكشاف الأخطاء وإصلاحها

- `Cannot find module '../src/aws-exports'`:
  - شغّل `amplify pull` (أو تدفق تهيئة Amplify مكافئ) لتوليد الإعداد المحلي.
- المصادقة تعمل لكن عمليات البيانات تفشل:
  - تأكد أن إعداد AppSync/API key/وضع المصادقة في بيئة Amplify يطابق الإعداد المحلي المُولّد.
- مشاكل رفع الصور:
  - تحقّق من صلاحيات S3 في Amplify storage وتأكد من منح الجهاز إذن الوصول لمكتبة الوسائط.
- بيانات الملف/الموجز فارغة:
  - تأكد من وجود سجلات `User`/`Post` مُهيأة وأن قواعد المصادقة الحالية تسمح بعمليات القراءة.

## 🗺️ خارطة الطريق

- إضافة علاقات اشتراك محفوظة والتحقق من الاستحقاق
- إضافة التحقق من الإدخالات ومعالجة أخطاء أغنى لتدفقات إنشاء/رفع المنشورات
- إضافة اختبارات (unit/integration/e2e) وخط أنابيب CI
- إضافة نسخ README متعددة اللغات وملء موارد `i18n/`
- تقوية قواعد المصادقة/الوصول (استبدال القواعد العامة الواسعة حيث يلزم)

## 🤝 المساهمة

المساهمات مرحّب بها.

تدفق مقترح:

```bash
git checkout -b feat/your-change
# implement change
git commit -m "feat: describe change"
git push origin feat/your-change
```

ثم افتح Pull Request يتضمن:
- ما الذي تغيّر
- لماذا تغيّر
- كيف يمكن تشغيله/اختباره

## 📄 الترخيص

لا يوجد ملف `LICENSE` حاليًا في هذا المستودع.

افتراض: جميع الحقوق محفوظة افتراضيًا ما لم يضف المسؤول ملف ترخيص صريحًا.
