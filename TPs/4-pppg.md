# TP4 : Plus petit plus grand

## 0. Contexte et objectifs

L'objectif de ce TP est de reprendre / démarrer le développement en Python.

Le langage Python est supposé [être mis en pratique depuis la seconde](https://eduscol.education.fr/1670/programmes-et-ressources-en-sciences-numeriques-et-technologie-voie-gt) si ce n'est avant.

Pour ce TP, nous réalisons d'abord quelques exercices simples avant d'implémenter un "plus petit plus grand", un jeu simpliste.

Ces exercices sont utiles conjugués à l'usage de la [documentation Python](https://docs.python.org/3.13/index.html) ainsi qu'aux bases du développement.

Si vous souhaitez en connaître plus sur Python, le [tutoriel de la documentation](https://docs.python.org/3.13/tutorial/index.html) fait une grande passe sur l'ensemble du langage.

## Pré-requis

La majorité de cette section est identique (ou similaire) aux précédents TPs.

### Système

Python fonctionne sous la majorité des systèmes, et est parfois livré de base sous les systèmes Linux.

### Installation Python

> [!Caution]
> Il existe deux versions majeures de Python.
> Python2 est historiquement présent et incompatible avec Python3.
> Seul Python3 nous intéresse.

Assurez-vous que Python est installé.

#### Linux

Python est disponible via aptitude ou n'importe quel package manager natif. Assurez-vous d'installer la version à jour de Python3.

#### Windows

Le [site de Python propose des installeurs](https://www.python.org/downloads/). Assurez-vous de prendre la version à jour de Python3.
Lors de l'installation, vous pouvez activer IDLE (l'éditeur de Python) si vous le souhaitez. Si PIP est optionnel, assurez-vous de l'activer.

### PIP

PIP est le gestionnaire de paquets de Python. Si vous avez installé Python via l'installeur, PIP est probablement déjà installé.
Sous Linux, vous pouvez installer `python3-pip` si ce n'est déjà fait.

Les packages PIP sont gérés par la commande `pip`.

### venv

Python peut fonctionner avec un système d'environnement virtuel ou venv.
Il est recommendé, pour un nouveau projet, d'utiliser un venv. Vous avez normalement, au fil des projets précédents 

La commande `py -m venv .venv` va créer un virtual environnement dans un dossier caché nommé `.venv`.

Une fois le venv créé, pensez que vous devez l'activez.
Plus d'informations sont disponibles sur [le site de Python](https://docs.python.org/3/library/venv.html) ainsi que sur les différents TPs déjà réalisés.

Si créer un venv peut être fait une seule fois,
l'activer est nécessaire à chaque fois qu'on ouvre un nouveau contexte d'exécution,
donc à chaque nouvelle console / terminal.

## Syntaxe de base

### Main et imports

Créez un fichier `hello.py` contenant le code suivant :

```py
print("Hello World !")
```

Testez l'exécution de votre code : `python3 hello.py`.

> [!Note]
> `print()` est une fonction native de Python,
> permettant l'affichage d'un contenu en console.
> Une fonction est un morceau de code
> dédié à l'accomplissement d'une mission,
> pouvant prendre des paramètres en entrée,
> et pouvant renvoyer une valeur.
> 
> Ici, on ne sait pas comment `print` fonctionne,
> mais uniquement ce qu'elle fait et ce dont elle a besoin.

Modifiez votre fichier `hello.py` pour utiliser une variable :

```py
h = "Hello World !"
print(h)
```

Et testez votre fichier.

> [!Note]
> `h` est ici une variable.
> Une variable est un espace mémoire réservé,
> comportant un nom, et pouvant posséder un type et une valeur,
> qui peuvent changer au fil des instructions.

Créons un nouveau fichier `rnd.py` et importons une librairie afin de générer des nombres aléatoires.

```py
import random

x = random.randint(0, 100)
print(x)
```

Testez votre fichier.

> [!Tip]
> Il existe un grand nombre de façons d'importer des librairies,
> et chaque façon a ses avantages et inconvénients.

Remplacez l'import par `from random import randint`
afin d'importer uniquement la méthode `randint`
et d'éviter d'avoir à spécifier le nom de la librairie lors de l'appel.

Enfin, dans votre fichier `hello.py`, importez `rnd`, puis testez `hello.py`.

Que constatez-vous ?

> [!Caution]
> Python exécute le code séquentiellement.
> Chaque instruction est lue et exécutée l'une après l'autre.

Remplacez le contenu de votre `hello.py` par le code suivant, afin de tenter d'utiliser la variable `x` définie dans `rnd` :

```py
import rnd

print("hello world")
print(x)
```

Que constatez-vous ?

> [!Note]
> Il n'existe pas de notion de `main` en Python, du [moins pas de la même manière qu'en C](https://docs.python.org/3.13/library/__main__.html).
> Le fichier que vous exécutez via la commande `python` est "le" main.
> Chaque fichier et dossier peut être considéré par python comme une librairie.
> 
> La portée des variables, fonctions... est limitée à la librairie de définition,
> et chaque élément doit être explicitement importé pour être utilisé hors de la librairie.

Comme vous aviez importé `randint` depuis la librairie `random`, importez `x` depuis la librairie `rnd` et testez à nouveau votre code.
Que constatez-vous ?

Une fois vos constats notés, vous pouvez supprimer les deux fichiers.

### Espaces blancs et structures

Créez un fichier `even.py`, dans lequel vous allez placer le code suivant :

```py
from random import randint

x = randint(0, 100)
print(x)
if x % 2 :
    print("Impair !")
else:
    print("Pair !")
```

Testez ce code.

Tentez de modifiez votre code pour introduire des espaces blancs de taille différente:

```py
if x % 2 :
    print("Impair !")
  print(".")
else:
    print("Pair !")
```

Que constatez-vous ?

> [!Note]
> Historiquement, afin de forcer les développeurs à utiliser des formes lisibles de blocs (conditions, structures, boucles...),
> Python a forcé l'usage d'espaces blancs afin d'indenter les éléments de structures.
> Ainsi, un bloc doit rester indenté de la même manière sur toute sa longueur.
> Si des [normes de bonne pratique existent](https://peps.python.org/pep-0008/), beaucoup d'applications Python les ignorent.

La fonction `range` permet de créer une liste entre bornes. Par exemple, `range(10)` va créer une liste de 10 éléments (`[0, 10[`).
Conjugué avec la boucle `for`, cela peut permettre de réaliser des boucles de `n` éléments:

```py
for i in range(n):
    print(i) # va afficher 0, puis 1, puis 2... jusque N non-compris
```

Modifiez votre code pour lancer la création d'un nombre aléatoire et l'affichage de si pair ou impair 15 fois de suite
(le nombre aléatoire doit changer à chaque passage de la boucle).

<details>
    <summary>Proposition de solution</summary>
    
```py
from random import randint

for i in range(15):
    x = randint(0, 100)
    print(x)
    if x % 2 :
        print("Impair !")
    else:
        print("Pair !")
```

</details>

Vous pouvez supprimer le fichier `even.py`.

### Saisie utilisateur

La fonction `input` permet de demander une saisie utilisateur.

C'est une fonction bloquante : lorsqu'elle est appellée,
le script est en pause jusqu'à ce que l'utilisateur effectue et valide (avec entrée) une saisie dans la console.

Créez un fichier `saisie.py` avec le contenu suivant :

```py
x = input("Saisissez un nombre : ")
x = x + 1
print(x)
```

Réalisez le test du fichier. Que constatez-vous ?

> [!important]
> Python n'autorise pas le mélange de types sans contrôle
> et requiert que vous réalisiez vous même explicitement
> des conversions de type.
> En cas d'erreur de ce type, une exception est levée.

Tentons de forcer le type de x comme étant un entier.
La fonction `str()` permet de forcer la conversion d'une variable en chaîne de caractères.
Dans la même idée, la fonction `int()` permet de faire la même chose vers un entier.

Modifiez votre fichier `saisie.py` pour forcer la conversion de `x` en entier.
Testez votre code, en saisissant un entier, puis en saisissant une chaîne, comme "test". Que constatez-vous ?

> [!important]
> Les erreurs sont des exceptions.
> Une exception est un objet spécial,
> qui peut être "attrapée", afin de gérer les erreurs,
> via l'usage d'un bloc `try..except`.
>
> Tout ce qui est dans un bloc `try` est considéré comme
> susceptible de jeter une exception.
> Lorsqu'une exception est jetée, l'exécution du bloc `try` s'interrompt,
> et le bloc `except` correspondant s'exécute.


Exemple :

```py
    try:
        x = float(input("Please enter a number: "))
        print(x) # ne s'exécutera pas si la ligne précédente lance une erreur
    except ValueError:
        print("Oops!  That was no valid number.  Try again...")
```

Ajoutez un contrôle dans votre code, afin de vous assurer que la saisie effectuée par l'utilisateur est bien un nombre,
et si ça n'est pas le cas, de lui demander à nouveau une saisie (et ainsi de suite).

> [!Tip]
> Si vous en avez besoin, sachez que les booléens en Python sont `True` et `False`.
> Attention aux majuscules !

<details>
    <summary>Proposition de solution</summary>
    
```py
saisieInvalide = True
while saisieInvalide:
    try:
        x = int(input("Saisissez un entier : "))
        saisieInvalide = False
    except:
        print("Saisie invalide")
        saisieInvalide = True
```

</details>

Ajoutons l'affichage de l'entier saisi.
Nous allons utiliser la syntaxe fstring,
qui consiste à préfixer une chaîne avec "f" afin d'activer le formatage : `print(f'Nombre saisi : {x}.')`.

## Plus petit plus grand

Vous avez désormais tout le nécessaire pour réaliser le plus petit plus grand.

Lorsque le jeu se lance, le programme choisit un nombre aléatoire entre 1 et 1000.
L'utilisateur démarre avec 10 points.
A chaque tour, on demande à l'utilisateur de saisir un nombre.
Si le nombre saisi est invalide, on lui redemande.
Si le nombre est plus petit ou plus grand,
l'utilisateur perd un point,
et le programme affiche si c'est plus grand ou plus petit.
Si le nombre est égal, l'utilisateur gagne.

### Extension : menu

Implémentez un menu basique en console
pour donner la possibilité au joueur de relancer une partie, ou de quitter.

### Extension : difficulté

Ajoutez différents modes de difficulté :
- facile (score démarrant à 10, nombre de 1 à 100)
- medium (score démarrant à 30, nombre de 1 à 1000)
- difficile (score démarrant à 80, nombre de 1 à 10000)

Le mode de difficulté doit pouvoir être choisi via le menu.

### Extension : score

Ajoutez la sauvegarde du score dans un fichier `score.txt`.
