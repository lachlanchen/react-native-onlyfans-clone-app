[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# Application full stack OnlyFans Clone

![Expo](https://img.shields.io/badge/Expo-48-000000?logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61DAFB?logo=react&logoColor=black)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-FF9900?logo=amazonaws&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android%20%7C%20Web-blue)
![Status](https://img.shields.io/badge/Status-Active%20Prototype-2ea44f)
![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?logo=nodedotjs&logoColor=white)
![Repo%20Size](https://img.shields.io/github/repo-size/GonzaloVolonterio/react-native-onlyfans-clone-app?label=Repo%20Size&color=0f766e)

Options de langue : **anglais (brouillon actuel)**. Les traductions sont disponibles dans `i18n/`.

### L'application clone OnlyFans est une app full stack mobile et web qui reproduit des fonctionnalités et des flux de type plateforme de créateurs.

Ce dépôt contient une application Expo + React Native avec un backend AWS Amplify (`Cognito`, `AppSync`, `DataStore`, `S3`) qui implémente un clone de plateforme de créateurs. Il inclut l'authentification, la navigation des créateurs, la création de posts, le téléversement de médias et les états d'abonnement côté interface utilisateur.

## 🧭 Vue d'ensemble

L'application est construite avec Expo Router dans `app/` et une couche locale Amplify liée aux ressources backend déclarées dans `amplify/`.

| Domaine | Implémentation actuelle |
|---|---|
| Frontend | Expo + React Native + Expo Router |
| Routage | Routage basé sur les fichiers dans `app/` |
| Auth | Amazon Cognito via `@aws-amplify/ui-react-native` |
| API | AWS AppSync GraphQL |
| Synchronisation des données | Amplify DataStore |
| Médias | S3 via Amplify Storage |
| Plateformes | iOS, Android, Web |

Après la connexion, `app/_layout.js` écoute les événements d'authentification Amplify Hub et tente de créer un enregistrement `User` dans AppSync. Cela est géré au démarrage de l'application.

## ✨ Fonctionnalités

- Flux d'authentification basé sur Cognito avec l'Authenticator Amplify
- Modèles GraphQL AppSync pour `User` et `Post`
- Persistance et synchronisation des données via Amplify DataStore
- Téléchargement et récupération d'images S3 via Amplify Storage
- Routage basé sur les fichiers dans Expo Router :
  - `app/index.js` : liste des créateurs et fil d'accueil
  - `app/user/[id].js` : profil créateur et posts
  - `app/newPost.js` : création de post
- Composants de présentation réutilisables :
  - `src/components/UserCard.js`
  - `src/components/UserProfileHeader.js`
  - `src/components/Post.js`

## 🛠️ Réalisé avec

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

Dépendances supplémentaires dans `package.json` :
- `@react-native-async-storage/async-storage`
- `@react-native-community/netinfo`
- `core-js`
- `expo-constants`, `expo-linking`, `expo-updates` et les outils d'icônes/écrans

## 🗂️ Structure du projet

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
│  └─ aws-exports.js (généré localement; non versionné)
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

## ✅ Prérequis

- Node.js 18+ (ou LTS récent)
- npm
- Expo CLI (peut être lancé via `npx expo`)
- Compte AWS et AWS Amplify CLI si vous devez générer `src/aws-exports.js`
- Simulateurs Apple/Android ou appareil physique avec Expo Go pour les tests de l'app

## 📥 Cloner le dépôt 🔧

```bash
git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ Installation 🔧

```bash
npm install
```

Scripts du dépôt depuis `package.json` :

```bash
npm start
npm run android
npm run ios
npm run web
```

Puis lancez l'application :

```bash
npm start
```

## 🔐 Configuration

### Backend Amplify

L'application importe `../src/aws-exports` dans `app/_layout.js`. Ce fichier est requis à l'exécution et n'est pas versionné volontairement.

Configuration locale typique :

```bash
npm install -g @aws-amplify/cli
amplify pull
```

Si nécessaire, sélectionnez le projet/environnement AWS Amplify existant pour ce dépôt.

### Hypothèses de modèle de données depuis le schéma versionné

- `User` : champs incluant `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` et la relation vers `Post`
- `Post` : champs incluant `id`, `text`, `image`, `likes`, `userID`
- Les deux modèles sont actuellement configurés pour une visibilité de lecture publique dans le schéma/auth configuré

### Expo / routage / Babel

- `index.js` branche l'entrée React Native et `expo-router/entry`
- `babel.config.js` inclut `expo-router/babel`, `react-native-reanimated/plugin` et le plugin `export-namespace-from`

## ▶️ Utilisation

1. Installez les dépendances et générez/obtenez le fichier local `src/aws-exports.js`
2. Lancez Metro :
   ```bash
   npm start
   ```
3. Ouvrez l'application dans Expo Go, un simulateur ou le web
4. Inscrivez-vous / connectez-vous via Authenticator
5. Parcourez les créateurs sur `/`
6. Ouvrez un profil créateur sur `/user/:id`
7. Basculez l'état d'abonnement dans l'UI
8. Créez des posts dans `/newPost`, avec une pièce jointe média optionnelle

## 🧱 Notes sur le modèle de données

Les modèles sont définis dans `amplify/backend/api/OnlyFansCloneApp/schema.graphql` et `src/models/schema.js`.

| Modèle | Champs clés |
|---|---|
| `User` | `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` |
| `Post` | `id`, `text`, `image`, `likes`, `userID` |

## 📱 Exemples

### Captures d'écran de la démo

![Screenshot_20230424-200925](https://user-images.githubusercontent.com/64506662/234364566-863bc1e1-e289-4b9b-9658-a11e737bebd8.png)
![Screenshot_20230424-200957](https://user-images.githubusercontent.com/64506662/234364579-8e32708f-cb69-4c1c-82e3-eefd7cb5f161.png)
![Screenshot_20230424-201003](https://user-images.githubusercontent.com/64506662/234364622-e9cc5d14-77f2-415f-9027-1d3ffe3e7c17.png)
![Screenshot_20230424-201006](https://user-images.githubusercontent.com/64506662/234364653-73de6b92-b7a6-4ef7-a3a6-c26411bfd46a.png)
![Screenshot_20230424-201031](https://user-images.githubusercontent.com/64506662/234364754-f5ce7da1-1ad1-4e90-bf85-40add436ad23.png)

## 🧪 Notes de développement

- `app/_layout.js` enregistre Amplify via `Amplify.configure` et souscrit aux événements Hub `auth`.
- À chaque événement de connexion, le code déclenche une mutation `createUser` afin d'initialiser un enregistrement backend.
- `app/newPost.js` téléverse une image optionnelle, compose la charge utile du post, puis la persiste via `DataStore.save`.
- `src/components/Post.js` résout dynamiquement les auteurs des posts et les URLs d'images lors du rendu des éléments du flux.
- Les données backend et de seed sont actuellement minimales, sans script d'initialisation automatisé dans le dépôt.
- Aucune suite de tests dédiée ni workflow CI n'est configuré dans ce dépôt.

## 🩺 Dépannage

- `Cannot find module '../src/aws-exports'`
  - Exécutez `amplify pull` (ou un flux `amplify init` équivalent) depuis la racine du dépôt pour générer la configuration locale.
- L'authentification fonctionne mais les requêtes/mutations échouent
  - Vérifiez que votre clé API/mode d'authentification/région AppSync correspondent à la configuration générée importée.
- Échec du téléversement d'image
  - Vérifiez que les permissions `Storage` sont présentes et que l'application a accès à la médiathèque.
- Données de créateurs/flux vides
  - Confirmez que les enregistrements initiaux `User`/`Post` existent dans DataStore/AppSync et que les règles de lecture publiques conviennent à votre cas d'usage.
- L'état d'abonnement du post ne persiste pas
  - L'implémentation actuelle semble uniquement locale côté UI; le modèle d'autorisation backend n'est pas encore implémenté.

## 🗺️ Feuille de route

- Persister les relations/ droits d'abonnement dans les modèles backend
- Ajouter des données de seed et un flux de réinitialisation compatible migration
- Améliorer la validation des posts et la gestion des erreurs
- Ajouter des tests automatisés (unitaires/intégration/e2e)
- Ajouter CI/CD ainsi que des vérifications lint/type
- Étendre la documentation internationale et garder les README i18n synchronisés
- Renforcer les règles d'authentification et d'accès aux données si nécessaire

## 🤝 Contribution

Les contributions sont les bienvenues.

Flux suggéré :

```bash
git checkout -b feat/your-change
# implement change
npm start
git commit -m "feat: describe your change"
git push origin feat/your-change
```

## 📄 Licence

Aucun fichier `LICENSE` n'est actuellement présent dans ce dépôt.

Hypothèse : tous les droits sont réservés tant que le mainteneur n'ajoute pas un fichier de licence explicite.


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
