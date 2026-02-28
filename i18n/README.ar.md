[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# تطبيق شامل لنموذج OnlyFans كامل

![Expo](https://img.shields.io/badge/Expo-48-000000?logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61DAFB?logo=react&logoColor=black)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-FF9900?logo=amazonaws&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android%20%7C%20Web-blue)
![Status](https://img.shields.io/badge/Status-Active%20Prototype-2ea44f)
![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?logo=nodedotjs&logoColor=white)
![Repo%20Size](https://img.shields.io/github/repo-size/GonzaloVolonterio/react-native-onlyfans-clone-app?label=Repo%20Size&color=0f766e)

خيارات اللغة: **الإنجليزية (المسودة الحالية)**. تتوفر الترجمات في مجلد `i18n/`.

### تطبيق شبيه بتطبيق OnlyFans هو تطبيق Full Stack للهواتف المحمولة والويب يُعيد تنفيذ ميزات تدفق العمل ونمط واجهة منصة إنشاء المحتوى.

يحتوي هذا المستودع على تطبيق Expo + React Native مع خلفية AWS Amplify (`Cognito` و `AppSync` و`DataStore` و`S3`) يُطبّق نسخة شبيهة بمنصة للمبدعين. ويشمل المصادقة، وتصفح المبدعين، وإنشاء المشاركات، ورفع الوسائط، وسير حالة الاشتراك في واجهة المستخدم.

## 🧭 نظرة عامة

تم بناء التطبيق باستخدام Expo Router داخل `app/` وطبقة بيانات Amplify محلية مرتبطة بموارد backend الملتزمة الموجودة في `amplify/`.

| المجال | التنفيذ الحالي |
|---|---|
| الواجهة الأمامية | Expo + React Native + Expo Router |
| التوجيه | التوجيه المستند إلى الملفات داخل `app/` |
| المصادقة | Amazon Cognito عبر `@aws-amplify/ui-react-native` |
| الواجهة البرمجية | GraphQL عبر AWS AppSync |
| مزامنة البيانات | Amplify DataStore |
| الوسائط | S3 عبر Amplify Storage |
| المنصات | iOS، Android، Web |

عند تسجيل الدخول، يستمع `app/_layout.js` لأحداث المصادقة من Amplify Hub ويحاول إنشاء سجل `User` في AppSync. يتم ذلك أثناء تهيئة التطبيق.

## ✨ المزايا

- تدفق مصادقة يعتمد على Cognito مع `Amplify Authenticator`
- نماذج GraphQL في AppSync للكائنات `User` و `Post`
- حفظ ومزامنة البيانات عبر Amplify DataStore
- رفع الصور واسترجاعها عبر Amplify Storage
- توجيه يعتمد على الملفات في Expo Router:
  - `app/index.js`: قائمة المبدعين والخلاصة الرئيسية
  - `app/user/[id].js`: ملف المبدع الشخصي والمشاركات
  - `app/newPost.js`: محرر إنشاء المشاركة
- مكونات عرض قابلة لإعادة الاستخدام:
  - `src/components/UserCard.js`
  - `src/components/UserProfileHeader.js`
  - `src/components/Post.js`

## 🛠️ مبني باستخدام

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

تشمل الاعتمادات الإضافية من `package.json`:
- `@react-native-async-storage/async-storage`
- `@react-native-community/netinfo`
- `core-js`
- `expo-constants`, `expo-linking`, `expo-updates`، وأدوات الأيقونات والشاشات

## 🗂️ هيكلة المشروع

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
│  └─ aws-exports.js (تم توليده محليًا؛ غير مرفوع)
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

## ✅ المتطلبات المسبقة

- Node.js 18+ (أو LTS حديث)
- npm
- Expo CLI (يمكن تشغيله عبر `npx expo`)
- حساب AWS وAmplify CLI إذا احتجت إنشاء `src/aws-exports.js`
- محاكي iOS/Android أو جهاز فعلي مع Expo Go لاختبار التطبيق

## 📥 استنساخ المستودع 🔧

```bash
git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ التثبيت 🔧

```bash
npm install
```

سكريبتات المستودع من `package.json`:

```bash
npm start
npm run android
npm run ios
npm run web
```

ثم تشغيل التطبيق:

```bash
npm start
```

## 🔐 الإعدادات

### backend Amplify

يستورد التطبيق الملف `../src/aws-exports` داخل `app/_layout.js`. هذا الملف مطلوب أثناء التشغيل ولم يتم تضمينه عمدًا في المستودع.

الإعداد المحلي النموذجي:

```bash
npm install -g @aws-amplify/cli
amplify pull
```

إذا طُلب منك، اختر مشروع AWS Amplify/البيئة الموجودة لهذا المستودع.

### افتراضات نموذج البيانات من المخطط الملتزم به

- `User`: الحقول تشمل `id` و `name` و `handle` و `bio` و `avatar` و `coverImage` و `subscriptionPrice` وعلاقة مع `Post`
- `Post`: الحقول تشمل `id` و `text` و `image` و `likes` و `userID`
- كلا النموذجين مهيأان حاليًا لقراءة عامة في مستويات الرؤية ضمن إعدادات المخطط/المصادقة الملتزم بها

### Expo / التوجيه / Babel

- `index.js` يهيئ نقطة دخول React Native و `expo-router/entry`
- `babel.config.js` يتضمن `expo-router/babel` و`react-native-reanimated/plugin` وبلجن اقتراح التصدير بالمساحات الاسمية

## ▶️ الاستخدام

1. ثبّت التبعيات وأنشئ/احصل على ملف `src/aws-exports.js` المحلي
2. شغّل Metro:
   ```bash
   npm start
   ```
3. افتح التطبيق داخل Expo Go أو محاكي أو الويب
4. سجّل الدخول أو أنشئ حسابًا عبر Authenticator
5. تصفّح المبدعين في `/`
6. افتح ملف المبدع في `/user/:id`
7. بدّل حالة الاشتراك في واجهة المستخدم
8. أنشئ المشاركات في `/newPost`، مع إرفاق وسائط اختياري

## 🧱 ملاحظات نموذج البيانات

النماذج معرفة في `amplify/backend/api/OnlyFansCloneApp/schema.graphql` و`src/models/schema.js`.

| النموذج | الحقول الرئيسية |
|---|---|
| `User` | `id` و `name` و `handle` و `bio` و `avatar` و `coverImage` و `subscriptionPrice` |
| `Post` | `id` و `text` و `image` و `likes` و `userID` |

## 📱 أمثلة

### لقطات تجريبية

![Screenshot_20230424-200925](https://user-images.githubusercontent.com/64506662/234364566-863bc1e1-e289-4b9b-9658-a11e737bebd8.png)
![Screenshot_20230424-200957](https://user-images.githubusercontent.com/64506662/234364579-8e32708f-cb69-4c1c-82e3-eefd7cb5f161.png)
![Screenshot_20230424-201003](https://user-images.githubusercontent.com/64506662/234364622-e9cc5d14-77f2-415f-9027-1d3ffe3e7c17.png)
![Screenshot_20230424-201006](https://user-images.githubusercontent.com/64506662/234364653-73de6b92-b7a6-4ef7-a3a6-c26411bfd46a.png)
![Screenshot_20230424-201031](https://user-images.githubusercontent.com/64506662/234364754-f5ce7da1-1ad1-4e90-bf85-40add436ad23.png)

## 🧪 ملاحظات التطوير

- `app/_layout.js` يسجل Amplify باستخدام `Amplify.configure` ويرتبط بأحداث `auth` من Hub.
- في كل حدث تسجيل دخول، تُنفّذ التعليمات البرمجية الطلوبة `createUser` حتى يتم تهيئة سجل في الخلفية.
- `app/newPost.js` يرفع صورة اختيارية، يجمع حمولة المشاركة، ثم يحفظها عبر `DataStore.save`.
- `src/components/Post.js` يحل مؤلفي المشاركات وعناوين الصور ديناميكيًا أثناء عرض عناصر الخلاصة.
- البيانات الأولية في الخلفية والحزم التهيئية حالياً محدودة ولا يوجد سكربت إعداد آلي في المستودع.
- لا توجد حزمة اختبارات مخصصة أو سير عمل CI مكوَّن في هذا المستودع.

## 🩺 استكشاف الأخطاء وإصلاحها

- `Cannot find module '../src/aws-exports'`
  - شغّل `amplify pull` (أو مسار `amplify init` المناظر له) من جذر المستودع لإنشاء ملف الإعداد المحلي.
- نجحت المصادقة لكن الاستعلامات/التعديلات تفشل
  - تأكد من تطابق مفتاح AppSync/API ونمط المصادقة والمنطقة الجغرافية مع ملف الإعداد المولّد المستورد.
- فشل رفع الصور
  - تأكد من وجود صلاحيات `Storage` وأن التطبيق يملك إذن الوصول إلى مكتبة الوسائط.
- البيانات في صفحة المبدعين/الخلاصة فارغة
  - تأكد من وجود سجلات أولية لـ `User` و`Post` في DataStore/AppSync وأن قواعد القراءة العامة تناسب حالة استخدامك.
- حالة الاشتراك في المشاركة لا تُحفظ
  - يبدو أن التنفيذ الحالي يعتمد على الواجهة فقط؛ نموذج الامتيازات الخلفي لم يُطبَّق بعد.

## 🗺️ خارطة الطريق

- تخزين علاقات/امتيازات الاشتراك بشكل دائم ضمن نماذج الخلفية
- إضافة بيانات تجريبية وتدفق إعادة تعيين صديق للهجرة
- تحسين التحقق من المشاركات وحالات الخطأ
- إضافة اختبارات آلية (وحدة/تكامل/نهاية إلى نهاية)
- إضافة CI/CD وفحوصات lint/type
- توسيع الوثائق الدولية والحفاظ على تزامن ملفات README الخاصة بـ i18n
- تعزيز قواعد المصادقة والوصول للبيانات عند الحاجة

## 🤝 المساهمة

المساهمات مرحّب بها.

المسار المقترح:

```bash
git checkout -b feat/your-change
# تنفيذ التغيير
npm start
git commit -m "feat: describe your change"
git push origin feat/your-change
```

## 📄 الترخيص

لا يوجد ملف `LICENSE` حاليًا في هذا المستودع.

يُفترض أن جميع الحقوق محفوظة ما لم يضف المشرف ملف ترخيص صريح.


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
