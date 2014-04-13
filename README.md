# Atelier CLI, Arborescence et `pstopdf`

### Table des matières

- [Préambule](#préambule)
- [Rappel](#rappel)
    - [Le caractère _espace_](#le-caractère-espace)
    - [La casse](#la-casse)
    - [Commande `ls`](#commande-ls)
- [Arborescence](#arborescence)
    - [Commande `ls` _vs._ `tree`](#commande-ls-vs-tree)
- [Localiser un exécutable](#localiser-un-exécutable)
    - [`which`](#which)
    - [`whereis`](#whereis)
- [Convertir un _PDF_ en _PS_ avec `pdftops`](#convertir-un-pdf-en-ps-avec-pdftops)
- [Chaîner des commandes](#chaîner-des-commandes)
- [Arborescence des processus avec `pstree`](#arborescence-des-processus-avec-pstree)
- [Discussion ](#discussion)

## Préambule

> Ce document s'adresse aux participants des [ateliers CLI organisés au LabX](https://www.labx.fr/) (_hackerspace_ de Bordeaux) à un publique **débutant**.
> 
> Il est évident que certains concepts sont simplifiés pour s'adapter au public. 

Si toutefois vous trouvez des erreurs, merci de les signaler à l'auteur via : 

* Mail : [dev+clilabx@edouard-lopez.com](dev+clilabx@edouard-lopez.com) ;
* Twitter : [@edouard_lopez](https://twitter.com/edouard_lopez) ;
* IRC : #giroll ou #labx ;
* en venant discuter à [Giroll](http://giroll.org/), au [LabX](www.labx.fr/), au [Node](http://bxno.de/) ou autres.

## Rappel

### Le caractère _espace_ 

L'espace est ce qu'on appel un caractère spécial dans le terminal. Il permet de séparé une commande (`ls`) de ses options (`-lA`) et de ses arguments (`/home/`) :

```bash
ls -lA /home/
```

### La casse

Le système Linux est sensible à la casse, c'est-à-dire que la **distinction entre majuscules et minuscules est importante**.

```bash
tree # ok
Tree # No command 'Tree' found
```

### Commande `ls`

Permet de visualiser directement le contenu d'un répertoire.

```bash
ls ./mon-répertoire/
```

Ça nous listera le contenu du répertoire `Images` qui est un sous-répertoire du chemin ou nous sommes, p. ex. dans le répertoire utilisateur.

## Arborescence

Nous avons déjà abordé la commande `ls` lors de précédent atelier, mais il semble que les participants aient du mal à l'appréhender. 

### Commande `ls` _vs._ `tree`
Nous allons la comparer avec la commande `tree` qui liste le contenu des répertoires sous forme d'arborescence. Nous utiliserons quelques options pour que le résultat de la commande soit plus lisible :

* `-d`: liste uniquement les répertoires (pas les autres fichiers) ;
* `-L 2`: on limite la profondeur de l'arborescence à deux niveaux ;
* `--charset utf-8`: utilise des caractères plus lisible pour la symbolique.

Résultat en image, à gauche la commande `ls -l ~`, à droite la commande [`tree . -d -L 2 --charset utf-8`](http://explainshell.com/explain?cmd=tree+.+--charset+utf-8+-d+-L+2)

![`ls -l` vs. `tree . --charset utf-8 -d -L 2`][ls-vs-tree]

Dans les deux cas nous listons le répertoire de l'utilisateur :

* avec `ls` nous utilisons le tilde `~` qui par [convention désigne le _répertoire de l’utilisateur_](https://fr.wikipedia.org/wiki/~#Tilde_chassant) ;
* avec `tree` nous utilisons le chemin `.` qui désigne le répertoire courant, et qui dans ce cas précis correspond au répertoire de l'utilisateur.

## Localiser un exécutable

### `which`
la commande `which` retourne les chemins vers les exécutables passer en argument.

```bash
which pdftops
# /usr/bin/pdftops
```

### `whereis`

La commande `whereis` à un comportement similaire, elle retourne l'emplacement de l'exécutable, et si elles sont présentes, les sources et les fichiers correspondant aux pages du manuel.

```bash
whereis pdftops
# pdftops: /usr/bin/pdftops /usr/bin/X11/pdftops /usr/share/man/man1/pdftops.1.gz
```

Ici, `/usr/bin/X11` est un lien vers le répertoire `/usr/bin/`. D'oú le doublon

## Convertir un _PDF_ en _PS_ avec `pdftops`


Nous avons également vu comment transformer un fichier _PDF_ en _PostScript_. Cette commande a été vue pour sur demande d'un participant.

Le format de fichiers `PS` utilise PostScript un langage de description de page pour les imprimantes. C'est un ancêtre du format `PDF`.

```bash
pdftops [options] <PDF-file> [<PS-file>]
```

L'utilisation de la commande est assez simple, car la forme canonique est tout simplement :

```bash
pdftops ./mon-fichier.pdf
```

La commande créera automatiquement un fichier portant le même nom, mais une extension `.ps`. On aura donc les fichiers `mon-fichier.pdf` et `mon-fichier.ps`. Pour créer un fichier avec un nom différent on utilisera :

```bash
pdftops ./mon-fichier.pdf ./nouveau-fichier.ps
```

## Chaîner des commandes

```bash
cmd1 ; cmd2 ; cmd3
```

le caractère `;` permet d’exécuter une séquence de commandes, et ainsi automatisé une série d'action. A noter que les commandes sont toutes exécutées même si l'une d'elle est en erreur.

## Arborescence des processus avec `pstree`

* def `pstree`
* def processus

## Discussion 

`RTFM`: expression que l'on vous répondra souvent lorsque votre question est triviale. Cela signifie "_Read The Fucking Manual_" et se traduit par « _Lit le fichu manuel_ ».

[ls-vs-tree]: ./ls-vs-tree-command.png
