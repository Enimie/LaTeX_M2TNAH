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

Avoir le package `perltk` d'installé. Si ce n'est pas le cas:
- Ouvrir un terminal
- Taper la commande suivante: `sudo apt install perl-tk` et valider par la touche "Retour"
- Taper votre mot de passe (il reste invisible, c'est normal), et valider par la touche "Retour"


### 2/ Télécharger le programme d'installation

Deux possibilités: 

1. Télécharger le fichier *via* le lien suivant: [install-tl-unx.tar.gz](https://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz)
2. Dans le terminal, placez-vous dans le dossier Téléchargement par la commande `cd ~/Téléchargements` puis taper `wget https://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz`

Une fois le fichier téléchargé, le décompresser. Pour cela, taper dans le terminal la commande `tar -xf install-tl-unx.tar.gz`


### 3/ Installer

1. Placez-vous dans le dossier que vous avez décompressé par la commande `cd` suivi du nom du dossier (`install-tl-20230926`; le nombre peut être différent). Vous pouvez utiliser la touche Tab pour activer l'autocomplétion du nom du dossier.
2. taper `sudo perl install-tl`
3. Si vous avez de la place sur votre ordinateur et une bonne connection internet: répondez `i` ("start installation to hard disk"). **Cette option est à privilégier**
4. Si votre connexion est mauvaise, ou que vous avez trop peu de place, vous pouvez au choix:
	- tapez`c` pour sélectionner quelques collections de packages à décocher. Vous pouvez enlever sans problème les collections désignées par les lettres suivantes: `iklmnowxyzABCPS`. Attention, certaines collections seront utiles si vous comptez utiliser les langues concernées (par exemple arabe ou persan dans la collection `arabit`. Dans ce cas, ne les indiquez pas).
	- Si même ainsi cela prend trop de place/de temps, tapez `j` pour selectionner un schéma et sélectionner "teTex"   

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

3. Tapez `source ~/.profile` pour que le changement soit pris en compte
4. Vérifiez que tout fonctionne en tapant `which xelatex` dans le terminal: vous devez avoir le chemin de la texlive 2023 qui s'affiche.


### 5/ Installer un éditeur de texte (TexStudio)

Tapez dans un terminal la commande suivante: `sudo apt install texstudio` puis entrez votre mot de passe.

## Évaluation

Les consignes seront données ultérieurement
Date de rendu: **XXX**

## (Très courte) bibliographie

ROUQUETTE, Maïeul, [XeLaTeX appliqué aux sciences humaines](https://halshs.archives-ouvertes.fr/halshs-00924546)

LOZANO, Vincent, [Tout ce que vous avez toujours voulu savoir sur LaTeX sans jamais oser le demander](https://archives.framabook.org/docs/latex/framabook5_latex_v1_art-libre.pdf)

OETIKER, Tobias, [Une courte (?) introduction à LaTeX](http://tug.ctan.org/tex-archive/info/lshort/french/lshort-fr.pdf)


## Trouver de l'aide

### Forums francophones

[Devellopez.com](https://www.developpez.net/forums/f149/autres-langages/autres-langages/latex/)

[TeXnique](https://texnique.fr/osqa/)

### Forums anglophones

[Latex Community](https://latex.org/forum/)

[StackExchange](https://tex.stackexchange.com/search?q=)
