# TP5 : Blackjack

## 0. Contexte

### 0.1 Description du jeu de base

Au blackjack, l'objectif est d'atteindre une main au plus proche de 21 points, sans dépasser.
Pour participer à une manche, un joueur doit miser un nombre fixé de jetons.
Au début de la manche, la banque distribue deux cartes à chaque joueur, et tire deux cartes.
Les cartes des joueurs sont visibles. Seule la première carte de la banque est visible.

Chaque joueur décide entre :
- se coucher, récupérant la moitié de sa mise (possible uniquement avant de tirer d'autres cartes)
- doubler, doublant sa mise, et tirant une unique carte (possible uniquement avant de tirer d'autres cartes)
- tirer une ou plusieurs cartes (une après l'autre)
- arrêter de tirer des cartes

Ensuite, la banque révèle sa main, puis tire des cartes tant qu'elle est à 16 ou moins.

N'a été ici décrit que le jeu de base. Classiquement, le blackjack comporte également les éléments indiqués dans la partie 2.


### 0.2 Valeur de cartes

- de 2 à 9 : la valeur de la carte
- 10, valet, dame, roi : 10
- As : dépend de la situation - soit 1 soit 11 selon ce qui "arrange" la personne ayant la carte en main

Exemples :
- Dame, 4 = 14
- Valet, 3, As = 14
- 10, As = 21
- As, As = 12

A noter une légère nuance : un blackjack est une main à 21 points lors du premier tirage.
Une main à 21 points à un autre moment (après tirage), est "simplement" une main à 21 points.


### 0.3 Résultats

| Valeur des cartes du joueur (horizontal) et de la banque (vertical) |	Supérieur à 21 | 	Blackjack |	21 |	20 |	19 |	18 |	17 |	Inférieur à 17 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Supérieur à 21 |	Perte |	Gain de 3 pour 2 |	Gain de 1 pour 1 |	Gain de 1 pour 1 |	Gain de 1 pour 1 |	Gain de 1 pour 1 |	Gain de 1 pour 1 |	Gain de 1 pour 1 |
| Blackjack |	Perte |	Égalité |	Perte |	Perte |	Perte |	Perte |	Perte |	Perte |
| 21 	Perte |	Gain de 3 pour 2 |	Égalité |	Perte |	Perte |	Perte |	Perte |	Perte |
| 20 	Perte |	Gain de 3 pour 2 |	Gain de 1 pour 1 |	Égalité |	Perte |	Perte |	Perte |	Perte |
| 19 	Perte |	Gain de 3 pour 2 |	Gain de 1 pour 1 |	Gain de 1 pour 1 |	Égalité |	Perte |	Perte |	Perte |
| 18 	Perte |	Gain de 3 pour 2 |	Gain de 1 pour 1 |	Gain de 1 pour 1 |	Gain de 1 pour 1 |	Égalité |	Perte |	Perte |
| 17 	Perte |	Gain de 3 pour 2 |	Gain de 1 pour 1 |	Gain de 1 pour 1 |	Gain de 1 pour 1 |	Gain de 1 pour 1 |	Égalité |	Perte  |



## 1. Jeu de base

> [!Note]
> Le jeu sera intégralement en console.


## 1.1 Algorithme / Algorigramme

Préparez d'abord votre algorithme et/ou algorigramme.
Vous pouvez décomposer les différentes fonctionnalités en fonction.
Pensez à la partie "interface" (menu principal de jeu) !


## 1.2 Développement du programme

Implémentez votre algorithme et/ou algorigramme en langage Python.


## 2. Ajouts

Ces ajouts font partie du jeu, et ont été séparés dans l'activité pour la structurer.

### 2.1 Persistence (manches)

Ajoutez la persistence de l'argent entre les manches.


### 2.2 Persistence (continue)

Ajoutez la persistence de l'argent, même entre les parties.
Pour cela, vous devrez sauvegarder l'argent actuellement possédé dans un fichier.


### 2.3 Mise variable

Au blackjack, la mise de départ n'est qu'une... mise de départ.
Le joueur peut décider d'effectuer une mise entre la mise minimale et la maximale, définies par le casino.

Dans notre casino, à chaque victoire, la mise maximale est doublée.


### 2.4 Assurance

Lorsque la banque tire un As en première carte, le joueur peut décider de prendre une assurance.
Une assurance coûte exactement la moitié (arrondie au supérieur) de la mise de départ du joueur.
Si la banque a effectivement un blackjack, alors le joueur reçoit le double de son assurance (mais perd sa mise, sauf s'il a lui-même un blackjack également).
Si la banque n'a pas de blackjacl, alors le joueur perd "simplement" son assurance.


### 2.5 Joueurs supplémentaires

Implémentez les autres joueurs !
Testez d'abord en implémentant un autre joueur, puis 3 autres, puis un nombre variable pour chaque manche.
Chaque joueur peut se comporter de la même manière, selon vos choix d'implémentation.


### 2.6 Split

Implémentez le split. Si le joueur obtient deux cartes de même valeur, il peut "split" son jeu,
créant deux mains, chacune avec une des deux cartes, et la banque distribue une carte à chacune des deux mains.
Le joueur dirige alors les deux mains, indépendemment.


## 3. Extensions 

### 3.1 Intelligence des joueurs

Implémentez une intelligence des joueurs, via des schémas de comportement.
Inutile de partir dans des intelligences artificielles;
on peut imaginer un joueur prudent, qui se couche à partir de 15,
un joueur "tête brûlée" ne se couchant qu'à 18,
un joueur calculateur, qui va chercher le meilleur plan selon les cartes en jeu...


### 3.2 Statistiques

Implémentez un enregistrement des statistiques (parties gagnées, perdues...) dans un ou plusieurs fichiers dédiés.
La consultation de ces statistiques sera possible via le menu principal du jeu.


