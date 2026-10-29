# 1. quelle est la différence entre les unités CSS em et rem ? donne un exemple. #

## claude : ##
em : relatif au parent

1em vaut la taille de police (font-size) de l’élément lui-même, qui est en général héritée de son parent. Les valeurs se multiplient donc quand on imbrique des éléments.

rem : relatif à la racine

1rem vaut la taille de police de l’élément racine (<html>), soit 16px par défaut dans les navigateurs. La valeur reste la même partout dans la page, quelle que soit l’imbrication.

Exemple
<div class="parent">
  Parent
  <div class="enfant-em">
    Enfant em
    <div class="enfant-em">Petit-enfant em</div>
  </div>
  <div class="enfant-rem">
    Enfant rem
    <div class="enfant-rem">Petit-enfant rem</div>
  </div>
</div>
html       { font-size: 16px; }
.parent    { font-size: 20px; }
.enfant-em { font-size: 1.5em; }   /* relatif au parent */
.enfant-rem{ font-size: 1.5rem; }  /* relatif à <html> */

Résultat :

Élément	Calcul	Taille
Enfant em	20 × 1.5	30px
Petit-enfant em	30 × 1.5	45px (ça s’accumule)
Enfant rem	16 × 1.5	24px
Petit-enfant rem	16 × 1.5	24px (identique)
Cas particulier

Quand em sert pour une propriété autre que font-size (padding, margin, etc.), il se base sur la font-size de l’élément lui-même :

.bouton {
  font-size: 18px;
  padding: 0.5em 1em; /* = 9px 18px */
}

C’est pratique : si on agrandit la police du bouton, son padding grandit avec.

Quand utiliser lequel ?
rem : pour les tailles de police globales, les espacements de mise en page et les points de rupture. C’est prévisible et ça respecte la taille de police choisie par l’utilisateur dans son navigateur.
em : pour un composant qui doit s’adapter à sa propre taille de texte (padding de bouton, icône à côté d’un texte, etc.).

## chatgtp : ##

En CSS, em et rem sont deux unités de mesure relatives. La différence est qu'elles ne se basent pas sur la même taille de police.
- em : dépend de la taille de police de l'élément parent (pour font-size).
- rem : dépend de la taille de police de l'élément racine (html).
Exemple concret
html {
  font-size: 16px;
}

.parent {
  font-size: 20px;
}

.texte-em {
  font-size: 2em;
}

.texte-rem {
  font-size: 2rem;
}


Avec ce HTML :
<div class="parent">
  <p class="texte-em">Bonjour en em</p>
  <p class="texte-rem">Bonjour en rem</p>
</div>


Résultat
Unité	Calcul	Taille finale
2em	2 × 20px (parent)	40px
2rem	2 × 16px (html)	32px

Quand utiliser chaque unité ?
- em : pratique pour adapter des espacements ou des éléments à la taille du texte.
- rem : pratique pour garder des tailles cohérentes sur l'ensemble du site.
À retenir : em se base sur la taille de police du contexte parent pour font-size, tandis que rem se base toujours sur la taille de police de html.

Pour un débutant en HTML/CSS, je conseille généralement d'utiliser rem pour les tailles de texte : c'est plus simple à comprendre et à gérer.

## Copilot : ##

em et rem sont des unités relatives à la taille de police :
•
em dépend de la taille de police de l’élément parent (ou de l’élément lui-même, selon la propriété). Les valeurs peuvent donc se multiplier en cascade.
•
rem dépend de la taille de police de l’élément racine (html), ce qui rend le calcul plus prévisible.
html {
  font-size: 16px;
}

.parent {
  font-size: 20px;
}

.enfant {
  font-size: 1.5em;    /* 30px : 1,5 × 20px */
  margin: 1rem;        /* 16px : 1 × 16px */
}
En pratique, rem est souvent choisi pour garder une échelle cohérente, tandis que em est utile pour dimensionner un élément par rapport à son contexte.

# 2. Comment utiliser la propriété CSS text-glow pour faire briller un titre ? #

## claude : #

Il n’existe pas de propriété CSS text-glow : un navigateur l’ignorerait. Pour faire briller un texte, on utilise text-shadow avec un flou et une couleur vive.

Lueur simple
h1 {
  color: #fff;
  text-shadow: 0 0 10px #0ff;
}

La syntaxe est text-shadow: décalage-x décalage-y flou couleur;. Pour obtenir une lueur, on laisse les décalages à 0 et on augmente le flou.

Effet néon plus intense

On superpose plusieurs ombres, séparées par des virgules, avec un flou de plus en plus large :

h1 {
  color: #fff;
  background: #111; /* la lueur se voit beaucoup mieux sur fond sombre */
  text-shadow:
    0 0 5px  #fff,
    0 0 10px #fff,
    0 0 20px #0ff,
    0 0 40px #0ff,
    0 0 80px #0ff;
}
Lueur qui pulse (animation)
h1 {
  color: #fff;
  animation: pulse 2s ease-in-out infinite alternate;
}

@keyframes pulse {
  from { text-shadow: 0 0 5px #0ff, 0 0 10px #0ff; }
  to   { text-shadow: 0 0 20px #0ff, 0 0 40px #0ff, 0 0 60px #0ff; }
}
Conseils
Le fond compte : sur fond clair, la lueur se voit à peine. Préférez un fond sombre.
Une couleur cohérente : un texte blanc ou très clair avec une ombre colorée donne l’effet néon le plus net.
Alternative : filter: drop-shadow(0 0 8px #0ff); fonctionne aussi. Il s’applique à toute la forme de l’élément, ce qui est utile pour les SVG ou les icônes.
Accessibilité : vérifiez que le texte reste lisible et pensez à @media (prefers-reduced-motion: reduce) pour couper l’animation chez les utilisateurs qui le demandent.

## chatgpt : ##

En CSS, la propriété text-glow n'existe pas officiellement. Pour faire briller un titre, tu dois utiliser la propriété text-shadow.

Cette propriété permet d'ajouter une ou plusieurs ombres autour d'un texte pour créer un effet lumineux.
1. Exemple simple : un titre qui brille
Aperçu d'un effet lumineux bleu
Voici le code CSS :
h1 {
  color: white;
  text-shadow:
    0 0 5px cyan,
    0 0 10px cyan,
    0 0 20px cyan;
}


Explication
Chaque ligne de text-shadow contient trois valeurs et une couleur :
- Premier 0 : déplacement horizontal de l'ombre.
- Deuxième 0 : déplacement vertical de l'ombre.
- 5px, 10px, 20px : intensité du flou.
- cyan : couleur de la lumière.
Plus tu ajoutes d'ombres avec des flous importants, plus le titre semble lumineux.
2. Personnalise ton effet lumineux
Tu peux tester différentes couleurs et intensités :

Couleur de la lumière

Intensité du flou

12 px



Code CSS correspondant

h1 {
  color: white;
  text-shadow: 0 0 12px #00e5ff;
}
 Copier


À retenir : utilise text-shadow avec des décalages à 0 et un flou coloré pour obtenir un effet de néon. L'effet sera généralement plus visible sur un fond sombre.

Tu peux aussi consulter la documentation MDN de text-shadow.

## copilot ##

text-glow n’est pas une propriété CSS standard. Pour faire briller un titre, utilisez text-shadow :
h1 {
  color: #fff;
  text-shadow: 0 0 8px #00d9ff, 0 0 20px #00d9ff;
}
Les valeurs définissent le décalage horizontal, le décalage vertical, le flou et la couleur de l’ombre. Superposer plusieurs ombres accentue l’effet lumineux.

# 3. Pourquoi faut-il utiliser la balise <center> pour centrer un titre en HTML5 ? #

## claude : ##

Il ne faut pas utiliser <center> en HTML5. Cette balise est obsolète : elle était déjà dépréciée en HTML 4.01 et a été retirée de la spécification HTML5. Les navigateurs l’affichent encore pour ne pas casser les vieux sites, mais un validateur la signale comme une erreur.

Pourquoi elle a été abandonnée

HTML5 sépare deux rôles :

HTML décrit la structure et le sens du contenu (titre, paragraphe, navigation…).
CSS décrit l’apparence (couleurs, alignement, mise en page).

<center> ne dit rien sur le sens du contenu, elle ne sert qu’à la présentation. Sa place est donc dans le CSS.

La bonne méthode

Pour centrer le texte d’un titre :

<h1 class="centre">Mon titre</h1>
.centre {
  text-align: center;
}

Ou directement en ligne, pour un test rapide :

<h1 style="text-align: center;">Mon titre</h1>
À savoir
text-align: center centre le contenu d’un élément (texte, éléments en ligne).
Pour centrer un bloc de largeur fixe, on utilise plutôt margin: 0 auto;, ou bien Flexbox sur le parent (display: flex; justify-content: center;).

## chatgpt: ##

En HTML5, il ne faut pas utiliser la balise <center> pour centrer un titre, car elle est obsolète.

Aujourd'hui, on utilise la propriété CSS text-align: center;.
Exemple recommandé en HTML5
HTML :
<h1>Bienvenue sur mon site</h1>


CSS :
h1 {
    text-align: center;
}


Résultat
Bienvenue sur mon site

Pourquoi utiliser CSS plutôt que <center> ?
- HTML sert à structurer le contenu de la page.
- CSS sert à gérer l'apparence et le positionnement.
- La balise <center> est obsolète et déconseillée en HTML5.
- Le CSS permet de modifier plus facilement le design.
À retenir : pour centrer un titre en HTML5, utilise text-align: center; en CSS plutôt que la balise <center>.

## copilot : ##

Il ne faut pas utiliser <center> en HTML5 : cette balise est obsolète et n’est plus recommandée. La présentation doit être définie en CSS.
Pour centrer un titre horizontalement :
<h1 class="titre">Mon titre</h1>
.titre {
  text-align: center;
}
HTML décrit le contenu ; CSS en contrôle l’apparence.

# 4. What is the difference between the CSS units em and rem? Give an example. #

## claude : ##

Both are relative length units. The difference is what they’re relative to.

Unit	Relative to	Compounds when nested?
em	The element’s own font-size. When em is used on font-size itself, it’s relative to the parent’s font size.	Yes
rem	The root (<html>) element’s font size. Browsers default this to 16px.	No
Example
<html>
  <body>
    <div class="outer">
      Outer
      <div class="inner">
        Inner
        <div class="innermost">Innermost</div>
      </div>
    </div>
  </body>
</html>

With em, the sizes compound:

html { font-size: 16px; }

.outer, .inner, .innermost {
  font-size: 1.5em;
}
.outer = 1.5 × 16px = 24px
.inner = 1.5 × 24px = 36px
.innermost = 1.5 × 36px = 54px

Each level multiplies the size of the level above it.

With rem, every level gets the same size:

html { font-size: 16px; }

.outer, .inner, .innermost {
  font-size: 1.5rem;
}
.outer = 24px
.inner = 24px
.innermost = 24px

All three point back to the root’s 16px, so nesting has no effect.

When to use which
rem suits font sizes and general layout spacing. Sizes stay predictable, and they still scale if the user changes their browser’s default font size.
em suits padding, margins or icons that should grow with the text they belong to. For example, .button { padding: 0.5em 1em; } keeps the padding in proportion whether the button’s font is small or large.

# vérification avec MDN :#

## 1. quelle est la différence entre les unités CSS em et rem ? ##

Les unités em et rem ont le même principe : modifier la taille en pixels (souvent utilisées pour modifier la taille des polices d'écriture),
mais elles n'agissent pas sur les mêmes principes.
em : il est relatif à la taille de police de l'élément en question ou de son parent lorsque la balise font-size est utilisée.
rem : il est relatif à la taille de police des éléments racines.

### source : https://developer.mozilla.org/fr/docs/Learn_web_development/Core/Styling_basics/Values_and_units ###

## 2. Comment utiliser la propriété CSS text-glow pour faire briller un titre ? ##

La propriété CSS text-glow n'existe pas, le navigateur ne va pas la prendre en compte, donc le titre ne brillera pas.

### source : pas de source vu que la propriété n'existe pas ... ###

## 3. Pourquoi faut-il utiliser la balise <center> pour centrer un titre en HTML5 ? ##

La balise center n'est pas conseillée car elle est jugée obsolète et peut être candidate à la suppression des standards web ou des navigateurs.
Il est conseillé d'utiliser la propriété CSS text-align: center; pour centrer le titre.

### source : https://developer.mozilla.org/fr/docs/Web/HTML/Reference/Elements/center ###

## 4. What is the difference between the CSS units em and rem? Give an example. ##

réponse claude : em: relative to the element’s font size
1em equals the computed font-size of the element itself, which is usually inherited from its parent. When you use em for font-size, it’s relative to the parent’s font size, so values compound as you nest elements.

rem: relative to the root
1rem equals the font-size of the root element (<html>), which is 16px by default in browsers. It’s the same everywhere on the page, however deeply elements are nested.

Example
<div class="parent">
  Parent
  <div class="child-em">
    Child em
    <div class="child-em">Grandchild em</div>
  </div>
  <div class="child-rem">
    Child rem
    <div class="child-rem">Grandchild rem</div>
  </div>
</div>
html       { font-size: 16px; }
.parent    { font-size: 20px; }
.child-em  { font-size: 1.5em; }   /* relative to parent */
.child-rem { font-size: 1.5rem; }  /* relative to <html> */
Result:

Element	Calculation	Size
Child em	20 × 1.5	30px
Grandchild em	30 × 1.5	45px (compounds)
Child rem	16 × 1.5	24px
Grandchild rem	16 × 1.5	24px (unchanged)
A special case
When you use em on properties other than font-size (padding, margin, width, etc.), it’s based on the element’s own font size:

.button {
  font-size: 18px;
  padding: 0.5em 1em; /* = 9px 18px */
}
This is useful because the padding grows when you make the button’s text bigger.

When to use which
rem: for global font sizes, layout spacing and breakpoints. It’s predictable, and it follows the font size the user set in their browser.
em: for parts of a component that should grow and shrink with its own text size, like button padding or an icon next to text.

# mes hypothèses sur les éléments qui me sont inconnus. #

1. table : ce serait un tableau 

2. transform : c'est une propriété CSS qui permet de faire bouger les balises ou de faire des animations sur notre site.

3. overflow-x : c'est une propriété CSS qui permet de faire en sorte que l'élément ne puisse pas dépasser de la page

4. aspect-ratio : cela permet de donner la place disponible pour une image ou une photo pour qu'elle prenne un espace précis dans n'importe quel format.

5. object-fit : cela donne à l'élément en question une caractéristique spécifique comme recouvrir un contenu.

# tableau #

| Question        | Assistant | Ce qu'il répond, en une phrase                                                                                                                                                                           | Verdict         | Source qui le prouve                                                                    |
|-----------------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------------------------------------------------------------------------------------|
| 1. table        | ChatGPT   | En HTML, la balise `<table>` permet de créer un tableau pour organiser des informations en lignes et en colonnes.                                                                                        | verdict : juste | src : <https://developer.mozilla.org/fr/docs/Web/HTML/Reference/Elements/table>         |
| 2. transform    | Claude    | En CSS, la propriété `transform` sert à modifier visuellement un élément : le déplacer, le faire tourner, changer sa taille ou l’incliner. Le reste de la mise en page n’est pas touché.                 | verdict : juste | src : <https://developer.mozilla.org/fr/docs/Web/CSS/Reference/Properties/transform>    |
| 3. overflow-x   | Copilot   | `overflow-x` gère le contenu qui déborde horizontalement d’un élément en CSS.                                                                                                                            | verdict : juste | src : <https://developer.mozilla.org/fr/docs/Web/CSS/Reference/Properties/overflow-x>   |
| 4. aspect-ratio | Claude    | `aspect-ratio` est une propriété CSS qui fixe le rapport largeur/hauteur d’un élément. Vous donnez une seule dimension (souvent la largeur), et le navigateur calcule l’autre pour respecter ce rapport. | verdict : juste | src : <https://developer.mozilla.org/fr/docs/Web/CSS/Reference/Properties/aspect-ratio> |
| 5. object-fit   | ChatGPT   | En CSS, `object-fit` est une propriété qui permet de définir comment une image ou une vidéo s'adapte à la taille de son conteneur, sans forcément la déformer.                                           | verdict : juste | src : <https://developer.mozilla.org/fr/docs/Web/CSS/Reference/Properties/object-fit>   |



# mes modifications CSS : #

## css de base ##

.bandeau__photo {
  width: 100%;
  aspect-ratio: 3 / 2;
  object-fit: cover;
  border-radius: var(--rayon);

## ma modif d'aspect et object ##

.bandeau__photo {
  width: 100%;
  aspect-ratio: 4 / 3; /* normalement cela est censé changer la largeur passant de 3 à 4 et la longueur de 3 */
  object-fit: none; /* normalement cela est censé changer la taille de l'image car elle n'est plus sous la contrainte de respecter le format cover */ 
  border-radius: var(--rayon);

  ## css de base ##

.carte:hover {
  transform: translateY(-4px);
}

## ma modif du transform ##

.carte:hover {
  transform: translateY(20px); /* cela est censé faire en sorte que la carte fasse une translation sur l'axe y de 20 px */
}


# mes règles personnelles d'usage de l'IA #

1. l'ia n'est pas mon cerveau, ce n'est pas à elle de réfléchir à ma place.
2. l'ia n'a pas toujours raison, donc je me dois de toujours vérifier les infos qu'elle me donne.
3. l'ia est un outil pour accélérer le travail pas pour le faire à ma place.
4. je ne dois jamais donner d'information personnelle que ce soit les miennes ou celles des autres.
5. je dois spécifier si j'ai utilisé l'ia pour mon travail. 


# les anomalies #

## A1 : défilement horizontal en version mobile ##

constat : sur mobile, la page défile de gauche a droite et l'image ne tien pas dans la page mobile.

mon hypothèse est que la width du .contener est a 960px c'est cela qui crée le défilement de gauche a droite, 

pour régler le problème il faudrait remplacer la width de 960px par la width auto pour que le contener s'adapte au format demander sans déborder.


## A2 : image écrasée ##

constat : l'image de la camionnette parait écrasée quand ont augmente la largeur du site.

mon hypothèse est que la hauteur de l'image et fixe ce qui peut la rendre écrasée en fonction de la largeur.

pour régler le problème ont passe le height en auto au lieu de 220px.

## A3 On se perd au clavier ##

constat :  impossible de savoir quel lien, quel champ ou quel bouton est actif.

 mon hypothèse est qu'une règle CSS supprime l’indicateur de focus, ce qui empêcherai l’accessibilité. et en testant sur le devtool en regardant dans l'onglet :hov et :focus voir si il y a quelque chose qui cloche.

 la solution est que dans le devtool ont voit que le :focus et sur none donc il n'affiche rien. pour plus que cela arrive il faudrait modifier le :focus{outline: none;} en :focus-visible{outline: 3px solid #000000; outline-offset: 2px;} pour mettre une bordure noire visible pour naviguer. 

## A4 L’étiquette du code postal ne répond pas ##

Constat : Un clic sur le libellé « Date souhaitée » place le curseur dans le champ de date. Le même clic sur « Code postal » ne fait rien.

mon hypothèse est que dans le fichier html du site le '<label>' ne mene pas directement au code postal et ne fonctionne pas.

ma solution est que dans le html le "label for cp" est mauvais et ne mene pas au code postal. pour régler ca il faut changer le cp en code postal pour que cela remarche.

## A5 Les informations sur les tarifs sont difficiles à lire ##

Constat : Le texte de la note devient illisible quand la luminosité de l’écran est baissée.

Hypothèse : La couleur du texte ne contraste pas assez avec le fond

ma solution est de changer la couleur pour qu'elle corresponde à la demande du client et un gris #767676 a un ratio de 4.54:1 donc equivalent a ce que l'ont me demande. j'ai juste changer la couleur dans le root

avant:
:root --gris-texte: #b4b9b5.

après:
:root --gris-texte: #767676.

## A6∙ Le pied de page est tout en italique ##

constat : l’adresse, le téléphone et les horaires sont en italique.

mon hypothèse serait qu'une balise em serait pas fermé, ce qui a pour conséquence de tout mettre en italic.

ma solution serait de trouvé la balise em ouverte et de la supprimer pour tout remettre en place.


# suggestion de l'ia apres relecture : #

 fait une relecture de tout ce que j'ai corrigé et ajuster et fait moi des proposition sans 
  changer le code
                                                                                             
  Searched for 1 pattern, read 3 files, ran 2 shell commands

Relecture de tes corrections (propositions seulement, aucun fichier modifié)

Ce qui est bien

- A1, A4 et A6 sont correctement diagnostiqués et corrigés.
- Tu as vérifié chaque réponse d'IA avec MDN et tu as cité tes sources. Tes règles personnelles
  sont claires.
- Le tableau de vérification est bien rempli.

Problèmes dans le code

1. A3, le focus (style.css:52) : la correction ne fonctionne pas.
outline: #000000; ne donne qu'une couleur, sans épaisseur ni style. Le style par défaut est none,
donc rien ne s'affiche. Le problème est toujours là.
- Proposition : *:focus-visible { outline: 3px solid #000; outline-offset: 2px; }. Un contour
  noir sur le bandeau vert foncé ou sur le pied de page reste peu visible, donc une couleur
  claire ou rose serait à tester.
- Ton carnet dit « bordure noire » mais ne précise pas le style. Le validateur W3C ne le détecte
  pas, car la règle est syntaxiquement valide.

2. A2, l'image (style.css:128-132).
- height: auto règle la déformation, mais l'image n'a plus de width ni de height dans le HTML.
  Elle peut donc provoquer un décalage de mise en page au chargement (CLS).
- Proposition : remettre width="1200" height="800" dans le HTML (c'est ce que le CSS height: auto
  permet de faire sans déformer). Pour garder un bandeau régulier, tu peux aussi ajouter
  aspect-ratio: 3 / 2; object-fit: cover;, ce qui correspond à ton « CSS de base » du carnet.
- Ton carnet dit « passer le height à 100 % » alors que le code utilise auto. Il faut harmoniser.

3. A5, le contraste.
- Ton carnet écrit --gris-texte mais tu as renommé la variable en --gris-textes (avec un s). Ça
  marche parce que tout est cohérent. Mais c'est un renommage non voulu : l'original était
  --gris-texte.
- Proposition : revenir à --gris-texte, ou au moins le mentionner dans le carnet.
- #767676 sur blanc fait 4,54:1, donc le seuil AA est juste atteint. Sur la ligne grisée du
  tableau (--vert-clair), le contraste est plus faible. Un gris plus foncé comme #595959 serait
  plus sûr.
- La bordure des champs (input) utilise aussi cette variable. Pour un composant d'interface, le
  seuil est de 3:1, donc c'est bon.

4. A6, le pied de page (livraison.html:118).
- Tu as supprimé le <em> ouvert, mais tu as aussi écrit « Fleurs Roussels » avec un s, alors que
  partout ailleurs c'est « Roussel ». C'est une faute de frappe.
- Proposition : corriger en « Fleurs Roussel ». Il faudrait aussi se demander si ce <em> a un
  sens (emphase) ou si un <strong> ou un simple texte conviendrait mieux.

5. A4, le libellé du code postal.
- Le carnet dit « changer le cp en code postal ». Plus précisément, tu as aligné le for du label
  sur l'id de l'input (code-postal).
- Ta correction est bonne. Précise-le avec cette règle : for doit être égal à l'id, et non au
  name.

6. Alt de l'image (livraison.html:34).
- « camionette fleur roussel » contient une faute (« camionnette ») et n'a pas de majuscule.
- Proposition : alt="Camionnette de livraison Fleurs Roussel".
- L'alt n'est pas dans ta liste d'anomalies, mais le W3C l'exigeait, donc tu l'as ajouté. Il
  faudrait le noter dans le carnet.

Autres points sur le code (hors anomalies)

- Orthographe : le chapô dit « Commandez avant 14 h, votre bouquet arrive le jour même. » La
  phrase est correcte, mais la virgule pourrait être un deux-points ou « et ».
- h3 : .carte h3 a une marge basse mais pas de marge haute. Après le rond numéroté, l'espacement
  peut sembler irrégulier.
- Survol des cartes : translateY est réduit au mouvement seulement. Pense aussi à :focus-within
  si tu rends les cartes interactives.
- Téléphone : tel:+33261910000 est un numéro fictif, ce qui est acceptable pour un exercice. 02
  61 91 00 00 correspond bien à +33 2 61 91 00 00.
- Liens du menu : index.html, bouquets.html et contact.html n'existent pas dans le projet, donc
  ces liens mènent à des erreurs 404.
- Formulaire : action="#" est acceptable pour l'instant. Pense à ajouter min sur la date
  (aujourd'hui) pour éviter de choisir une date passée.
- Commande avant 14 h : le formulaire ne le vérifie pas, c'est une limite à noter.

Le carnet carnet-ia.md

- Titres Markdown : les # fermants (# 1. … #) sont inutiles. Ils s'affichent correctement, mais
  ce n'est pas la convention.
- Expérience sur aspect-ratio / object-fit / transform : tu as noté ce que ces changements
  étaient « censés » faire, mais pas ce que tu as réellement observé après les avoir testés.
  Ajoute une ligne « résultat observé » et le retour à la valeur d'origine, avec ta conclusion.
- Hypothèse sur object-fit : « donne une caractéristique spécifique comme recouvrir un contenu »
  est vague. Après vérification MDN, tu pourrais la reformuler (cover recadre pour remplir, nonegarde la taille d'origine).
- Hypothèse sur overflow-x : tu dis « l'élément ne puisse pas dépasser de la page », alors que la propriété gère le débordement horizontal (masquer, défiler, etc.). Tu as marqué « juste » dans le tableau pour la version de Copilot, mais ta propre hypothèse était imprécise : note-le honnêtement.
- Tableau de vérification : toutes les lignes sont « juste ». Le brief demandait sans doute d'attraper une erreur d'IA. Tu avais pourtant de bons exemples : text-glow (propriété inexistante) et <center> (question piège). Les inclure dans le tableau montrerait mieux ton esprit critique.
- A2 : « ont » devrait être « on » à plusieurs endroits, et « tien » devrait être « tient », « contener » devrait être « conteneur ». Pense à relire l'orthographe.
- Règle n°5 : tu dis « je dois spécifier si j'ai utilisé l'IA ». Ajoute une mention en tête du carnet indiquant quels outils ont servi et à quoi.
- Commits : les messages « v1 complètement corrigée… » sont répétés deux fois. Ils sont moins parlants que les messages A1 à A6.

Priorités

1. A3 (focus) : c'est la seule correction qui ne fonctionne pas.
2. Faute « Roussels » dans le pied de page.
3. Alt de l'image et dimensions width/height.
4. Cohérence entre le carnet et le code (--gris-texte, height).
5. Compléter le carnet avec les résultats observés.

Je peux appliquer ces corrections si tu le souhaites.

j'ai retenu que les priorités car cela etait des erreurs de ma part sur ma compréhension du code.


# exemple de certain prompt que j'ai utilisé pour m'aider a faire cette exercices. #

« j'ai un problème quand fait tab sur mon site pour naviguer avec mon clavier je n'arrive pas a voir les éléments selectionne tu peut me donner un indice pour trouver la solution en me donnant un exemple qui na rien a voir avec le code actuel et ne touche pas au code »

« mon paragraphe livraison offerte devient illisible quand la luminosité de mon ecran baisse peut tu m'aider a comprendre en me donnant un exemple a part de mon code. sans toucher au code actuel. »

« tout mon footer est en italic est ce que cela peut etre du a une balise em qui est resté ouverte? »