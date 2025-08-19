# TP7 : Mastermind

Rappels des principes du jeu

Un code secret de N éléments (couleurs) est décidé.
Un nombre de tentatives de décodage par déduction est possible.
Au bout de ces tentatives, la personne jouant a perdu.
Le code doit être trouvé avant d'épuiser toutes les tentatives.
A chaque tentative est affiché nombre d'éléments trouvés dans la combinaison,
soit à une position correcte soit incorrecte.
- Correct : bonne couleur au bon emplacement
- Partiel : bonne couleur au mauvais emplacement

Consignes

Le projet peut être réalisé en solo ou en équipe de deux maximum.
Le versionning est obligatoire, sur Github, sous le nom "polytech-dijon-soutien".
L'auteur de chaque commit doit être clairement identifiable.
Les outils pour réaliser vos commits sont à votre discrétion.
Aucun commit = aucun travail réalisé !

Vous devez être capable d'expliquer l'intégralité de votre code.
A cette fin, l'usage d'IA génératives est déconseillé.

Etapes

MVP

Le jeu se fait en console (saisie et sortie).
Chaque couleur est codifiée par une lettre parmi
> Red, Green, Blue, Yellow, Purple, White
ou
> Rouge, Vert, Bleu, Jaune, Mauve, Noir

Le code doit être choisi au hasard.
Il peut comporter, deux, trois ou même quatre fois la même couleur.
Tant que le joueur n’a pas trouvé le code ou effectué 12 essais infructueux, le jeu continue.

Au début du jeu, un rappel des couleurs est effectué.
Chaque essai comporte une question à l’utilisateur, qui peut saisir le code sous la forme des quatre couleurs.
> Par exemple « RGYP »


A chaque essai, un retour est fait sous la forme suivante:
« Correct : X | Partiel : Y » en remplaçant X et Y par les valeurs adéquates

A la fin, le score est indiqué, celui-ci étant calculé comme `12 - nombre de tentatives`.


Modularité

Il doit être aisé de changer les couleurs disponibles.
A la fois les couleurs, leur « lettre » mais aussi leur nombre.
Il doit être aisé de changer le nombre d’éléments du code secret.
Il doit être aisé de changer le nombre maximal de tentatives.
Ces changements se font dans le code; mais il doivent pouvoir être réalisés en moins de 5 minutes par un néophyte.


Rejouabilité

Il doit être possible de rejouer autant de fois que souhaité;
pour cela, prévoir une option « rejouer ».
Le score doit être conservé;
pour cela, penser à un stockage en fichier.

Chaque statistique peut être enregistré dans un fichier à part.
- nombre de parties
- score total

Les fichiers en question doivent être « cachés » dans le même dossier que le jeu.
On se contentera d'un masquage standard Linux.

Les statistiques seront affichées au lancement du jeu et en fin de partie.
Au lancement, on pourra:
- Jouer
- Remettre à zéro les statistiques
- Quitter

Après une partie terminée, on pourra:
- Rejouer
- Remettre à zéro les statistiques
- Quitter


Mode inversé

Ajouter la possibilité de résolution automatique
Le joueur humain choisit une combinaison
Par essai, d’abord aléatoire, puis par déduction, le programme tente de trouver la combinaison correcte
Pour permettre une chance, un facteur aléatoire sera rajouté quant au choix d’une « bonne » décision ou non

Le score final de chaque partie est alors décidé en soustrayant le score « humain » avec le score « programme »


GUI

Utilisez pygame pour ajouter une GUI sur votre programme.


