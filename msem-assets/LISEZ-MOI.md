# MSEM — Ressources d'identité visuelle

## Contenu du dossier
```
msem-assets/
├─ css/msem-identity.css      ← styles (fond d'écran, symboles animés, rail, coutures)
├─ js/msem-identity.js        ← script autonome (les tracés SVG sont intégrés dedans)
├─ symbols/                   ← les 17 symboles extraits de votre 2e image, un SVG chacun
│   ├─ cauri, continent, lame, goutte, chevron, sceptre, masque, epine, collier,
│   │  spirales-a, spirales-b, plume, feuille, profil, aiguille, cuir, croissant (.svg)
│   └─ symboles-sprite.svg    ← tous les symboles dans un seul fichier (<symbol id="ms-…">)
├─ img/
│   ├─ bogolan-fond-terre.webp / -ivoire.webp / -or.webp  ← fond d'écran (1re image), 3 couleurs
│   ├─ bogolan-alpha.png      ← 1re image en masque (pour mask-image, teintable en CSS)
│   ├─ motif-icones-alpha.png ← 2e image complète en masque
│   ├─ logo-fonce.webp/.png   ← logo (fond transparent) pour fonds clairs
│   ├─ logo-clair.webp/.png   ← logo en ivoire pour fonds sombres (pied de page)
│   └─ frise.webp             ← frise or/brun, répétable sans coupure (repeat-x)
├─ demo.html                  ← page de test (ouvrez-la pour voir l'effet seul)
├─ symboles-apercu.html/.png  ← galerie des symboles
└─ LISEZ-MOI.md
```
Chaque symbole n'existe qu'une seule fois (pas de doublons). Les SVG utilisent
`currentColor` : changez leur couleur avec la propriété CSS `color`.

## Intégration dans votre page (3 modifications)
1. Copiez le dossier `msem-assets` à côté de votre fichier HTML.
2. Dans le `<head>`, **après** votre `<style>` :
   `<link rel="stylesheet" href="./msem-assets/css/msem-identity.css">`
3. Juste avant `</body>` :
   `<script src="./msem-assets/js/msem-identity.js"></script>`

Nettoyage recommandé :
- Supprimez la ligne `<div class="bg-image" alt=""> </div>` et la règle CSS `.bg-image{…}`
  (le fond d'écran est maintenant géré par `msem-identity.css`).
- Dans votre `:root`, supprimez `--bogo`, `--icons`, `--frise` : la feuille les redéfinit
  avec les versions à fond transparent (vos PNG d'origine ont un fond blanc opaque, donc
  `mask-image` les affichait comme des rectangles pleins).
- Pied de page : `<img src="./msem-assets/img/logo-clair.webp" …>` à la place de `./logo.webp`.

Le script repère vos sections par leurs ids (`#trust`, `#histoire`, `#sur-mesure`,
`#bientot`, `#contact`) et ajoute tout seul : fond bogolan, symboles flottants,
rail de symboles sous la réassurance, frise avant « Notre histoire », coutures sous les titres.

## Réglages courants
- **Intensité du fond d'écran** : `--ms-wall-o` dans le CSS (0.055 par défaut).
- **Intensité / position des symboles** : tableaux dans `msem-identity.js`
  (`[nom, x, y, largeur max, rotation, profondeur, opacité, durée, délai]`).
- **Désactiver un élément** : supprimez sa ligne dans le JS (symboles fixes, rail, frise…).
- Le mouvement s'arrête si le visiteur a activé « réduire les animations », et le fond
  disparaît en mode contraste élevé et à l'impression.

## Remarque
Si vous utilisez `mask-image` avec des fichiers locaux, servez la page avec un petit serveur
(Live Server, `npx serve`…) : Chrome bloque les masques chargés depuis `file://`.
Le script `msem-identity.js` n'en a pas besoin (SVG intégrés).
