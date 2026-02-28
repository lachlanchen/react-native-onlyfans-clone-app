[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# OnlyFans-Klon Full-Stack-App

![Expo](https://img.shields.io/badge/Expo-48-000000?logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61DAFB?logo=react&logoColor=black)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-FF9900?logo=amazonaws&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android%20%7C%20Web-blue)
![Status](https://img.shields.io/badge/Status-Active%20Prototype-2ea44f)
![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?logo=nodedotjs&logoColor=white)
![Repo%20Size](https://img.shields.io/github/repo-size/GonzaloVolonterio/react-native-onlyfans-clone-app?label=Repo%20Size&color=0f766e)

Sprachoptionen: **Englisch (aktueller Entwurf)**. Übersetzungen sind unter `i18n/` verfügbar.

### OnlyFans-Klon-App ist eine Full-Stack-App für Mobile und Web, die Funktionen und Abläufe einer Creator-Plattform nachbildet.

Dieses Repository enthält eine Expo + React Native App mit einem AWS Amplify Backend (`Cognito`, `AppSync`, `DataStore`, `S3`), die einen Creator-Plattform-Klon implementiert. Sie enthält Authentifizierung, Creator-Browsing, Beitragserstellung, Medien-Uploads und UI-Statusflüsse für Abonnements.

## 🧭 Überblick

Die App basiert auf Expo Router in `app/` und einer lokalen Amplify-Datenebene mit den im Repository vorhandenen Backend-Ressourcen unter `amplify/`.

| Bereich | Aktuelle Implementierung |
|---|---|
| Frontend | Expo + React Native + Expo Router |
| Routing | Datei-basiertes Routing in `app/` |
| Authentifizierung | Amazon Cognito über `@aws-amplify/ui-react-native` |
| API | AWS AppSync GraphQL |
| Datensynchronisierung | Amplify DataStore |
| Medien | S3 über Amplify Storage |
| Plattformen | iOS, Android, Web |

Bei der Anmeldung lauscht `app/_layout.js` auf Auth-Events von Amplify Hub und versucht, in AppSync einen `User`-Datensatz anzulegen. Das wird beim App-Start ausgeführt.

## ✨ Features

- Authentifizierungsfluss mit Cognito via Amplify Authenticator
- AppSync-GraphQL-Modelle für `User` und `Post`
- Datenspeicherung und Synchronisierung über Amplify DataStore
- Bild-Upload und Abruf über Amplify Storage
- Datei-basiertes Routing in Expo Router:
  - `app/index.js`: Creator-Liste und Hauptfeed
  - `app/user/[id].js`: Creator-Profil und Beiträge
  - `app/newPost.js`: Beitragsersteller
- Wiederverwendbare Präsentationskomponenten:
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

Zusätzliche Abhängigkeiten aus `package.json`:
- `@react-native-async-storage/async-storage`
- `@react-native-community/netinfo`
- `core-js`
- `expo-constants`, `expo-linking`, `expo-updates` und Icon-/Screen-Tools

## 🗂️ Projektstruktur

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
│  └─ aws-exports.js (lokal generiert; nicht committed)
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

## ✅ Voraussetzungen

- Node.js 18+ (oder moderne LTS-Version)
- npm
- Expo CLI (kann via `npx expo` ausgeführt werden)
- AWS-Konto und Amplify CLI, falls du `src/aws-exports.js` erzeugen musst
- Apple/Android-Simulatoren oder ein physisches Gerät mit Expo Go zum Testen

## 📥 Repository klonen 🔧

```bash
git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ Installation 🔧

```bash
npm install
```

Skripte aus `package.json`:

```bash
npm start
npm run android
npm run ios
npm run web
```

Starte danach die App:

```bash
npm start
```

## 🔐 Konfiguration

### Amplify Backend

Die App importiert `../src/aws-exports` in `app/_layout.js`. Diese Datei wird zur Laufzeit benötigt und ist absichtlich nicht versioniert.

Typischer lokaler Setupablauf:

```bash
npm install -g @aws-amplify/cli
amplify pull
```

Wenn du dazu aufgefordert wirst, wähle das bestehende AWS Amplify Projekt/die vorhandene Umgebung dieses Repositories aus.

### Annahmen zum Datenmodell aus dem committen Schema

- `User`: Felder inkl. `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` und Beziehung zu `Post`
- `Post`: Felder inkl. `id`, `text`, `image`, `likes`, `userID`
- Beide Modelle sind im committen Schema/der Auth-Konfiguration aktuell für öffentliches Lesezugriffsniveau konfiguriert

### Expo / Routing / Babel

- `index.js` bindet den React Native Entry und `expo-router/entry` ein
- `babel.config.js` enthält `expo-router/babel`, `react-native-reanimated/plugin` und das Namespace-Export-Vorschlags-Plugin

## ▶️ Nutzung

1. Abhängigkeiten installieren und lokale `src/aws-exports.js` erstellen/beschaffen
2. Metro starten:
   ```bash
   npm start
   ```
3. App in Expo Go, Simulator oder im Web öffnen
4. Anmeldung/Registrierung über den Authenticator
5. Creators auf `/` durchsuchen
6. Ein Creator-Profil unter `/user/:id` öffnen
7. Abo-Status in der UI umschalten
8. Beiträge in `/newPost` erstellen, optional mit Medienanhang

## 🧱 Hinweise zum Datenmodell

Modelle sind in `amplify/backend/api/OnlyFansCloneApp/schema.graphql` und `src/models/schema.js` definiert.

| Modell | Schlüsselfelder |
|---|---|
| `User` | `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` |
| `Post` | `id`, `text`, `image`, `likes`, `userID` |

## 📱 Beispiele

### Demo-Screenshots

![Screenshot_20230424-200925](https://user-images.githubusercontent.com/64506662/234364566-863bc1e1-e289-4b9b-9658-a11e737bebd8.png)
![Screenshot_20230424-200957](https://user-images.githubusercontent.com/64506662/234364579-8e32708f-cb69-4c1c-82e3-eefd7cb5f161.png)
![Screenshot_20230424-201003](https://user-images.githubusercontent.com/64506662/234364622-e9cc5d14-77f2-415f-9027-1d3ffe3e7c17.png)
![Screenshot_20230424-201006](https://user-images.githubusercontent.com/64506662/234364653-73de6b92-b7a6-4ef7-a3a6-c26411bfd46a.png)
![Screenshot_20230424-201031](https://user-images.githubusercontent.com/64506662/234364754-f5ce7da1-1ad1-4e90-bf85-40add436ad23.png)

## 🧪 Entwicklungshinweise

- `app/_layout.js` registriert Amplify mit `Amplify.configure` und abonniert Hub-`auth`-Events.
- Bei jedem Sign-in Event löst der Code eine `createUser` Mutation aus, damit ein Datensatz im Backend initialisiert wird.
- `app/newPost.js` lädt optional ein Bild hoch, baut die Beitragsnutzlast auf und speichert dann via `DataStore.save`.
- `src/components/Post.js` löst Beitragssender und Bild-URLs dynamisch beim Rendern von Feed-Einträgen auf.
- Backend- und Seed-Daten sind derzeit minimal, ohne automatisiertes Setup-Skript im Repo.
- Eine dedizierte Test-Suite oder CI-Workflow ist im Repository nicht konfiguriert.

## 🩺 Fehlerbehebung

- `Cannot find module '../src/aws-exports'`
  - Führe `amplify pull` aus (oder einen passenden `amplify init`-Ablauf), um die lokale Konfiguration zu erzeugen.
- Authentifizierung erfolgreich, aber Queries/Mutationen schlagen fehl
  - Überprüfe, ob AppSync/API-Schlüssel/Auth-Modus und Region zur importierten generierten Konfiguration passen.
- Bild-Upload schlägt fehl
  - Stelle sicher, dass die `Storage`-Berechtigungen vorhanden sind und die App Zugriff auf die Medienbibliothek hat.
- Leere Creator-/Feed-Daten
  - Bestätige, dass initiale `User`/`Post`-Datensätze in DataStore/AppSync existieren und die öffentlichen Lese-Regeln zu deinem Use Case passen.
- Abo-Status eines Beitrags wird nicht gespeichert
  - Aktuell scheint die Implementierung nur lokal in der UI zu leben; das Backend-Entitlement-Modell ist noch nicht umgesetzt.

## 🗺️ Roadmap

- Abo-Beziehungen/-Ansprüche in Backend-Modellen persistieren
- Seed-Daten hinzufügen und einen migrationsfreundlichen Reset-Flow bereitstellen
- Post-Validierung und Fehlerzustände verbessern
- Automatisierte Tests ergänzen (Unit-/Integrations-/E2E)
- CI/CD sowie Lint- und Typprüfungen ergänzen
- Internationale Dokumentation ausbauen und i18n-READMEs synchron halten
- Authentifizierung und Datenzugriffsregeln dort härten, wo nötig

## 🤝 Mitwirken

Beiträge sind willkommen.

Vorgeschlagener Ablauf:

```bash
git checkout -b feat/your-change
# implement change
git commit -m "feat: describe your change"
git push origin feat/your-change
```

Erstelle danach einen Pull Request mit:
- Was sich geändert hat
- Warum es geändert wurde
- Wie man es ausführt/testet

## 📄 Lizenz

In diesem Repository ist aktuell keine `LICENSE`-Datei vorhanden.

Annahme: Standardmäßig sind alle Rechte vorbehalten, sofern der Maintainer keine explizite Lizenzdatei hinzufügt.


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
