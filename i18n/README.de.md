[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# OnlyFans-Klon Full Stack App

![Expo](https://img.shields.io/badge/Expo-48-000000?logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61DAFB?logo=react&logoColor=black)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-FF9900?logo=amazonaws&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android%20%7C%20Web-blue)
![Status](https://img.shields.io/badge/Status-Active%20Prototype-2ea44f)

### Die OnlyFans-Klon-App ist eine Full-Stack-App mit Frontend und Backend für Mobile und bildet dieselben Features und Funktionen nach.

Dieses Repository enthält eine Expo + React Native App mit einem AWS Amplify Backend (Cognito, AppSync, DataStore, S3), das zentrale Creator-Plattform-Abläufe umsetzt:
- Authentifizierung mit Amplify Authenticator
- Creator-Liste und Profil-Browsing
- Abo-Status-Umschalter in der UI (in der aktuellen Implementierung clientseitig)
- Beitragserstellung mit optionalem Bildupload
- Beitrags-Feed-Rendering mit Autor- und Medienabruf

## 🧭 Überblick

Die App nutzt dateibasiertes Routing mit `expo-router` unter `app/`, während Amplify-Backend-Ressourcen unter `amplify/` verwaltet werden. Beim User-Sign-in lauscht die App auf Amplify Hub Auth-Events und versucht, einen zugehörigen `User`-Datensatz in AppSync anzulegen.

| Bereich | Aktuelle Implementierung |
|---|---|
| Frontend | Expo + React Native + Expo Router |
| Auth | Amazon Cognito über Amplify Authenticator |
| API | AWS AppSync GraphQL |
| Datensynchronisierung | Amplify DataStore |
| Medien | S3 über Amplify Storage |
| Plattformen | iOS, Android, Web |

## ✨ Funktionen

- Auth-Flow mit Cognito über `@aws-amplify/ui-react-native`
- AppSync-GraphQL-Modelle für `User` und `Post`
- Datenpersistenz und Synchronisierung über Amplify DataStore
- S3-Medienupload und -abruf über Amplify Storage
- Expo Router Screens:
  - `app/index.js` Creator-Liste/Home
  - `app/user/[id].js` Creator-Profil + Beiträge
  - `app/newPost.js` Beitragserstellung

## 🛠️ Erstellt Mit

(Ursprüngliche Stack-Liste beibehalten und zur Klarheit erweitert.)

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

Zusätzliche Repository-Abhängigkeiten in `package.json`:
- `expo-router`
- `@react-native-async-storage/async-storage`
- `@react-native-community/netinfo`
- `core-js`

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

## ✅ Voraussetzungen

- Node.js 18+ empfohlen
- npm
- Expo CLI Nutzung über `npx expo ...`
- AWS-Account und Amplify CLI für Backend-Provisionierung/Pull
- Eine generierte Amplify-Client-Konfigurationsdatei, die als `src/aws-exports` von der App importiert wird

## 📥 Repository klonen 🔧

```bash
https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app
```

Gleichwertiger Befehl:

```bash
git clone https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app.git
cd react-native-onlyfans-clone-app
```

## ⚙️ Installation 🔧

(Ursprüngliche Installationsbefehle beibehalten.)

```bash
npm install

npx expo start or npm start
```

Repository-Skripte:

```bash
npm start
npm run android
npm run ios
npm run web
```

## 🔐 Konfiguration

### Amplify Backend

Die App importiert `../src/aws-exports` in `app/_layout.js`. Diese Datei ist nicht versioniert und muss lokal generiert werden.

Typischer Setup-Ablauf (Annahme basierend auf dem versionierten `amplify/`-Ordner und `.gitignore`):

```bash
npm install -g @aws-amplify/cli
amplify pull
```

Wenn du dazu aufgefordert wirst, nutze das bestehende Amplify-Projekt/Environment aus deinem AWS-Account. Die versionierte Backend-Konfiguration weist auf Folgendes hin:
- Auth: Cognito (email username, signup attributes include `NAME` and `NICKNAME`)
- API: AppSync + API key auth enabled in config
- Storage: S3 bucket resource configured

### Expo / Babel / Router

- `babel.config.js` enthält:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`
- `index.js` initialisiert `core-js/full/symbol/async-iterator` und `expo-router/entry`

## ▶️ Nutzung

1. Starte die App:
   ```bash
   npm start
   ```
2. Öffne sie in Expo Go/Emulator/Web.
3. Registriere dich oder melde dich über die Amplify Authenticator UI an.
4. Durchsuche Creator auf dem Home-Screen.
5. Öffne ein Creator-Profil (`/user/[id]`).
6. Schalte den Abo-Status in der UI um.
7. Erstelle einen neuen Beitrag über `New post`, optional mit Bild aus der Medienbibliothek.

## 🧱 Datenmodell

Aus `amplify/backend/api/OnlyFansCloneApp/schema.graphql`:

- `User`: `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`, relation to posts
- `Post`: `id`, `text`, `image`, `likes`, `userID`

Beide Modelle verwenden im aktuellen Schema öffentliche Auth-Regeln.

| Modell | Schlüsselfelder |
|---|---|
| `User` | `id`, `name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` |
| `Post` | `id`, `text`, `image`, `likes`, `userID` |

## 📱 App-Beispiele

### Du musst ein kostenloses Konto erstellen, um die App zu verwenden

![Screenshot_20230424-200925](https://user-images.githubusercontent.com/64506662/234364566-863bc1e1-e289-4b9b-9658-a11e737bebd8.png)
![Screenshot_20230424-200957](https://user-images.githubusercontent.com/64506662/234364579-8e32708f-cb69-4c1c-82e3-eefd7cb5f161.png)
![Screenshot_20230424-201003](https://user-images.githubusercontent.com/64506662/234364622-e9cc5d14-77f2-415f-9027-1d3ffe3e7c17.png)
![Screenshot_20230424-201006](https://user-images.githubusercontent.com/64506662/234364653-73de6b92-b7a6-4ef7-a3a6-c26411bfd46a.png)
![Screenshot_20230424-201031](https://user-images.githubusercontent.com/64506662/234364754-f5ce7da1-1ad1-4e90-bf85-40add436ad23.png)

## 🧪 Hinweise zur Entwicklung

- `app/_layout.js` lauscht auf Amplify Hub `auth` Sign-in-Events und führt eine `createUser` GraphQL-Mutation aus.
- Neue Beiträge werden mit DataStore gespeichert, optionale Bilder werden mit `Storage.put` hochgeladen.
- Das Abo-Verhalten im Profil ist derzeit lokaler UI-Status und wird nicht als Backend-Abo-Modell persistiert.
- Das Repository enthält derzeit keine explizite automatisierte Test-Suite oder CI-Workflow-Dateien.

## 🩺 Fehlerbehebung

- `Cannot find module '../src/aws-exports'`:
  - Führe `amplify pull` aus (oder einen gleichwertigen Amplify-Init-Workflow), um die lokale Konfiguration zu erzeugen.
- Auth funktioniert, aber Datenoperationen schlagen fehl:
  - Prüfe, ob die AppSync/API-key/Auth-Mode-Konfiguration in deiner Amplify-Umgebung mit der lokal generierten Konfiguration übereinstimmt.
- Probleme beim Bildupload:
  - Verifiziere S3-Berechtigungen in Amplify Storage und stelle sicher, dass das Gerät Zugriff auf die Medienbibliothek hat.
- Leerer Feed/Profildaten:
  - Stelle sicher, dass initiale `User`/`Post`-Datensätze vorhanden sind und die aktuellen Auth-Regeln Lesezugriffe erlauben.

## 🗺️ Roadmap

- Persistente Abo-Beziehungen und Entitlement-Checks hinzufügen
- Validierungen und robusteres Fehlerhandling für Beitragserstellung/Upload-Flows ergänzen
- Tests (unit/integration/e2e) und CI-Pipeline hinzufügen
- Mehrsprachige README-Varianten hinzufügen und `i18n/`-Ressourcen befüllen
- Auth-/Zugriffsregeln härten (breite öffentliche Regeln bei Bedarf ersetzen)

## 🤝 Mitwirken

Beiträge sind willkommen.

Empfohlener Ablauf:

```bash
git checkout -b feat/your-change
# implement change
git commit -m "feat: describe change"
git push origin feat/your-change
```

Öffne danach einen Pull Request mit:
- Was sich geändert hat
- Warum es geändert wurde
- Wie man es ausführt/testet

## 📄 Lizenz

In diesem Repository ist aktuell keine `LICENSE`-Datei vorhanden.

Annahme: Standardmäßig sind alle Rechte vorbehalten, sofern der Maintainer keine explizite Lizenzdatei hinzufügt.
