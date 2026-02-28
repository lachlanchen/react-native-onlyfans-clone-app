[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# Clon de OnlyFans App Full Stack

![Expo](https://img.shields.io/badge/Expo-48-000000?logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61DAFB?logo=react&logoColor=black)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-FF9900?logo=amazonaws&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android%20%7C%20Web-blue)
![Status](https://img.shields.io/badge/Status-Active%20Prototype-2ea44f)

### La app clon de OnlyFans es una aplicación full stack, frontend y backend para móvil, que replica las características y funcionalidades.

Este repositorio contiene una app Expo + React Native con backend en AWS Amplify (Cognito, AppSync, DataStore, S3) que implementa los flujos principales de una plataforma para creadores:
- Autenticación con Amplify Authenticator
- Lista de creadores y navegación de perfiles
- Cambio de estado de suscripción en la UI (del lado cliente en la implementación actual)
- Creación de publicaciones con subida opcional de imágenes
- Renderizado del feed de publicaciones con recuperación de autor y medios

## 🧭 Resumen

La app usa enrutamiento basado en archivos con `expo-router` en `app/`, mientras que los recursos del backend de Amplify se rastrean en `amplify/`. Al iniciar sesión, la app escucha eventos de autenticación de Amplify Hub e intenta crear un registro `User` correspondiente en AppSync.

| Área | Implementación actual |
|---|---|
| Frontend | Expo + React Native + Expo Router |
| Auth | Amazon Cognito mediante Amplify Authenticator |
| API | AWS AppSync GraphQL |
| Sincronización de datos | Amplify DataStore |
| Medios | S3 mediante Amplify Storage |
| Plataformas | iOS, Android, Web |

## ✨ Funcionalidades

- Flujo de autenticación impulsado por Cognito mediante `@aws-amplify/ui-react-native`
- Modelos GraphQL de AppSync para `User` y `Post`
- Persistencia y sincronización de datos mediante Amplify DataStore
- Subida y recuperación de medios en S3 mediante Amplify Storage
- Pantallas de Expo Router:
  - `app/index.js` lista de creadores/inicio
  - `app/user/[id].js` perfil del creador + publicaciones
  - `app/newPost.js` compositor de publicaciones

## 🛠️ Tecnologías

(Lista de stack original conservada y ampliada para mayor claridad.)

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

Dependencias adicionales del repositorio en `package.json` incluyen:
- `expo-router`
- `@react-native-async-storage/async-storage`
- `@react-native-community/netinfo`
- `core-js`

## 🗂️ Estructura del proyecto

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

## ✅ Prerrequisitos

- Node.js 18+ recomendado
- npm
- Uso de Expo CLI mediante `npx expo ...`
- Cuenta de AWS y Amplify CLI para aprovisionamiento/pull del backend
- Un archivo de configuración de cliente de Amplify generado e importado por la app como `src/aws-exports`

## 📥 Clonar repositorio 🔧

```bash
https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app
```

Comando equivalente:

```bash
git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ Instalación 🔧

(Comandos de instalación originales conservados.)

```bash
npm install

npx expo start or npm start
```

Scripts del repositorio:

```bash
npm start
npm run android
npm run ios
npm run web
```

## 🔐 Configuración

### Backend de Amplify

La app importa `../src/aws-exports` en `app/_layout.js`. Ese archivo no está versionado y debe generarse localmente.

Flujo de configuración típico (suposición basada en la carpeta `amplify/` versionada y `.gitignore`):

```bash
npm install -g @aws-amplify/cli
amplify pull
```

Si se solicita, usa el proyecto/entorno de Amplify existente de tu cuenta AWS. La configuración del backend versionada indica:
- Auth: Cognito (usuario por email, atributos de registro incluyen `NAME` y `NICKNAME`)
- API: AppSync + autenticación con API key habilitada en la configuración
- Storage: recurso de bucket S3 configurado

### Expo / Babel / Router

- `babel.config.js` incluye:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`
- `index.js` inicializa `core-js/full/symbol/async-iterator` y `expo-router/entry`

## ▶️ Uso

1. Inicia la app:
   ```bash
   npm start
   ```
2. Abre en Expo Go/emulador/web.
3. Regístrate/inicia sesión mediante la UI de Amplify Authenticator.
4. Explora creadores en la pantalla principal.
5. Abre un perfil de creador (`/user/[id]`).
6. Cambia el estado de suscripción en la UI.
7. Crea una publicación nueva desde `New post`, adjuntando opcionalmente una imagen desde la biblioteca multimedia.

## 🧱 Modelo de datos

De `amplify/backend/api/OnlyFansCloneApp/schema.graphql`:

- `User`: `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`, relación con publicaciones
- `Post`: `id`, `text`, `image`, `likes`, `userID`

Ambos modelos usan reglas de autenticación pública en el esquema actual.

| Modelo | Campos clave |
|---|---|
| `User` | `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` |
| `Post` | `id`, `text`, `image`, `likes`, `userID` |

## 📱 Ejemplos de la app

### Necesitas crear una cuenta gratuita para usar la app

![Screenshot_20230424-200925](https://user-images.githubusercontent.com/64506662/234364566-863bc1e1-e289-4b9b-9658-a11e737bebd8.png)
![Screenshot_20230424-200957](https://user-images.githubusercontent.com/64506662/234364579-8e32708f-cb69-4c1c-82e3-eefd7cb5f161.png)
![Screenshot_20230424-201003](https://user-images.githubusercontent.com/64506662/234364622-e9cc5d14-77f2-415f-9027-1d3ffe3e7c17.png)
![Screenshot_20230424-201006](https://user-images.githubusercontent.com/64506662/234364653-73de6b92-b7a6-4ef7-a3a6-c26411bfd46a.png)
![Screenshot_20230424-201031](https://user-images.githubusercontent.com/64506662/234364754-f5ce7da1-1ad1-4e90-bf85-40add436ad23.png)

## 🧪 Notas de desarrollo

- `app/_layout.js` escucha eventos `auth` de Amplify Hub al iniciar sesión y ejecuta una mutación GraphQL `createUser`.
- Las publicaciones nuevas se guardan con DataStore y las imágenes opcionales se suben con `Storage.put`.
- El comportamiento de suscripción en el perfil actualmente es estado local de UI y no se persiste como modelo de suscripción en backend.
- Actualmente el repositorio no tiene una suite de pruebas automatizadas ni archivos de workflow de CI explícitos.

## 🩺 Solución de problemas

- `Cannot find module '../src/aws-exports'`:
  - Ejecuta `amplify pull` (o el flujo equivalente de init en Amplify) para generar la configuración local.
- La autenticación funciona pero fallan las operaciones de datos:
  - Confirma que la configuración de AppSync/API key/modo de auth en tu entorno Amplify coincide con la configuración generada localmente.
- Problemas al subir imágenes:
  - Verifica permisos de S3 en Amplify Storage y asegúrate de que el dispositivo tenga acceso a la biblioteca multimedia.
- Feed/perfil sin datos:
  - Asegúrate de que existan registros `User`/`Post` iniciales y de que las reglas de auth actuales permitan operaciones de lectura.

## 🗺️ Hoja de ruta

- Añadir relaciones de suscripción persistentes y validaciones de permisos
- Añadir validaciones y manejo de errores más completo para flujos de creación/subida de publicaciones
- Añadir pruebas (unit/integration/e2e) y pipeline de CI
- Añadir variantes README multilingües y poblar recursos en `i18n/`
- Endurecer reglas de auth/acceso (reemplazar reglas públicas amplias cuando corresponda)

## 🤝 Contribuciones

Las contribuciones son bienvenidas.

Flujo sugerido:

```bash
git checkout -b feat/your-change
# implement change
git commit -m "feat: describe change"
git push origin feat/your-change
```

Luego abre un Pull Request con:
- Qué cambió
- Por qué cambió
- Cómo ejecutarlo/probarlo

## 📄 Licencia

Actualmente no hay un archivo `LICENSE` en este repositorio.

Suposición: todos los derechos están reservados por defecto, a menos que el mantenedor añada un archivo de licencia explícito.
