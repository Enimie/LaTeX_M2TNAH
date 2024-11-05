
# Gérer sa bibliographie: biblatex, biber et Zotero

## Principes

1.  un fichier au format `.bib` contient toutes les références bibliographiques ("entrées") (= fichier BibTex)
- à chaque entrée est associée une clef ("key") qui l'identifie 
- chaque entrée comporte un certain nombre d'éléments de description bibliographique (nature de la référence, titre, auteur, date, etc), chacun indiqué dans le champ correspondant.
- exemple d'entrée: 

```
@Book{maieul_rouquette_2012, 
  author = {Maïeul Rouquette and Enimie Rouquette and Brendan Chabannes},
  title = {(Xe)\LaTeX{}  appliqué aux sciences humaines},
  publisher = {Atramenta},
  date = {2012},
  address = {Tampere},
  url = {https://halshs.archives-ouvertes.fr/halshs-00924546}
}
```

Dans cet exemple, la référence est un livre (`@book`), sa clef est `maieul_rouquette_2012`, et les éléments indiqués sont les auteurs, le titre, l'éditeur, la date, le lieu de publication, et l'url pour la publication en ligne.

2. Dans le préambule, on charge le package `biblatex` et on indique le chemin du fichier `.bib` avec la commande `\addbibresource{#1}`. C'est `biblatex` qui affiche les citations selon un style choisi, en utilisant le moteur `biber`.

Exemple de préambule appelant `biblatex` et un fichier bibliographique:

```
\documentclass[a4paper]{book}
\usepackage{fontspec}
\usepackage{xunicode}
\usepackage{polyglossia}
\setmainlanguage{french}
\usepackage{biblatex}
\addbibresource{/home/user/Documents/memoire/bibliographie.bib}
```

**nb** il est possible d'appeler plusieurs fichiers bibliographiques.

3. Exemple de commandes `biblatex`:
- pour faire une citation dans le corps du texte et en note de bas de page: `\cite[#1][#2]{#3}` et `\footcite[#1][#2]{#3}`, où `#1`= une prénote (texte avant la référence), `#2`=postnote (numéro de page, texte après la référence), `#3̀`=la clef de la référence bibliographique
	- S'il n'y a qu'un seul argument optionnel, il est considéré comme l'argument `postnote`. Si l'on veut l'argument `prenote` sans `postnote`, il faut mettre l'argument `#2` vide
	- Si `#2` ne contient que le numéro de la page, le préfixe (p., pp., col.,) s'affiche automatiquement. (par défaut, on pagine en pages. Si l'on veut paginer en colonnes, il faut ajouter dans l'entrée bibliographique le champ `pagination` avec pour valeur `column` ; voir le manuel pour d'autres valeurs possibles)
	- Si la postnote contient aussi du texte, il faut faire précéder le numéro de pagination de la commande `\pno~`. 

Exemples: 

	 `\footcite[Sur ce sujet, voir][99]{maieul_rouquette_2012}`
 	 `\footcite[Sur ce sujet, voir][]{maieul_rouquette_2012}`
	 `\footcite[\pno~99 et suivantes]{maieul_rouquette_2012}`

- pour ne citer respectivement que l'auteur et le titre d'une référence: `\citeauthor{clef}`et `\citetitle{clef}`

- pour imprimer la bibliographie: `\printbibliography`

4. Trois compilations sont nécessaires: 
- compilation avec `XeLaTeX`
- compilation avec `Biber`
- nouvelle compilation avec `XeLaTeX`

- Configurer TexStudio pour compiler avec biber: `options - configurer texstudio - production - moteur de bibliographie par défaut - biber`. Il faut parfois indiquer le chemin de `biber` dans l'onglet `compilation` des configurations: on le connait en tapant `which biber` dans le terminal (pour linux)
- Pour compiler soi-même: dans un terminal, se placer là où est le fichier à compiler, et taper `xelatex nom_du_fichier`, puis `biber nom_du_fichier`.

 **nb**: 
- la première compilation produit un fichier auxiliaire `.bbl`, c'est lui que l'on compile avec Biber (mais ce n'est pas la peine de mettre l'extension si l'on compile dans le terminal)
- Si l'on compile manuellement dans le terminal, il est possible d'utiliser la commande `latexmkr`  qui fait automatiquement les compilations nécessaires. Voir sur ce sujet le blog [geekographie maïeulesque](https://geekographie.maieul.net/206)


## La base de données bibliographiques

### Types d'entrées

Quelques types d'entrées possibles; pour plus d'entrées, voir le manuel de `biblatex` p.8sq, ainsi que 
ROUQUETTE, Maïeul, [XeLaTeX appliqué aux sciences humaines](https://halshs.archives-ouvertes.fr/halshs-00924546), p.81-82 sq

|Nom|type d'entrée|
|-- |-- |
|@article| Article de revue|
|@book| Livre|
|@bookinbook|Livre dans un livre, par exemple différents écrits d'un auteur rassemblés en un seul volume|
|@collection| Ouvrage collectif mais avec des parties distinctes par auteur|
|@inbook| Partie d’un livre|
|@incollection| Partie individuelle (avec un auteur propre) dans un ouvrage collectif|
|@inproceedings| Contribution à un colloque|
|@inreference| Article de dictionnaire, d’encyclopédie, etc|
|@misc| Entrée générique, pour tout type d’entrée non catégorisable|
|@online| Ressource internet (sans équivalent physique)|
|@periodical| Numéro précis d’un périodique|
|@proceedings| Acte de colloque|
|@suppbook| Partie annexe d’un livre, comme par exemple la préface ou les appendices||
|@reference| Dictionnaire, encyclopédie, etc|
|@thesis| Thèse de doctorat, mémoire de maîtrise ou tout travail rédigen vue de l’obtention d’un titre scolaire ou universitaire.
|@unpublished| Ouvrage non publié|


### Quelques champs

Pour plus de champs, voir le manuel de `biblatex` p.17sq, ainsi que 
ROUQUETTE, Maïeul, [XeLaTeX appliqué aux sciences humaines](https://halshs.archives-ouvertes.fr/halshs-00924546), p.83 sq

*Champs de personnes*

- Les valeurs des champs de personnes sont de type "Prénom Nom" ou "Nom, Prénom". Pour considérer un ensemble de mot comme le "nom" (par exemple pour les auteurs antiques), le mettre entre accolades.
- Lorsqu'il y a plusieurs personnes dans un même champ, elles sont séparés par `and`

exemples: 
- `author = {Maïeul Rouquette and Enimie Rouquette and Brendan Chabannes}`

ou: `author = {Rouquette, Maïeul and Rouquette, Enimie and Chabannes, Brendan}`
-  `author  = {{Eugène de Tolède}}`


|Champ|Explication|
|-- |-- |
|annotator| Auteur(s) des annotations|
|author| Auteur(s) de l’œuvre|
|commentator| Auteur(s) des commentaires|
|editor| Éditeur(s) scientifique(s). On peut en préciser le rôle grâce au champ `editortype`|
|foreword| Auteur(s) de la préface|
|introduction| Auteur(s) de l’introduction|
|translator| Traducteur(s)|

Lorsque des champs possèdent des valeurs égales, biblatex fusionne ces champs lors de l’affichage. Par exemple, si `translator` et `editor` sont identiques, on obtient "édité et traduit par..."

*Champs de titre*

|Champ|Explication|
|-- |-- |
|booktitle| Titre du livre dans lequel l’entrée se situe|
|chapter| Chapitre d’un livre. Pour les entrées de type @inbook|
|issuetitle| Titre d’un numéro spécifique d’un périodique|
|journaltitle| Titre d’un périodique|
|maintitle| Titre d’une œuvre en plusieurs volumes|
|maintitleaddon| Ajout au titre d’une œuvre en plusieurs volumes|
|subtitle| Sous-titre de l’œuvre|
|title| Titre de l’œuvre|
|titleaddon| Ajout au titre de l’œuvre|


*Champs d'information sur la publication*

Pour plus de champs, voir le manuel et 
ROUQUETTE, Maïeul, [XeLaTeX appliqué aux sciences humaines](https://halshs.archives-ouvertes.fr/halshs-00924546), p.88 sq

|Champ|Explication|
|-- |-- |
|address| Lieu de publication.|
|date| Date de publication|
|edition| Numéro d’édition si plusieurs éditions existent|
|institution| Institution dans laquelle l’œuvre a été produite, pour les entrées de type @thesis|
|issue| Détail d’un numéro spécifique d’un périodique |
|number| Numéro d’un périodique ou numéro au sein d’une collection|
|origdate| Date de l’édition originale|
|origlanguage| Langue originelle|
|pagination|Le type de pagination (par défaut: `page`|
|pages| Pages de l’article ou de la partie du livre étudiée|
|publisher| Éditeur commercial|
|type| Pour les entrées de type @thesis, précise le type de travail|
|url| Url (adresse électronique) d’une publication en ligne|
|urldate| Date à laquelle une publication électronique a été consultée|
|volume| Volume dans une œuvre en plusieurs volumes|
|volumes| Nombre de volumes dans une œuvres en plusieurs volumes|



## Les styles bibliographiques

- Il est possible de charger différents styles pour les citations et pour la bibliographie, dans l'argument optionnel de l'appel du package:
	+ L'option `style=nom_du_style` charge à la fois le style de citation et le style bibliographique
	+ Les options `bibstyle=nom_du_style` et `citestyle=nom_du_style` chargent respectivement le style bibliographique et le style de citation

Exemples de style:

|Style|Description|
|-- |-- |
|numeric| chaque entrée se voit attribuer un numéro, qui est appellé lorsque l'on renvoie à cee entrée.|
|authortitle| sont indiqués seulement l'auteur et le titre de l’œuvre|
|verbose| la description complète de l’entrée est donnée la première fois, une version abrégée est affichée ensuite.|
|verbose-ibid| Comme verbose, mais avec l’abréviation *ibidem*|
|verbose-trad1, verbose-trad2, verbose-trad3|Comme verbose-ibid, mais avec également les abréviations *op. cit.*, *ibidem*, etc.|

Pour plus de précisions, voir le manuel p.74 sq

- Il existe un style de citations qui suit les normes de l'École des Chartes:
	+  [biblatex-enc](https://ctan.org/pkg/biblatex-enc)
	+ on peut l'installer dans son dossier `texmf local` (par exemple `/usr/local/texlive/texmf-local/tex/latex/biblatex-enc`) (voir le readme du style).
	+ **nb**: pour en apprendre plus sur l'arborescence d'une distribution TeX et ce que signifie `texmf local`, voir: [Guide pratique de Tex Live 2023](https://www.tug.org/texlive/doc/texlive-fr/texlive-fr.pdf) p.7, ou Daniel Flipo, [Admninistration d'une installation TeX](http://daniel.flipo.free.fr/doc/tex-admin/TeX-admin.pdf)
	+ On le passe ensuite en option à `biblatex`: `\usepackage[style=enc]{biblatex}`

**Attnetion** La dernière version de polyglossia provoque des erreurs de compilation avec ce style. Deux possibilités:
- télécharger et utiliser localement la version antérieure de polyglossia en attendant que ce problème soit résolu
- utiliser le package `babel` à la place de `polyglossia` (voir dans la définition du préambule)

----

**RQ**
- Pour que les œuvres anonymes soient classées en début de bibliographie, par titre, il faut utiliser le package `biblatex-anonymous`, et ajouter l'option `sorting` à l'appel du package  `biblatex`: 

```
\usepackage[style=enc,sorting=anonymous]{biblatex}
\usepackage{biblatex-anonymous}
```

- l'appel du package `biblatex-anonymous` doit se faire après l'appel du package `biblatex`

**Attention** biblatex-anonymous ne fonctionne pas avec babel mais simplement avec polyglossia.


## Imprimer sa bibliographie

- commande `\printbibliography`
- l'option `\nocite{#1}` permet d'imprimer dans la bibliographie des entrées non citées dans le corps du texte. L'argument peut-être soit un astérisque, pour indiquer que toutes les entrées du fichier .bib doivent être imprimées, soit une liste de clefs séparées par des virgules: `\nocite{*}`, `\nocite{clef1, clef2, clef3,...}`
- Il est possible de n'imprimer que des entrées ayant, ou n'ayant pas, un mot-clef:  options `keyword=xx` et `notkeyword=xx`; on peut de cette façon imprimer plusieurs sous-parties de bibliographie.

 Exemple: 

```
\printbibliography[keyword=sources-primaires]
\printbibliography[notkeyword=sources-primaires]
```

 D'autres choix sont possible (imprimer des bibliographies intermédiaires par exemple). Voir le manuel p. 90 et p. 140
- Pour modifier le titre de la ou des bibliographies: 
	+ dans le préambule, `\defbibheading{#1}{#2}`, où `#1`=une clef attribuée au titre et `#2` le titre
	+ dans l'argument optionnel de la commande `\printbibliography`, `heading=clef`

Exemple: 

```
\documentclass[a4paper]{book}
\usepackage{fontspec}
\usepackage{xunicode}
\usepackage{polyglossia}
\setmainlanguage{french}
\usepackage{biblatex}
\addbibresource{/home/user/Documents/memoire/bibliographie.bib}


\defbibheading{primaires}{\subsection*{Sources primaires}}
\defbibheading{secondaires}{\subsection*{Sources secondaires}}


\begin{document}
...
\section*{Bibliographie}
\printbibliography[heading=primaires, keyword=sources-primaires]
\printbibliography[heading=secondaires, notkeyword=sources-primaires]
\end{document}
```





## Zotero et LaTeX

###  Importer une bibliographie BibTex vers Zotero: 

- `Fichier-Importer` : 
	+  les clefs de citation restent telles quelles.
	+ les *keywords* sont importées dans "marqueurs"
- Remarques:
	+ certains champs bibtex  n'existent pas dans zotero. Ex: *maintitle*, *volumes*, *gender*, *venue*. Ils sont importés dans *extra* sous la forme: `tex.maintitle: XXX`. 
	+ Le formatage au sein d'un champ (des italiques par exemple) est possible au moyen de balises html. AInsi `\emph{xx}`devient `<i>xx</i>`. Pour les autres possibilités de formatage, voir la [Documentation Zotero](https://www.zotero.org/support/kb/rich_text_bibliography).

-> on peut exploiter ces possibilités pour donner plus de souplesse à Zotero

### Le module BetterBibTex

- Le module [BetterBibTex](https://retorque.re/zotero-better-bibtex/)  permet de répercuter dans un fichier BibTex les modifications apportées dans une collection (ou un ensemble de collections) gérée avec Zotero
- l’inverse n’est pas vrai : les modifications apportées dans le fichier BibTeX ne sont pas “remontées” dans Zotero.

Installation: 

1. télécharger le XPI file et le sauvegarder. **attention: sous firefox, faire clic droit et enregistrer la cible du lien** (un simple clic sur le lien ne marchera pas)
2. Dans zotero: `extension - ajouter depuis un fichier - installer - redémarrer zotero`
4. Configurer Betterbibtex pour l'exportation: `outils - betterbibtex -  ouvrir les preference de betterbitex`: 
-  onglet `exportation`: 
	-  decocher "exporter les caractères unicodes"
	-  choisir "ajouter les url à l'exportation dans le champs url"
	- onglet divers: décocher "appliquer la capitalisation aux titres"
- onglet `clef de citation`: possibilité de choisir la façon dont les clefs seront générées
3. Mettre en place la synchronisation  entre un fichier BibTex et une collection dans Zotero: faire un clic-droit sur la collection à exporter: `exporter - choisir betterbibtex` - cocher "garder à jour"

**RQ** Quand vous "aspirez" une référence bibliographique dans Zotero, pensez à vérifier que les informations sont bien entrées; vous pouvez utiliser le champs "extra" pour rajouter des champs propres à bibtex (voir supra)



