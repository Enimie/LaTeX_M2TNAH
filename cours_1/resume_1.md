## La structure d'un document

- un préambule
- le corps du texte entre les balises `begin{document}` et `\end{document}`

```
\documentclass[12pt,a4paper]{article} %appel de classe
%appel des packages:
\usepackage{fontspec} %package pour gérer les fontes
\usepackage{xunicode} %package pour gérer l'unicode
\usepackage{polyglossia} %package pour gérer les langues
\setmainlanguage{french}

%d'autres packages peuvent être appelés ici
%des commandes et des environnements peuvent être (re)définis ici

\begin{document}
corps du texte
\end{document}
```

- Quelques classes possibles: `article book beamer memoir`
- Quelques options possibles de l'appel de classe:
	
|option|effet|
|---   |-----  |
|`10pt`| pour une police de base en 10 pt|
|`11pt`| pour une police de base en 11 pt|
|`12pt`| pour une police de base en 12 pt|
|`onecolumn`| pour un texte sur une seule colonne (par défaut pour les classes présentées)|
|`twocolumn`| pour un texte sur deux colonnes|
|`oneside`| pour une impression en recto seulement|
|`twoside`| pour une impression en recto-verso|
|`notitlepage`| pour ne pas avoir de page de titre spécifique (par défaut pour la classe `article`)|
|`titlepage`| pour avoir une page de titre spécifique (par défaut pour la classe `book`|

## Taper en LaTeX


- le nombre d'espaces ne change rien
- un retour à la ligne  &rarr; un espace
- un tile (`~`) &rarr; espace insécable
- deux retours à la ligne ou plus &rarr; nouveau paragraphe
- `--` &rarr; demi-cadratin, `---` &rarr; cadratin
- gestion des espaces automatique avant ponctuation
- tout ce qui suit le caractère `%` est ignoré (commentaire)
- attention, certains caractères sont utilisés par LaTeX: `\ ~ ^ { } % _ & $ #`. Pour insérer ces caractères dans un texte, il faut taper: `\textbackslash  \textasciitilde \textasciicircum \{ \} \% \_ \& \$ \#`


## Les packages

- *Package*:   code permettant de définir un ensemble de commandes orienté vers utilisation spécifique.  l'ensemble de ce code est contenu dans un fichier avec l'extension .sty
- Appeler un package: dans le préambule, `\usepackage{nom_du_package}`
- Obtenir la documentation: taper dans un terminal `texdoc nom_du_package`

## Les commandes

- *Commande*: bout de code qui va être interprété par le compilateur.
 - *Argument* paramètre passé à une commande et qui en modifie le comportement ou qui indique ce sur quoi elle  doit s'appliquer . 
- Syntaxe d'une commande:

1. backslash (`\` + nom de la commande)
2. entre crochets: arguments optionnels
3. entre accolades: arguments obligatoires



## Structurer un document


### Faire apparaître le titre du document

- dans le préambule: `\title{titre_du_document} \author{auteur_du_document} \date{date_du_document}` (pour qu'un de ces éléments n'apparaisse pas, laisser l'argument vide. Par défaut, si elle n'est pas indiquée, la date est celle du jour)
- dans le corps du document `maketitle`

### Commandes de section

|Commande| Sens| Numéro de niveau|
|-- |-- |-- |
|`\part{#1}`| Titre de partie| -1|
|`\chapter{#1}`| Titre de chapitre| 0|
|`\section{#1}`| Titre de section| 1|
|`\subsection{#1}`| Titre de sous-section| 2|
|`\subsubsection{#1}`| Titre de sous-sous-section| 3|
|`\paragraph{#1}`| Titre de paragraphe |4|
|`\subparagraph{#1} `| Titre de sous-paragraphe| 5|

- l'argument (`#1`) est le titre que l'on donne à la section.
- La commande `\chapter` n'existe que pour la classe `book`
- Le numéro des  niveaux de titre sert lors de l’affichage de la table des matières pour définir sa profondeur (voir dernier cours)
-  Les niveaux dont les numéros sont inférieurs à 1 provoquent un changement de page.
-  Les niveaux dont les numéros sont supérieurs à 3 ne provoquent pas de changement de paragraphe.


- Faire apparaître la table des matières: `\tableofcontents`
- Les commandes de section peuvent avoir un argument optionnel: c'est celui qui sera utilisé pour la table des matières
- Les commandes de section étoilées (par exemple `\section*{#1}`) ne sont pas numérotées et n'apparaissent pas dans la table des matières
- Pour les faire apparaître:  `\addcontentsline{toc}{#1}{#2}`. `#1` = le niveau de titre (section, chapter, etc); `#2` = le titre que l'on veut faire apparaître dans la table des matières





## Les environnements

- *environnement*:  portion de document qui a une signification spécifique et subit un traitement spécifique. L'environnement accepte le saut de paragraphe. On peut  utiliser des commandes au sein d'environnements.
- syntaxe d'un environnement:  `\begin{nom_de_l_environnement} \end{nom_de_l_environnemen}`. Tout ce qui se trouve entre ces deux balises est à l'intérieur de l'environnement
- exemple: l'environnement `abstract` de la classe `article`

