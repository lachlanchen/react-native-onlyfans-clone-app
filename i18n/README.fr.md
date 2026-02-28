[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# Clone OnlyFans Full Stack

![Expo](https://img.shields.io/badge/Expo-48-000000?logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61DAFB?logo=react&logoColor=black)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-FF9900?logo=amazonaws&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android%20%7C%20Web-blue)
![Status](https://img.shields.io/badge/Status-Active%20Prototype-2ea44f)

### L’application clone OnlyFans est une application full stack, front-end et back-end pour mobile, qui reproduit les mêmes fonctionnalités.

Ce dépôt contient une application Expo + React Native avec un backend AWS Amplify (Cognito, AppSync, DataStore, S3) qui implémente les principaux flux d’une plateforme de créateurs :
- Authentification avec Amplify Authenticator
- Liste des créateurs et navigation des profils
- Bascule de l’état d’abonnement dans l’UI (côté client dans l’implémentation actuelle)
- Création de posts avec upload d’image optionnel
- Rendu du flux de posts avec récupération de l’auteur et des médias

## 🧭 Vue d’ensemble

L’application utilise le routage basé sur les fichiers avec `expo-router` sous `app/`, tandis que les ressources backend Amplify sont suivies sous `amplify/`. Lors de la connexion d’un utilisateur, l’app écoute les événements d’authentification Amplify Hub et tente de créer un enregistrement `User` correspondant dans AppSync.

| Zone | Implémentation actuelle |
|---|---|
| Frontend | Expo + React Native + Expo Router |
| Auth | Amazon Cognito via Amplify Authenticator |
| API | AWS AppSync GraphQL |
| Synchronisation des données | Amplify DataStore |
| Médias | S3 via Amplify Storage |
| Plateformes | iOS, Android, Web |

## ✨ Fonctionnalités

- Flux d’authentification propulsé par Cognito via `@aws-amplify/ui-react-native`
- Modèles GraphQL AppSync pour `User` et `Post`
- Persistance et synchronisation des données via Amplify DataStore
- Upload et récupération de médias S3 via Amplify Storage
- Écrans Expo Router :
  - `app/index.js` liste des créateurs/accueil
  - `app/user/[id].js` profil créateur + posts
  - `app/newPost.js` composition de post

## 🛠️ Construit avec

(Liste de stack d’origine conservée et étendue pour plus de clarté.)

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

Les dépendances supplémentaires du dépôt dans `package.json` incluent :
- `expo-router`
- `@react-native-async-storage/async-storage`
- `@react-native-community/netinfo`
- `core-js`

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

## ✅ Prérequis

- Node.js 18+ recommandé
- npm
- Utilisation d’Expo CLI via `npx expo ...`
- Compte AWS et Amplify CLI pour le provisioning/pull du backend
- Un fichier de config client Amplify généré, importé par l’app sous `src/aws-exports`

## 📥 Cloner le dépôt 🔧

```bash
https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app
```

Commande équivalente :

```bash
git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ Installation 🔧

(Commandes d’installation d’origine conservées.)

```bash
npm install

npx expo start or npm start
```

Scripts du dépôt :

```bash
npm start
npm run android
npm run ios
npm run web
```

## 🔐 Configuration

### Backend Amplify

L’application importe `../src/aws-exports` dans `app/_layout.js`. Ce fichier n’est pas versionné et doit être généré localement.

Flux de configuration typique (hypothèse basée sur le dossier `amplify/` versionné et `.gitignore`) :

```bash
npm install -g @aws-amplify/cli
amplify pull
```

Si vous y êtes invité, utilisez le projet/environnement Amplify existant depuis votre compte AWS. La configuration backend versionnée indique :
- Auth : Cognito (nom d’utilisateur e-mail, attributs d’inscription incluant `NAME` et `NICKNAME`)
- API : AppSync + auth par clé API activée dans la config
- Storage : ressource bucket S3 configurée

### Expo / Babel / Router

- `babel.config.js` inclut :
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`
- `index.js` initialise `core-js/full/symbol/async-iterator` et `expo-router/entry`

## ▶️ Utilisation

1. Démarrez l’application :
   ```bash
   npm start
   ```
2. Ouvrez-la dans Expo Go/émulateur/web.
3. Inscrivez-vous/connectez-vous via l’interface Amplify Authenticator.
4. Parcourez les créateurs sur l’écran d’accueil.
5. Ouvrez un profil créateur (`/user/[id]`).
6. Basculez l’état d’abonnement dans l’UI.
7. Créez un nouveau post depuis `New post`, avec éventuellement une image de la bibliothèque multimédia.

## 🧱 Modèle de données

Depuis `amplify/backend/api/OnlyFansCloneApp/schema.graphql` :

- `User` : `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`, relation vers les posts
- `Post` : `id`, `text`, `image`, `likes`, `userID`

Les deux modèles utilisent des règles d’autorisation publiques dans le schéma actuel.

| Modèle | Champs clés |
|---|---|
| `User` | `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` |
| `Post` | `id`, `text`, `image`, `likes`, `userID` |

## 📱 Exemples de l’app

### Vous devez créer un compte gratuit pour utiliser l’application

![Screenshot_20230424-200925](https://user-images.githubusercontent.com/64506662/234364566-863bc1e1-e289-4b9b-9658-a11e737bebd8.png)
![Screenshot_20230424-200957](https://user-images.githubusercontent.com/64506662/234364579-8e32708f-cb69-4c1c-82e3-eefd7cb5f161.png)
![Screenshot_20230424-201003](https://user-images.githubusercontent.com/64506662/234364622-e9cc5d14-77f2-415f-9027-1d3ffe3e7c17.png)
![Screenshot_20230424-201006](https://user-images.githubusercontent.com/64506662/234364653-73de6b92-b7a6-4ef7-a3a6-c26411bfd46a.png)
![Screenshot_20230424-201031](https://user-images.githubusercontent.com/64506662/234364754-f5ce7da1-1ad1-4e90-bf85-40add436ad23.png)

## 🧪 Notes de développement

- `app/_layout.js` écoute les événements de connexion `auth` d’Amplify Hub et exécute une mutation GraphQL `createUser`.
- Les nouveaux posts sont enregistrés avec DataStore et les images optionnelles sont uploadées via `Storage.put`.
- Le comportement d’abonnement du profil est actuellement un état UI local et n’est pas persisté dans un modèle d’abonnement backend.
- Le dépôt ne contient actuellement aucune suite de tests automatisés explicite ni fichier de workflow CI.

## 🩺 Dépannage

- `Cannot find module '../src/aws-exports'` :
  - Exécutez `amplify pull` (ou un flux d’initialisation Amplify équivalent) pour générer la config locale.
- L’auth fonctionne mais les opérations de données échouent :
  - Vérifiez que la configuration AppSync/clé API/mode d’auth dans votre environnement Amplify correspond à la config locale générée.
- Problèmes d’upload d’image :
  - Vérifiez les permissions S3 dans le storage Amplify et assurez-vous que l’appareil a l’accès à la bibliothèque multimédia.
- Flux/profil vides :
  - Assurez-vous que des enregistrements `User`/`Post` existent et que les règles d’auth actuelles autorisent les opérations de lecture.

## 🗺️ Feuille de route

- Ajouter des relations d’abonnement persistées et des vérifications de droits
- Ajouter des validations et une meilleure gestion des erreurs pour les flux de création/upload de posts
- Ajouter des tests (unitaires/intégration/e2e) et un pipeline CI
- Ajouter des variantes README multilingues et remplir les ressources `i18n/`
- Renforcer les règles d’auth/accès (remplacer les règles publiques larges si nécessaire)

## 🤝 Contribution

Les contributions sont les bienvenues.

Flux suggéré :

```bash
git checkout -b feat/your-change
# implement change
git commit -m "feat: describe change"
git push origin feat/your-change
```

Ensuite, ouvrez une Pull Request avec :
- Ce qui a changé
- Pourquoi ce changement
- Comment l’exécuter/le tester

## 📄 Licence

Aucun fichier `LICENSE` n’est actuellement présent dans ce dépôt.

Hypothèse : tous les droits sont réservés par défaut tant que le mainteneur n’ajoute pas de fichier de licence explicite.
