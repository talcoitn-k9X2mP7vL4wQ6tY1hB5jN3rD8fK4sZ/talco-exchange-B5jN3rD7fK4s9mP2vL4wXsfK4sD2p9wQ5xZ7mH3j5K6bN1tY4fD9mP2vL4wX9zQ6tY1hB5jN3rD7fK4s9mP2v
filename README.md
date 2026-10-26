# TalcoExchange

Messagerie du portail Talco ITN : un seul compte pour toutes les applications.

## Fichiers à mettre sur GitHub Pages
- `exchange.html`
- le dossier `icons/` (contenu de `icons.zip`)

## Console Firebase (projet exchange-f4322)
1. **Authentication > Sign-in method** : activer **E-mail/Mot de passe** (pas « lien par e-mail »).
2. **Authentication > Paramètres > Domaines autorisés** : ajouter `natlacaxi.github.io`.
3. **Realtime Database** : créer la base et vérifier son adresse (haut de l'onglet Données). Si elle
   diffère de `databaseURL` au début du script de `exchange.html`, la recopier.
   Onglet **Règles** : coller `database.rules.json`, puis **Publier**.
4. **Realtime Database > Données** : ajouter `config` > `signupCode` = `26866569389`.
5. **Firestore Database** : créer la base. Onglet **Règles** : coller `firestore.rules`, puis **Publier**.
6. (Facultatif) **Authentication > Modèles** : personnaliser l'URL d'action des e-mails de vérification
   et de réinitialisation avec l'adresse de `exchange.html`.

## Fonctions principales
- Connexion par e-mail ou nom d'utilisateur, création de compte en 3 pages, code d'invitation.
- Liste des discussions à gauche sur ordinateur ; plein écran sur téléphone, avec ouverture de la
  conversation au toucher et retour par le bouton « précédent » du téléphone.
- Messages texte, photos, messages vocaux (45 s max), réponses, réactions, modification,
  messages éphémères, favoris, accusés de lecture, présence en ligne.
- Paramètres en sous-pages : compte, confidentialité, discussions, notifications, apparence,
  code PIN, favoris, aide.

## En cas de problème
Le lien **Diagnostic** sur la page de connexion (ou `exchange.html?diag`) teste chaque élément et
indique ce qui manque (mode E-mail/Mot de passe, domaine, base de données, règles...).

## Repartir de zéro
`node reset-firebase.js serviceAccount.json <databaseURL> --yes` supprime TOUS les comptes et données.
