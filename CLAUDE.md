# LaCitadelle-paques2026

## Ce projet fait partie de Toolkit

- Emplacement : `projets/lacitadelle-paques2026/`, à l'intérieur du dossier Toolkit
  (la racine de Toolkit est donc `../..` depuis ce dossier).
- Ce projet peut être modifié librement depuis n'importe quel éditeur (VS Code, Android
  Studio, Notepad++…), sans passer par Toolkit.
- Sa fiche `projet.json` décrit le projet pour Toolkit (nom, type, point d'entrée,
  actions…). **Garde-la à jour** si tu changes le point d'entrée, ajoutes ou modifies une
  action (bouton), etc. Le format est documenté dans `../../app/docs/projet-json.md`.
- Explique ce que tu fais en français, simplement.
- Git : fais des **commits locaux** réguliers avec des messages clairs en français.
  **Ne fais jamais de push** : l'utilisateur pousse lui-même depuis Toolkit.
  Ne versionne jamais de secrets (clés, mots de passe, keystores, `.env`, `local.properties`).

## Rôle du projet

Galerie photo de l'évent Pâques 2026 (La Citadelle) : une page unique (`index.html`) avec
un en-tête animé (particules), une grille de captures d'écran Minecraft et une visionneuse
(précédent / suivant, flèches du clavier, Échap, mode image plein écran). Elle contient
97 captures prises du 20 au 27 avril 2026.

## Technologies

Outil HTML (HTML, CSS, JavaScript), ouvert dans un onglet de Toolkit.

Tout est dans `index.html` (CSS et JS intégrés, aucune bibliothèque). Dépend d'Internet :
polices Google Fonts (Cinzel, Nunito) et surtout l'API GitHub pour la liste des photos.

## Photos : où elles sont, comment elles s'affichent

- Les photos sont dans `images/` (PNG, noms au format des captures Minecraft
  `AAAA-MM-JJ_HH.MM.SS.png`). Formats reconnus : png, jpg/jpeg, gif, webp, avif.
- **La page ne lit pas le dossier local.** Au chargement, elle demande la liste des fichiers à
  l'API GitHub (`api.github.com/repos/<GITHUB_USER>/<GITHUB_REPO>/contents/images`) et
  affiche les images depuis GitHub (`download_url`). Réglages en haut du 2ᵉ `<script>` :
  `GITHUB_USER`, `GITHUB_REPO`, `IMAGES_FOLDER`.
- Ordre : tri par nom de fichier (tri numérique), donc chronologique avec les noms Minecraft.
- Légende : le nom du fichier sans extension, `-` et `_` remplacés par des espaces.

## Ajouter des photos

1. Copier les images dans `images/` (garder le nommage `AAAA-MM-JJ_HH.MM.SS` pour l'ordre).
2. Commit local, puis l'utilisateur pousse depuis Toolkit.
3. Elles n'apparaissent qu'**après le push**, même dans Toolkit (la page lit GitHub, pas le disque).

## Publication

Dépôt GitHub `Eldrazy-Git/LaCitadelle-paques2026` (remote `origin`). Le dépôt doit rester
**public** : l'API est appelée sans authentification. Aucun hébergement (GitHub Pages ou
autre) n'est configuré dans le projet : à demander à l'utilisateur si on veut une adresse
publique pour la page.

## Pièges

- `GITHUB_REPO` vaut `"LaCitadelle-paque2026"` (sans « s ») alors que le dépôt s'appelle
  `LaCitadelle-paques2026`. Non vérifié : ça ne marche que si GitHub redirige un ancien nom.
  Si la galerie affiche « La galerie attend vos aventures », c'est la première chose à
  regarder (une erreur 404 de l'API s'affiche comme une galerie vide, pas comme une erreur).
- API GitHub sans jeton : 60 requêtes par heure par adresse IP, et au plus 1 000 fichiers
  listés par dossier.
- Les PNG sont bruts (jusqu'à 17 Mo chacun, `images/` ≈ 1,1 Go ; dépôt ≈ 1,06 Go). Pas de
  miniatures : la grille charge les images en taille réelle (`loading="lazy"`). GitHub
  refuse les fichiers de plus de 100 Mo et déconseille les dépôts de plus de 1 Go :
  compresser (ou convertir en WebP) les nouvelles photos avant de les ajouter.
- Les noms de fichiers sont insérés tels quels dans le HTML : éviter `<`, `>`, `"` et `&`.
- Sans Internet, la page reste en « Chargement… » puis affiche une erreur réseau.

## Lancer ou compiler

Ouvrir dans Toolkit (double-clic). F5 recharge après une modification.
