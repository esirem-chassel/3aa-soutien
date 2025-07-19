# TP2 : Linux et développement python

## 0. Contexte

Ce TP vous conduit à travers la découverte, l'installation et la personnalisation d'une instance Django,
un framework Web Python. Il est une reprise des tutoriaux officiels de la documentation du site de Django :
- Installation Django
- Tutoriel Django

Ce TP est néanmoins bien plus guidé.
Il est déconseillé de suivre uniquement les documentations officielles pour ce TP,
et encore plus fortement déconseillé d'utiliser des Intelligences Artificielles.

Utilisez ce TP pour décomplexer l'usage de Linux.
La touche `Tab` est une alliée !
L'aide via `man` est très utile !

Les parties X à Y sont des parties devant être réalisées en commun.
Les parties suivantes peuvent être réalisées sur un compte utilisateur et des instances Django à part.

Enfin, ce TP est un avant-goût de votre prochain TP noté.

> [!Caution]
> Dans ce TP, vous trouverez régulièrement une notation avec des chevrons (`<>`) comme suit : `<user>`.
> Cela signifie que vous devrez remplacer l'ensemble de la chaîne, chevrons compris, par l'élément pertinent correspondant.


## 1. Configuration initiale du système

Lancez la configuration initiale de votre Raspberry Pi, en prenant soin de :
- ne pas utiliser l'outil de mise à jour graphique
- bien noter les identifiants utilisés
- configurer le service SSH pour vous permettre une connexion à distance
- ajouter les utilisateurs nécessaires pour les membres de votre groupe

### Installations de base

Assurez-vous que les packages suivants soient installés :
- python
- git

Vérifiez la version de Python. Celle-ci doit être supérieure ou égale à 3.8.

> [!Note]
> Vous pourriez avoir python2 et python3 d'installé.
> Ces versions sont incompatibles mais cohabitent via deux commandes différentes.
> Testez `python --version` pour connaître la version de python.
> Si la commande n'est pas disponible, `python3` le sera, testez.

### Installation de PostGreSQL

Installez `postgresql`.

> [!Warning]
> Des packages supplémentaires seront nécessaires par la suite pour l'intégration avec Django,
> mais leur mode d'installation (via `pip`) sera abordée par la suite.

Une fois l'installation réalisée, tentez de vous connecter à l'utilisateur `postgres` via `sudo su`.

> [!Note]
> Vous vous rappellez évidemment comment faire, ou à défaut comment obtenir de l'aide sur la commande `su` ?

Une fois connecté sur l'user spécial `postgres`, vous pouvez vous connecter au serveur PostGreSQL local en mode superadmin : `psql`.

> [!Tip]
> Lorsque vous vous connectez à PostGreSQL en local, en étant connecté sous l'user linux `postgres`, sans options particulières,
> vous serez automatiquement connecté en mode superadmin.
> Nous allons créer, par la suite, autant d'utilisateurs que nécessaire.

Pour chacun·e des membres de votre équipe, créez : 
- une base SQL (via CREATE DATABASE)
- un utilisateur SQL (via creatuser)
- une permission SQL (via GRANT)

Testez les différentes connexions !

## PIP

Vérifiez, si pip est installé : `pip -v`.
Si ça n'est pas le cas, installez-le simplement avec aptitude (paquet `python3-pip` ).

## Virtual Env

Maintenant que l'ensemble des outils systèmes nécessaires sont créés,
nous allons commencer à installer et créer les différents éléments spécifiques au projet Django.

Pour commencer, nous allons créer un venv (virtual environnement). 
Un venv est un dossier spécifique permettant de monter des permissions et exécutables spécifiques à un projet Python.
Quand un venv est activé, toutes les commandes en rapport avec python seront obtenues depuis l'intérieur du venv.

Créez un venv : `python3 -m venv .venv` __**dans votre dossier utilisateur spécifique**__.

> [!Caution]
> La commande indiquée peut échouer, car venv n'est pas installé.
> Si c'est le cas, installez simplement `python3-venv` avant de tester à nouveau.

Une fois le venv créé, activez-le : `source .venv/bin/activate`.
Vous devriez voir un changement dans votre console,
indiquant que vous êtes dans le contexte d'un venv.

## Installation Django de base

Installons Django !

> [!Danger]
> Soyez sûr d'être dans votre contexte venv pour toute opération impliquant python.

`pip install django` va installer les éléments nécessaires à Django.
Rappellez-vous : cela va les installer dans le contexte du venv.
Vous devez toujours créer un projet Django : `django-admin startproject <nom du projet>`.

Cette commande va créer un projet Django "vide", un "squelette".
Déplacez-vous dans le dossier `<nom du projet>` pour la suite.

### Démarrage du serveur

Testez le serveur : `python3 manage.py runserver`

> [!Tip]
> Oui, la console est désormais en mode "contrôlée" sur le processus en cours.
> Vous pouvez (et devriez) en ouvrir une autre.
> N'ayez pas peur d'ouvrir autant de terminaux que nécessaires.
> Il existe des outils intégrés dans Linux,
> comme `screen` ou `tmux` permettant d'avoir même plusieurs consoles disponibles dans une même session SSH si nécessaire.

Vous interagir avec cette console :
`Ctrl+C` va couper le processus en cours, donc le serveur django
`Ctrl+Z` va suspendre le processus, le mettant en pause, redonnant la main dans la console

Une fois un processus en suspens, vous pouvez le relancer en arrière-plan via la commande `bg`.

> [!Important]
> Même quand un processus est relancé en arrière-plan, il reste "lié" à la console en cours.
> Cela signifie que la sortie du processus va continuer à s'afficher dans la console en cours,
> et que si une session SSH était ouverte pour accéder à cette console, la console va se fermer
> à la fermeture de la session, coupant ainsi le processus !

Vous pouvez ramener un processus en avant via la commande `fg`.

### Authentification

Ajoutons le module d'authentification, en modifiant le fichier `<nom du projet>/settings.py`,
et en ajoutant (s'il n'y est pas déjà), dans le tableau `INSTALLED_APPS` la valeur `'django.contrib.auth'`.

Puis, lançons les migrations pour appliquer l'installation des modules : `python manage.py migrate`.

### Création d'un superadmin et site admin

## Personnalisation

### Base PotsgreSQL

### Modèle Humeur

### Tâche d'extraction

### Automatisation

## Annexes

### PostGreSQL : createuser

Source : https://www.postgresql.org/docs/current/app-createuser.html

La commande createuser est une commande spécifique PostGreSQL.
Comme pour la connexion par défaut à PSQL, vous devez être connecté sous l'user linux `postgres` pour l'utiliser.
Attention à bien lire la documentation !

### SQL : création d'une base de données

```sql
create database "<nom de la database>";
```

Vous pouvez vérifier si votre base a bien été créée via la commande psql spéciale : `\list`.

### SQL : permissions

La commande `GRANT` permet d'ajouter des permissions à un utilisateur.

Exemple pour ajouter toutes les permissions sur une base pour un utilisateur :

```sql
grant all privileges on database "<database>" to "<user>";
```

