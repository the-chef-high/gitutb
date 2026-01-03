# Master Lab High — PWA / Capacitor / Electron starter

Ce dépôt contient votre application web (index.html) prête à être :
- servie comme PWA (navigateur / installable),
- packagée pour iOS & Android via Capacitor,
- packagée pour desktop via Electron.

Important : vérifiez la législation locale et les règles des stores (App Store / Google Play) avant toute publication. Ajoutez une page d'avertissement légal / contrôle d'âge et la politique de confidentialité si nécessaire.

## Arborescence minimale
- index.html
- manifest.json
- service-worker.js
- package.json
- capacitor.config.json
- electron/main.js
- icons/ (ajoutez vos icônes ici : icon-192.png, icon-512.png)

## Pré-requis
- Node.js (16+ recommandé)
- npm ou yarn
- Pour iOS : macOS + Xcode + compte dev Apple
- Pour Android : Android Studio + Android SDK + keystore pour signature
- Pour Electron : rien de spécial pour dev ; pour build, installez dépendances natives si demandé

## Installation locale (PWA)
1. Installer les dépendances dev :
   npm install

2. Lancer un serveur local (pour tester Service Worker/manifest) :
   npm run pwa:serve
   => Ouvrez http://localhost:5000

3. Ouvrir la console DevTools / Application pour vérifier l'installation PWA (manifest + service worker).

## Préparer Capacitor (Android / iOS)
1. Installer Capacitor si pas déjà fait :
   npm install @capacitor/core @capacitor/cli --save-dev

2. Initialiser Capacitor (si vous n'avez pas encore initialisé) :
   npx cap init
   - renseignez `appId` (ex : com.votreorg.masterlabhigh) et `appName`.

3. (Optionnel) Si vous avez un build web (ex : bundler), exécutez votre build et placez la sortie dans le dossier configuré par `webDir`. Ici, `webDir` est `./` par défaut (fichiers statiques à la racine).

4. Ajouter plateformes :
   npx cap add android
   npx cap add ios

5. Copier les assets web vers les projets natifs :
   npx cap copy

6. Ouvrir le projet natif dans Android Studio / Xcode :
   npx cap open android
   npx cap open ios

7. Dans Android Studio / Xcode : configurer signatures (keystore / provisioning), tester sur appareils réels ou émulateurs, puis générer les fichiers à soumettre (APK/AAB pour Android, archive pour iOS).

Remarques :
- Xcode et build iOS nécessitent macOS.
- Respectez les règles des stores (contrôle d'âge, contenu lié aux drogues, etc.).

## Electron (desktop)
1. Installer dépendances :
   npm install

2. Lancer en mode dev :
   npm run electron:start

3. Pour créer des paquets (ex : Windows/macOS/Linux) utilisez electron-builder.
   - Exemples :
     npm run electron:pack   # build non signée dans dossier
     npm run electron:build  # création de packages selon config electron-builder

   Vous devrez ajouter la section `build` dans package.json pour configurer targets/signing si nécessaire.

## Icônes
Créez le dossier `icons/` et ajoutez :
- icon-192.png (192x192)
- icon-512.png (512x512)

Ces icônes sont référencées dans `manifest.json`. Pour Android/iOS ajoutez les icônes natives via les projets Capacitor.

## Conseils pratiques
- Ajoutez une page "A propos / Politique de confidentialité" si vous collectez des données ou analytics.
- Ajoutez un "age gate" (contrôle d'âge) et un avertissement légal si vous publiez sur un store.
- Testez l'accessibilité (contraste, keyboard navigation, lecteurs d'écran).
- Utilisez HTTPS en production (les service workers et l'installation PWA nécessitent HTTPS).

Si vous voulez, je peux :
- Générer l'ensemble de l'arborescence (incl. .gitignore, icons placeholders),
- Ajouter un fichier de build electron-builder dans package.json,
- Préparer automatiquement la commande `npx cap init` avec `capacitor.config.json` rempli,
- Ou préparer un workflow GitHub Actions pour builds Android/Electron.

Dites-moi ce que vous souhaitez que je génère ensuite (arborescence complète + .gitignore + fichiers de build signés, ou seulement Android, ou seulement Electron, etc.).