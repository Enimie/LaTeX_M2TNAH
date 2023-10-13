# Cours 3 - Approfondissements: Éléments non textuels; édition de texte


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

- **nb** Pour éviter que le flottant n'aille torp loin de l'endroit où on l'a appelé, utiliser la commande `\FloatBarrier` du package `placeins`:  tous les floants appelés avant la commande sont placés avant celle-ci.
- Le  package `wrapfig` permet de mettre du texte autour du flottant (voir le manuel)

5.5. -> 


### Insérer une image 

- Pour insérer une image, il faut utiliser la commande  `\includegraphics[⟨options⟩]{⟨chemin de l’image⟩}` du package `graphicx`. Pour régler la taille de l'image, indiquer dans l'argument optionnel `scale=xx` où xx est une valeur numérale (au dessus de 1: l'image est aggrandie; en-dessous de 1, elle est diminuée). Pour les autres options, voir le manuel.
- L'environnement `landscape` du package  `lscape` permet de mettre l'image (ou tout autre élément: tableau, texte) en format paysage.

### Insérer tableau

- Utiliser l'assistant de Texstudio, très efficace.
- Environnement `tabular`

- assez pénible en latex. Mais texstudio permet de le faire très facilement
1. faire un tableau 3x3 en fusionnant 1ere ligne colonnes 1/2
2. Explication fonctionnement d'un tableau
3. Pour choisir taille des col, arg à modifier. Nécessite le package array
- je ne dev pas, l'assistant marche bien. Je mets un lien vers un tuto.
bon tuto [ici](https://lataix-sebastien.developpez.com/tutoriels/latex/les-tableaux-sous-latex/) 

- **RQ** Pour faire tableau sur plusieurs page, ou qui peuvent prendre footnote: longtable 
**RQ**: faire des faux tableau (aligner du texte en colonne)/ Parfois correspond mieux à ce qu'on veut faire. Renvoi à l'explication [tabbing](https://latexref.xyz/fr/tabbing.html)



### exo3_1 C.  premiers graphiques avec tikz: 

- tikz: package graphisme. Assez compliqué de s'en servir. Livre TiKz pour l'impatient, ref ds la biblio
- on va voir: pour faire stemma/arbre généalogique. Ici j'ai déjà mis, enevez commentaire au fur et à mesure. Je reprend ex de Maieul rouquette
- car tikz a une syntaxe spécifique
- environnement `tikzpicture` . Peut avoir un argument pour passer option (épaisseur des traits par ex; cf tikz pour imptient et manuel)
- on place un noeud, `\node{1}`/ = un bloc de texte (peut être customizé aussi)
- associer un noeud à ce noeud: child
- nbre d'accolades et imbrication important
- Qd stemma plus compliqué: on peut avoir besoin de positionner sur une grille. Renvoi à article de Maieul sur son site: [stemma](https://geekographie.maieul.net/89)
- Outils pour simplifier: utiliser géogébra puis exporter en tex; utiliser application pour faire des arbres en latex. Je mets liens sur le readme

### pgfplots

On peut aussi faire courbes, histogrammes, etc. Un certains nbre de packages concus pour simplifier utilisation de tikz. Ici on va parler de `pgfplots` (plot=graphique)

 
- type de graphique: stemma codicum; histogrammes diagrammes en baton; courbes; camembert; etc.
- pour faire diagramme: on peut utiliser autre logiciel, faire image et importer avec includegraphics.
- Mais: ne marche pas toujours bien; image perd en qualités; pas toujours vectorisée; des détails disparaissent; la typo change...
	+ envirnnement tikzpicture, et dedan env `axis`. Compiler -> affiche coordonnées par défaut. Vont se modifier avec les coordonnés
	+ axis peut prendre option, comme la taille, scale, xscale, yscale etc, faire apparaître la grille; Cf manuel.On en verra qq unes
	+ ds axis, ajouter un ensemble de "points": `\addplot coordinates { };` 
	+ on retrouve syntaxe de tikz
	+ ds coordinnate: chaque points est indiqué entre parenthèse par : `abscisse-virgule-ordonnée`.
	+ **Attention** chiffre avec virgule: virgule remplacé par point (systeme anglo-saxon)

-  Exemple: temps de travail hommes/femme
	+ leur faire faire d'abord une, puis 2 lignes addplots
	+ faire ajouter xlabel, ylabel
	+ pb de format de la date: 
	- mettre en barre: option ybar; rq: pas même apparence si on met ca en option de axis ou en option de chaque addplot. `ybar stacked`: sont l une sur l'autre
	+ pb date: soit mettre en option `style={/pgf/number format/1000 sep=}`; soit :
	+ `\pgfplotsset` ds preambule pour faire reglages pour tous: `\pgfplotsset{/pgf/number 	format/1000 sep=}`. Vous pouvez enlever le commentaire ligne 15
	+ la seconde option: pour que les virgules ds les chiffres soient compris comme chiffre (à la française, pas à l'anglaise). Je vous conseille de garder ces réglages.
	+ transformer en barre: option ybar; à mettre ds axis ou ds chaque addplots: pas meme apparence
	+ ajouter légende `\legend{hommes,femmes}` au sein de exis: area legend

- **RQ** un autre package pour faire diagramme camembert, `pgf-pie`; très simple d'usage, dc je renvoie au manuel.

## Importer données pour obtenir tableaux et graphes
- Bcp plus intéressant: importer données.
- But: partir d'un fichier contenant données et les faire transformer automatiquement 
- package pgfplotstable

1. avec le même fichier travail_domestique
- importer des donnée: `\pgfplotstableread[col sep=comma]{travail_domestique_insee.csv}{\travail}`: on passe les données ds une variable qu'on créé: on lui donne le nom qu'on veut (pas nom d'une commande)
- comme fichier csv: col séparée par virgule: on le lui indique
- \pgfplotstabletypesetfile{\travail}: lit le contenu de travail et le transforme en tableau.
- pour le faire en diagramme: on reprend même environnement tikz avec axis
- à la place de coordinates, on met table[option]{\travail}. il faut indiquer à pgfplots quelles ligne choisir: en option, x=NOM de la colonne voulue; y=...].  **RQ**: si tableau avec seuleent 2 colonne, on met une seule ligne addplot...
- option `[xtick=data]` permet de n'avoir en x que les données qui apparaissent, pas toutes les dates

2. Avec le fichier classemnt_prenom. On commence par importer
-  on met axis, option ybar
-  \addplot table {\prenoms}; **pb**: les prénoms ne sont pas des nbre...
- Donc ds option de addplot table: on indique `x expr=\coordindex`
- **PB** 2: les prénoms n'apparaissent pas.  indiquer qu'en x, comme "label", on prend les donnée d'une certaine colonnes: `xticklabels from table={\prenoms}{Prénom}`; on met aussi ` xtick=data` pour que sélectionne chaque data comme xticks
- dernier pb: mettre les prénoms ds e bon sens: ajouter option `x tick label style={rotate=90}`
-pour ajouter légende: on peut mettre ds environnement table

- Customiser: la customisation se fait soit pour chaque tableau: en arg optionnel à `\pgfplotstabletypesetfile`, soit 
pour tous les tableaux: Enlever les commentaires lignes 16-18

3. Exemple d'importation de tableau plus long: un tableau avec catégories socio-professionnelle

- ouvrir tableau. Exporter en csv. RQ: choisir TAB car il y a des virgules: on ne veut pas que ces virgules soient prises pour un chgt de colonne. Ce sont les virgule des nbres décimaux
- nettoyer fichier obtenu: enlever ce qui n'est pas ds colonnes (titre, note, etc)
- `\pgfplotstabletypesetfile[string type]{\table}` string type: indique qu'il faut prendre tel quel ce qu'il y a ds les colonnes. Sinon se demande pourquoi il y a des virgules.
- Vous remarquerez que prend aussi les espaces sous employés...
- RQ: on peut transformer en longtable pour insérer notes, je vous invite à lire manuel de pgfplotstable si besoin. 
<!---  option begin table=\begin{longtable},
%		end table=\caption{tableau 2}\end{longtable}  -->




### On continue. Reledmac et reledpar pour édition

- présentation rapide d'un outil très puissant et complexe pour édition critique: reledmac pour edition critique, reledpar pour vis à vis (vont ensemble).

1. Principe: numéroter ligne. `	\beginnumbering	 \pstart \pend \endnumbering`. Choisir de ne pas numéroter un paragraphe
- on peut changer si on veut tous les combien les lignes sont numérotées. Renvoi au manuel. On peut faire numéroter chaque paragraphe: `\numberpstarttrue`
- Une syntaxe spéciale pour les vers. renvoi maneul

2. Apparat critique: familiar notes: celle appelées par un appel de notes; critical notes: sans appel de note, mais ds la note on a: le numéro de vers et un lemme (le morceau de texte qui a une variante); notes de fin
+ appellés respectivement `\footnoteA, \Afootnote, \Aendnote`; 5 série, de A à E, pour chaque note.
+ faire une note familiar A, une B. Pb: même appel de note.
+ ->  Enlever commentaire ligne 10. 4 façon de faire apparaître un compteur: alph, Alph, roman, Roman (cf résumé cours 2). Essayer de mettre roman à la place
+ faire note critique: pas très prtaique. Il faut commande `\edtext{#1}{#2}`. Arg 1: le mot qui va apparaître comme lemme; arg 2: la footnote critique avec son texte
+  Mettre mot phasellus en lemme.
+ Rq: typiquement le genre de situation où il vaut mieux se créer ses commandes... Je vais donner un exo maison sur ça. 

3. Faire du vis à vis. package Reledpar.
- environnements Leftside pour le texte de gauche, Rightside pour le texte de droite. Ces deux environnements sont eux-mêmes ds un environnement pages ou pairs. Pour que ca s'imprime, il faut à la fin de l'environnement pages ou columns mettre `\Pages` ou `\Columns`
- Le package ledpar fait correspondre en vis-à-vis chaque « boîte » d’un texte à la boîte correspondante de l’autre texte : il faut donc qu’il y ait le même nombre de boîtes des deux côtés. 
- Pour la poésie, chaque vers est une boîte
- en prose, les boîtes sont délimitées par \pstart et \pend. Il est recommandé, en prose, de mere chaque paragraphe dans une boîte pour obtenir une synchronisation la plus fine possible. Si on a encodé en XML un texte, on peut ensuite facielement obtenir ça.
- Exo: mettre ds les environnement voulus, faire apparaitre en vis à vis. **RQ**: il faut plusieurs compilation pour ca. créé des tas de fichiers auxiliaires: c ce qui permet de mettre bien vis à vis

- **RQ bis**: si vous utilisez ce package, vous allez vous faire: pour le texte, un fichier; pour la trad, un autre fichiers; et créer un fichier mettre avec la structure de ces environnements emboité ds lesquels vous appelerez vos fichers, selon la méthode qu'on verra au dernier cours
-si vous l'employez: lisez bien intro: comment économiser de la mémoire avec ce package notamment.
 
+ verbatim

+ Manipuler les compteurs

+ Bibleref

<mark>a mettre ds resume cours 2 créer ses commandes et environnements (2): arguments optionnels, présentation rapide de etoolbox</mark>



 - Des exo: je mettrai le corrigé; si vous ne comprenez pas, vous pourrez poser question
- En attendant mars: vous pouvez aller regarder ouvrage xelatex appliqués aux SHS
- Vous pouvez commencer à mettre des ref ds zotéro: je vous apprendrai à les utiliser
- pratiquez latex. pas pour notes de cours (markdown plus prtaique) mais par ex si vous prenez notes sur bouquins
- faites une liste au fur et à mesure de ch dont vous pourriez avoir besoin en latex, pour me poser questions
- ds le readme, je vais mettre liste d'erreurs de compilation

