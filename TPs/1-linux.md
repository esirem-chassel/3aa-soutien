# TP 1 : Linux, shell, SSH

## Installation physique

> [!WARNING]
> Assurez-vous bien que la carte SD soit bien insérée avant de le brancher votre Raspberry !

Connectez votre Raspberry : écran, clavier, souris et alimentation.
A la première connexion, vous devrez sélectionner plusieurs paramètres initiaux, parmi :
- le nom d'utilisateur (utilisez le nom de votre groupe) et mot de passe (conservez-le bien !!)
- la configuration de la langue et TZ (sélectionnez Europe/Paris et France)
- la configuration du clavier (testez votre clavier pour cela)
- la connexion Wi-Fi (passez cette étape)
- les mises à jour (passez également cette étape)

Connectez ensuite le câble à paires torsadées à connectique RJ45 pour protocole Ethernet (le câble Ethernet en gros) pour relier votre Pi au réseau.

## Démarrage 

Au lancement de votre raspberry, une fois l'étape initiale passée, ouvrez un terminal.

### Mises à jour

Lancez les mises à jour : `sudo apt update` puis `sudo apt upgrade`.

> [!NOTE]
> `sudo` permet de demander une dérogation au superuser (root) pour réaliser une opération.

### Terminal

Observez votre ligne de commandes.

Celle-ci vous donne déjà quelques informations, car la partie gauche est systématiquement sous la forme : `<username>@<host>:<path><mode>`.

`<username>` est le nom d'utilisateur, `<host>` est le nom d'hôte, `<path>` est le chemin actuellement parcouru et `<mode>` est le mode actuel d'édition (`$` par exemple).

## Bash

### Exploration

Utilisez cd pour vous déplacer dans le dossier `Documents` : `cd Documents`. Que constatez-vous dans votre ligne de commandes ?

> [!TIP]
> On dit que `Documents` est l'argument donné à la commande `cd`

La commande `pwd` affiche votre répertoire de travail (actuellement parcouru). Testez cette commande. Qu'obtenez-vous ?

Pour se "déplacer" dans le dossier parent, on peut faire un `cd ..`, la suite de caractères `..` permettant, en Unix/Linux, de désigner le dossier parent. Le caractère seul `.` permet de désigner le dossier courant.

Que ferait donc `cd .` ?

Déplacez-vous dans `/tmp` et effectuez un `pwd`. Que constatez-vous ?

Le système hiérarchique des systèmes X se base sur une racine `/`.
Quand le premier caractère d'un chemin est un `/`, cela signifie qu'on "part" de la racine du système.
Quand les premiers caractères d'un chemin sont `./` cela signifie qu'on "part" du dossier courant.

Cela signifie que `/home/pi/../test/./Images` est identique à `/home/test/Images`.

Il existe d'autres caractères spéciaux, notemment `~` désignant le dossier "home" de l'utilisateur actuellement connecté.

Déplacez-vous dans votre dossier utilisateur, soit via `cd` soit via `cd ~`.


### Listing et propriétés (bases)

Dans votre dossier utilisateur, effectuez un `ls`. Cette commande permet de lister les fichiers et dossiers.
D'après vous, quels éléments sont des fichiers ? Quels éléments sont des dossiers ?

L'argument derrière `ls` permet d'indiquer le chemin à "explorer".

La commande ls peut prendre un grand nombre d'options. Effectuez un `man ls` pour afficher l'aide sur la commande `ls`.

> [!TIP]
> Cette aide utilise un lecteur identique à celui de la commande `less`.
> Ce lecteur permet la recherche (en tapant `/` suivi de la chaîne de recherche souhaitée),
> le défilement lent (avec les flèches directionnelles), le défilement de pages (avec espace ou encore les doubles flèches)...
> Pour quitter ce lecteur, appuyez simplement sur `q`. Une aide complète est disponible en appuyant simplement sur `h` dans le lecteur.

Par exemple, `ls -a` permet de lister tous les fichiers et dossiers, y compris ceux cachés (commençant par un point), y compris `.` (dossier courant) et `..` (dossier parent).
La commande `ls -lt` liste les fichiers et dossiers, triés par date de modification, sous un format liste un peu plus lisible.

Quelle est la taille du fichier `.bashrc` ?

Testez la commande `ls -hlt`. Que constatez-vous ? Comment obtiendirez-vous cette même liste en incluant les fichiers et dossiers cachés ?

L'option `-l` permet notemment de voir différentes informations quant aux fichiers et dossiers:
- les attributs ou flags
- le nombre d'éléments contenus
- le propriétaire
- le groupe
- la taille
- la date de modification
- le nom (et possiblement la cible - nous verrons ça plus tard)

Nous allons nous intéresser aux attributs.
Le premier attribut indique le type d'élément; par exemple `d` est un dossier (`d`irectory), `l` un lien symbolique (sym`l`ink), alors que `-` indique un fichier.
Les neufs attributs suivants indiquent les droits affectés au propriétaire (trois caractères), au groupe (trois caractères) et à tous les utilisateurs (trois caractères).
Chaque groupe de trois attributs de droits est composé de flags : `rwx`. Le première caractère (ou flag) indique le droit de lecture, le deuxième le droit d'écriture et le troisième le droit d'exécution.
Par exemple, `r-x` indique que nous pouvons lire et exécuter le fichier, mais pas écrire dedans.

Quels sont les droits du fichier `.bashrc` ? Ceux du dossier `Images` ?

Quels sont les droits du dossier `/tmp` ?

### Edition

Créez un fichier vide via touch : `touch test.txt`.
Editez ensuite ce fichier via nano : `nano test.txt` afin d'y ajouter une phrase, votre slogan, un principe de vie ou peu importe.

> [!Info]
> Nano est l'éditeur en ligne de commande le plus basique à disposition dans la plupart des installations X.
> Il fonctionne grâce à des raccourcis claviers basés sur la touche `CTRL` (indiqué sous le caractère `^`) indiqués en base d'interface.

Sauvegardez votre fichier et quittez nano.

Créez un nouveau dossier `edir` : `mkdir edir`.

Maintenant, nous allons déplacer notre fichier `test.txt` vers le dossier `edir`, via la commande `mv`.
Commencez à saisir la commande (ne la validez pas de suite !) : `mv test.txt ./ed` puis appuyez sur la touche `TAB` de votre clavier (la tabulation).
La commande se complète automatiquement. Validez.

> [!TIP]
> La tabulation est un des outils les plus puissants et simples à la fois de ces systèmes.
> Un appui sur tabulation va compléter commandes et chemins de fichiers.
> Si plusieurs choix sont possibles, un double tab va faire apparaître la liste des choix.
> Utilisez la tabulation pour complétez vos commandes.

Nous allons désormais créer une copie de notre fichier `test.txt`.
Déplacez-vous dans le dossier `edir` et effectuez un `cp test.txt test.txt.bck`.
Vérifiez vos opérations via `ls`.

### Bash history

Appuyez sur la touche directionnelle haut de votre clavier, dans le terminal. Que constatez-vous ?

Ouvrez le fichier `~/.bash_history`. Qu'en déduisez-vous ?

La recherche dans l'historique peut également se faire via l'appui sur `Ctrl+R`, qui attend ensuite une chaîne pour recherche la commande dans l'historique.

### Création et gestion des utilisateurs

Deux commandes existent pour créer des utilisateurs :
- useradd crée un utilisateur
- adduser démarre un assistant afin de créer un utilisateur

La première commande est "brute" et permet la personnalisation via des options (donc est très complète), alors que la seconde, plus simple, permet de créer un utilisateur classique.

Utilisez `adduser` afin de créer un nouvel utilisateur "test". Que se passe-t-il ?

Ce genre de commandes nécessite en effet une élévation de privilèges : d'être superuser ou root. Deux solutions s'offrent à nous :
- basculer en `root` via `su`
- demander à effectuer cette commande en tant que `root` via `sudo`

Effectuez donc un `sudo adduser test`. Notez bien son mot de passe !

Listez les fichiers et dossiers du dossier `/home`. Que constatez-vous ?

Pouvez-vous lister les fichiers et dossiers dans `/home/test` ? Pourquoi ?

## SSH

### Connexion

SSH est un protocole de sécurisation d'accès distance. Il permet la connexion distante à une machine, mais aussi l'empaquetage d'autres protocoles dans son propre protocole de communication.
Il existe plusieurs modes de connexion SSH :
- par hôte certifié
- par mot de passe
- par clef

SSH étant un protocole client / serveur, on parle d'un client SSH qui se connecte à un serveur SSH. Pour vous connecter sur un serveur SSH, ce serveur doit "tourner" et le port associé (généralement le 22) doit être accessible.

Sur le poste faisant office de **serveur** SSH, activez le service. Raspbian rend ça aisé, via un bouton dans le menu de configuration de Raspberry PI, onglet Interfaces. Assurez-vous bien de valider et fermer la fenêtre.

Testez votre connexion SSH depuis votre client (qui peut être un poste de travail sous Windows ou Linux ou encore un autre Raspberry) : `ssh <user>@<ip>` (en remplaçant évidemment `<user>` par le nom d'utilisateur à utiliser et `<ip>` par l'adresse IP du serveur).

Les fichiers de configuration du démon (la tâche de fond qui garde le serveur "vivant") SSH se situe dans le dossier `/etc/sshd`. En parcourant ces fichiers, modifiez le port d'écoute SSH, par défaut à 22, vers un autre port moins évident (au-dessus du port 2048). Testez votre modification.

### Clefs SSH

Jusqu'ici vous avez testé la connexion par mot de passe. Nous allons maintenant générer et utiliser des clefs SSH. Sur votre client, génerez une paire de clefs via la commande `ssh-keygen`.

> [!NOTE]
> SSH utilise des clefs asymétriques, via une paire de clefs : une privée et une publique.
> La clef privée est utilisée pour chiffrer et est garante de l'intégrité. Elle ne doit __**JAMAIS**__ être communiquée.

Enfin, envoyez votre clef publique vers le serveur via la commande `ssh-copy-id <user>@<ip>`. Comme cela est votre première connexion en envoyant les clefs, vous devrez saisir, pour cette fois, votre mot de passe. Une fois la connexion validée, les clefs seront utilisées, et vous n'aurez plus besoin de saisir votre mot de passe pour vous connecter entre ces machines !

> [!WARNING]
> Trois paramètres valident la connexion : la clef, l'utilisateur et l'IP. Si l'un des trois change, la connexion peut être refusée.
> Si votre IP ou l'IP du serveur change, vous aurez un avertissement concernant la connexion. Réflechissez à deux fois avant de valider !
