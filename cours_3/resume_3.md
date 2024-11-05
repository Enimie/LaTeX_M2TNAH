# Cours 3 - Approfondissements: Éléments non textuels; édition de texte


## Créer ses commandes et environnements (2)

### Syntaxe pour créer une commande ou un environnement avec argument optionnel


- Syntaxe pour créer une commande avec argument optionel, grâce au package `xargs`:

- `\newcommandx{#1}[#2][#3]{#4}` `#1`=nom de la commande; `#2`= nombre d'arguments; `#3`=liste des arguments optionnels (liste de numéros indiquant la position des arguments optionnels dans la commande). Une  valeur par défaut peut être attribuée aux arguments optionnels, consulter le manuel de `xarg`; `#4`= le code

- Pour créer un environnement avec arguments optionnels, utilisez le package `xargs`



- Tester si un argument est vide grâce au packet `etoolbox`: utiliser la commande `\ifstrempty{#1}{#2}{#3}`. `#1`=la chaine de caractères que l'on va tester (ça peut être un argument de notre ouvelle commande, par exemple `#1`); `#2`=ce qui se passe si la chaine est vide; `#3`=ce qui se passe sinon.

### Appeler un argument dans la dernière partie d'un nouvel environnement


-  Il n'est pas possible d'appeler l'argument du nouvel environnement dans la *dernière partie* de la commande `newenvironment` (celle qui indique le code qui sera appelé à la fermeture de l'environnement). Il faut:
-  créer une "boite de sauvegarde" en mettant, avant la définition du nouvel environnement, `\newsavebox{\boite}` (on peut bien sûr donner un autre nom à la boite). 
- Dans le code appelé à l'ouverture du nouvel environnement, mettre l'argument dans cette boite, par exemple: `\savebox{\boite}{#1}`
- Dans le code appelé à la fermeture de l'environnement, on peut utiliser cette boite (et donc le contenu de l'argument) en utilisant: `\usebox{\boite}`.
- Pour des exemples d'utilisation, voir l'ouvrage de LOZANO, Vincent, cité plus haut et mis dans la biliographie.

## Les éléments non textuels

### Les flottants 


- Lorsque l'on insère un tableau, une image ou un graphique, ils apparaissent  exactement là où ils sont appelés, ce qui peut poser des problèmes de mise en page. De plus, ils ne comportent pas de légende. 
- Il faut donc les transformer en flottant.
- *Flottant*: élément non textuel dont l'insertion dans la page va être calculée de façon à maintenir une mise en page correcte. 
- Deux environnements pour faire des flottants: `figure` et `table`
- Au sein de ces environnements, la commande `\caption{#1}` permet d'insérer une légende (**nb**: on peut lui passer un argument optionnel: ce qui apparaîtra dans la liste des figures ou des tables)
- Insérer la liste des figures:  `\listoffigures`; insérer la liste des tableaux: `\listeoftable`

- Pour préciser où l'on souhaite insérer le flottant, on peut mettre un argument optionnel à ces environnements. Valeurs possibles:

|valeur|effet|
|-- |-- |
|h|positionne le flottant à l'emplacement de son appel|
|t|positionne le flottant en haut d'une page|
|b|positionne le flottant en bas d'une page|
|p|positionne le flottant sur une page dédiée aux flottants|

- **nb** Pour éviter que le flottant n'aille trop loin de l'endroit où on l'a appelé, utiliser la commande `\FloatBarrier` du package `placeins`:  tous les floants appelés avant la commande sont placés avant celle-ci.
- Le  package `wrapfig` permet de mettre du texte autour du flottant (voir le manuel)




### Insérer une image 

- Pour insérer une image, il faut utiliser la commande  `\includegraphics[⟨options⟩]{⟨chemin de l’image⟩}` du package `graphicx`. Pour régler la taille de l'image, indiquer dans l'argument optionnel `scale=xx` où xx est une valeur numérale (au-dessus de 1: l'image est agrandie; en dessous de 1, elle est diminuée). Pour les autres options, voir le manuel.
- L'environnement `landscape` du package  `lscape` permet de mettre l'image (ou tout autre élément: tableau, texte) en format paysage.

### Insérer tableau

- Environnement `tabular` Utiliser l'assistant de Texstudio, très efficace. Syntaxe:
	- l'argument de tabular permet d'indiquer le nombre de colonnes et la position du texte (centré: `c`, aligné à gauche: `l`, aligné à droite `r`). Le signe `|` indique que les colonnes doivent être séparées par une bande verticale
	- `hline` permet de tracer des traits horizontaux entre les lignes
	- Au sein d'une ligne: on indique un changement de colonne par le signe `&`, et la fin de la ligne par  `\\`
	- Il est possible également d'indiquer la taille des colonnes. Voir par exemple le tutoriel ici:  
[tabular](https://lataix-sebastien.developpez.com/tutoriels/latex/les-tableaux-sous-latex/), ou utiliser simplement l'assistant de Texstudio.


- **nb** Il existe un package `longtable` permettant de faire des tableaux allant sur plusieurs pages et pouvant recevoir des notes de bas de page (`\footnote`).
- Le package `tabbing` permet d'aligner du texte en colonne sans réellement faire de tableau. Il est parfois plus adapté que l'environnement `tabular` ; vous trouverez un tutoriel ici:[tabbing](https://latexref.xyz/fr/tabbing.html)



### Faire un graphique avec TikZ 

- Utiliser l'environnement `tikzpicture` du package `tikz`.
- `tikz` a une syntaxe spécifique. Notamment, chaque commande doit être terminée par un `;`.
- Tutoriels très clairs pour utiliser `TikZ`: [Tutoriels tikz Maïeul](https://geekographie.maieul.net/spip.php?page=recherche&recherche=tikz). Vous pouvez aussi vous référer à l'ouvrage [TikZ pour l'impatient](http://math.et.info.free.fr/TikZ/bdd/TikZ-Impatient.pdf) (p.21 pour une explication sur geogebra)
- un site pour créer rapidement des arbres avec TikZ: [arbres](http://math.et.info.free.fr/TikZ/Arbres.html)

### Faire des  histogrammes avec TikZ et le package pgfplots 

- Un tutoriel ici: [pgfplots](http://lesfichesabebert.fr/TeX/tikz/Pgfplot.html). **Attention**, l'auteur donne à chaque fois également les commandes pour ceux qui utilisent `ConTeXt`: ne pas en tenir compte
- Dans l'environnement `tikzpicture`, utiliser l'environnement  `axis` pour créer des abscisses et des ordonnées.
- Dans l'environnement `axis`, la commande `\addplot coordinates {#1};` permet d'ajouter des points (en `#1`):
	+ chaque point est indiqué entre parenthèses par : `abscisse-virgule-ordonnée`.
	+ **Attention** pour les valeurs décimales, utiliser non une virgule mais un point (notation anglo-saxonne)
- Il peut y avoir plusieurs commandes `addplots` à la suite.
- Pour indiquer la légende: `\legend{#1}`. S'il y a plusieurs ensembles de données (plusieurs `\addplot`), il doit y avoir plusieurs éléments dans la légende, séparés par une virgule. Exemple: `\legend{légende pour le premier \addplot,légende pour le second \addplot}`
- Pour faire un diagramme en barres verticales ou horizontales: passer à l'environnement `axis` l'option `ybar` et `xbar`; `ybar stacked` pour que les barres soient les unes sur les autres
- l'option `xtick=data` permet de régler les "labels": de  ne faire apparaître sur la ligne des abscisses que les données utilisées.
- Pour que les nombres supérieurs à 999 ne soient pas notés avec une virgule (notation anglo-saxonne), insérer dans le préambule la commande `\pgfplotsset{/pgf/number 	format/1000 sep=}`


Pour des exemples, voir les exercices.

- **nb** Pour faire un   diagramme camembert, utiliser le package `pgf-pie`.


## Importer des données d'un fichier . csv pour obtenir tableaux et graphes avec TikZ, pgfplots et le package pgfplotstable

- Pour des exemples, voir les exercices.

### Étape préliminaire: stocker les données dans une variable


-  `\pgfplotstableread[col sep=XX]{#1}{#2}`, où XX peut prendre comme valeur `comma` ou `tab` selon le fichier csv que l'on importe (s'il y a des virgules dans les données importées, utiliser `tab`);  `#1`=chemin du fichier (avec l'extension); `#2`=nom donné à une variable ainsi créée et qui va stocker les données du fichier. 
- Exemple: `\pgfplotstableread[col sep=comma]{mon_fichier.csv}{\table}` 

- Mettre dans le préambule `\pgfplotsset{/pgf/number format/read comma as period}` pour que les virgules dans les nombres décimaux  soient bien comprises comme telles (notation française *vs* notation anglo-saxonne)

### Importer les données dans un tableau

- `\pgfplotstabletypesetfile{#1}`: lit le contenu de la variable précédemment créée et indiquée en `#1` et le transforme en tableau. Exemple: `\pgfplotstabletypesetfile{\table}`
-  Pour modifier apparence des tableaux: passer des arguments  optionnels à `\pgfplotstabletypesetfile`, ou régler l'apparence de tous les tableaux dans le préambule avec la commande `\pgfplotstableset`. Pour des exemples, voir les exercices et le manuel de `pgfplotstable` 

- **Quand les données ne sont pas des données numérales mais des chaînes de caractères**:  passer   à `\pgfplotstabletypesetfile` l'option `string type`.



### Importer les données dans un diagramme
-  reprendre l'environnement `axis` au sein de  `tikzpicture`
- avec la commande `\addplot`, à la place de `coordinates`, mettre: ` table[option]{#1}`, où `#1`=le nom de la variable où l'on a stocké les données. 
- Pour indiquer à `pgfplotstable` quelles colonnes du fichier utiliser, indiquer en option:  `x=nom de la colonne, y=nom de la colonne`. 

- **Quand les données ne sont pas des données numérales mais des chaînes de caractères**: 
1. Passer comme option à `\addplot table`: `x expr=\coordindex` 
2. Indiquer que les données (non numériques) d'une colonne doivent apparaître comme label sur la ligne des abscisses: passer comme option à `axis` :  `xticklabels from table={#1}{#2}`, où `#1`=le nom de la variable où l'on a stocké les données, et `#2`=le nom de la colonne utilisée.
3. Pour faire tourner sur la ligne des abscisses les "labels" pour qu'ils apparaissent à la verticale, passer en option à `axis`:  `x tick label style={rotate=90}`





## Les packages  `reledmac` et `reledpar` pour l'édition critique

### reledmac

1. Pour numéroter les  lignes:  
```
\beginnumbering  
 \pstart
Le texte à numéroter
 \pend
 \endnumbering
``` 
 
 Pour que chaque paragraphe soit automatiquement mis entre les balises `\pstart`et `\pend`, il faut mettre `\autopar` au début du texte et terminer le texte par une ligne blanche ou la commande `\par`
 
 ```
\beginnumbering  
 \autopar
premier paragraphe

deuxième paragraphe

etc
 
 \endnumbering
``` 
 
 
Pour configurer la numérotation, voir le manuel; idem pour la syntaxe des vers. Voir aussi le chapitre 20 de l'ouvrage   [XeLaTeX appliqué aux sciences humaines](https://halshs.archives-ouvertes.fr/halshs-00924546)

Dans le cas de vers, nous aurons: 

```
\beginnumbering
 \stanza
un vers.&
le dernier vers de la strophe\&
 \endnumbering
``` 


2. Apparat critique: 
- les "familiar notes":`\footnoteA{#1},\footnoteB{#1}`, etc (cinq niveaux, jusqu') `\footnoteE`
- les "critical notes" (sans appel de note, mais avec, dans  la note, le numéro de ligne ou de vers et un lemme, c'est-à-dire le morceau de texte pour lequel on indique des variantes): :`\Afootnote{#1},\Bfootnote{#1}`, etc (cinq niveaux, jusqu') `\Efootnote`
- les notes de fin (`\Aendnote{#1}`, etc, jusqu'à `\Eendnote`)

- Pour faire une note critique (avec lemme): `\edtext{#1}{#2}`, où `#1`= le mot qui va apparaître comme lemme, et `#2`= la "critical note". 

Pour des exemples, voir les exercices.

### reledpar

- à charger avec `reledmac`. Sert à mettre deux textes en vis-à-vis. Syntaxe:

```
\begin{pages} %Mettre en vis-à-vis sur deux pages
	\begin{Leftside}
Texte de gauche
	\end{Leftside}

	\begin{Rightside}
	Texte de droite
\end{Rightside}
\end{pages}
\Pages %imprimer le vis-à-vis
```

- Pour avoir un vis-à-vis en colonnes, remplacer l'environnement `pages` par `pairs` et la commande `\Pages` par `\Columns`

- Le package `reledpar` fait correspondre en vis-à-vis chaque "boîte" d’un texte à la boîte correspondante de l’autre texte : il faut donc qu’il y ait le même nombre de boîtes des deux côtés. 
- Pour la poésie, chaque vers est une boîte
- en prose, les boîtes sont délimitées par `\pstart` et `\pend`.
