# liquid

Un gabarit responsive en Grid Layout.

**Liquid** est un agencement CSS Grid Layout conçu pour gérer facilement des éléments qui s'étendent sur toute la largeur de la page (communément appelés _full-bleed_, _breakout_, _hero_ ou _splash_), tout en maintenant un contenu principal centré et lisible.

## Fonctionnalités

- **Contenu principal centré** : Le conteneur `[data-layout="liquid"]` définit une largeur maximale pour le contenu et le centre horizontalement.
- **Marges latérales dynamiques** : Un espacement minimal est conservé sur les côtés, assurant que le contenu ne touche jamais les bords de la fenêtre, même sur de petits écrans.
- **Éléments pleine largeur (Splash)** : L'attribut `data-layout="splash"` permet à un élément enfant de s'étendre sur toute la largeur disponible.
- **Variantes de positionnement** :
  - `data-layout="splash-start"` : l'élément s'étend du bord gauche jusqu'à la fin de la zone de contenu.
  - `data-layout="splash-end"` : l'élément s'étend du début de la zone de contenu jusqu'au bord droit.
  - `data-layout="splash-half-start"` : l'élément s'étend du bord gauche jusqu'au milieu de la page.
  - `data-layout="splash-half-end"` : l'élément s'étend du milieu de la page jusqu'au bord droit.
- **Flexibilité d'application** : L'attribut `data-layout="liquid"` peut être appliqué à n'importe quel conteneur, y compris l'élément `<body>`.

## Comment ça marche ?

Le système repose sur une grille CSS à quatre colonnes principales, dont les lignes de séparation sont nommées pour faciliter le positionnement des éléments enfants :

- `liquid-start` : Début de la grille (bord gauche de la page).
- `content-start` : Début de la zone de contenu principale.
- `half` : Milieu de la zone de contenu principale.
- `content-end` : Fin de la zone de contenu principale.
- `liquid-end` : Fin de la grille (bord droit de la page).

Les enfants directs du conteneur `[data-layout="liquid"]` se placent par défaut dans la zone de contenu (`content-start` / `content-end`). Les attributs spécifiques (`data-layout="splash"`, `data-layout="splash-start"`, etc.) utilisent `grid-column` pour s'étendre sur différentes zones de cette grille.

## Utilisation

1. Liez le fichier `styles.css` à votre page HTML.
2. Appliquez l'attribut `data-layout="liquid"` à un élément conteneur (par exemple, `<body>` ou un `<div>` principal).
3. Utilisez les attributs `data-layout="splash"`, `data-layout="splash-start"`, `data-layout="splash-end"`, `data-layout="splash-half-start"`, ou `data-layout="splash-half-end"` sur les éléments enfants que vous souhaitez voir s'étendre au-delà de la zone de contenu principale.

Exemple de structure HTML :

```html
<body data-layout="liquid">
  <header>
    <h1>Titre du site</h1>
  </header>

  <section data-layout="splash">
    <p>Contenu pleine largeur</p>
  </section>

  <main>
    <p>Contenu principal centré.</p>
  </main>

  <section data-layout="splash-start">
    <p>
      Contenu aligné à gauche, s'étendant jusqu'à la fin de la zone de contenu.
    </p>
  </section>

  <footer data-layout="splash">
    <p>Pied de page pleine largeur</p>
  </footer>
</body>
```

## Personnalisation

Vous pouvez personnaliser l'apparence et le comportement de `liquid` en modifiant les variables CSS suivantes dans `styles.css` :

- `--liquid-spacer`: L'espacement minimal sur les côtés de la page (défaut : `2rem`).
- `--liquid-content`: La largeur maximale de la zone de contenu principale (défaut : `1024px`).

Extrait du CSS :

```css
[data-layout="liquid"] {
  --liquid-spacer: 2rem;
  --liquid-content: 1024px;

  display: grid;
  grid-template-columns:
    [liquid-start] minmax(var(--liquid-spacer), 1fr)
    [content-start] minmax(auto, calc(var(--liquid-content) / 2))
    [half] minmax(auto, calc(var(--liquid-content) / 2))
    [content-end] minmax(var(--liquid-spacer), 1fr)
    [liquid-end];
}
```

## Démonstration

Le fichier `index.html` de ce dépôt sert de page de démonstration pour visualiser les différentes possibilités de l'agencement `liquid`. Il inclut également un outil de débogage pour afficher les lignes de la grille.

## Ressources

- [Full-Bleed Layout Using CSS Grid](https://www.joshwcomeau.com/css/full-bleed/) par Josh W. Comeau
- [A centered CSS grid with full-width components](https://www.stefanjudis.com/snippets/a-centered-css-grid-with-full-width-components/) par Stefan Judis
- [How to create a full-bleed layout using CSS grid](https://blog.logrocket.com/full-bleed-layout-css-grid/) par LogRocket
- L'idée de l'inspecteur de grille est inspirée du [Codepen de Ryan Mulligan](https://codepen.io/hexagoncircle/pen/dyejrpE?editors=1100).

## Auteur

Raphaël Goetter, Alsacreations.
