# Fonctions

## Principe et généralités

En programmation, les **fonctions** sont très utiles pour réaliser plusieurs fois la même opération au sein d'un programme. Elles rendent également le code plus lisible et plus clair en le fractionnant en blocs logiques.
Vous connaissez déjà certaines fonctions *Python*. Par exemple `math.cos(angle)` du module `math` renvoie le cosinus de la variable `angle` exprimé en radian. Vous connaissez aussi des fonctions internes à *Python* comme `range()` ou `len()`. Pour l'instant, une fonction est à vos yeux une sorte de « boîte noire » (voir figure 1) :

1.    À laquelle vous passez aucune, une ou plusieurs variable(s) entre parenthèses. Ces variables sont appelées **arguments**. Il peut s'agir de n'importe quel type d'objet Python.
1.    Qui effectue une action.
1.    Et qui renvoie un objet *Python* ou rien du tout.

Fonctionnement schématique d'une fonction.

Par exemple, si vous appelez la fonction `len()` de la manière suivante :

```python
>>> len([0, 1, 2])
3
```

voici ce qui se passe :

1.    vous appelez `len()` en lui passant une liste en argument (ici la liste `[0, 1, 2]`) ;
1.    la fonction calcule la longueur de cette liste ;
1.    elle vous renvoie un entier égal à cette longueur.

Autre exemple, si vous appelez la méthode `ma_liste.append()` (n'oubliez pas, une **méthode** est une **fonction** qui agit sur l'objet auquel elle est attachée par un point) :

```python
>>> ma_liste.append(5)
```

1.    Vous passez l'entier 5 en argument ;
1.    la méthode `append()` ajoute l'entier 5 à l'objet `ma_liste` ;
1.    et elle ne renvoie rien.

Aux yeux du programmeur au contraire, une fonction est une portion de code effectuant une suite d'instructions bien particulière. Mais avant de vous présenter la syntaxe et la manière de construire une fonction, revenons une dernière fois sur cette notion de « boîte noire » :

*    Une fonction effectue une tâche. Pour cela, elle reçoit éventuellement des arguments et renvoie éventuellement quelque chose. L'algorithme utilisé au sein de la fonction n'intéresse pas directement l'utilisateur. Par exemple, il est inutile de savoir comment la fonction math.cos() calcule un cosinus. On a juste besoin de savoir qu'il faut lui passer en argument un angle en radian et qu'elle renvoie le cosinus de cet angle. Ce qui se passe à l'intérieur de la fonction ne regarde que le programmeur.
*    Chaque fonction effectue en général une tâche unique et précise. Si cela se complique, il est plus judicieux d'écrire plusieurs fonctions (qui peuvent éventuellement s'appeler les unes les autres). Cette modularité améliore la qualité générale et la lisibilité du code. Vous verrez qu'en Python, les fonctions présentent une grande flexibilité.

Pour finir sur les généralités, nous avons utilisé dans la Figure 1 le terme **programme principal** (*main* en anglais) pour désigner l'endroit depuis lequel on appelle une fonction (on verra plus tard que l'on peut en fait appeler une fonction de n'importe où). Le programme principal désigne le code qui est exécuté lorsqu'on lance le script *Python*, c'est-à-dire toute la suite d'instructions en dehors des fonctions. En général, dans un script *Python*, on écrit d'abord les fonctions puis le programme principal. Nous aurons l'occasion de revenir sur cette notion de programme principal plus tard dans ce chapitre ainsi que dans le chapitre 12 *Plus sur les fonctions*.

## Définition

Pour définir une fonction, *Python* utilise le mot-clé `def`. Si on souhaite que la fonction renvoie quelque chose, il faut utiliser le mot-clé `return`. Par exemple :

```python
>>> def carre(x):
...     return x**2
...
>>> print(carre(2))
4
```

Notez que la syntaxe de `def` utilise les deux-points comme les boucles `for` et `while` ainsi que les tests `if`, un bloc d’instructions est donc attendu. De même que pour les boucles et les tests, l'**indentation** de ce bloc d'instructions (qu'on appelle le corps de la fonction) est **obligatoire**.

Dans l'exemple précédent, nous avons passé un argument à la fonction `carre()` qui nous a renvoyé (ou retourné) une valeur que nous avons immédiatement affichée à l'écran avec l'instruction `print()`. Que veut dire valeur renvoyée ? Et bien cela signifie que cette dernière est récupérable dans une variable :

```python
>>> res = carre(2)
>>> print(res)
4
```

Ici, le résultat renvoyé par la fonction est stocké dans la variable `res`. Notez qu'une fonction ne prend pas forcément un argument et ne renvoie pas forcément une valeur, par exemple :

```python
>>> def hello():
...     print("bonjour")
...
>>> hello()
bonjour
```

Dans ce cas la fonction, `hello()` se contente d'afficher la chaîne de caractères `"bonjour"` à l'écran. Elle ne prend aucun argument et ne renvoie rien. Par conséquent, cela n'a pas de sens de vouloir récupérer dans une variable le résultat renvoyé par une telle fonction. Si on essaie tout de même, *Python* affecte la valeur `None` qui signifie rien en anglais:

```python
>>> var = hello()
bonjour
>>> print(var)
None
```

Ceci n'est pas une faute car *Python* n'émet pas d'erreur, toutefois cela ne présente, la plupart du temps, guère d'intérêt.

## Passage d'arguments

Le nombre d'arguments que l'on peut passer à une fonction est variable. Nous avons vu ci-dessus des fonctions auxquelles on passait 0 ou 1 argument. Dans les chapitres précédents, vous avez rencontré des fonctions internes à *Python* qui prenaient au moins 2 arguments. Souvenez-vous par exemple de `range(1, 10)` ou encore `range(1, 10, 2)`. Le nombre d'argument est donc laissé libre à l'initiative du programmeur qui développe une nouvelle fonction.
Une particularité des fonctions en *Python* est que vous n'êtes pas obligé de préciser le type des arguments que vous lui passez, dès lors que les opérations que vous effectuez avec ces arguments sont valides. *Python* est en effet connu comme étant un langage au « typage dynamique », c'est-à-dire qu'il reconnaît pour vous le type des variables au moment de l'exécution. Par exemple :

```
>>> def fois(x, y):
...     return x*y
...
>>> fois(2, 3)
6
>>> fois(3.1415, 5.23)
16.430045000000003
>>> fois("to", 2)
'toto'
>>> fois([1,3], 2)
[1, 3, 1, 3]
```

L'opérateur `*` reconnaît plusieurs types (entiers, *floats*, chaînes de caractères, listes). Notre fonction *fois()* est donc capable d'effectuer des tâches différentes ! Même si *Python* autorise cela, méfiez-vous tout de même de cette grande flexibilité qui pourrait conduire à des surprises dans vos futurs programmes. En général, il est plus judicieux que chaque argument ait un type précis (entiers, *floats*, chaînes de caractères, etc) et pas l'un ou l'autre.

## Renvoi de résultats

Un énorme avantage en *Python* est que les fonctions sont capables de renvoyer plusieurs objets à la fois, comme dans cette fraction de code :

```python
>>> def carre_cube(x):
...     return x**2, x**3
...
>>> carre_cube(2)
(4, 8)
```

En réalité *Python* ne renvoie qu'un seul objet, mais celui-ci peut être séquentiel, c'est-à-dire contenir lui même d'autres objets. Dans notre exemple *Python* renvoie un objet de type *tuple*, type que nous verrons dans le chapitre 13 *Dictionnaires et tuples* (grosso modo, il s'agit d'une sorte de liste avec des propriétés différentes). Notre fonction pourrait tout autant renvoyer une liste :

```python
>>> def carre_cube2(x):
...     return [x**2, x**3]
...
>>> carre_cube2(3)
[9, 27]
```

Renvoyer un `tuple` ou une liste de deux éléments (ou plus) est très pratique en conjonction avec l'**affectation multiple**, par exemple :

```python
>>> z1, z2 = carre_cube2(3)
>>> z1
9
>>> z2
27
```

Cela permet de récupérer plusieurs valeurs renvoyées par une fonction et de les affecter à la volée à des variables différentes.

## Arguments positionnels et arguments par mot-clé

Jusqu'à maintenant, nous avons systématiquement passé le nombre d'arguments que la fonction attendait. Que se passe-t-il si une fonction attend deux arguments et que nous ne lui en passons qu'un seul ?

```python
>>> def fois(x, y):
...     return x*y
...
>>> fois(2, 3)
6
>>> fois(2)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: fois() missing 1 required positional argument: 'y'
```

On constate que passer un seul argument à une fonction qui en attend deux conduit à une erreur.

!!! note "Définition"
    Lorsqu'on définit une fonction `def fct(x, y):` les arguments `x` et `y` sont appelés **arguments positionnels** (en anglais *positional arguments*). Il est strictement obligatoire de les préciser lors de l'appel de la fonction. De plus, il est nécessaire de respecter le même ordre lors de l'appel que dans la définition de la fonction. Dans l'exemple ci-dessus, `2` correspondra à `x` et `3` correspondra à `y`. Finalement, tout dépendra de leur position, d'où leur qualification de positionnel.

Mais il est aussi possible de passer un ou plusieurs argument(s) de manière facultative et de leur attribuer une valeur par défaut :

```python
>>> def fct(x=1):
...     return x
...
>>> fct()
1
>>> fct(10)
10
```

Définition

Un argument défini avec une syntaxe def fct(arg=val): est appelé argument par mot-clé (en anglais keyword argument). Le passage d'un tel argument lors de l'appel de la fonction est facultatif. Ce type d'argument ne doit pas être confondu avec les arguments positionnels présentés ci-dessus, dont la syntaxe est def fct(arg):.

Il est bien sûr possible de passer plusieurs arguments par mot-clé :

>>> def fct(x=0, y=0, z=0):
...     return x, y, z
...
>>> fct()
(0, 0, 0)
>>> fct(10)
(10, 0, 0)
>>> fct(10, 8)
(10, 8, 0)
>>> fct(10, 8, 3)
(10, 8, 3)

On observe que pour l'instant, les arguments par mot-clé sont pris dans l'ordre dans lesquels on les passe lors de l'appel. Comment pourrions-nous faire si on souhaitait préciser l'argument par mot-clé z et garder les valeurs de x et y par défaut ? Simplement en précisant le nom de l'argument lors de l'appel :

>>> fct(z=10)
(0, 0, 10)

Python permet même de rentrer les arguments par mot-clé dans un ordre arbitraire :

>>> fct(z=10, x=3, y=80)
(3, 80, 10)
>>> fct(z=10, y=80)
(0, 80, 10)

Que se passe-t-il lorsque nous avons un mélange d'arguments positionnels et par mot-clé ? Et bien les arguments positionnels doivent toujours être placés avant les arguments par mot-clé :

>>> def fct(a, b, x=0, y=0, z=0):
...     return a, b, x, y, z
...
>>> fct(1, 1)
(1, 1, 0, 0, 0)
>>> fct(1, 1, z=5)
(1, 1, 0, 0, 5)
>>> fct(1, 1, z=5, y=32)
(1, 1, 0, 32, 5)

On peut toujours passer les arguments par mot-clé dans un ordre arbitraire à partir du moment où on précise leur nom. Par contre, si les deux arguments positionnels a et b ne sont pas passés à la fonction, Python renvoie une erreur.

>>> fct(z=0)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: fct() missing 2 required positional arguments: 'a' and 'b'

Conseils

Préciser le nom des arguments par mot-clé lors de l'appel d'une fonction est une pratique que nous vous recommandons. Cela les distingue clairement des arguments positionnels.

L'utilisation d'arguments par mot-clé est habituelle en Python. Elle permet de modifier le comportement par défaut de nombreuses fonctions. Par exemple, si on souhaite que la fonction print() n'affiche pas un retour à la ligne, on peut utiliser l'argument end :

>>> print("Message ", end="")
Message >>>

Nous verrons, dans le chapitre 20 Fenêtres graphiques et Tkinter, que l'utilisation d'arguments par mot-clé est systématique lorsqu'on crée un objet graphique (une fenêtre, un bouton, etc.).
9.6 Variables locales et variables globales

Lorsqu'on manipule des fonctions, il est essentiel de bien comprendre comment se comportent les variables. Une variable est dite locale lorsqu'elle est créée dans une fonction. Elle n'existera et ne sera visible que lors de l'exécution de ladite fonction.

Une variable est dite globale lorsqu'elle est créée dans le programme principal. Elle sera visible partout dans le programme.

Ceci ne vous paraît pas clair ? Nous allons prendre un exemple simple qui vous aidera à mieux saisir ces concepts. Observez le code suivant :

# définition d'une fonction carre()
def carre(x):
    y = x**2
    return y

# programme principal
z = 5
resultat = carre(z)
print(resultat)

Pour la suite des explications, nous allons utiliser l'excellent site Python Tutor qui permet de visualiser l'état des variables au fur et à mesure de l'exécution d'un code Python. Avant de poursuivre, nous vous conseillons de prendre 5 minutes pour tester ce site.

Regardons maintenant ce qui se passe dans le code ci-dessus, étape par étape :

    Étape 1 : Python est prêt à lire la première ligne de code.

Étape 1.
Figure 2. Étape 1.

    Étape 2 : Python met en mémoire la fonction carre(). Notez qu'il ne l'exécute pas ! La fonction est mise dans un espace de la mémoire nommé Global frame, il s'agit de l'espace du programme principal. Dans cet espace, seront stockées toutes les variables globales créées dans le programme. Python est maintenant prêt à exécuter le programme principal.

Étape 2.
Figure 3. Étape 2.

    Étape 3 : Python lit et met en mémoire la variable z. Celle-ci étant créée dans le programme principal, il s'agira d'une variable globale. Ainsi, elle sera également stockée dans le Global frame.

Étape 3.
Figure 4. Étape 3.

    Étape 4 : La fonction carre() est appelée et on lui passe en argument l'entier z. La fonction s'exécute et un nouveau cadre est créé dans lequel Python Tutor va indiquer toutes les variables locales à la fonction. Notez bien que la variable passée en argument, qui s'appelle x dans la fonction, est créée en tant que variable locale. On remarquera aussi que les variables globales situées dans le Global frame sont toujours là.

Étape 4.
Figure 5. Étape 4.

    Étape 5 : Python est maintenant prêt à exécuter chaque ligne de code de la fonction.

Étape 5.
Figure 6. Étape 5.

    Étape 6 : La variable y est créée dans la fonction. Celle-ci est donc stockée en tant que variable locale à la fonction.

Étape 6.
Figure 7. Étape 6.

    Étape 7 : Python s'apprête à renvoyer la variable locale y au programme principal. Python Tutor nous indique le contenu de la valeur renvoyée.

Étape 7.
Figure 8. Étape 7.

    Étape 8 : Python quitte la fonction et la valeur renvoyée par celle-ci est affectée à la variable globale resultat. Notez bien que lorsque Python quitte la fonction, l'espace des variables alloué à la fonction est détruit. Ainsi, toutes les variables créées dans la fonction n'existent plus. On comprend pourquoi elles portent le nom de locales puisqu'elles n'existent que lorsque la fonction est exécutée.

Étape 8.
Figure 9. Étape 8.

    Étape 9 : Python affiche le contenu de la variable resultat et l'exécution est terminée.

Étape 9.
Figure 10. Étape 9.

Nous espérons que cet exemple guidé facilitera la compréhension des concepts de variables locales et globales. Cela viendra aussi avec la pratique. Nous irons un peu plus loin sur les fonctions dans le chapitre 12. D'ici là, essayez de vous entraîner au maximum avec les fonctions. C'est un concept ardu, mais il est impératif de le maîtriser.

Enfin, comme vous avez pu le constater, Python Tutor nous a grandement aidé à comprendre ce qui se passait. N'hésitez pas à l'utiliser sur des exemples ponctuels, ce site vous aidera à visualiser ce qui se passe lorsqu'un code ne fait pas ce que vous attendez.
9.7 Principe DRY

L'acronyme DRY signifie Don't Repeat Yourself. Les fonctions permettent de satisfaire ce principe en évitant la duplication de code. En effet, plus un code est dupliqué plusieurs fois dans un programme, plus il sera source d'erreurs, notamment lorsqu'il faudra le faire évoluer.

Considérons par exemple le code suivant qui convertit plusieurs températures des degrés Fahrenheit en degrés Celsius :

>>> temp_in_fahrenheit = 60
>>> (temp_in_fahrenheit - 32) * (5/8)
17.5
>>> temp_in_fahrenheit = 80
>>> (temp_in_fahrenheit - 32) * (5/8)
30.0
>>> temp_in_fahrenheit = 100
>>> (temp_in_fahrenheit - 32) * (5/8)
42.5

Malheureusement il y a une erreur dans la formule de conversion. En effet la formule exacte est :
temp_celsius=(temp_fahrenheit−32)×59

Il faut alors reprendre les lignes 2, 5 et 8 précédentes et les corriger. Cela n'est pas efficace, surtout si le même code est utilisé à différents endroits dans le programme.

En écrivant qu'une seule fois la formule de conversion dans une fonction, on applique le principe DRY :

>>> def convert_fahrenheit_to_celsius(temperature):
...     return (temperature - 32) * (5/9)
... 
>>> temp_in_fahrenheit = 60
>>> convert_fahrenheit_to_celsius(temp_in_fahrenheit)
15.555555555555557
>>> temp_in_fahrenheit = 80
>>> convert_fahrenheit_to_celsius(temp_in_fahrenheit)
26.666666666666668
>>> temp_in_fahrenheit = 100
>>> convert_fahrenheit_to_celsius(temp_in_fahrenheit)
37.77777777777778

Et s'il y a une erreur dans la formule, il suffira de le corriger qu'une seule fois, dans la fonction convert_fahrenheit_to_celsius().
