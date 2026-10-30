# TalcoExchange

Messagerie du portail Talco ITN : un seul compte pour toutes les applications.

## Deux façons de publier le site

### Option A : envoi manuel (simple)
Mets sur GitHub Pages : `exchange.html` + le dossier `icons/`.

### Option B : configuration Firebase en secrets GitHub (déploiement automatique)
La config Firebase n'est alors plus écrite dans le dépôt : un workflow la remplace au déploiement.
Mets dans le dépôt : `exchange.template.html`, `.github/workflows/deploy-pages.yml` et `icons/`.
**Ne mets pas `exchange.html`** (il contient les vraies valeurs).

1. Settings > Pages > Source : **GitHub Actions**.
2. Settings > Secrets and variables > Actions > New repository secret. Crée ces 7 secrets
   (valeurs : console Firebase > Paramètres du projet > Vos applications > Configuration) :
   - `FIREBASE_API_KEY` (apiKey)
   - `FIREBASE_AUTH_DOMAIN` (authDomain)
   - `FIREBASE_DATABASE_URL` (adresse de Realtime Database)
   - `FIREBASE_PROJECT_ID` (projectId)
   - `FIREBASE_STORAGE_BUCKET` (storageBucket)
   - `FIREBASE_MESSAGING_SENDER_ID` (messagingSenderId)
   - `FIREBASE_APP_ID` (appId)
3. Onglet Actions > « Déployer TalcoExchange » > Run workflow (ou simplement un push sur `main`).
   Si ta branche s'appelle autrement que `main`, change `branches: [main]` dans le fichier du workflow.
4. Le workflow publie TOUT le dépôt (ITN, etc.), pas seulement Exchange.

Remarque : la configuration Firebase d'un site web est publique par conception : elle reste visible
dans le code de la page déployée. La vraie protection, ce sont les règles Firebase (dossier `firebase/`).

## Console Firebase (projet exchange-f4322)
1. **Authentication > Sign-in method** : activer **E-mail/Mot de passe**.
2. **Authentication > Paramètres > Domaines autorisés** : ajouter `natlacaxi.github.io`.
3. **Realtime Database** : créer la base, vérifier son adresse (haut de l'onglet Données).
   Onglet **Règles** : coller `firebase/database.rules.json`, puis **Publier**.
4. **Realtime Database > Données** : ajouter `config` > `signupCode` = le code d'invitation.
5. **Firestore Database** : créer la base. Onglet **Règles** : coller `firebase/firestore.rules`, puis **Publier**.
6. (Facultatif) **Authentication > Modèles** : URL d'action = adresse de `exchange.html`.

## Fonctions principales
- Connexion par e-mail ou nom d'utilisateur, création de compte en 3 pages, code d'invitation.
- Liste des discussions à gauche sur ordinateur ; plein écran sur téléphone (retour par le bouton du téléphone).
- Messages texte, photos, vocaux (45 s), réponses, réactions, modification, éphémères, favoris,
  accusés de lecture, présence en ligne, code PIN, paramètres en sous-pages.

## En cas de problème
Le lien **Diagnostic** de la page de connexion (ou `exchange.html?diag`) teste chaque élément.

## Repartir de zéro
`node outils/reset-firebase.js serviceAccount.json <databaseURL> --yes` supprime TOUS les comptes et données.
