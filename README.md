# Portail ISTM Mahagi

La page utilise Google Identity Services : le bouton ouvre le sélecteur officiel de comptes Google (choisir un compte ou en ajouter un), récupère le profil et redirige vers `accueil.html`.

## Configuration du client OAuth

Dans Google Cloud Console → **API et services → Identifiants** :

1. Utilisez le client OAuth de type **Application Web** déjà configuré dans `index.html`.
2. Dans **Origines JavaScript autorisées**, ajoutez les origines exactes utilisées pour ouvrir le site :
   - `http://localhost:8000`
   - `http://127.0.0.1:8000`
3. Si l’écran de consentement est en mode test, ajoutez le compte Google utilisé à la liste des utilisateurs test.
4. N’ajoutez aucun Client Secret dans une page Web.

## Lancer le site

Dans ce dossier, lancez :

```powershell
python -m http.server 8000
```

Ouvrez <http://localhost:8000> ou <http://127.0.0.1:8000>. Ne double-cliquez pas sur `index.html` : une page ouverte avec `file://` n’a pas d’origine Web autorisée par OAuth et Google bloque la connexion.

## Limite importante

La connexion Google et la redirection fonctionnent côté navigateur. Le profil est stocké temporairement dans `sessionStorage` pour être affiché sur la page d’accueil. Comme ce projet est uniquement statique, cette page ne constitue pas un contrôle d’accès sécurisé : avant d’y mettre des données privées, il faudra un serveur qui vérifie les jetons Google.
