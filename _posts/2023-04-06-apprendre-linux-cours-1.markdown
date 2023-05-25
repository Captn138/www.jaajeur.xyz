---
title: Apprendre Linux - Cours 1
author: malmeida
date: 2023-04-07 10:00:00 +0200
categories: [Tutorial, Easy, French]
tags: [linux, shell]
---

Difficulté: Débutant

Ce cours vous donnera les bases pour utiliser un shell Linux.
Ce premier cours sera orienté vers la navigation à travers le shell.

![GNU/Linux Tux](/courslinux/gnulinux-tux.webp)

# Qu'est-ce que Linux ?

Au sens strict du terme Linux est ce qu'on appelle un *kernel* (un noyau en français).
C'est le coeur d'un OS (*operating system*, système d'exploitation en français) qui contient simplement des jeux de fonctions du plus bas niveau afin de permettre à tout le reste du système de se développer autour.
Le terme *GNU/Linux* désigne un OS qui embarque le kernel Linux.
Aujourd'hui, on généralise le terme *Linux* à sa signification d'OS.

Si on regarde le marché, on trouve donc 3 majeurs OS pour ordinateurs :
- Windows (Microsoft)
- MacOS (Apple)
- Linux

Le graphique ci-dessous montre la répartition estimée des systèmes d'exploitation dans le monde.

![PC shares](/courslinux/pcshares.webp)

Le monde du gaming montre des chiffres assez différents, dû à l'imposition de Windows comme le seul OS pour jouer dans les années 90 et 2000.

![Gaming PC shares](/courslinux/gamingpcshares.webp)

A l'inverse, le monde du serveur montre une écrasante majorité d'utilisation de Linux.

![Server shares](/courslinux/serverpcshares.webp)

Linux est dérivé en quelques centaines de *distros* (distributions en français), gérées et maintenues par des ONG, des organismes à but non lucratifs, des groupes d'anonymes, des gens seuls ou encore des entreprises.
Il existe cependant quelques grands "groupes" Linux :
- Le groupe *Debian*, dont un exemple est *Ubuntu*
- Le groupe *Gentoo*, dont un exemple est *ChromeOS*
- Le groupe *RedHat*, dont un exemple est *Fedora*
- Le groupe *Arch*, dont un exemple est *Manjaro*
- Le groupe *SlackWare*, dont un exemple est *OpenSuse*
- Le groupe *Android*

Chaque groupe de distribution va posséder certaines techniques, certains paquets spécifiques, et potentiellement une petite philosophie individuelle, mais il faut bien comprendre que tous sont basés sur le kernel Linux et donc, par définition, on peut faire exactement la même chose sur tous ces OS différents.

# Introduction

## Hiérarchie de fichiers

Avant toute chose, il faut comprendre l'architecture d'un système Linux.
La liste ci-dessous montre les dossiers communs et leur utilité.
On appelle cette architecture la *hiérarchie de fichiers*.

> On utilise le caractère slash ( / ) pour séparer les dossiers.
{: .prompt-info}

- **/** : la racine de la hiérarchie de fichiers.
    - **/boot** : contient les fichiers nécessaire au boot, c'est-à-dire au démarrage de la machine, extrèmement sensible.
    - **/dev** : signifie *devices*, c'est un dossier virtuel, c'est-à-dire que son contenu n'existe pas dans le disque. Ce dossier virtuel contient des fichiers référençant tous les *devices* du système (disques, partitions, processeur, etc).
    - **/etc** : signifie *et cetera* ou *editable text config*, c'est là qu'on trouvera toutes les configurations des programmes du système, généralement dans un dossier au nom du programme
    - **/home** : ce dossier contient un dossier personnel par utilisateur. Ces dossiers sont privés. D'autres utilisateurs du systèmes peuvent être créés afin de faire fonctionner un service, on ne peut pas se connecter avec eux et ils n'ont pas de dossier *home*, on les appelle utilisateurs système.
    - **/opt** : signifie *optionnal*, c'est un dossier dans lequel on peut un peu tout faire, mais surtoût installer des applications qui ne peuvent pas être réparties dans le reste de la hiérarchie de fichiers.
    - **/tmp** : signifie *temporary*, c'est un dossier virtuel qui est monté dans la mémoire vive de l'ordinateur. Sa particularité est qu'il sera donc vidé à chaque extinction du système. Tout le monde peut y placer des fichiers.
    - **/usr** : signifie *user*, c'est un répertoire contenant d'autres répertoires usuels accessibles par les utilisateurs du système.
        - **/usr/bin** : signifie *binaries*, ce sont les fichiers binaires exécutables, c'est-a-dire les commandes exécutables depuis un shell.
        - **/usr/sbin** : signifie *system binaries*, ce sont les fichiers binares exécutables relatifs au coeur du sytstème. Ils sont généralement restreints en permissions.
        - **/usr/lib** : signifie *libraries*, ce sont les fichiers contenant les fonctions compilées partagées nécessaires à l'exécutions des programmes.
        - **/usr/local** : variante du dossier */usr* pour les applications compilées manuellement. Il possède également un dossier *bin*.
    - **/var** : signifie *variable*, ce sont des fichiers variables, c'est-à-dire qu'ils évoluent avec le temps et l'utilisation d'un programme.
        - **/var/logs** : un des exemples les plus représentatifs des fichiers variables sont les journaux d'évènements, ou *logs*. Ces fichiers sont remplis par les informations d'exécution ainsi que les erreurs générées par les programmes.

> Aujourd'hui, on trouve encore des dossiers */bin* et */sbin* par exemple. Ce sont des reliquats d'un fonctionnement ancien et sont généralement un raccourci respectivement vers */usr/bin* et */usr/sbin*.
{: .prompt-info}

## Chemins absolus et relatifs

Le chemin d'un dossier s'exprime généralement de deux manières : soit avec le **chemin absolu**, soit avec le **chemin relatif**.
- Un chemin absolu s'exprime par la suite de dossiers de la racine ( / ) du système jusqu'à l'élément en question.

> Le raccourci vers son propre dossier home est ~.
{: .prompt-info}

*Exemple : /home*
- Un chemin relatif s'exprime par la suite de dossiers de l'emplacement actuel à l'élément en question.
Pour ce faire, on utilise deux symboles :
    - Le simple point ( . ) indique le dossier actuel, c'est-à-dire le dossier dans lequel nous nous trouvons. Dans la plupart des cas, il peut être ômis.
    - Le double point ( .. ) indique le dossier précédent le dossier actuel, c'est-à-dire le dossier qui contient le dossier dans lequel nous nous trouvons.
*Exemples : ../myfolder et ./mynewfoler*

## Affichage du Shell

Le standard d'affichage du shell est d'avoir une indication de l'utilisateur avec lequel on est connecté, la machine sur laquelle on est connecté (séparé de l'utilisateur avec un @ généralement), le chemin du dossier actuel et un indicateur d'utilisateur (\$ pour un utilisateur standard et # pour l'utilisateur racine *root*).

*Exemple : mickael@culture-numerique:~ $*


# Commandes de navigation

## pwd

*pwd* est une commande qui permet d'afficher le dossier actuel.

```bash
mickael@culture-numerique:~ $ pwd
/home/mickael/
```

## ls

*ls* est une commande permettant de lister les éléments présent à un certain chemin. Elle signifie *list*.

PARAMETRES : aucun, un ou plusieurs dossiers. Si aucun dossier n'est spécifié, elle utilisera le dossier actuel.

OPTIONS :
- -a : permet d'afficher également le dossier actuel, le dossier parent et les fichiers cachés. Un fichier caché est un fichier qui commence par un point.
- -l : permet d'afficher le contenu sous forme de liste avec les permissions, le propriétaire, le groupe propriétaire, la taille et la date de dernière modification.
- -h : à combiner avec *-l*, permet d'afficher les tailles en unités humaines.

```bash
mickael@culture-numerique:~ls
myfile1 myfile2
mickael@culture-numerique:~ $ ls /home
mickael/
mickael@culture-numerique:~ $ ls /home /tmp
/home:
mickael/

/tmp:
mytemporaryfile
```

## cd

*cd* est une commande qui permet de se déplacer dans un autre dossier. Elle signifie *change directory*.

PARAMETRES : un ou aucun dossier existant où se déplacer. Si aucun paramètre, prend le *home* de l'utilisateur.

```bash
mickael@culture-numerique:~ $ cd /tmp
mickael@culture-numerique:/tmp $ cd
mickael@culture-numerique:~ $
```

## touch

*touch* est une commande qui permet de créer un fichier si il n'existe pas, mais encore de mettre à jour la dernière date de modification du fichier si il existe déjà.

PARAMETRES : un ou plusieurs fichiers à créer ou mettre à jour

```bash
mickael@culture-numerique:~ $ ls
mickael@culture-numerique:~ $ touch file
mickael@culture-numerique:~ $ ls -l
-rw-rw-r--  1 mickael mickael    0 Apr  7 20:00 file
mickael@culture-numerique:~ $ touch file
mickael@culture-numerique:~ $ ls -l
-rw-rw-r--  1 mickael mickael    0 Apr  7 20:01 file
```

## mkdir

*mkdir* est une commande qui permet de créer un ou plusieurs dossiers. Elle signifie *make directory*.

PARAMETRES : un ou plusieurs dossiers à créer

OPTIONS :
- -p : signifie *parent*, créée les dossiers parents si ils n'existent pas.

```bash
mickael@culture-numerique:~ $ ls
mickael@culture-numerique:~ $ mkdir -p dir1/dir2
mickael@culture-numerique:~ $ ls
dir1/
mickael@culture-numerique:~ $ ls dir1
dir2/
mickael@culture-numerique:~ $ mkdir dir3 dir4
mickael@culture-numerique:~ $ ls
dir1/ dir3/ dir4/
```

## rmdir

*rmdir* est une commande qui permet de supprimer un dossier. Pour ce faire, le dossier doit être vide. Elle signifie *remove directory*.

PARAMETRES : un ou plusieurs dossiers à supprimer

```bash
mickael@culture-numerique:~ $ mkdir dir1
mickael@culture-numerique:~ $ rmdir dir1
mickael@culture-numerique:~ $ ls
mickael@culture-numerique:~ $ mkdir dir2
mickael@culture-numerique:~ $ touch dir2/file
mickael@culture-numerique:~ $ rmdir dir2
rmdir: failed to remove 'dir2': Directory not empty
mickael@culture-numerique:~ $ ls
dir2/
```

## rm

*rm* est une commande qui permet de supprimer un fichier ou un dossier. Elle signifie *remove*.

PARAMETRES : un ou plusieurs éléments à supprimer

OPTIONS :
- -r : signifie *recursive*, permet effectivement de supprimer un dossier et son contenu.

```bash
mickael@culture-numerique:~ $ mkdir dir2
mickael@culture-numerique:~ $ touch dir2/file
mickael@culture-numerique:~ $ rm -r dir2
mickael@culture-numerique:~ $ ls
```

# Exercice d'application

L'exercice suivant permettra de revoir les commandes apprises lors de ce premier cours.
L'objectif est d'effectuer les actions suivantes de la façon la plus synthétique possible.

```
Vous démarrez dans votre dossier personnel (exemple : /home/mickael).
Créer deux dossiers 'dir1' et 'dir2'.
Dans le dossier 'dir2', créer le dossier 'dir3'.
Créer les fichiers 'fic1', 'fic2' et 'fic3'.
Dans le dossier 'dir3', créer les fichiers 'fic4' et 'fic5'.
Supprimer le dossier 'dir2', ainsi que les fichiers 'fic2' et 'fic5'.
Enfin, se déplacer dans le dossier '/opt'.
```
