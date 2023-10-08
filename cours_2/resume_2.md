# Mettre en sens, mettre en forme

## Mettre en sens

### Le paratexte

|Commande|Effet|
|-- |-- |
|`\footnote{#1}`|Note de bas de page|
|`\marginpar{#1}`|Note marginale|

- L'apparence du numéro dans la note de bas de page peut être modifiée avec `polyglossia`. Mettre  à la commande `\setmainlanguage{french}`, dans l'argument optionnel, l'option `frenchfootnote=true`


### Listes

- Au sein des environnements de liste, chaque nouvelle entrée est appelée par la commande `\item`

|Environnement|Effet|
|-- |-- |
|`itemize`|liste simple|
|`enumerate`|liste numérotée|
|`description`|liste faisant correspondre deux valeurs ensemble. La première valeur est mis dans l'argument optionnel de `\item`|

- Si l'on met un argument optionnel à `\item`, on peut modifier ponctuellement le label (l'élément précédant l'entrée dans la liste: tiret, point,...)

- Pour modifier sur l'ensemble du document le label des environnements `itemize`:  mettre  à la commande `\setmainlanguage{french}` l'option `[frenchitemlabels=true]{french}` pour obtenir un cadratin; pour choisir le label, ajouter ensuite comme option `itemlabels= ` avec le label choisi. 
- Exemple: `\setmainlanguage[frenchitemlabels=true, itemlabels=\textendash]{french}` pour obtenir un demi-cadratin.

- Pour modifier le label d'un environnement `enumerate` donné, il faut utiliser le package `enumerate`. 
Exemple: `\begin{enumerate}[label=(\Roman*)]` pour numéroter la liste en chiffres romains entre parenthèses. 
Compteurs possibles: `\alph*` (lettres de l'alphabet), `\Alph*` (lettres en majuscules), `roman*` (chiffres romains en minuscule), `\Roman*` (chiffres romains en majuscule). 
-**nb**: La commande de compteur (`\alph*`, etc) ne doit pas directement être accolée au signe =

### Les citations

|Commande ou environnement|Effet|
|-- |-- |
|`\enquote{#1}` (requiert le package `csquotes`)|Guillemets|
|`quote`|Citation sur un paragraphe|
|`quotation`|Citation sur plusieurs paragraphes|
|`\textelp{}` (requiert le package `csquotes`)|Indiquer une citation tronquée. Si l'argument est vide: met simplement des points de suspension|
|`\textins{#1}` (requiert le package `csquotes`)|Indiquer une modification de la citation|
|`\url{#1}`|Créer un lien vers une URL|
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
|{\tiny }|
|{\scriptsize }|
|{\footnotesize }|
|{\small }|
|{\normalsize }|
|{\large }|
|{\Large }|
|{\LARGE }|
|{\huge }|
|{\Huge }|


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

**nb**: `\newpage` va mettre tout l'espace disponible restant en bas de la page; `\pagebreak` va répartir cet espace sur la page. Pour cette raison, `\newpage` vous sera plus utile.


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

### Syntaxe pour créer un environnement

-`\newenvironment{#1}[#2]{#3}{#4}`. `#1`= nom de l'environnement; `#2`=nombre d'arguments du nouvel environnement; `#3`= code appelé à l'ouverture de l'environnement; `#4` = code appelé à la fermeture de l'environnement




