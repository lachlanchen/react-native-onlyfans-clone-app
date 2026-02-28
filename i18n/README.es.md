[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# Aplicación Full Stack clon de OnlyFans

![Expo](https://img.shields.io/badge/Expo-48-000000?logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61DAFB?logo=react&logoColor=black)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-FF9900?logo=amazonaws&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android%20%7C%20Web-blue)
![Status](https://img.shields.io/badge/Status-Active%20Prototype-2ea44f)
![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?logo=nodedotjs&logoColor=white)
![Repo%20Size](https://img.shields.io/github/repo-size/GonzaloVolonterio/react-native-onlyfans-clone-app?label=Repo%20Size&color=0f766e)

Language options: **Inglés (borrador actual)**. Las traducciones están disponibles en `i18n/`.

### La app clon de OnlyFans es una aplicación full stack para móvil y web que replica funciones y flujos al estilo de plataformas de creadores de contenido.

Este repositorio contiene una app de Expo + React Native con un backend de AWS Amplify (`Cognito`, `AppSync`, `DataStore`, `S3`) que implementa un clon de plataforma de creadores. Incluye autenticación, exploración de creadores, creación de publicaciones, carga de medios y estados de suscripción en la UI.

## 🧭 Vista general

La app está construida con Expo Router en `app/` y una capa local de datos de Amplify ligada a recursos de backend ya versionados en `amplify/`.

| Área | Implementación actual |
|---|---|
| Frontend | Expo + React Native + Expo Router |
| Enrutado | Enrutado basado en archivos en `app/` |
| Auth | Amazon Cognito vía `@aws-amplify/ui-react-native` |
| API | AWS AppSync GraphQL |
| Sincronización de datos | Amplify DataStore |
| Medios | S3 mediante Amplify Storage |
| Plataformas | iOS, Android, Web |

Al iniciar sesión, `app/_layout.js` escucha eventos de autenticación de Amplify Hub y trata de crear un registro `User` en AppSync. Esto se gestiona al arrancar la app.

## ✨ Características

- Flujo de autenticación potenciado por Cognito con el Autenticador de Amplify
- Modelos GraphQL de AppSync para `User` y `Post`
- Persistencia y sincronización de datos mediante Amplify DataStore
- Carga y recuperación de imágenes en S3 vía Amplify Storage
- Enrutado basado en archivos con Expo Router:
  - `app/index.js`: lista de creadores y feed principal
  - `app/user/[id].js`: perfil del creador y publicaciones
  - `app/newPost.js`: creador de publicaciones
- Componentes de presentación reutilizables:
  - `src/components/UserCard.js`
  - `src/components/UserProfileHeader.js`
  - `src/components/Post.js`

## 🛠️ Construido con

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

Dependencias adicionales en `package.json`:
- `@react-native-async-storage/async-storage`
- `@react-native-community/netinfo`
- `core-js`
- `expo-constants`, `expo-linking`, `expo-updates` y herramientas de iconos/pantallas

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
│  │  ├─ index.js
│  │  ├─ schema.js
│  │  └─ schema.d.ts
│  └─ aws-exports.js (generado localmente; no se incluye en el repo)
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

## ✅ Requisitos previos

- Node.js 18+ (o LTS moderno)
- npm
- Expo CLI (se puede ejecutar con `npx expo`)
- Cuenta AWS y AWS Amplify CLI si necesitas generar `src/aws-exports.js`
- Simuladores de Apple/Android o un dispositivo físico con Expo Go para probar la app

## 📥 Clonar repo 🔧

```bash
git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ Instalación 🔧

```bash
npm install
```

Scripts del repositorio en `package.json`:

```bash
npm start
npm run android
npm run ios
npm run web
```

Luego inicia la app:

```bash
npm start
```

## 🔐 Configuración

### Backend de Amplify

La app importa `../src/aws-exports` en `app/_layout.js`. Este archivo es obligatorio en tiempo de ejecución y, por diseño, no se incluye en el repositorio.

Configuración local típica:

```bash
npm install -g @aws-amplify/cli
amplify pull
```

Si se solicita, selecciona el proyecto/entorno de AWS Amplify existente para este repositorio.

### Supuestos del modelo de datos desde el esquema versionado

- `User`: los campos incluyen `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` y la relación con `Post`
- `Post`: los campos incluyen `id`, `text`, `image`, `likes`, `userID`
- Ambos modelos están configurados actualmente con visibilidad pública de lectura en el esquema/configuración auth versionados

### Expo / enrutado / Babel

- `index.js` conecta la entrada de React Native y `expo-router/entry`
- `babel.config.js` incluye `expo-router/babel`, `react-native-reanimated/plugin` y el plugin de exportación de namespaces

## ▶️ Uso

1. Instala dependencias y genera/obtén el `src/aws-exports.js` local
2. Inicia Metro:
   ```bash
   npm start
   ```
3. Abre la app en Expo Go, en un simulador o en web
4. Regístrate / inicia sesión mediante Authenticator
5. Explora creadores en `/`
6. Abre un perfil de creador en `/user/:id`
7. Alterna el estado de suscripción en la interfaz
8. Crea publicaciones en `/newPost`, con adjunto de medio opcional

## 🧱 Notas del modelo de datos

Los modelos se definen en `amplify/backend/api/OnlyFansCloneApp/schema.graphql` y `src/models/schema.js`.

| Modelo | Campos clave |
|---|---|
| `User` | `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` |
| `Post` | `id`, `text`, `image`, `likes`, `userID` |

## 📱 Ejemplos

### Capturas de ejemplo

![Screenshot_20230424-200925](https://user-images.githubusercontent.com/64506662/234364566-863bc1e1-e289-4b9b-9658-a11e737bebd8.png)
![Screenshot_20230424-200957](https://user-images.githubusercontent.com/64506662/234364579-8e32708f-cb69-4c1c-82e3-eefd7cb5f161.png)
![Screenshot_20230424-201003](https://user-images.githubusercontent.com/64506662/234364622-e9cc5d14-77f2-415f-9027-1d3ffe3e7c17.png)
![Screenshot_20230424-201006](https://user-images.githubusercontent.com/64506662/234364653-73de6b92-b7a6-4ef7-a3a6-c26411bfd46a.png)
![Screenshot_20230424-201031](https://user-images.githubusercontent.com/64506662/234364754-f5ce7da1-1ad1-4e90-bf85-40add436ad23.png)

## 🧪 Notas de desarrollo

- `app/_layout.js` registra Amplify con `Amplify.configure` y se suscribe a los eventos `auth` de Hub.
- En cada evento de inicio de sesión, el código dispara una mutación `createUser` para inicializar un registro en el backend.
- `app/newPost.js` sube una imagen opcional, compone el payload de publicación y luego persiste mediante `DataStore.save`.
- `src/components/Post.js` resuelve autores de publicaciones y URLs de imágenes dinámicamente al renderizar elementos del feed.
- El backend y los datos semilla son actualmente mínimos, sin script automatizado de configuración en el repositorio.
- No hay una suite de pruebas dedicada ni flujo de CI configurado en este repositorio.

## 🩺 Solución de problemas

- `Cannot find module '../src/aws-exports'`
  - Ejecuta `amplify pull` (o un flujo equivalente de `amplify init`) desde la raíz del repositorio para generar la configuración local.
- La autenticación funciona, pero fallan consultas/mutaciones
  - Verifica que tu clave de API/AppSync, modo de auth y región de AppSync coincidan con la configuración generada importada.
- Falla la carga de imágenes
  - Asegúrate de que existan permisos `Storage` y que la app tenga acceso a la librería multimedia.
- Datos vacíos en creador/feed
  - Confirma que existan registros iniciales de `User`/`Post` en DataStore/AppSync y que las reglas de lectura pública encajen con tu caso de uso.
- El estado de suscripción del post no se persiste
  - La implementación actual parece ser solo de estado local en UI; el modelo de derecho de suscripción en backend aún no está implementado.

## 🗺️ Hoja de ruta

- Persistir relaciones de suscripción/entitlements en modelos de backend
- Añadir datos semilla y flujo de reinicio compatible con migraciones de datos
- Mejorar validación de publicaciones y estados de error
- Añadir pruebas automatizadas (unit/integración/e2e)
- Añadir CI/CD y revisiones de lint/tipos
- Expandir documentación internacional y mantener sincronizados los README en i18n
- Endurecer autenticación y reglas de acceso a datos donde sea necesario

## 🤝 Contribuciones

Las contribuciones son bienvenidas.

Flujo sugerido:

```bash
git checkout -b feat/tu-cambio
# implementa el cambio
npm start
git commit -m "feat: describe tu cambio"
git push origin feat/tu-cambio
```

Luego abre un Pull Request indicando:
- Qué cambió
- Por qué cambió
- Cómo se ejecuta/probar

## 📄 Licencia

Actualmente no existe un archivo `LICENSE` en este repositorio.

Supuesto: todos los derechos quedan reservados salvo que el mantenedor añada un archivo de licencia explícito.


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
