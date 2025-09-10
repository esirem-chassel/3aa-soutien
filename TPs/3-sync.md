# TP3 : Mise en application

## 0. Objectif

Nous allons réaliser la mise en place d'un site web Django, avec synchronisation régulière de la base de données vers un serveur de sauvegarde.

Le site en question réalise de la génération de rainbow tables sur le temps, de manière automatisée.

La partie 1 peut être réalisée en commun. Les parties suivantes sont individuelles.

Aucun rendu n'est nécessaire, mais des questions vous seront posées pour vérifier votre avancement, votre compréhension, ainsi que vos compétences travaillées.

## 1. Installation Pi

Réalisez l'installation classique du Raspberry Pi, en étant attentif :
- activez SSH
- prévoyez un utilisateur par membre de votre équipe
- vérifiez l'installation de python3, pip et venv
- installez git et sqlite

## 2. Installation Django

Clonez [le dépôt rainbow](https://github.com/esirem-chassel/rainbow) dans votre répertoire utilisateur.
Créez un venv, et installez les packages nécessaires : `pip install -r requirements.txt`

> [!Note]
> Le fichier requirements.txt est un fichier standard PIP pour lister les dépendances d'une application.
> En lançant la commande précédente, vous allez lancer l'installation de tous les packages indiqués,
> ainsi que de leurs dépendances.

## 3. Tests

En vous aidant de la documentation du projet rainbow, testez d'ajouter une ou plusieurs flavors de rainbow table.

Testez également la génération d'enregistrements via ligne de commande.

## 4. Crontab

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

Ajoutez une tâche cron pour générer un nouveau élément de rainbow table toutes les 2 minutes.

## 5. Rsync

RSync est un utilitaire de sychronisation de fichiers et/ou dossiers entre hôtes potentiellement distants, à travers SSH.

La syntaxe est assez simple : `rsync <src> <target>`,
mais la puissance de rsync vient du fait qu'on peut spécifier la source et/ou la cible comme étant distante,
via une syntaxe proche de SSH : `<user>@<host>:<path>`.

Par exemple, la commande `rsync abc@192.168.0.5:/var/tmp/test.txt qsd@192.168.10.22:/home/qsd/tv.txt`
va synchroniser le fichier `/var/tmp/test.txt` situé sur le poste `192.168.0.5`
avec le fichier `/home/qsd/tv.txt` situé sur le poste `192.168.10.22`.

En utilisant crontab, et après tests,
synchronisez automatiquement votre base sqlite vers le serveur indiqué par votre enseignant.

## 6. Supplément : plus loin !

En utilisant rsync, rapatriez les autres bases, afin de mettre en commun, via un script de votre cru, les différents enregistrements rainbow afin de créer une gigantesque rainbow table.

Plus d'informations sur Python et SQLite : https://docs.python.org/3/library/sqlite3.html
