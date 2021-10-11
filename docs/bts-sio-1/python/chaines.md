# Plus sur les chaînes de caractères

## Chaînes de caractères et listes


Les chaînes de caractères peuvent être considérées comme des listes (de caractères) un peu particulières :

```python
>>> animaux = "girafe tigre"
>>> animaux
'girafe tigre'
>>> len(animaux)
12
>>> animaux[3]
'a'
```


Nous pouvons donc utiliser certaines propriétés des listes comme les tranches :

```python
>>> animaux = "girafe tigre"
>>> animaux[0:4]
'gira'
>>> animaux[9:]
'gre'
>>> animaux[:-2]
'girafe tig'
>>> animaux[1:-2:2]
'iaetg'
```

Mais a contrario des listes, les chaînes de caractères présentent toutefois une différence notable, ce sont des listes non modifiables. Une fois une chaîne de caractères définie, vous ne pouvez plus modifier un de ses éléments. Le cas échéant, Python renvoie un message d'erreur :

```python
>>> animaux = "girafe tigre"
>>> animaux[4]
'f'
>>> animaux[4] = "F"
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
```

Par conséquent, si vous voulez modifier une chaîne de caractères, vous devez en construire une nouvelle. Pour cela, n'oubliez pas que les opérateurs de concaténation (+) et de duplication (`*`) (introduits dans le chapitre 2 Variables) peuvent vous aider. Vous pouvez également générer une liste, qui elle est modifiable, puis revenir à une chaîne de caractères (voir plus bas).


### Caractères spéciaux


Il existe certains caractères spéciaux comme `\n` que nous avons déjà vu (pour le retour à la ligne). Le caractère \t produit une tabulation. Si vous voulez écrire des guillemets simples ou doubles et que ceux-ci ne soient pas confondus avec les guillemets de déclaration de la chaîne de caractères, vous pouvez utiliser \' ou \".

```python
>>> print("Un retour à la ligne\npuis une tabulation\t puis un guillemet\"")
Un retour à la ligne
puis une tabulation     puis un guillemet"
>>> print('J\'affiche un guillemet simple')
J'affiche un guillemet simple
```


Vous pouvez aussi utiliser astucieusement des guillemets doubles ou simples pour déclarer votre chaîne de caractères :

```python
>>> print("Un brin d'ADN")
Un brin d'ADN
>>> print('Python est un "super" langage de programmation')
Python est un "super" langage de programmation
```


Quand on souhaite écrire un texte sur plusieurs lignes, il est très commode d'utiliser les guillemets triples qui conservent le formatage (notamment les retours à la ligne) :

```python
>>> x = """souris
... chat
... abeille"""
>>> x
'souris\nchat\nabeille'
>>> print(x)
souris
chat
abeille
```


Attention, les caractères spéciaux n'apparaissent intérprétés que lorsqu'ils sont utilisés avec la fonction print(). Par exemple, le \n n'apparait comme un saut de ligne que lorsqu'il est dans une chaîne de caractères passée à la fonction print() :

```python
>>> "bla\nbla"
'bla\nbla'
>>> print("bla\nbla")
bla
bla
```


### Préfixe de chaîne de caractères

Nous avons vu au chapitre 3 la notion de f-string. Il s'agit d'un mécanisme pour formater du texte au sein d'une chaîne de caractères. Par exemple :

```python
>>> var = "f-string"
>>> f"voici une belle {var}"
'voici une belle f-string'
```


Que signifie le f que l'on accole aux guillements de la chaîne de caractères ? Celui-ci est appelé « préfixe de chaîne de caractères » ou stringprefix.

Remarque

Un stringprefix modifie la manière dont Python va interpréter la dite string. Celui-ci doit être systématiquement « collé » à la chaîne de caractères, c'est-à-dire pas d'espace entre les deux.

Il existe différents stringprefixes en Python, nous vous montrons ici les deux qui nous apparaissent les plus importants.

    Le préfixe r mis pour raw string qui force la non-interprétation des caractères spéciaux :

```python
>>> s = "Voici un retour à la ligne\nEt là une autre ligne"
>>> s
'Voici un retour à la ligne\nEt là une autre ligne'
>>> print(s)
Voici un retour à la ligne
Et là une autre ligne
>>> s = r"Voici un retour à la ligne\nEt là une autre ligne"
>>> s
'Voici un retour à la ligne\\nEt là une autre ligne'
>>> print(s)
Voici un retour à la ligne\nEt là une autre ligne
```


L'ajout du r va forcer Python à ne pas interpréter le \n comme un retour à la ligne, mais comme un backslash littéral suivi d'un n. Quand on demande à l'interpréteur d'afficher cette chaîne de caractères, celui-ci met deux backslashes pour signifier qu'il s'agit d'un backslash littéral (le premier échappe le second). Finalement, l'utilisation de la syntaxe r"Voici un retour à la ligne\nEt là une autre ligne" renvoie une chaîne de caractères normale, puisqu'on voit ensuite que le r à disparu lorsqu'on demande à Python d'afficher le contenu de la variable s. Comme dans var = 2 + 2, d'abord Python évalue 2 + 2 et c'est ce résultat qui est affecté à la variable var. Enfin, on notera que seule l'utilisation du print() mène à l'interprétation des caractères spéciaux comme \n, comme expliqué dans la rubrique précédente.

Les caractères spéciaux non interprétés dans les raw strings sont de manière générale tout ce dont le backslash modifie la signification, par exemple un \n, un \t, etc.

    Le préfixe f mis pour formatted string qui met en place l'écriture formattée comme vue au chapitre 3 Affichage :

```python
>>> animal = "renard"
>>> animal2 = "poulain"
>>> s = f"Le {animal} est un animal gentil\nLe {animal2} aussi"
>>> s
'Le renard est un animal gentil\nLe poulain aussi'
>>> print(s)
Le renard est un animal gentil
Le poulain aussi
>>> s = "Le {animal} est un animal gentil\nLe {animal2} aussi"
>>> s
'Le {animal} est un animal gentil\nLe {animal2} aussi'
>>> print(s)
Le {animal} est un animal gentil
Le {animal2} aussi
```


La f-string remplace le contenu des variables situées entre les accolades et interprète le \n comme un retour à la ligne. Pour rappel, consultez le chapitre 3 si vous souhaitez plus de détails sur le fonctionnement des f-strings.

Conseils

Il existe de nombreux autres détails concernant les préfixes qui vont au delà de ce cours. Pour en savoir plus, vous pouvez consulter la documentations officielle.

10.5 Méthodes associées aux chaînes de caractères

Voici quelques méthodes spécifiques aux objets de type str :

```python
>>> x = "girafe"
>>> x.upper()
'GIRAFE'
>>> x
'girafe'
>>> 'TIGRE'.lower()
'tigre'
```


Les méthodes .lower() et .upper() renvoient un texte en minuscule et en majuscule respectivement. On remarque que l'utilisation de ces méthodes n'altère pas la chaîne de caractères de départ mais renvoie une chaîne de caractères transformée.

Pour mettre en majuscule la première lettre seulement, vous pouvez faire :

```python
>>> x[0].upper() + x[1:]
'Girafe'
```


ou plus simplement utiliser la méthode adéquate :

```python
>>> x.capitalize()
'Girafe'
```


Il existe une méthode associée aux chaînes de caractères qui est particulièrement pratique, la méthode .split() :

```python
>>> animaux = "girafe tigre singe souris"
>>> animaux.split()
['girafe', 'tigre', 'singe', 'souris']
>>> for animal in animaux.split():
...     print(animal)
...
girafe
tigre
singe
souris
```


La méthode .split() découpe une chaîne de caractères en plusieurs éléments appelés champs, en utilisant comme séparateur n'importe quelle combinaison « d'espace(s) blanc(s) ».

Définition

Un espace blanc (whitespace en anglais) correspond aux caractères qui sont invisibles à l'œil, mais qui occupent de l'espace dans un texte. Les espaces blancs les plus classiques sont l'espace, la tabulation et le retour à la ligne.

Il est possible de modifier le séparateur de champs, par exemple :

```python
>>> animaux = "girafe:tigre:singe::souris"
>>> animaux.split(":")
['girafe', 'tigre', 'singe', '', 'souris']
```


Attention, dans cet exemple, le séparateur est un seul caractères « : » (et non pas une combinaison de un ou plusieurs :) conduisant ainsi à une chaîne vide entre singe et souris.

Il est également intéressant d'indiquer à .split() le nombre de fois qu'on souhaite découper la chaîne de caractères avec l'argument maxsplit :

```python
>>> animaux = "girafe tigre singe souris"
>>> animaux.split(maxsplit=1)
['girafe', 'tigre singe souris']
>>> animaux.split(maxsplit=2)
['girafe', 'tigre', 'singe souris']
```


La méthode .find(), quant à elle, recherche une chaîne de caractères passée en argument :

```python
>>> animal = "girafe"
>>> animal.find("i")
1
>>> animal.find("afe")
3
>>> animal.find("z")
-1
>>> animal.find("tig")
-1
```


Si l'élément recherché est trouvé, alors l'indice du début de l'élément dans la chaîne de caractères est renvoyé. Si l'élément n'est pas trouvé, alors la valeur -1 est renvoyée.

Si l'élément recherché est trouvé plusieurs fois, seul l'indice de la première occurrence est renvoyé :

```python
>>> animaux = "girafe tigre"
>>> animaux.find("i")
1
```


On trouve aussi la méthode .replace() qui substitue une chaîne de caractères par une autre :

```python
>>> animaux = "girafe tigre"
>>> animaux.replace("tigre", "singe")
'girafe singe'
>>> animaux.replace("i", "o")
'gorafe togre'
```


La méthode .count() compte le nombre d’occurrences d'une chaîne de caractères passée en argument :

```python
>>> animaux = "girafe tigre"
>>> animaux.count("i")
2
>>> animaux.count("z")
0
>>> animaux.count("tigre")
1
```


La méthode .startswith() vérifie si une chaîne de caractères commence par une autre chaîne de caractères :

```python
>>> chaine = "Bonjour monsieur le capitaine !"
>>> chaine.startswith("Bonjour")
True
>>> chaine.startswith("Au revoir")
False
```


Cette méthode est particulièrement utile lorsqu'on lit un fichier et que l'on veut récupérer certaines lignes commençant par un mot-clé. Par exemple dans un fichier PDB, les lignes contenant les coordonnées des atomes commencent par le mot-clé ATOM.

Enfin, la méthode .strip() permet de « nettoyer les bords » d'une chaîne de caractères :

```python
>>> chaine = "  Comment enlever les espaces au début et à la fin ?       "
>>> chaine.strip()
'Comment enlever les espaces au début et à la fin ?'
```


La méthode .strip() enlève les espaces situés sur les bords de la chaîne de caractère mais pas ceux situés entre des caractères visibles. En réalité, cette méthode enlève n'importe quel combinaison « d'espace(s) blanc(s) » sur les bords, par exemple :

```python
>>> chaine = "  \tfonctionne avec les tabulations et les retours à la ligne\n"
>>> chaine.strip()
'fonctionne avec les tabulations et les retours à la ligne'
```


La méthode .strip() est très pratique quand on lit un fichier et qu'on veut se débarrasser des retours à la ligne.


## Extraction de valeurs numériques d'une chaîne de caractères


Une tâche courante en Python est de lire une chaîne de caractères (provenant par exemple d'un fichier), d'extraire des valeurs de cette chaîne de caractères pour ensuite les manipuler.

On considère par exemple la chaîne de caractères val :

```python
>>> val = "3.4 17.2 atom"
```


On souhaite extraire les valeurs 3.4 et 17.2 pour ensuite les additionner.

Dans un premier temps, on découpe la chaîne de caractères avec la méthode .split() :

```python
>>> val2 = val.split()
>>> val2
['3.4', '17.2', 'atom']
```


On obtient alors une liste de chaînes de caractères. On transforme ensuite les deux premiers éléments de cette liste en floats (avec la fonction float()) pour pouvoir les additionner :

```python
>>> float(val2[0]) + float(val2[1])
20.599999999999998
```


Remarque

Retenez bien l'utilisation des instructions précédentes pour extraire des valeurs numériques d'une chaîne de caractères. Elles sont régulièrement employées pour analyser des données extraites d'un fichier.

10.7 Conversion d'une liste de chaînes de caractères en une chaîne de caractères

On a vu dans le chapitre 2 Variables la conversion d'un type simple (entier, float et chaîne de caractères) en un autre avec les fonctions int(), float() et str(). La conversion d'une liste de chaînes de caractères en une chaîne de caractères est particulière puisqu'elle fait appelle à la méthode .join().

```python
>>> seq = ["A", "T", "G", "A", "T"]
>>> seq
['A', 'T', 'G', 'A', 'T']
>>> "-".join(seq)
'A-T-G-A-T'
>>> " ".join(seq)
'A T G A T'
>>> "".join(seq)
'ATGAT'
```


Les éléments de la liste initiale sont concaténés les uns à la suite des autres et intercalés par un séparateur qui peut être n'importe quelle chaîne de caractères. Ici, on a utilisé un tiret, un espace et rien (une chaîne de caractères vide).

Attention, la méthode .join() ne s'applique qu'à une liste de chaînes de caractères.

```python
>>> maliste = ["A", 5, "G"]
>>> " ".join(maliste)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: sequence item 1: expected string, int found
```


On espère qu'après ce petit tour d'horizon vous serez convaincu de la richesse des méthodes associées aux chaînes de caractères. Pour avoir une liste exhaustive de l'ensemble des méthodes associées à une variable particulière, vous pouvez utiliser la fonction dir().

```python
>>> animaux = "girafe tigre"
>>> dir(animaux)
['__add__', '__class__', '__contains__', '__delattr__', '__dir__',
'__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '_
_getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '_
_init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mo
d__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__'
, '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__',
'__str__', '__subclasshook__', 'capitalize', 'casefold', 'center',
'count', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'for
mat_map', 'index', 'isalnum', 'isalpha', 'isdecimal', 'isdigit', 'i
sidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'is
title', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans',
 'partition', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition',
 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip',
 'swapcase', 'title', 'translate', 'upper', 'zfill']
```


Pour l'instant, vous pouvez ignorer les méthodes qui commencent et qui se terminent par deux tirets bas (underscores) `__`.

Vous pouvez également accéder à l'aide et à la documentation d'une méthode particulière avec help(), par exemple pour la méthode .split() :

```python
>>> help(animaux.split)
Help on built-in function split:

split(...)
    S.split([sep [,maxsplit]]) -> list of strings

    Return a list of the words in the string S, using sep as the
    delimiter string.  If maxsplit is given, at most maxsplit
    splits are done. If sep is not specified or is None, any
    whitespace string is a separator.
(END)
```


Attention à ne pas mettre les parenthèses à la suite du nom de la méthode. L'instruction correcte est help(animaux.split) et non pas help(animaux.split()).
