# Portfolio — Réalisation

## Contexte

Portfolio personnel. HTML/CSS vanilla, aucun framework, déployable statiquement.
Objectif : présenter le profil Security Engineer avec les projets les plus représentatifs.

---

## Stack

| Couche      | Choix                                                 |
| ----------- | ----------------------------------------------------- |
| Structure   | HTML5 sémantique                                      |
| Style       | CSS vanilla avec custom properties                    |
| Animations  | CSS 3D transforms (`preserve-3d`)                     |
| Dark mode   | `body.dark` + `localStorage` + JS vanilla (20 lignes) |
| Fonts       | Poppins via Google Fonts                              |
| Déploiement | GitHub Pages / Vercel (statique)                      |

Zéro dépendance. Zéro build step.

---

## Architecture CSS

### Custom properties

Toutes les valeurs variables centralisées dans `:root`. Dark mode = redéfinir les mêmes variables sous `body.dark`.

```css
:root { --accent: #40672b; --bg: #ffffff; ... }
body.dark { --accent: #5cb840; --bg: #070d07; ... }
```

### Formes géométriques 3D

Cinq formes, même principe : `transform-style: preserve-3d` + `@keyframes Rotate`.

| Forme         | Technique                                    |
| ------------- | -------------------------------------------- |
| Pyramide      | 4 triangles CSS (border trick) en 3D         |
| Cube          | 6 faces `div` positionnées avec `translateZ` |
| Ring          | Cercle `border-radius: 50%` qui tourne en 3D |
| Diamond       | Carré avec `rotateZ(45deg)` dans le keyframe |
| Triangle plat | Border trick, tourne librement               |

La pyramide utilise `--s` comme unique variable de taille. Tout dérive de là :

```css
.pyramid {
  --s: 200px;
}
.triangle {
  border: calc(var(--s) / 2) solid transparent;
}
.two {
  transform-origin: calc(var(--s) / 2) 0;
}
```

Changer `--s` en inline style suffit pour une version plus petite.

### Dark mode glow

- Cubes : `box-shadow` sur `.face` (ne casse pas `preserve-3d`)
- Pyramides : `filter: drop-shadow` sur le wrapper (aplatit le 3D, acceptable pour les décos)
- Ring / Diamond : `box-shadow` double couche
- Triangle : `filter: drop-shadow`

---

## Sections

| Section  | Contenu                                                                                                                   |
| -------- | ------------------------------------------------------------------------------------------------------------------------- |
| Hero     | Nom, tagline, CTA, pyramide principale animée                                                                             |
| About    | Bio courte, skills chips (Languages / Security / Infra)                                                                   |
| Projects | Webserv (featured) + 5 cards : Inception, ft_transcendence, Minishell, EssenceMoinsCher, Security Toolkit, Security track |
| Contact  | Email + GitHub                                                                                                            |

---

## Responsive

- `860px` : grilles 2 colonnes -> 1 colonne
- `640px` : nav links cachés, hero en colonne, formes déco cachées, pyramid réduite via `--s: 130px`
- `400px` : chips et tags rétrécissent

---

## Reste à faire

- Section Experience (WTJ + MagicMakers avec métriques)
- Logo personnalisé
- SEO : meta description, og:image, og:title
- Déploiement
