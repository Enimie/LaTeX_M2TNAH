# Mettre en sens, mettre en forme

## Mettre en sens

### Le paratexte

|Commande|Effet|
|-- |-- |
|`\footnote{#1}`|Note de bas de page|
|`\marginpar{#1}`|Note marginale|

- L'apparence du numéro dans la note de bas de page peut être modifiée avec `polyglossia`. Mettre  à la commande `\setmainlanguage{french}`, dans l'argument optionnel, l'option `frenchfootnote=true`
- Ceci n'est pas nécessaire si on utilise le package `babel`

### Listes

- Au sein des environnements de liste, chaque nouvelle entrée est appelée par la commande `\item`

|Environnement|Effet|
|-- |-- |
|`itemize`|liste simple|
|`enumerate`|liste numérotée|
|`description`|liste faisant correspondre deux valeurs ensemble. La première valeur est mis dans l'argument optionnel de `\item`|

- Si l'on met un argument optionnel à `\item`, on peut modifier ponctuellement le label (l'élément précédant l'entrée dans la liste: tiret, point,...)

- Pour modifier sur l'ensemble du document le label des environnements `itemize`:  mettre  à la commande `\setmainlanguage{french}` l'option `[frenchitemlabels=true]{french}` pour obtenir un cadratin; pour choisir le label, ajouter ensuite comme option `itemlabels= ` avec le label choisi. 
- Exemple: `\setmainlanguage[frenchitemlabels=true, 
itemlabels=\textendash]{french}` pour obtenir un demi-cadratin.
- **nb** si l'on utilise le package `babel` plutôt que `polyglossia`, les items sont déjà des cadratins

- Pour modifier le label d'un environnement `enumerate` donné, il faut utiliser le package `enumerate`. 
Exemple: `\begin{enumerate}[(I)]` pour numéroter la liste en chiffres romains entre parenthèses; `\begin{enumerate}[exemple 1:]` pour faire précéder chaque item de `exemple` suivi du numéro et de deux points.
Compteurs possibles: `a` (lettres de l'alphabet), `A` (lettres en majuscules), `i` (chiffres romains en minuscule), `I` (chiffres romains en majuscule), `1` (chiffres arabes, par défaut). 

### Les citations

|Commande ou environnement|Effet|
|-- |-- |
|`\enquote{#1}` (requiert le package `csquotes`)|Guillemets|
|`quote`|Citation sur un paragraphe|
|`quotation`|Citation sur plusieurs paragraphes|
|`\textelp{}` (requiert le package `csquotes`)|Indiquer une citation tronquée. Si l'argument est vide: met simplement des points de suspension|
|`\textins{#1}` (requiert le package `csquotes`)|Indiquer une modification de la citation|
|`\url{#1}`|Créer un lien vers une URL. Utiliser le package `hyperref` pour avoir un lien cliquable (à charger EN DERNIER) pour éviter des problèmes de compatibilité avec d'autres package|
|`verse` (requiert le package `verse`|Pour citer des vers. Voir le manuel|


## Mettre en forme: quelques commandes et environnements

### Commandes portant sur le style de caractères


|Commande|Effet|
|--- |--- |
|`\textit{#1}`|Italique|
|`\emph{#1}`|Emphase (à préférer à `textit`)|
|`\textbf{#1}`|Gras|
|`\textsc{#1}`|Petites capitales|
|`\underline{#1}`|Souligné|
|`\textsuperscript{#1}`|Exposant|
|`\textsubscript{#1}`|Indice|
|`\textcolor{#1}{#2}` (nécessite le package `xcolor`) |Mettre en couleur|


**nb** 
- `#1` est le texte à mettre en forme, sauf pour `\textcolor` où: `#1`=nom de la couleur, `#2`=texte à mettre en couleur
- La commande `\emph` n'accepte pas les sauts de ligne. Pour mettre en emphase un texte plus long, utiliser l'environnement `em`

### Commandes "à bascule" pour changer  la taille des caractères

- Si l'on veut modifier sur une portion de texte donnée la taille des caractères, il faut utiliser une commande à bascule. Le comportement de ce type de commandes est différent: elles ne prennent pas d'argument, mais sont insérées entre accolades; le texte dont la taille change est entre les accolades, après la commande.
- Exemple: {\large un texte plus gros}
- La taille obtenue est relative: elle dépend de la taille définie lors de l’appel de classe.

 Liste des commandes à bascule, pour un résultat du plus petit au plus gros (`normalsize` correspond à la taille du corps du texte, `footnotesize` à la taille des notes de bas de page):

|Commande|
|-- |
|`{\tiny }`|
|`{\scriptsize }`|
|`{\footnotesize }`|
|`{\small }`|
|`{\normalsize }`|
|`{\large }`|
|`{\Large }`|
|`{\LARGE }`|
|`{\huge }`|
|`{\Huge }`|


### Environnements modifiant l'alignement du texte

|Environnement|Effet|
|-- |--|
|`flushleft`|Justifié à gauche|
|`flushright`|Justifié à droite|
|`center`|Centré|



### Commandes modifiant ponctuellement la mise en page

|Commande|Effet|
|--|--|
|`\newline` ou `\\`|Saut de ligne; la ligne suivante n'est pas indentée|
|`\newpage` ou `\pagebreak`|Commencer une nouvelle page|
|`\noindent`|Pas d'indentation au début du paragraphe|
|`\par`|Nouveau paragraphe (à utiliser dans la définition de commandes ou d'environnements)|

**nb**: 

- `\newpage` va mettre tout l'espace disponible restant en bas de la page; `\pagebreak` va répartir cet espace sur la page. Pour cette raison, `\newpage` vous sera plus utile.
- `\newline` ou `\\`, de même que `\par`, sont à réserver pour la définition de commandes ou d'environnement, et ne doivent qu'exceptionnellement être utilisé dans le corps du texte. Ces commandes **ne doivent pas être utilisées**  pour créer des paragraphes au cours de la phrase (il suffit de laisser une ligne blanche!) , car elles peuvent provoquer des problèmes de répartition di blanc dans la page. 

### Encadrer du texte en le mettant dans des boites

|Commande/environnement|Effet|
|-- |--|
|`\fcolorbox{#1}{#2}{#3}` (requiert le package `xcolor`)|Mettre du texte (`#3`) dans une boite de la couleur choisie (`#1` pour le cadre, `#2` pour le fond)|
|`\fbox{#1}` (ou `\framebox{#1}`|Texte court encadré (sans changement de ligne/de paragraphe)|
|`framed`(requiert le packae `framed`)|Encadre des textes qui peuvent courir sur plusieurs lignes/paragraphes|

Il existe aussi le package `fancybox` pour créer des boites encadrées

Sur la notion de boites dans LaTeX, voir LOZANO, Vincent, [Tout ce que vous avez toujours voulu savoir sur LaTeX sans jamais oser le demander](https://archives.framabook.org/docs/latex/framabook5_latex_v1_art-libre.pdf), p. 73 *sq*.

## Créer ses commandes et environnements (1)

### Syntaxe pour créer une commande

-  `\newcommand{#1}[#2]{#3}`. `#1`= nom de la commande; `#2`=nombre d'arguments de la nouvelle commande; `#3`= code de la nouvelle commande
- Les commandes doivent être créées dans le préambule.

- Syntaxe pour créer une commande avec argument optionel, grâce au package `xargs`:

- `\newcommandx{#1}[#2][#3]{#4}` `#1`=nom de la commande; `#2`= nombre d'arguments; `#3`=liste des arguments optionnels (liste de numéros indiquant la position des arguments optionnels dans la commande). Une  valeur par défaut peut être attribuée aux arguments optionnels, consulter le manuel de `xarg`; `#4`= le code

- Tester si un argument est vide grâce au packet `etoolbox`: utiliser la commande `\ifstrempty{#1}{#2}{#3}`. `#1`=la chaine de caractères que l'on va tester (ça peut être un argument de notre ouvelle commande, par exemple `#1`); `#2`=ce qui se passe si la chaine est vide; `#3`=ce qui se passe sinon.

### Syntaxe pour créer un environnement

-`\newenvironment{#1}[#2]{#3}{#4}`. `#1`= nom de l'environnement; `#2`=nombre d'arguments du nouvel environnement; `#3`= code appelé à l'ouverture de l'environnement; `#4` = code appelé à la fermeture de l'environnement

- Pour créer un environnement avec arguments optionnels, utilisez le package `xargs`


- **nb** Il n'est pas possible d'appeler l'argument du nouvel environnement dans la *dernière partie* de la commande `newenvironment` (celle qui indique le code qui sera appelé à la fermeture de l'environnement). Il faut:
-  créer une "boite de sauvegarde" en mettant, avant la définition du nouvel environnement, `\newsavebox{\boite}` (on peut bien sûr donner un autre nom à la boite). 
- Dans le code appelé à l'ouverture du nouvel environnement, mettre l'argument dans cette boite, par exemple: `\savebox{\boite}{#1}`
- Dans le code appelé à la fermeture de l'environnement, on peut utiliser cette boite (et donc le contenu de l'argument) en utilisant: `\usebox{\boite}`.
- Pour des exemples d'utilisation, voir l'ouvrage de LOZANO, Vincent, cité plus haut et mis dans la biliographie.
