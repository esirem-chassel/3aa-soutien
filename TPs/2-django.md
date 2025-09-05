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

Les parties 1 à 3 sont des parties devant être réalisées en commun.
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

## 2. PIP

Vérifiez, si pip est installé : `pip -v`.
Si ça n'est pas le cas, installez-le simplement avec aptitude (paquet `python3-pip` ).

## 3. Virtual Env

Maintenant que l'ensemble des outils systèmes nécessaires sont créés,
nous allons commencer à installer et créer les différents éléments spécifiques au projet Django.

Pour commencer, nous allons créer un venv (virtual environnement). 
Un venv est un dossier spécifique permettant de monter des permissions et exécutables spécifiques à un projet Python.
Quand un venv est activé, toutes les commandes en rapport avec python seront obtenues depuis l'intérieur du venv.

Créez un venv : `python3 -m venv .venv` __**dans votre dossier utilisateur spécifique**__.

> [!Warning]
> La commande indiquée peut échouer, car venv n'est pas installé.
> Si c'est le cas, installez simplement `python3-venv` avant de tester à nouveau.

Une fois le venv créé, activez-le : `source .venv/bin/activate`.
Vous devriez voir un changement dans votre console,
indiquant que vous êtes dans le contexte d'un venv.

## 4. Installation Django de base

Installons Django !

> [!Caution]
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

En suivant la procédure en annexe, créez un administrateur superadmin.
Attention à bien noter vos identifiants !

Ensuite, connectez-vous au site administrateur, en accédant à la page de votre Django mais en ajoutant `/admin/` à la fin de votre URI,
par exemple `http://127.0.0.1:8000/admin/` .

Entrez vos identifiants - vous serez sur le site admin de votre instance Django.

## 5. Personnalisation

### Bases de Django

Django sépare Projet et App de manière distincte.
Un projet est un ensemble d'applications avec une configuration spécifique.
Une application (ou app) est un module répondant à un besoin précis et délimité.

Nous avons créé le projet, il nous reste à créer notre application, qui va contenir un suivi de notre humeur au fil des heures et des jours.

Via la commande `python manage.py startapp moods` (attention à être dans le bon dossier !), nous créons l'app `moods`.

Une fois l'app créée, listez vos fichiers dans cette app.

> [!Note]
> Ne tenez pas compte des `__init__.py` qui sont un mécanisme interne à Python.

D'après vous, à quoi sert chacun des fichiers et dossiers ?

### Modèle Humeur

Ajoutez un modèle à votre application : le relevé d'humeur.
Nous allons simplement le nommer `Statement`, pour "relevé".

Les modèles, dans Django, sont une façon de décrire la manipulation et la représentation d'une donnée.

Par exemple, on peut représenter des modèles Question et Choice de la façon suivante :

```py
from django.db import models


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField("date published")


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```
Chaque entité de la base de données est représentée sous la forme d'une classe héritant de `models.Model`, et chaque propriété de cette entité est un attribut de la classe, dont la valeur correspond à sa définition, parmi [les différents types répertoriés](https://docs.djangoproject.com/en/5.2/ref/models/fields/).

Créez donc le modèle `Statement`, composé d'une date, incluant une heure, un texte facultatif, ainsi qu'une note de 1 à 5 représentant l'état d'humeur de ce jour (1 étant affreux, 5 étant euphorique).

Une fois le code du modèle intégré, nous allons activer l'app `moods` dans votre projet.
Dans le fichier `<nom du projet>/apps.py`, ajoutez la ligne suivante dans la liste `INSTALLED_APPS` : `"moods.apps.MoodsConfig"`.

Le bloc `INSTALLED_APPS` dans le fichier `apps.py` pourrait ainsi ressembler à ceci :

```py
INSTALLED_APPS = [
    "moods.apps.MoodsConfig",
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
]
```

A présent que votre projet Django sait qu'il doit inclure cette app, lançons la génération des migrations correspondant à nos modèles :
`python manage.py makemigrations moods`.

> [!Tip]
> La gestion des modifications de votre base via migrations est un système usuel dans les applications modernes.
> En règle générale, il est conseillé de rassembler les migrations initiales en un unique fichier, donc d'effectuer le `makemigrations` le plus tard possible.
> Ce n'est pas une règle absolue. Ne vous en formalisez pas pour le moment.

Notez le numéro indiqué pour la migration (par exemple `001`). Si vous désirez visualiser la migration à venir sans l'exécuter, vous pouvez lancer la commande `python manage.py sqlmigrate moods <numéro de la migration>`.

Enfin, pour lancer la migration (et toutes celles potentiellement nécessaires en attente !), la commande `python manage.py migrate` se charge de cela.


### Site admin

Dans le cadre de ce TP, nous allons utiliser uniquement le site admin pour manipuler nos entités.

La configuration de la disponibilité d'une app dans le site admin est extrêmement simple. Ouvrez le fichier `moods/admin.py`, et enregistrez votre modèle comme suit (cet exemple est pour un modèle `Question`, à vous de vous adapter !) :

```py
from django.contrib import admin

from .models import Question

admin.site.register(Question)
```

En rechargeant le site admin, vous verrez votre modèle apparaître !


### Tâche d'extraction

Après avoir "joué" avec vos modèles en ajoutant des entrées dans votre base de données via le site admin, nous allons tester l'extraction de données, en vue de sauvegardes régulières.
Pour cela, consultez les annexes, afin de connaître la démarche pour "dump" une base existante dans un fichier.


### Automatisation

L'utilitaire `crontab`, très largement disponible sous les systèmes Linux, permet de lancer des scripts de manière automatisée.

Davantage d'informations vous sont aimablement données dans les annexes.

Ajoutez une tâche crontab pour lancer un export automatisé de votre base toutes les 10 minutes.


## 6. Extension

### Mood actual

Nous allons ajouter un modèle `Actual`, qui définit le "mood" actuel.
Celui-ci n'est qu'une référence vers un `Statement` existant.

### Marqueurs

Nous allons ajouter des marqueurs, des questions supplémentaires ajoutés à chaque relevé.
Chaque marqueur, ou `Indicator` est représenté sous un titre, et une question (ou texte).
Enfin, pour chaque `Statement`, on doit pouvoir ajouter un `Indicator` en indiquant sa valeur.

Un exemple d'interaction pourrait être un `Indicator` nommé "Objectifs" avec le contenu "Avez-vous rempli vos objectifs de la journée ?".
Sur chaque `Statement`, on peut alors indiquer, pour l'`Indicator` "Objectifs", une valeur, comme "Presque !" ou "Non, la flemme lmao".

## Annexes

### PostGreSQL : createuser

Source : https://www.postgresql.org/docs/current/app-createuser.html

La commande createuser est une commande spécifique PostGreSQL.
Comme pour la connexion par défaut à PSQL, vous devez être connecté sous l'user linux `postgres` pour l'utiliser.
Attention à bien lire la documentation !

### SQL

#### SQL : création d'une base de données

```sql
create database "<nom de la database>";
```

Vous pouvez vérifier si votre base a bien été créée via la commande psql spéciale : `\list`.

#### SQL : permissions

La commande `GRANT` permet d'ajouter des permissions à un utilisateur.

Exemple pour ajouter toutes les permissions sur une base pour un utilisateur :

```sql
grant all privileges on database "<database>" to "<user>";
```

#### SQL : dump

Il existe un utilitaire de dump (ou extraction) d'une base PostGreSQL : pg_dump.
Plus d'informations sont disponibles dans la documentation associée : https://www.postgresql.org/docs/current/app-pgdump.html

### Django

#### Django : Création d'un superadmin

La procédure est très simple. Lancez l'utilitaire en ligne de commande `python manage.py createsuperuser` puis suivez les indications.

#### Django : Création d'une app 

La création d'une app est lancée via `python manage.py startapp <nom de l'app>`.

> [!Caution]
> L'app va être créée là où votre ligne de commande est.
> Donc assurez-vous d'être dans le bon dossier.
> A noter que Django conseille quelque chose que beaucoup de développeurs ne font pas : de créer des apps HORS des projets.
> Dans le cadre de ces exercices, je vous conseille de créer vos apps dans le premier niveau de votre projet, cela vous simplifiera certaines opérations.

### Crontab

La crontab, sur les systèmes Linux, est un système automatisé de lancement de tâches planifiées.

La commande associée, `crontab`, permet d'éditer et modifier les tâches en question.

Le format des fichiers `crontab` est assez simple (mais il faut le comprendre !),
et vous pouvez en voir un exemple via la commande `crontab -e` ou encore dans `/etc/crontab`.

```
  * * * * * <command to execute>
# | | | | |
# | | | | day of the week (0–6) (Sunday to Saturday; 
# | | | month (1–12)             7 is also Sunday on some systems)
# | | day of the month (1–31)
# | hour (0–23)
# minute (0–59)
```

La table suivante par exemple :

```
0 5 * * 6 /tmp/sup.sh # va se lancer à 5h00 tous les samedi
*/30 * * * * /tmp/try.sh # va se lancer toutes les demi-heures
```

