# Naviguer dans un long document

## Les renvois internes

- Package `hyperref` (rappel: à charger après tous les packages, sauf exception, comme par exemple le package `glossaries`)
- Poser un label: `\label{nom_du_label}`
- Renvoyer au label au cours du texte (dans le corps du texte ou au sein d'un flottan):
	+ `\pageref{nom_du_label}`: renvoie à la page où se trouve le label
	+ `\ref{nom_du_label}`: renvoie au numéro de section/de flottant où se trouve le label
	+ `\nameref{nom_du_label}`: renvoie au titre de la section où se trouve le label

- **Attention**: dans un flottant, le label doit être placé *après* `\caption`
- Rq: le package `hyperef` crée également automatiquement des signets dans le pdf, qui suivent la table des matières.

## Les index

### Création d'un index simple

- Dans le préambule: 
```
\usepackage{imakeidx}
 \makeindex
```

- Indexer un mot dans le corps du texte: `\index{mot}`
- **Attention**: l'argument de la commande `\index{}` n'apparait *pas* dans le texte. Il faut donc taper, par exemple,  "Auguste\index{Auguste}"
- Imprimer l'index: `\printindex`. (il faut trois compilations)


- Les mots commençant par des caractères accentués sont mis en fin d'index. Pour résoudre les problèmes de tri avec les accents, indexer de cette façon: `\index{mot utilisé pour le tri dans l'index @ mot qui apparaîtra dans l'index}`
- Exemple: `\index{Elisabeth@Élisabeth}` permettra de faire apparaître "Élisabeth" dans l'index à la lettre E
- Il est possible de faire des subdivisions d'entrées: `\index{Empereur!Auguste}`, `\index{Empereur!Caligula}`
- Faire des références croisées (qui appraîtront dans l'index sous la forme: "xx, *voir* yy'): `Bonaparte\index{Bonaparte|see{Napoléon}}\index{Napoléon}`.
- Faire apparaître l'index dans la table des matières: mettre l'option `intoc` à la commande  `\makeindex`: `\makeindex[intoc]`

- **rq**: la création d'index génère des fichiers auxiliares `.idx`, `.ilg` et `.ind`

### Créer plusieurs index

- Pour chaque index que l'on veut créer, mettre en préambule une commande `\makeindex`, avec dans l'argument optionnel `title="nom de l'index` et `name="clef de l'index"`
- Exemple: 

```
\usepackage{imakeidx}
\makeindex[intoc, title=Index général]
\makeindex[intoc, name=aut, title=Index des auteurs]
```
- Pour indexer une entrée dans un index en particulier, il faut mettre en argument optionnel à l'entrée `\index` la clef correspondante. Exemple: `\index{Entrée}` sera indexé dans l'index général, tandis que `\index[aut]{entrée}`sera indexé dans l'index des auteurs.

- pour imprimer un index précis, ajouter en argument optionnel à  `\printindex` la clef correspondante. Exemple: `\printindex[aut]`


- Pour indexer des auteurs cités avec biblatex, voir [XeLaTeX appliqué aux sciences humaines](https://halshs.archives-ouvertes.fr/halshs-00924546) p.149 




## Les glossaires

```
\usepackage[toc=true]{glossaries}%doit être appelé après hyperref (exception à la règle)
\makeglossaries
```
- Définir les entrées de glossaire dans le préambule ou dans un fichier à part, avec la commande `\newglossaryentry{#1}{#2}` où `#1` = la clef de l'entrée, et  `#2` contient le mot et sa définition.  Exemples:

```
\newglossaryentry{ex}{%
	name={exemple},%
	description={Illustration% 
		d'un concept}}

\newglossaryentry{co}{%
	name={concept},%
	description={Idée générale, représentation mentale et abstraite que l’on a d’un objet}}
```
- on appele dans le corps du texte les  mots définis dans le glossaire au moyen de la commande `\gls{entree_du_glossaire}`. Exemple: `\gls{ex}`
-  pour compiler le glossaire, si l'on a en plus un index,  il faut lancer de le terminal la commande `makeglossaries nomdufichier`. Texstudio le fait avec la commande: `outil-glossaire` (F9)
- Pour imprimer le glossaire: `\printglossary`. On peut modifier le titre en argument optionnel: `\printglossary[title=le nouveau titre]`
- Pour faire apparaître le glossaire dans la table des matière, on passe une option à l'appel de package `\usepackage[toc=true]{glossaries}`
- on peut créer un glossaire dans un fichier à part et l'appeler dans le preambule par `\loadglsentries{fichier.tex}`




## Modifier les césures automatiques

- Il est possible d'indiquer des règles d'hyphénation (de césure) pour des mots précis, par langue:

```
\begin{hyphenrules}{french}
	\hyphenation{}
\end{hyphenrules}
```

- Dans la commande `\hyphenation{#1}`, l'argument comprend une liste de mots séparés par un espace. Chaque mot comporte un ou plusieurs tirets indiquant les endroits possibles pour une césure. S'il n'y a pas de tiret, le mot est insécable. 
- Exemple: `\hyphenation{Orléans inter-li-né-aire}`

## Créer un compteur

- Créer un nouveau compteur: `\newcounter{#1}` où `#1`= le nom du compteur. Exemple `\newcounter{ex}`. Par défaut, ce compteur est mis à zéro
- Mettre une autre valeur au compteur: `\setcounter{#1}{#2}` où `#1`= le nom du compteur et `#2`=une valeur. Ex: 
 `\setcounter{ex}{5}`: le compteur "ex" est mis sur 5
- incrémenter le compteur:`\addtocounter{#1}{#2}` où `#1`= le nom du compteur et `#2`=une valeur.
Exemple;  `\addtocounter{ex}{1}`: on ajoute 1 au compteur "ex".
- Afficher la valeur actuelle du compteur: `\theNom_du_compteur`. Exemple; `\theex`
affichera la valeur du compteur `ex`
- autres façon d'afficher la valeur du compteur: 
   + `\roman{ex}` affichera la valeur du compteur "ex" en  nombre romains minuscules  
   + `\Roman{ex}` affichera la valeur du compteur "ex" en nombre romains majuscules 
   + `\alph{ex}` affichera la valeur du compteur "ex" en lettres minuscules   
   + `\Alph{ex}` affichera la valeur du compteur "ex" en lettres majuscules 

- Exemple d'utilisation de compteur dans un nouvel environnement:
```
\newcounter{ex}%création du compteur "ex"
\newenvironment{exemple}%
{\addtocounter{ex}{1}\textbf{Exemple \theex}}%à l'ouverture de l'environnement, on ajoute 1 au compteur "ex", et on fait apparaître en gras le numéro de l'exemple avec \theex
{}%il ne se passe rien à la fermeture de l'environnement
```
ce qui donnera l'utilisation suivante, où les exemples seront numérotés:
```
\begin{exemple}
Un premier exemple
\end{exemple}

\begin{exemple}
Un second exemple
\end{exemple}
```

# Utiliser un document maître

- Créer un document (ou utiliser celui fourni) contenant le préambule, les balises `\begin{document}` et `\end{document}`, et au sein de ces balises les grandes divisions (`\frontmatter` et `\appendix` si besoin, `\mainmatter`pour le corps du texte et `\backmatter` pour la bibliographie, le(s) index et table(s) des figures ou des tableaux,  la table des matières
- Créer un document `.tex` par structure logique (chapitre ou section, selon la taille du travail).
	+ ces documents "enfants" ne **doivent pas** avoir de préambule, puisque le préambule est contenu dans le document maître
	+ appeler dans le document "maître" ces documents "enfants" avec la commande `\input{}` en indiquant le chemin relatif (par exemple: `\input{./frontmatter/section1.tex}` où le point indique l'emplacement du document maître et chaque `/` le passage à un autre dossier-enfant)
- Compiler le document maître. **nb** Avec TexStudio, il est possible de déclarer un document comme document maître: Option - Document maître - déclarer le document en cours comme document maître explicite. Cela permet ensuite de compiler directement depuis les fichiers enfants (du moment qu'ils sont bien appelés dans le document maître)
- Autre possibilité: garder l'option "détecter automatiquement le document maître". On pourra compiler depuis n'importe quel fichier appelé dans le document maître, du moment que celui-ci a aussi été ouvert une première fois
