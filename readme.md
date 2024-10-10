![LaTeX](LaTeX_logo.svg.png)

# LaTeX et la rédaction de mémoire (ENC 2556)

Vous trouverez sur ce dépôt le contenu pédagogique du cours *LaTeX et la rédaction de mémoire*  du M2 Technologies Numériques Appliquées à l'Histoire à l'École des chartes.

## Planning

| Date | Horaires | Programme |
| ---- | -------- | --------- |
| 16 octobre 2024  | 13h-15h | Notions de base|
| 23 octobre 2024 | 13h-15h | Mettre en forme, mettre en sens |
| 6 novembre 2024 | 13h-15h | Les éléments non textuels    |
| 19 novembre 2024     | 13h-15h  | Gérer sa bibliographie |
|19 mars 2025|13h-15h|Rédiger un mémoire en LaTeX|

## Installation de LaTeX (sur Linux)

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

1. Dans le terminal, placez-vous dans le dossier que vous avez décompressé par la commande `cd` suivie du nom du dossier (`install-tl-20241009`; le nombre peut être différent). Vous pouvez utiliser la touche Tab pour activer l'autocomplétion du nom du dossier.
2. Tapez `sudo perl install-tl`
3. Si vous avez de la place sur votre ordinateur et une bonne connexion internet: répondez `i` ("start installation to hard disk"). **Cette option est à privilégier**
4. Si votre connexion est mauvaise, ou que vous avez trop peu de place, vous pouvez au choix:
	- tapez`c` pour sélectionner quelques collections de packages à décocher. Vous pouvez enlever sans problème les collections désignées par les lettres suivantes: `iklmnowxyzABCPS`. Attention, certaines collections seront utiles si vous comptez utiliser les langues concernées (par exemple arabe ou persan dans la collection `arabit`. Dans ce cas, ne les indiquez pas).
	- Si même ainsi cela prend trop de place/de temps, tapez `j` pour sélectionner un schéma et choisissez "teTex"   

	-> Tapez ensuite `r` pour retourner au menu principal, et `i` pour lancer l'installation.  
Il sera de toute façon possible d'installer plus tard ces collections si vous en avez besoin. 

### 4/ Configurer

Il ne reste plus qu'à configurer votre installation:

1. Tapez dans le terminal  `sudo nano  ~/.profile`. Vous devrez ensuite taper votre mot de passe (qui reste invisible, c'est normal!)
2. Dans le fichier qui s'ouvre, ajoutez les lignes suivantes: 

```
PATH=/usr/local/texlive/2024/bin/x86_64-linux:$PATH; export PATH
MANPATH=/usr/local/texlive/2024/texmf/doc/man:$MANPATH; export MANPATH
INFOPATH=/usr/local/texlive/2024/texmf/doc/info:$INFOPATH; export INFOPATH
```

3. Enregistrez le fichier, et tapez dans le terminal `source ~/.profile` pour que le changement soit pris en compte.
4. Vérifiez que tout fonctionne en tapant `which xelatex` dans le terminal: vous devez avoir le chemin de la texlive 2024 qui s'affiche.


### 5/ Installer un éditeur de texte (TexStudio)

Tapez dans un terminal la commande suivante: `sudo apt install texstudio` puis entrez votre mot de passe.

## Évaluation

Choix entre deux sujets:
 
**Sujet 1 — Production d’une édition scientifique en LATEX**

- Ce sujet est à réaliser en même temps que l'évaluation du cours XSLT de J.D GENERO, et à déposer sur le même dépôt git. Veuillez m'indiquer le lien du dépôt.
- Au document déposé pour le sujet "XSLT vers LaTeX", devra être ajouté un fichier .tex, compilable avec `xelatex` (ou `pdflatex`: dans ce cas, précisez-le), dans lequel vous fournirez: 
	+ la présentation de l’édition : source travaillée, enjeux et
particularités, choix de modélisation, etc.
	+ les choix que vous avez fait  pour produire cette édition en LaTeX (packages utilisés, éventuelles créations de commandes, etc).


**Sujet 2 — Production d’un mémoire universitaire en LATEX** 

- Votre mémoire de M2 sera évalué par rapport à votre utilisation de LaTeX.
- Seront examinés: le ou les documents .tex et le document .pdf
- Le mémoire sera produit à partir du document maître fourni
- Il devra contenir au moins: 
	+  une page de titre
	+   deux chapitres
	+  une bibliographie propre
	+ un index et/ou un glossaire
- Au sein du document, il faudra produire :
	+ au moins un tableau
	+ au moins une figure ou un schéma
	+ au moins une nouvelle commande, commentée
	+ des paragraphes structurés, respectant les normes typographiques françaises.
- Tout package appelé devra être brièvement présenté par un commentaire


