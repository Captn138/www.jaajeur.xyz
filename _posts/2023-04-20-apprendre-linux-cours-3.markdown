---
title: Apprendre Linux - Cours 3
author: malmeida
date: 2023-04-21 10:00:00 +0200
categories: [Tutorial, Easy, French]
tags: [linux, shell]
pin: true
---

Difficulté: Débutant

Ce cours vous donnera les bases pour utiliser un shell Linux.
Ce troisième cours sera orienté vers la création d'un script bash.

![GNU/Linux Tux](/courslinux/gnulinux-tux.webp)

# Permissions

Le système de permissions Linux est assez simple mais robuste.
Les permissions pour un élément sont séparées en 3 blocs :
- Un pour le propriétaire de l'élément
- Un pour le groupe associé à l'élément
- Un pour les autres utilisateurs

Chaque bloc possède 3 permissions indépendantes :
- Lecture (r pour read)
- Ecriture (w pour write)
- Exécution (x pour execute)

On peut voir les permissions avec la commande *ls -l*.
Le premier caractère représente le type de l'objet :
- Fichier (-)
- Dossier (d)
- Lien (l)

Les 9 caractères suivants sont les 3 blocs de 3 permissions.

```bash
mickael@culture-numerique:~ $ touch file
mickael@culture-numerique:~ $ ls -l
-rw-rw-r-- 1 mickael mickael   0 Apr 20 14:51 file
```

Dans l'exemple précédent, file est un fichier (-).
Le propriétaire possède les permissions de lecture et d'écriture (rw-).
Le groupe possède les mêmes permissions (rw-).
Les autres utilisateurs n'ont que le droit de lecture (r--).

# Script

Un script est un fichier exécutable, qui va être lu par le système et contenant une suite d'instructions spécifiques écrites en clair (c'est-à-dire que ce n'est pas un programme compilé).
On débute un script par un *she-bang*.
Un *she-bang* est une suite de caractères permettant de spécifier le programme qui va lire les instructions (#!).
Le *she-bang* est donc suivi du chemin du programme.

```bash
#!/usr/bin/bash
```

# Variables

Une variable sert à stocker du texte.
Dans *bash*, une variable ne peut contenir que du texte.
On peut cependant traiter ce texte de différentes manières.
pour créer une variable et lui donner une valeur, on écrit le nom de la variable, suivi du caractère '=', suivi de la valeur à donner.

> Attention à ne pas ajouter d'espaces autour du caractère '=' car cela casse la syntaxe.
{: .prompt-info}

Pour utiliser une variable, on place le caractère '$' devant.
Pour enregistrer le STDOUT d'une commande dans une variable, on place la commande dans les parenthèses de l'indicateur suivant : '$()'.

```bash
mickael@culture-numerique:~ $ mavariable=texte
mickael@culture-numerique:~ $ echo $mavariable
texte
mickael@culture-numerique:~ $ mavariable="beaucoup de texte"
mickael@culture-numerique:~ $ echo $mavariable
beaucoup de texte
mickael@culture-numerique:~ $ mavariable=$(ls -l /home)
mickael@culture-numerique:~ $ echo $mavariable
drwxr-x--- 6 mickael mickael 4096 Apr 01 09:49 mickael
```

# Commandes

## which
*which* est une commande qui permet d'obtenir le chemin absolu d'un exécutable.

PARAMETRES : un exécutable dont le chemin est à trouver

```bash
mickael@culture-numerique:~ $ which bash
/usr/bin/bash
```

## read
*read* est une commande qui permet de lire une entrée utilisateur.

PARAMETRES : une variable dans laquelle stocker l'entrée utilisateur

OPTIONS :
- -p : signifie *prompt*, permet d'entrer une chaîne de caractères qui sera affichée avant d'attendre l'entrée utilisateur
- -s : signifie *secret*, permet de ne pas afficher l'entrée utilisateur

```bash
mickael@culture-numerique:~ $ read -p "Entrez du texte: " texte
Entrez du texte: Ceci est du texte écrit par l'utilisateur
mickael@culture-numerique:~ $ echo $texte
Ceci est du texte écrit par l'utilisateur
mickael@culture-numerique:~ $ read -s -p "Mon secret:" secret
Mon secret:
mickael@culture-numerique:~ $ echo $secret
Ceci est un secret écrit par l'utilisateur
```

## chmod
*chmod* est une commande qui permet de changer les permissions d'un élément

PARAMETRES : l'action à effectuer ou les nouvelles permissions à donner, suivi de l'élément à changer

Une action de permissions utilise les éléments suivants :
- Bloc de permission :
  - Propriétaire (u pour user)
  - Groupe associé (g pour group)
  - Autres utilisateurs (o pour other)
  - Tous les blocs en même temps (a pour all)
- Une action de permission :
  - Ajouter une permission (+)
  - Supprimer une permission (-)
  - Donner exactement une ou des permissions (=)
- La permissions en question (r, w, x)

Les permissions peuvent aussi être données de façon binaire.
On doit imaginer chaque permission comme une suite de 1 et 0 : 1 pour donner la permission et 0 pour ne pas la donner.
On écrit ensuite chaque bloc de 3 bits en un chiffre décimal.
> Cette syntaxe est assez avancée, elle ne sera donc pas expliquées plus en détails ici.
{: .prompt-info}

```bash
mickael@culture-numerique:~ $ touch file
mickael@culture-numerique:~ $ ls -l
-rw-rw-r-- 1 mickael mickael   0 Apr 20 15:27 file
mickael@culture-numerique:~ $ chmod u+x file
-rwxrw-r-- 1 mickael mickael   0 Apr 20 15:27 file
mickael@culture-numerique:~ $ chmod 400 file
-r-------- 1 mickael mickael   0 Apr 20 15:27 file
```
