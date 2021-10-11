# Fichiers
## Lecture dans un fichier

Une grande partie de l'information en *Data Science* est stockée dans des fichiers. Pour traiter cette information, vous devez le plus souvent lire ou écrire dans un ou plusieurs fichiers. *Python* possède pour cela de nombreux outils qui vous simplifient la vie.

###  Méthode `.readlines()`

Avant de passer à un exemple concret, créez un fichier dans un éditeur de texte que vous enregistrerez dans votre répertoire courant avec le nom zoo.txt et le contenu suivant :

```python
girafe
tigre
singe
souris
```

Ensuite, testez le code suivant dans l'interpréteur *Python* :

````python {.line-numbers}
>>> filin = open("zoo.txt", "r")
>>> filin
<_io.TextIOWrapper name='zoo.txt' mode='r' encoding='UTF-8'>
>>> filin.readlines()
['girafe\n', 'tigre\n', 'singe\n', 'souris\n']
>>> filin.close()
>>> filin.readlines()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: I/O operation on closed file.
````

Il y a plusieurs commentaires à faire sur cet exemple :

Ligne 1.  
L'instruction `open()` ouvre le fichier `zoo.txt`. Ce fichier est ouvert en lecture seule, comme l'indique le second argument `r` (pour *read*) de la fonction `open()`.  
Remarquez que le fichier n'est pas encore lu, mais simplement ouvert (un peu comme lorsqu'on ouvre un livre, mais qu'on ne l'a pas encore lu).  
Le curseur de lecture est prêt à lire le premier caractère du fichier. L'instruction `open("zoo.txt", "r")` suppose que le fichier `zoo.txt` est dans le répertoire depuis lequel l'interpréteur *Python* a été lancé.  
Si ce n'est pas le cas, il faut préciser le chemin d'accès au fichier. Par exemple, `/home/pierre/zoo.txt` pour *Linux* ou *Mac OS X* ou `C:\Users\pierre\zoo.txt` pour *Windows*.

Ligne 2.  
Lorsqu'on affiche le contenu de la variable filin, on se rend compte que *Python* la considère comme un objet de type fichier ouvert (ligne 3).

Ligne 4.  
Nous utilisons à nouveau la syntaxe `objet.méthode()`. Ici la méthode `.readlines()` agit sur l'objet `filin` en déplaçant le curseur de lecture du début à la fin du fichier, puis elle renvoie une liste contenant toutes les lignes du fichier (dans notre analogie avec un livre, ceci correspondrait à lire toutes les lignes du livre).

Ligne 6.  
Enfin, on applique la méthode `.close()` sur l'objet `filin`, ce qui, vous vous en doutez, ferme le fichier (ceci correspondrait à fermer le livre). Vous remarquerez que la méthode .close() ne renvoie rien mais modifie l'état de l'objet filin en fichier fermé. Ainsi, si on essaie de lire à nouveau les lignes du fichier, Python renvoie une erreur car il ne peut pas lire un fichier fermé (lignes 7 à 10).

Voici maintenant un exemple complet de lecture d'un fichier avec *Python*.  


```python
>>> filin = open("zoo.txt", "r")
>>> lignes = filin.readlines()
>>> lignes
['girafe\n', 'tigre\n', 'singe\n', 'souris\n']
>>> for ligne in lignes:
...     print(ligne)
...
girafe

tigre

singe

souris

>>> filin.close()
```


Vous voyez qu'en cinq lignes de code, vous avez lu, parcouru le fichier et affiché son contenu.  


> Remarque
>
> * Chaque élément de la liste `lignes` est une chaîne de caractères. C'est en effet sous forme de chaînes de caractères que *Python* lit le contenu d'un fichier.
> * Chaque élément de la liste lignes se termine par le caractère `\n`. Ce caractère un peu particulier correspond au « saut de ligne » qui permet de passer d'une ligne à la suivante. Ceci est codé par un caractère spécial que l'on représente par `\n`.
> * Par défaut, l'instruction *print()* affiche quelque chose puis revient à la ligne. Ce retour à la ligne dû à `print()` se cumule alors avec celui de la fin de ligne (`\n`) de chaque ligne du fichier et donne l'impression qu'une ligne est sautée à chaque fois.


Il existe en *Python* le mot-clé `with` qui permet d'ouvrir et de fermer un fichier de manière efficace. Si pour une raison ou une autre l'ouverture ou la lecture du fichier conduit à une erreur, l'utilisation de `with` garantit la bonne fermeture du fichier, ce qui n'est pas le cas dans le code précédent. Voici donc le même exemple avec `with` :


```python
>>> with open("zoo.txt", 'r') as filin:
...     lignes = filin.readlines()
...     for ligne in lignes:
...         print(ligne)
...
girafe

tigre

singe

souris

>>>
```


> Remarque
>
> * L'instruction `with` introduit un bloc d'indentation. C'est à l'intérieur de ce bloc que nous effectuons toutes les opérations sur le fichier.
> * Une fois sorti du bloc d'indentation, *Python* fermera automatiquement le fichier. Vous n'avez donc plus besoin d’utiliser la méthode `.close()`.


### Méthode `.read()`


Il existe d'autres méthodes que `.readlines()` pour lire (et manipuler) un fichier. Par exemple, la méthode `.read()` lit tout le contenu d'un fichier et renvoie une chaîne de caractères unique.


```python
>>> with open("zoo.txt", "r") as filin:
...     filin.read()
...
'girafe\ntigre\nsinge\nsouris\n'
>>>
```


### Méthode `.readline()`

La méthode `.readline()` (sans s à la fin) lit une ligne d'un fichier et la renvoie sous forme de chaîne de caractères. À chaque nouvel appel de `.readline()`, la ligne suivante est renvoyée. Associée à la boucle `while`, cette méthode permet de lire un fichier ligne par ligne.

```python   
>>> with open("zoo.txt", "r") as filin:
...     ligne = filin.readline()
...     while ligne != "":
...         print(ligne)
...         ligne = filin.readline()
...
girafe

tigre

singe

souris

>>>
```


### Itérations directe sur le fichier


*Python* essaie de vous faciliter la vie au maximum. Voici un moyen à la fois simple et élégant de parcourir un fichier.

```python
>>> with open("zoo.txt", "r") as filin:
...     for ligne in filin:
...         print(ligne)
...
girafe

tigre

singe

souris

>>>
```


L'objet `filin` est « itérable », ainsi la boucle `for` va demander à *Python* d'aller lire le fichier ligne par ligne.

> Conseils
> 
> Privilégiez cette méthode par la suite.


> Remarque
> 
> Les méthodes abordées précédemment permettent d'accéder au contenu d'un fichier, soit ligne par ligne (méthode `.readline()`), soit globalement en une seule chaîne de caractères (méthode `.read()`), soit globalement avec les lignes différenciées sous forme d'une liste de chaînes de caractères (méthode `.readlines()`). Il est également possible en *Python* de se rendre à un endroit particulier d'un fichier avec la méthode `.seek()` mais qui sort du cadre de cet ouvrage.


## Écriture dans un fichier


Écrire dans un fichier est aussi simple que de le lire. Voyez l'exemple suivant :

```python
>>> animaux2 = ["poisson", "abeille", "chat"]
>>> with open("zoo2.txt", "w") as filout:
...     for animal in animaux2:
...         filout.write(animal)
...
7
7
4
```


Quelques commentaires sur cet exemple :

Ligne 1.  
Création d'une liste de chaînes de caractères `animaux2`.

Ligne 2.  
Ouverture du fichier `zoo2.txt` en mode écriture, avec le caractère `w` pour *write*. L'instruction with crée un bloc d'instructions qui doit être indenté.

Ligne 3.  
Parcours de la liste `animaux2` avec une boucle `for`.

Ligne 4.  
À chaque itération de la boucle, nous avons écrit chaque élément de la liste dans le fichier. La méthode `.write()` s'applique sur l'objet `filout`. Notez qu'à chaque utilisation de la méthode `.write()`, celle-ci nous affiche le nombre d'octets (équivalent au nombre de caractères) écrits dans le fichier (lignes 6 à 8). Ceci est valable uniquement dans l'interpréteur, si vous créez un programme avec les mêmes lignes de code, ces valeurs ne s'afficheront pas à l'écran.

Si nous ouvrons le fichier `zoo2.txt` avec un éditeur de texte, voici ce que nous obtenons :

`poissonabeillechat`

Ce n'est pas exactement le résultat attendu car implicitement nous voulions le nom de chaque animal sur une ligne. Nous avons oublié d'ajouter le caractère fin de ligne après chaque nom d'animal.

Pour ce faire, nous pouvons utiliser l'écriture formatée :


```python
>>> animaux2 = ["poisson", "abeille", "chat"]
>>> with open("zoo2.txt", "w") as filout:
...     for animal in animaux2:
...         filout.write(f"{animal}\n")
...
8
8
5
```


Ligne 4.  
L'écriture formatée permet d'ajouter un retour à la ligne (`\n`) après le nom de chaque animal.

Lignes 6 à 8.  
Le nombre d'octets écrits dans le fichier est augmenté de 1 par rapport à l'exemple précédent car le caractère retour à la ligne compte pour un seul octet.


Le contenu du fichier `zoo2.txt` est alors :

```python
poisson
abeille
chat
```


Vous voyez qu'il est extrêmement simple en *Python* de lire ou d'écrire dans un fichier.


### Ouvrir deux fichiers avec l'instruction `with`


On peut avec l'instruction `with` ouvrir deux fichiers (ou plus) en même temps. Voyez l'exemple suivant :

```python
with open("zoo.txt", "r") as fichier1, open("zoo2.txt", "w") as fichier2:
    for ligne in fichier1:
        fichier2.write("* " + ligne)
```


Si le fichier `zoo.txt` contient le texte suivant :

```python
souris
girafe
lion
singe
```


alors le contenu de zoo2.txt sera :

```python
* souris
* girafe
* lion
* singe
```


Dans cet exemple, `with` permet une notation très compacte en s'affranchissant de deux méthodes `.close()`.

Sachez que l'instruction with est plus générale et est utilisable dans d'autres contextes.
