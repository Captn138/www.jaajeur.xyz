---
title: Apprendre Linux - Cours 2
author: malmeida
date: 2023-04-14 10:00:00 +0200
categories: [Tutorial, Easy, French]
tags: [linux, shell]
---

Difficulté: Débutant

Ce cours vous donnera les bases pour utiliser un shell Linux.
Ce deuxième cours sera orienté vers la manipulation de fichiers à travers le shell.

![GNU/Linux Tux](/courslinux/gnulinux-tux.webp)

# Editeur de texte

Sous les systèmes Linux, il existe différentes maniéres d'écrire du texte ou de la donnée dans un fichier.
Pour un utilisateur, la méthode la plus simple est d'utiliser un *éditeur de texte*.
Parmi les éditeurs de texte en ligne de commande, *vim* et *nano* font parti des plus connus.
Par simplicité, je ne traiterai ici que de nano.
Pour éditer un fichier avec *nano*, on tape la commande 'nano' suivie du ou des fichiers à éditer.
Lorsqu'on "édite plusieurs fichiers", ils sont en réalité mis en queue et on édite le premier, puis lorsqu'on ferme le premier, on édite le deuxième et caetera.

Lorsqu'on ouvre *nano*, nous trouvons en bas une barre des raccourcis, et sur le reste de l'écran la zone éditable.
![nano](/courslinux/nano.webp)
Voici quelques raccourcis utiles à connaître :
- CTRL + S : sauvegarder
- CTRL + X : quitter
- CTRL + W : rechercher
- CTRL + C : annuler (par exemple le menu recherche)
- CTRL + SHIFT + K : supprimer la ligne

# Commandes de manipulation

## cat

*cat* est une commande qui permet d'afficher le contenu d'un fichier. Elle signifie *concatenate*.

PARAMETRES : un ou plusieurs fichiers à afficher.

```bash
mickael@culture-numerique:~ $ cat /etc/os-release
PRETTY_NAME="Ubuntu 22.04.2 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.2 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
```

## cp

*cp* est une commande qui permet de copier un élément. Elle signifie *copy*.

PARAMETRES : un élément à copier et sa destination (qui permet effectivement de nommer la copie différemment) ou plusieurs éléments à copier et leur destination qui doit être un dossier existant

OPTIONS :
- -r : signifie *recursive*, permet de copier le contenu des dossiers

```bash
mickael@culture-numerique:~ $ touch file1
mickael@culture-numerique:~ $ cp file1 file2
mickael@culture-numerique:~ $ ls
file1 file2
mickael@culture-numerique:~ $ mkdir dir1
mickael@culture-numerique:~ $ cp file1 file2 dir1
mickael@culture-numerique:~ $ ls dir1
file1 file2
```

## mv

*mv* est une commande qui permet de déplacer un élément. Elle signifie *move*.

PARAMETRES : un élément à déplacer et sa destination (qui permet effectivement de renommer l'élément) ou plusieurs éléments à déplacer et leur destination qui doit être un dossier existant

```bash
mickael@culture-numerique:~ $ touch file1
mickael@culture-numerique:~ $ mv file1 file2
mickael@culture-numerique:~ $ ls
file2
mickael@culture-numerique:~ $ mkdir dir1
mickael@culture-numerique:~ $ touch file3
mickael@culture-numerique:~ $ mv file2 file3 dir1
mickael@culture-numerique:~ $ ls dir1
file2 file3
```

## ln

*ln* est une commande qui permet de créer un lien pour un élément. Elle signifie link.
Une modification de contenu effectuée sur un lien est répercutée sur l'élément source.

PARAMETRES : un élément source dont le chemin est absolu et une destination.

OPTIONS :
- -s : signifie *symbolic*, c'est l'option qu'on va quasiment toujours utiliser car elle est plus flexible qu'un lien classique

```bash
mickael@culture-numerique:~ $ cat file1
ceci est du texte
mickael@culture-numerique:~ $ ln -s /home/mickael/file1 file2
mickael@culture-numerique:~ $ ls
file1 file2
mickael@culture-numerique:~ $ cat file2
ceci est du texte
```

## echo

*echo* est une commande qui permet d'écrire du texte dans le terminal.

PARAMETRES : ce qu'il faut écrire

OPTIONS :
-e : signifie *escape*, permet d'inclure des caractères "échappés" : *\t* pour le caractère "tab" ou *\n* pour le caractère "retour à la ligne" par exemple

```bash
mickael@culture-numerique:~ $ echo hello world
hello world
mickael@culture-numerique:~ $ echo -e "hello\n\tworld"
hello
        world
```

# Flux de données

Il existe 3 flux de données lors de l'exécution d'une commande:
- stdin : signifie *standard input*, c'est le flux entrant dans la commande, généralement tapé par l'utilisateur
- stdout : signifie *standard output*, c'est le flux créé par la commande, qui s'affiche généralement dans le terminal
- stderr : signifie *standard error*, c'est le flux contenant les messages d'erreurs créé par la commande, qui s'affiche généralement dans le terminal

On peut manipuler les flux d'une commande grâce à des *redirecteurs* :
- \> : permet de rediriger le STDOUT dans un fichier
- \| : permet de rediriger le STDOUT vers le STDIN d'une autre commande
- 2> : permet de rediriger le STDERR vers un fichier
- &> : permet de rediriger le STDERR dans le STDOUT
- < : permet de diriger le contenu d'un fichier dans le STDIN

> Chacun des chevrons peut être doublé ( >> ) afin d'écrire à la suite du fichier. Dans le cas contraire, on remplace le contenu du fichier.
{: .prompt-info}

```bash
mickael@culture-numerique:~ $ cat fichier1
ceci est du texte
mickael@culture-numerique:~ $ cat fichier1 > fichier2
mickael@culture-numerique:~ $ cat fichier2
ceci est du texte
mickael@culture-numerique:~ $ cat fichier3 2> fichiererreurs
mickael@culture-numerique:~ $ cat fichiererreurs
cat: fichier3: No such file or directory
mickael@culture-numerique:~ $ cat < fichier1
ceci est du texte
mickael@culture-numerique:~ $ cat fichier1 >> fichier2
mickael@culture-numerique:~ $ cat fichier2
ceci est du texte
ceci est du texte
```

# Exercice d'application

L'exercice suivant permettra de revoir les commandes apprises lors de ces deux premiers cours.
L'objectif est d'effectuer les actions suivantes de la façon la plus synthétique possible.
L'utilisation d'un éditeur de texte est interdite.

```
Vous démarrez dans votre dossier personnel (exemple pour moi : /home/mickael).
Afficher le contenu du fichier /etc/os-release et envoyer son contenu dans un fichier nommé os-release.
Copier le fichier os-release dans un fichier fichier1.
Renommer le fichier os-release en release.
Créer le fichier fichier2.
Ecrire dans ce fichier "hello world".
A la suite, écrire dans le fichier fichier2 le contenu du fichier fichier1.
Supprimer le fichier fichier1.
Créer le dossier dir1 et le dossier dir2 dans le dossier dir1.
Créer un lien symbolique du fichier /etc/easteregg dans le dossier dir2.
Afficher le contenu du fichier easteregg présent dans le dossier dir2.
Supprimer le dossier dir2, ainsi que les fichiers release et fichier2.
```
