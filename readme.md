![LaTeX](LaTeX_logo.svg.png)

# LaTeX et la rédaction de mémoire (ENC 2556)

Vous trouverez sur ce dépôt le contenu pédagogique du cours *LaTeX et la rédaction de mémoire*  du M2 Technologies Numériques Appliquées à l'Histoire à l'École des chartes.

## Planning

| Date | Horaires | Programme |
| ---- | -------- | --------- |
| 4 octobre 2023  | 13h-15h | Notions de base| |-----------------|---------|----------------|
| 11 octobre 2023 | 13h-15h | Mettre en forme, mettre en sens |
| 18 octobre 2023 | 13h-15h | Approfondissements    |
| 4 mars 2024     | 9h-11h  | LaTeX pour le mémoire |

## Installation de LaTeX

### 1/ Pré-requis

Avoir le package `perltk` installé. Si ce n'est pas le cas:
- Ouvrez un terminal
- Tapez la commande suivante: `sudo apt install perl-tk` et validez par la touche "Retour"
- Tapez votre mot de passe (il reste invisible, c'est normal), et validez par la touche "Retour"


### 2/ Télécharger le programme d'installation

Deux possibilités: 

1. Téléchargez le fichier *via* le lien suivant: [install-tl-unx.tar.gz](https://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz)
2. Dans le terminal, placez-vous dans le dossier Téléchargement par la commande `cd ~/Téléchargements` puis tapez `wget https://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz`

Une fois le fichier téléchargé, décompressez-le. Pour cela, double-cliquez dessus ou tapez dans le terminal la commande `tar -xf install-tl-unx.tar.gz`


### 3/ Installer la texlive

1. Placez-vous dans le dossier que vous avez décompressé par la commande `cd` suivie du nom du dossier (`install-tl-20230926`; le nombre peut être différent). Vous pouvez utiliser la touche Tab pour activer l'autocomplétion du nom du dossier.
2. Tapez `sudo perl install-tl`
3. Si vous avez de la place sur votre ordinateur et une bonne connexion internet: répondez `i` ("start installation to hard disk"). **Cette option est à privilégier**
4. Si votre connexion est mauvaise, ou que vous avez trop peu de place, vous pouvez au choix:
	- tapez`c` pour sélectionner quelques collections de packages à décocher. Vous pouvez enlever sans problème les collections désignées par les lettres suivantes: `iklmnowxyzABCPS`. Attention, certaines collections seront utiles si vous comptez utiliser les langues concernées (par exemple arabe ou persan dans la collection `arabit`. Dans ce cas, ne les indiquez pas).
	- Si même ainsi cela prend trop de place/de temps, tapez `j` pour sélectionner un schéma et choisissez "teTex"   

	-> Tapez ensuite `r` pour retourner au menu principal, et `i` pour lancer l'installation.  
Il sera de toute façon possible d'installer plus tard ces collections si vous en avez besoin. 

### 4/ Configurer

Il ne reste plus qu'à configurer votre installation:

1. Tapez`sudo mousepad ~/.profile`
2. Dans le fichier qui s'ouvre, ajoutez les lignes suivantes: 

```
PATH=/usr/local/texlive/2023/bin/x86_64-linux:$PATH; export PATH
MANPATH=/usr/local/texlive/2023/texmf/doc/man:$MANPATH; export MANPATH
INFOPATH=/usr/local/texlive/2023/texmf/doc/info:$INFOPATH; export INFOPATH
```

3. Enregistrez le fichier, et tapez dans le terminal `source ~/.profile` pour que le changement soit pris en compte.
4. Vérifiez que tout fonctionne en tapant `which xelatex` dans le terminal: vous devez avoir le chemin de la texlive 2023 qui s'affiche.


### 5/ Installer un éditeur de texte (TexStudio)

Tapez dans un terminal la commande suivante: `sudo apt install texstudio` puis entrez votre mot de passe.

## Évaluation

Les consignes seront données ultérieurement
Date de rendu: **XXX**


## Quelques *packages* 

Vous pouvez chercher des packages adaptés à vos besoins sur le site du [CTAN](https://www.ctan.org/) (The Comprehensive TeX Archive Network). Je vous propose ici une liste (non-exhaustive)  de quelques packages qui pourraient vous servir.

|Package|Usage|
|-- |-- |
|`biblatex`|Bibliographie|
|`biblatex-manuscripts-philology`|Décrire dans une base bibliographique des manuscripts|
|`biblatex-multiple-dm`|Pouvoir utiliser plusieurs modèles de données avec `biblatex`|
|`bibleref-french`|Références bibliques (français)|
|`csquotes`|Gérer les guillemets|
|`endnote`|Créer des notes de fin|
|`enumitem`|Modifier l'apparence des listes|
|`etoolbox`|Commandes LaTeX remplaçant des commandes TeX (difficulté +++ ; pour ceux qui aiment programmer!). Comporte des commandes pour des instructions de type if... then.. else|
|`fancyhdr`[Personnaliser la mise en page|Améliorer l'environnement `tabular`: indiquer par exemple la taille des colonnes`|
|`framed`|Encadrer, surligner,... du texte|
|`geometry`|Modifier la géométrie de la page (marges)|
|`graphicx`|Insérer des images, manipuler des boites (rotation,...)|
|`hyperref`|Hyperliens. (Appel du package à mettre à la fin; amélioré si utilisé avec `bookmark`)|
|`ifthen`|Commandes pour écrire une instruction if then else. Moins pratique que les commandes du package `etoolbox`, mais plus simple à comprendre|
|`indextools`|Faire un ou plusieurs index (fork de `imakeidx`)|
|`lettrines`|Insérer des lettrines|
|`lscape`|Pour inclure des pages en format paysage|
|`pdflscape`|Inclure des pdf en format paysage|
|`perpage`|Faire redémarrer un compteur à chaque page|
|`pgf-pie`|Faire un diagramme "camembert"|
|`minted`|Colorer des citations de code informatique (attention, nécessite une compilation en ligne de commande avec une option: voir le manuel, section 3.1)|
|`multicol`|Mettre un texte sur plusieurs colonnes|
|`pict2e`|Tracer des dessins|
|`placeins`|Mettre une barrière aux flottants|
|`reledmac`|Éditions critiques|
|`reledpar`|Vis-à-vis (avec `reledmac`)|
|`setspace`|Modifier l'interligne|
|`tikz`|Faire des schémas|
|`verse`|Citer des vers|
`wrapfig`|Mettre du texte autour de flottants|
|`xargs`|Créer commandes et environnements avec plusieurs arguments optionnels|
|`xcolor`|Mettre de la couleur|
|`xspace`|Insérer un espace sauf avant certains signes de ponctuation|



## Quelques messages d'erreurs courants

- `!Emergency stop` suivi de `(job aborted, no legal \end found`: il manque `\end{document}`
- `!Undefined control sequence`: la commande n'existe pas - son nom est mal tapé, ou le package qui la définit n'a pas été chargé
- `LaTeX Error: \begin{<nom>} on input line 8 ended by \end{document}`: l'environnement n'a pas été fermé
- `! LaTeX Error: \begin{<nom1>} on input line 9 ended by \end{<nom2>}`: deux environnements se superposent, ou un environnement est fermé par la balise d'un autre environnement
- `! File ended while scanning use of \<nom de la commande>`: on a oublié l'accolade fermant la commande .
- `! LaTeX Error: Command \<nom> already defined` : on a essayé de définir une nouvelle commande ou un nouvel environnement en lui donnant le nom d'une commande ou d'un environnement existants.
- `! File ended while scanning use of \@argdef`: une accolade n'est pas fermée dans la définition d'une nouvelle commande
- `! File ended while scanning use of \@newenv`:  une accolade n'est pas fermée dans la définition d'un nouvel environnement
- `! Missing number, treated as zero`: on a appelé un argument dans la définition d'une nouvelle commande ou d'un nouvel environnement, sans indiquer en option qu'il y aurait un argument
- `! Illegal parameter number in definition of \<nom>`: on appelle, dans la définition d'une nouvelle commande ou d'un nouvel environnement, un argument d'un nombre plus élevé que le nombre d'argument indiqué en option
- ` Missing $ inserted`: on a tapé une commande mathématique sans la mettre entre les symboles `$`.
 



## (Très courte) bibliographie

ROUQUETTE, Maïeul, [XeLaTeX appliqué aux sciences humaines](https://halshs.archives-ouvertes.fr/halshs-00924546)

LOZANO, Vincent, [Tout ce que vous avez toujours voulu savoir sur LaTeX sans jamais oser le demander](https://archives.framabook.org/docs/latex/framabook5_latex_v1_art-libre.pdf)

OETIKER, Tobias, [Une courte (?) introduction à LaTeX](http://tug.ctan.org/tex-archive/info/lshort/french/lshort-fr.pdf)

TISSEAU, Gérard et DUMAS, Jacque, [TikZ pour l'impatient](http://math.et.info.free.fr/TikZ/bdd/TikZ-Impatient.pdf)

## Autres ressources

[Geekographie maïeulesque](https://geekographie.maieul.net/)

[Les fiches à Bébert](https://lesfichesabebert.fr/TeX/TeX.html)

## Trouver de l'aide

### Forums francophones

[Developpez.com](https://www.developpez.net/forums/f149/autres-langages/autres-langages/latex/)

[TeXnique](https://texnique.fr/osqa/)

### Forums anglophones

[Latex Community](https://latex.org/forum/)

[StackExchange](https://tex.stackexchange.com/search?q=)



