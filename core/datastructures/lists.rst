######
Listas
######

.. image:: img/mike-arney-9r-_2gzP37k-unsplash.jpg

Las listas permiten **almacenar objetos** mediante un **orden definido** y con posibilidad de duplicados. Las listas son estructuras de datos **mutables**, lo que significa que podemos añadir, eliminar o modificar sus elementos. [#wishlist-unsplash]_

**************
Creando listas
**************

Una lista está compuesta por *cero* o *más elementos*. En Python debemos escribir estos elementos separados por *comas* y dentro de *corchetes*. Veamos algunos ejemplos de listas::

    >>> empty_list = []

    >>> languages = ['Python', 'Ruby', 'Javascript']

    >>> fibonacci = [0, 1, 1, 2, 3, 5, 8, 13]

    >>> data = ['Tenerife', {'cielo': 'limpio', 'temp': 24}, 3718, (28.2933947, -16.5226597)]

.. note:: Una lista puede contener tipos de **datos heterogéneos**, lo que la hace una estructura de datos muy versátil.

Ejecución **paso a paso** a través de *Python Tutor*:

.. only:: latex

    https://cutt.ly/Ofiiare

.. only:: html

    .. raw:: html

        <iframe width="800" height="425" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=empty_list%20%3D%20%5B%5D%0A%0Alanguages%20%3D%20%5B'Python',%20'Ruby',%20'Javascript'%5D%0A%0Afibonacci%20%3D%20%5B0,%201,%201,%202,%203,%205,%208,%2013%5D%0A%0Adata%20%3D%20%5B'Tenerife',%20%7B'cielo'%3A%20'limpio',%20'temp'%3A%2024%7D,%203718,%20%2828.2933947,%20-16.5226597%29%5D&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

.. warning::
    Aunque está permitido, **NUNCA** llames ``list`` a una variable porque destruirías la función que nos permite crear listas. Y tampoco uses nombres derivados como ``_list`` o ``list_`` ya que no son nombres representativos que :ref:`identifiquen el propósito de la variable <core/datatypes/data:convenciones para nombres>`.

.. admonition:: Ejercicio
    :class: exercise

    Cree una lista con las 5 ciudades que más le gusten.

    .. only:: html
    
        |solution| :download:`love_cities.py <files/love_cities.py>`

**********
Conversión
**********

Para convertir otros tipos de datos en una lista podemos usar la función ``list()``::

    >>> # conversión desde una cadena de texto
    >>> list('Python')
    ['P', 'y', 't', 'h', 'o', 'n']

Si nos fijamos en lo que ha pasado, al convertir la cadena de texto ``Python`` se ha creado una lista con *6* elementos, donde cada uno de ellos representa un carácter de la cadena. Podemos *extender* este comportamiento a cualquier otro tipo de datos que permita ser iterado (*iterables*).

Otro ejemplo interesante de conversión puede ser la de los :ref:`rangos <core/controlflow/loops:Secuencias de números>`. En este caso queremos obtener una **lista explícita** con los valores que constituyen el rango :math:`[0, 9]`::

    >>> list(range(10))
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

Lista vacía
===========

Existe una manera particular de usar ``list()`` y es no pasarle ningún argumento. En este caso estaremos queriendo convertir el "vacío" en una lista, con lo que obtendremos una *lista vacía*::

    >>> list()
    []

.. tip:: Para crear una lista vacía, se suele recomendar el uso de ``[]`` frente a ``list()``, no sólo por ser más *pitónico* sino por tener (en promedio) un mejor rendimiento en tiempos de ejecución.

**********************
Operaciones con listas
**********************

Obtener un elemento
===================

Igual que en el caso de las :ref:`cadenas de texto <core/datatypes/strings:Obtener un carácter>`, podemos obtener un elemento de una lista a través del **índice** (lugar) que ocupa. Veamos un ejemplo::

    >>> shopping = ['Agua', 'Huevos', 'Aceite']

    >>> shopping[0]
    'Agua'

    >>> shopping[1]
    'Huevos'

    >>> shopping[2]
    'Aceite'

    >>> shopping[-1]  # acceso con índice negativo
    'Aceite'

El *índice* que usemos para acceder a los elementos de una lista tiene que estar comprendido entre los límites de la misma. Si usamos un índice antes del comienzo o después del final obtendremos un error (*excepción*)::

    >>> shopping = ['Agua', 'Huevos', 'Aceite']

    >>> shopping[3]
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    IndexError: list index out of range

    >>> shopping[-5]
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    IndexError: list index out of range

Trocear una lista
=================

El troceado de listas funciona de manera totalmente análoga al :ref:`troceado de cadenas <core/datatypes/strings:Trocear una cadena>`. Veamos algunos ejemplos::

    >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

    >>> shopping[0:3]
    ['Agua', 'Huevos', 'Aceite']

    >>> shopping[:3]
    ['Agua', 'Huevos', 'Aceite']

    >>> shopping[2:4]
    ['Aceite', 'Sal']

    >>> shopping[-1:-4:-1]
    ['Limón', 'Sal', 'Aceite']

    >>> # Equivale a invertir la lista
    >>> shopping[::-1]
    ['Limón', 'Sal', 'Aceite', 'Huevos', 'Agua']

En el troceado de listas, a diferencia de lo que ocurre al obtener elementos, no debemos preocuparnos por acceder a *índices inválidos* (fuera de rango) ya que Python los restringirá a los límites de la lista::

    >>> shopping
    ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

    >>> shopping[10:]
    []

    >>> shopping[-100:2]
    ['Agua', 'Huevos']

    >>> shopping[2:100]
    ['Aceite', 'Sal', 'Limón']

.. important:: Ninguna de las operaciones anteriores modifican la lista original, simplemente devuelven una lista nueva.

Invertir una lista
==================

Python nos ofrece, al menos, tres mecanismos para invertir los elementos de una lista:

**Conservando la lista original**:
    *Opción 1*: Mediante :ref:`troceado <core/datastructures/lists:Trocear una lista>` de listas con *step* negativo::

        >>> shopping
        ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

        >>> shopping[::-1]
        ['Limón', 'Sal', 'Aceite', 'Huevos', 'Agua']

    *Opción 2*: Mediante la función ``reversed()``::

        >>> shopping
        ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

        >>> list(reversed(shopping))
        ['Limón', 'Sal', 'Aceite', 'Huevos', 'Agua']

**Modificando la lista original**:
    Utilizando la función ``reverse()`` (nótese que es sin *"d"* al final)::

        >>> shopping
        ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

        >>> shopping.reverse()

        >>> shopping
        ['Limón', 'Sal', 'Aceite', 'Huevos', 'Agua']

Añadir al final de la lista
===========================

Una de las operaciones más utilizadas en listas es añadir elementos al final de las mismas. Para ello Python nos ofrece la función ``append()``. Se trata de un método "destructivo" que modifica la lista original::

    >>> shopping = ['Agua', 'Huevos', 'Aceite']

    >>> shopping.append('Atún')

    >>> shopping
    ['Agua', 'Huevos', 'Aceite', 'Atún']

Creando desde vacío
-------------------

Una forma muy habitual de trabajar con listas es empezar con una vacía e ir añadiendo elementos poco a poco. Se podría hablar de un **patrón creación**.

Supongamos un ejemplo en el que queremos construir una lista con los números pares del :math:`[0, 20)`::

    >>> even_numbers = []

    >>> for i in range(20):
    ...     if i % 2 == 0:
    ...         even_numbers.append(i)
    ...

    >>> even_numbers
    [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]

Ejecución **paso a paso** a través de *Python Tutor*:

.. only:: latex

    https://cutt.ly/2fiS9Ax

.. only:: html

    .. raw:: html

        <iframe width="800" height="410" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=even_numbers%20%3D%20%5B%5D%0A%0Afor%20i%20in%20range%2820%29%3A%0A%20%20%20%20if%20i%20%25%202%20%3D%3D%200%3A%0A%20%20%20%20%20%20%20%20even_numbers.append%28i%29%0A%0Aprint%28even_numbers%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Añadir en cualquier posición de una lista
=========================================

Ya hemos visto cómo añadir elementos al final de una lista. Sin embargo, Python ofrece una función ``insert()`` que vendría a ser una generalización de la anterior, para incorporar elementos en cualquier posición. Simplemente debemos especificar el índice de inserción y el elemento en cuestión. También se trata de una función *destructiva* [#destructive]_::

    >>> shopping = ['Agua', 'Huevos', 'Aceite']

    >>> shopping.insert(1, 'Jamón')

    >>> shopping
    ['Agua', 'Jamón', 'Huevos', 'Aceite']

    >>> shopping.insert(3, 'Queso')

    >>> shopping
    ['Agua', 'Jamón', 'Huevos', 'Queso', 'Aceite']

.. note:: El índice que especificamos en la función ``insert()`` lo podemos intepretar como la posición *delante* (a la izquierda) de la cual vamos a colocar el nuevo valor en la lista.

Al igual que ocurría con el :ref:`troceado de listas <core/datastructures/lists:Trocear una lista>`, en este tipo de inserciones no obtendremos un error si especificamos índices fuera de los límites de la lista. Estos se ajustarán al principio o al final en función del valor que indiquemos::

    >>> shopping = ['Agua', 'Huevos', 'Aceite']

    >>> shopping.insert(100, 'Mermelada')

    >>> shopping
    ['Agua', 'Huevos', 'Aceite', 'Mermelada']

    >>> shopping.insert(-100, 'Arroz')

    >>> shopping
    ['Arroz', 'Agua', 'Huevos', 'Aceite', 'Mermelada']

.. hint:: Aunque es posible utilizar ``insert()`` para añadir **elementos al final de una lista**, siempre se recomienda usar ``append()`` por su mayor legibilidad:

    .. code-block::
        :emphasize-lines: 2
    
        >>> values = [1, 2, 3]
        >>> values.append(4)
        >>> values
        [1, 2, 3, 4]

        >>> values = [1, 2, 3]
        >>> values.insert(len(values), 4)  # don't do it!
        >>> values
        [1, 2, 3, 4]

Repetir elementos
=================

Al igual que con las :ref:`cadenas de texto <core/datatypes/strings:Repetir cadenas>`, el operador ``*`` nos permite repetir los elementos de una lista::

    >>> shopping = ['Agua', 'Huevos', 'Aceite']

    >>> shopping * 3
    ['Agua',
     'Huevos',
     'Aceite',
     'Agua',
     'Huevos',
     'Aceite',
     'Agua',
     'Huevos',
     'Aceite']

Combinar listas
===============

Python nos ofrece dos aproximaciones para combinar listas:

**Conservando la lista original**:
    Mediante el operador ``+`` o ``+=``::

        >>> shopping = ['Agua', 'Huevos', 'Aceite']
        >>> fruitshop = ['Naranja', 'Manzana', 'Piña']

        >>> shopping + fruitshop
        ['Agua', 'Huevos', 'Aceite', 'Naranja', 'Manzana', 'Piña']

**Modificando la lista original**:
    Mediante la función ``extend()``::

        >>> shopping = ['Agua', 'Huevos', 'Aceite']
        >>> fruitshop = ['Naranja', 'Manzana', 'Piña']

        >>> shopping.extend(fruitshop)

        >>> shopping
        ['Agua', 'Huevos', 'Aceite', 'Naranja', 'Manzana', 'Piña']

Hay que tener en cuenta que ``extend()`` funciona adecuadamente si pasamos una **lista como argumento**. En otro caso, quizás los resultados no sean los esperados. Veamos un ejemplo::

    >>> shopping = ['Agua', 'Huevos', 'Aceite']

    >>> shopping.extend('Limón')

    >>> shopping
    ['Agua', 'Huevos', 'Aceite', 'L', 'i', 'm', 'ó', 'n']

El motivo es que ``extend()`` "recorre" (o itera) sobre cada uno de los elementos del objeto en cuestión. En el caso anterior, al ser una cadena de texto, está formada por caracteres. De ahí el resultado que obtenemos.

Se podría pensar en el uso de ``append()`` para combinar listas. La realidad es que no funciona exactamente como esperamos; la segunda lista se añadiría como una *sublista* de la principal::

    >>> shopping = ['Agua', 'Huevos', 'Aceite']
    >>> fruitshop = ['Naranja', 'Manzana', 'Piña']

    >>> shopping.append(fruitshop)

    >>> shopping
    ['Agua', 'Huevos', 'Aceite', ['Naranja', 'Manzana', 'Piña']]

Modificar una lista
===================

Del mismo modo que se :ref:`accede a un elemento <core/datastructures/lists:Obtener un elemento>` utilizando su índice, también podemos modificarlo:

.. code-block::
    :emphasize-lines: 6

    >>> shopping = ['Agua', 'Huevos', 'Aceite']

    >>> shopping[0]
    'Agua'

    >>> shopping[0] = 'Jugo'

    >>> shopping
    ['Jugo', 'Huevos', 'Aceite']

En el caso de acceder a un *índice no válido* de la lista, incluso para modificar, obtendremos un error::

    >>> shopping[100] = 'Chocolate'
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    IndexError: list assignment index out of range

Modificar con troceado
----------------------

No sólo es posible modificar un elemento de cada vez, sino que podemos asignar valores a trozos de una lista::

    >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

    >>> shopping[1:4]
    ['Huevos', 'Aceite', 'Sal']

    >>> shopping[1:4] = ['Atún', 'Pasta']

    >>> shopping
    ['Agua', 'Atún', 'Pasta', 'Limón']

.. note:: La lista que asignamos no necesariamente debe tener la misma longitud que el trozo que sustituimos.

Borrar elementos
================

Python nos ofrece, al menos, cuatro formas para borrar elementos en una lista:

**Por su índice**:
    Mediante la sentencia ``del``::

        >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

        >>> del shopping[3]

        >>> shopping
        ['Agua', 'Huevos', 'Aceite', 'Limón']


**Por su valor**:
    Mediante la función ``remove()``::

        >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

        >>> shopping.remove('Sal')

        >>> shopping
        ['Agua', 'Huevos', 'Aceite', 'Limón']

    .. warning:: Si existen valores duplicados, la función ``remove()`` sólo borrará la primera ocurrencia.

**Por su índice (con extracción)**:
    La sentencia ``del`` y la función ``remove()`` efectivamente borran el elemento indicado de la lista, pero no "devuelven" [#return]_ nada. Sin embargo, Python nos ofrece la función ``pop()`` que además de borrar, nos "recupera" el elemento; algo así como una *extracción*. Lo podemos ver como una combinación de *acceso* + *borrado*::

        >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

        >>> product = shopping.pop()  # shopping.pop(-1)
        >>> product
        'Limón'

        >>> shopping
        ['Agua', 'Huevos', 'Aceite', 'Sal']

        >>> product = shopping.pop(2)
        >>> product
        'Aceite'

        >>> shopping
        ['Agua', 'Huevos', 'Sal']

    .. note:: Si usamos la función ``pop()`` sin pasarle ningún argumento, por defecto usará el índice *-1*, es decir, el último elemento de la lista. Pero también podemos indicarle el índice del elemento a extraer.

**Por su rango**:
    Mediante troceado de listas::

        >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

        >>> shopping[1:4] = []

        >>> shopping
        ['Agua', 'Limón']        

Borrado completo de la lista
----------------------------

Python nos ofrece, al menos, dos formas para borrar una lista por completo:

1. Utilizando la función ``clear()``::

    >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

    >>> shopping.clear()  # Borrado in-situ

    >>> shopping
    []

2. "Reinicializando" la lista a vacío con ``[]``::

    >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

    >>> shopping = []  # Nueva zona de memoria

    >>> shopping
    []
    
|advlev|

La diferencia entre ambos métodos tiene que ver con cuestiones internas de gestión de memoria y de rendimiento::

    >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']
    >>> id(shopping)
    4416018560
    >>> shopping.clear()
    >>> id(shopping)  # se mantiene la misma "posición de memoria"
    4416018560

    >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']
    >>> id(shopping)
    4458688576
    >>> shopping = []
    >>> id(shopping)  # se crea una nueva "posición de memoria"
    4458851520

.. seealso::
    La memoria que queda "en el limbo" después de asignar un nuevo valor a la lista es detectada por el **recolector de basura** de Python, quien se encarga de liberar aquellos datos que no están referenciados por ninguna variable.

Encontrar un elemento
=====================

Si queremos descubrir el **índice** que corresponde a un determinado valor dentro la lista podemos usar la función ``index()`` para ello::

    >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

    >>> shopping.index('Huevos')
    1

Tener en cuenta que si el elemento que buscamos no está en la lista, obtendremos un error::

    >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

    >>> shopping.index('Pollo')
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    ValueError: 'Pollo' is not in list

.. note:: Si buscamos un valor que existe más de una vez en una lista, la función ``index()`` sólo nos devolverá el índice de la primera ocurrencia.

.. warning::
    En listas no disponemos de la función ``find()`` que sí estaba disponible para :ref:`cadenas de texto <core/datatypes/strings:realizar búsquedas>`.

Pertenencia de un elemento
==========================

Si queremos comprobar la existencia de un determinado elemento en una lista, podríamos buscar su índice, pero la forma **pitónica** de hacerlo es utilizar el operador ``in``::

    >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

    >>> 'Aceite' in shopping
    True

    >>> 'Pollo' in shopping
    False

.. note:: El operador ``in`` siempre devuelve un valor booleano, es decir, verdadero o falso.

.. admonition:: Ejercicio
    :class: exercise

    Determine si una cadena de texto dada es un **isograma**, es decir, no se repite ninguna letra.

    Ejemplos válidos de isogramas:

    - *lumberjacks*
    - *background*
    - *downstream*
    - *six-year-old*

    .. only:: html
    
        |solution| :download:`isogram.py <files/isogram.py>`

Número de ocurrencias
=====================

Para contar cuántas veces aparece un determinado valor dentro de una lista podemos usar la función ``count()``::

    >>> sheldon_greeting = ['Penny', 'Penny', 'Penny']

    >>> sheldon_greeting.count('Howard')
    0

    >>> sheldon_greeting.count('Penny')
    3

Convertir lista a cadena de texto
=================================

Dada una lista, podemos convetirla a una cadena de texto, uniendo todos sus elementos mediante algún **separador**. Para ello hacemos uso de la función ``join()`` con la siguiente estructura:

.. figure:: img/join-list.jpg
    :align: center

    Estructura de llamada a la función ``join()``

::

    >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

    >>> ','.join(shopping)
    'Agua,Huevos,Aceite,Sal,Limón'
    
    >>> ' '.join(shopping)
    'Agua Huevos Aceite Sal Limón'

    >>> '|'.join(shopping)
    'Agua|Huevos|Aceite|Sal|Limón'

Hay que tener en cuenta que ``join()`` sólo funciona si *todos sus elementos son cadenas de texto*::

    >>> ', '.join([1, 2, 3, 4, 5])
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    TypeError: sequence item 0: expected str instance, int found

.. tip:: Esta función ``join()`` es realmente la **opuesta** a la de ``split()`` para :ref:`dividir una cadena <core/datatypes/strings:Dividir una cadena>`.

.. admonition:: Ejercicio
    :class: exercise

    Consiga la siguiente transformación:

    ``12/31/20`` ➡️ ``31-12-2020``

    .. only:: html
    
        |solution| :download:`fixdate.py <files/fixdate.py>`

Ordenar una lista
=================

Python proporciona, al menos, dos formas de ordenar los elementos de una lista:

**Conservando lista original**:
    Mediante la función ``sorted()`` que devuelve una nueva lista ordenada::

        >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

        >>> sorted(shopping)
        ['Aceite', 'Agua', 'Huevos', 'Limón', 'Sal']

**Modificando la lista original**:
    Mediante la función ``sort()``::

        >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

        >>> shopping.sort()

        >>> shopping
        ['Aceite', 'Agua', 'Huevos', 'Limón', 'Sal']

**Ambos métodos** admiten un *parámetro* "booleano" ``reverse`` para indicar si queremos que la ordenación se haga en **sentido inverso**::

    >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

    >>> sorted(shopping, reverse=True)
    ['Sal', 'Limón', 'Huevos', 'Agua', 'Aceite']

Longitud de una lista
=====================

Podemos conocer el número de elementos que tiene una lista con la función ``len()``::

    >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

    >>> len(shopping)
    5

Iterar sobre una lista
======================

Al igual que :ref:`hemos visto con las cadenas de texto <for-sentence>`, también podemos *iterar* sobre los elementos de una lista utilizando la sentencia ``for``::

    >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

    >>> for product in shopping:
    ...     print(product)
    ...
    Agua
    Huevos
    Aceite
    Sal
    Limón

.. note:: También es posible usar la sentencia ``break`` en este tipo de bucles para abortar su ejecución en algún momento que nos interese.

.. admonition:: Ejercicio

    pycheck_: **chars_list**

Iterar usando enumeración
-------------------------

Hay veces que no sólo nos interesa "visitar" cada uno de los elementos de una lista, sino que también queremos **saber su índice** dentro de la misma. Para ello Python nos ofrece la función ``enumerate()``::

    >>> shopping = ['Agua', 'Huevos', 'Aceite', 'Sal', 'Limón']

    >>> for i, product in enumerate(shopping):
    ...     print(i, product)
    ...
    0 Agua
    1 Huevos
    2 Aceite
    3 Sal
    4 Limón

Ejecución **paso a paso** a través de *Python Tutor*:

.. only:: latex

    https://cutt.ly/TfiuIZ0

.. only:: html

    .. raw:: html

        <iframe width="800" height="360" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=shopping%20%3D%20%5B'Agua',%20'Huevos',%20'Aceite',%20'Sal',%20'Lim%C3%B3n'%5D%0A%0Afor%20i,%20product%20in%20enumerate%28shopping%29%3A%0A%20%20%20%20print%28i,%20product%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

.. tip::
    Es posible utilizar el parámetro ``start`` con ``enumerate()`` para indicar el índice en el que queremos comenzar. Por defecto es 0.

Iterar sobre múltiples listas
-----------------------------

Python ofrece la posibilidad de iterar sobre **múltiples listas en paralelo** utilizando la función ``zip()``. Se basa en ir "juntando" ambas listas elemento a elemento:

.. figure:: img/zip.png
    :align: center

    Funcionamiento de ``zip()``

Veamos un ejemplo en el que añadimos ciertos detalles a nuestra lista de la compra::

    >>> shopping = ['Agua', 'Aceite', 'Arroz']
    >>> details = ['mineral natural', 'de oliva virgen', 'basmati']

    >>> for product, detail in zip(shopping, details):
    ...     print(product, detail)
    ...
    Agua mineral natural
    Aceite de oliva virgen
    Arroz basmati

Ejecución **paso a paso** a través de *Python Tutor*:

.. only:: latex

    https://cutt.ly/lfioilG

.. only:: html

    .. raw:: html

        <iframe width="800" height="380" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=shopping%20%3D%20%5B'Agua',%20'Aceite',%20'Arroz'%5D%0Adetails%20%3D%20%5B'mineral%20natural',%20'de%20oliva%20virgen',%20'basmati'%5D%0A%0Afor%20product,%20detail%20in%20zip%28shopping,%20details%29%3A%0A%20%20%20%20print%28product,%20detail%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

.. note:: En el caso de que las listas no tengan la misma longitud, la función ``zip()`` realiza la combinación hasta que se agota la lista más corta.

Dado que ``zip()`` produce un *iterador*, si queremos obtener una **lista explícita** con la combinación en paralelo de las listas, debemos construir dicha lista de la siguiente manera::

    >>> shopping = ['Agua', 'Aceite', 'Arroz']
    >>> details = ['mineral natural', 'de oliva virgen', 'basmati']

    >>> list(zip(shopping, details))
    [('Agua', 'mineral natural'),
     ('Aceite', 'de oliva virgen'),
     ('Arroz', 'basmati')]
    
.. admonition:: Ejercicio
    :class: exercise

    Dados dos vectores (listas) de la misma dimensión, utilice la función ``zip()`` para calcular su `producto escalar`_.

    **Ejemplo**
        * Entrada::

            v1 = [4, 3, 8, 1]
            v2 = [9, 2, 7, 3]

        * Salida: ``101``

        :math:`v1 \cdot v2 = [4 \cdot 9 + 3 \cdot 2 + 8 \cdot 7 + 1 \cdot 3] = 101`
    
    .. only:: html
    
        |solution| :download:`scalar_prod.py <files/scalar_prod.py>`

Comparar listas
=================

Supongamos este ejemplo::

    >>> [1, 2, 3] < [1, 2, 4]
    True

Python llega a la conclusión de que la lista ``[1, 2, 3]`` es menor que ``[1, 2, 4]`` porque va comparando elemento a elemento:

- El ``1`` es igual en ambas listas.
- El ``2`` es igual en ambas litas.
- El ``3`` es menor que el ``4``, por lo que la primera lista es menor que la segunda.

Entender la forma en la que se comparan dos listas es importante para poder aplicar otras funciones y obtener los resultados deseados.

.. seealso::
    Esta comparación funciona de forma totalmente análoga a la :ref:`comparación de cadenas de texto <core/datatypes/strings:comparar cadenas>`.

**********************
Cuidado con las copias
**********************

|intlev|

Las listas son estructuras de datos :ref:`mutables <core/datatypes/data:Mutabilidad>` y esta característica nos obliga a tener cuidado cuando realizamos copias de listas, ya que la modificación de una de ellas puede afectar a la otra.

Veamos un ejemplo sencillo::

    >>> original_list = [4, 3, 7, 1]

    >>> copy_list = original_list

    >>> original_list[0] = 15

    >>> original_list
    [15, 3, 7, 1]

    >>> copy_list
    [15, 3, 7, 1]

Ejecución **paso a paso** a través de *Python Tutor*:

.. only:: latex

    https://cutt.ly/pfi5PC5
    

.. only:: html

    .. raw:: html

        <iframe width="800" height="430" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=original_list%20%3D%20%5B4,%203,%207,%201%5D%0A%0Acopy_list%20%3D%20original_list%0A%0Aoriginal_list%5B0%5D%20%3D%2015%0A%0Aprint%28original_list%29%0Aprint%28copy_list%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

.. note:: A través de *Python Tutor* se puede ver claramente el motivo de por qué ocurre esto. Dado que las variables "apuntan" a la misma zona de memoria, al modificar una de ellas, el cambio también se ve reflejado en la otra.

Una **posible solución** a este problema es hacer una "copia dura". Para ello Python proporciona la función ``copy()``:

.. code-block::
    :emphasize-lines: 3

    >>> original_list = [4, 3, 7, 1]

    >>> copy_list = original_list.copy()

    >>> original_list[0] = 15

    >>> original_list
    [15, 3, 7, 1]

    >>> copy_list
    [4, 3, 7, 1]

Ejecución **paso a paso** a través de *Python Tutor*:

.. only:: latex

    https://cutt.ly/Dfi6oLk    


.. only:: html

    .. raw:: html

        <iframe width="800" height="430" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=original_list%20%3D%20%5B4,%203,%207,%201%5D%0A%0Acopy_list%20%3D%20original_list.copy%28%29%0A%0Aoriginal_list%5B0%5D%20%3D%2015%0A%0Aprint%28original_list%29%0Aprint%28copy_list%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Existe **otra aproximación** a este problema, y es utilizar un :ref:`troceado <core/datastructures/lists:trocear una lista>` completo de la lista, lo que nos devuelve una "copia desvinculada" de manera implícita:

.. code-block::
    :emphasize-lines: 3

    >>> original_list = [4, 3, 7, 1]

    >>> copy_list = original_list[:]

    >>> id(original_list) != id(copy_list)
    True

.. tip:: En el caso de que estemos trabajando con listas que contienen elementos mutables, debemos hacer uso de la función ``deepcopy()`` dentro del módulo ``copy`` de la librería estándar.

******************
Veracidad múltiple
******************

Si bien podemos usar :ref:`sentencias condicionales <core/controlflow/conditionals:Condicionales>` para comprobar la veracidad de determinadas expresiones, Python nos ofrece dos funciones "built-in" con las que podemos evaluar si se cumplen **todas** las condiciones ``all()`` o si se cumple **alguna** condición ``any()``. Estas funciones trabajan sobre iterables, y el caso más evidente es una **lista**.

Supongamos un ejemplo en el que queremos comprobar si una determinada palabra cumple las siguientes condiciones:

- Su longitud total es mayor que 4.
- Empieza por "p".
- Contiene, al menos, una "y".

Veamos la **versión clásica**::

    >>> word = 'python'

    >>> if len(word) > 4 and word.startswith('p') and word.count('y') >= 1:
    ...     print('Cool word!')
    ... else:
    ...     print('No thanks')
    ...
    Cool word!

Veamos la **versión con veracidad múltiple** usando ``all()``, donde se comprueba que se cumplan **todas** las expresiones:

.. code-block::
    :emphasize-lines: 7

    >>> word = 'python'

    >>> enough_length = len(word) > 4            # True
    >>> right_beginning = word.startswith('p')   # True
    >>> min_ys = word.count('y') >= 1            # True

    >>> is_cool_word = all([enough_length, right_beginning, min_ys])

    >>> if is_cool_word:
    ...     print('Cool word!')
    ... else:
    ...     print('No thanks')
    ...
    Cool word!

Veamos la **versión con veracidad múltiple** usando ``any()``, donde se comprueba que se cumpla **alguna** expresión:

.. code-block::
    :emphasize-lines: 7

    >>> word = 'yeah'

    >>> enough_length = len(word) > 4            # False
    >>> right_beginning = word.startswith('p')   # False
    >>> min_ys = word.count('y') >= 1            # True

    >>> is_fine_word = any([enough_length, right_beginning, min_ys])

    >>> if is_fine_word:
    ...     print('Fine word!')
    ... else:
    ...     print('No thanks')
    ...
    Fine word!

.. hint:: Este enfoque puede ser interesante cuando se manejan muchas condiciones o bien cuando queremos separar las condiciones y agruparlas en una única lista.

**********************
Listas por comprensión
**********************

|intlev|

Las **listas por comprensión** establecen una técnica para crear listas de forma más **compacta** basándose en el concepto matemático de `conjuntos definidos por comprensión <http://recursostic.educacion.es/descartes/web/materiales_didacticos/conjuntos_y_operaciones_agsm/conjuntos_12.html>`_.

Podríamos decir que su sintaxis sigue un modelo **VLC (Value-Loop-Condition)** tal y como se muestra en la siguiente figura:

.. figure:: img/list-comprehensions.png
    :align: center

    Estructura de una lista por comprensión

En primer lugar veamos un ejemplo en el que convertimos una cadena de texto con valores numéricos en una lista con los mismos valores pero convertidos a enteros. En su **versión clásica** haríamos algo tal que así::

    >>> values = '32,45,11,87,20,48'

    >>> int_values = []

    >>> for value in values.split(','):
    ...     int_value = int(value)
    ...     int_values.append(int_value)
    ...

    >>> int_values
    [32, 45, 11, 87, 20, 48]

Ahora veamos el código utilizando una **lista por comprensión**::

    >>> values = '32,45,11,87,20,48'

    >>> int_values = [int(value) for value in values.split(',')]

    >>> int_values
    [32, 45, 11, 87, 20, 48]

.. figure:: img/list-comprehensions-transformation.jpg
    :align: center

    Transformación de estructura clásica en lista por comprensión


Condiciones en comprensiones
============================

También existe la posibilidad de incluir condiciones en las **listas por comprensión**.

Continuando con el ejemplo anterior, supongamos que sólo queremos crear la lista con aquellos valores que empiecen por el dígito 4::

    >>> values = '32,45,11,87,20,48'

    >>> int_values = [int(v) for v in values.split(',') if v.startswith('4')]

    >>> int_values
    [45, 48]

Anidamiento en comprensiones
============================

|advlev|

En la iteración que usamos dentro de la lista por comprensión es posible usar :ref:`bucles anidados <core/controlflow/loops:Bucles anidados>`.

Veamos un ejemplo en el que generamos todas las combinaciones de una serie de valores::

    >>> values = '32,45,11,87,20,48'
    >>> svalues = values.split(',')

    >>> combinations = [f'{v1}x{v2}' for v1 in svalues for v2 in svalues]

    >>> combinations
    ['32x32',
     '32x45',
     '32x11',
     '32x87',
     '32x20',
     '32x48',
     '45x32',
     '45x45',
     ...
     '48x45',
     '48x11',
     '48x87',
     '48x20',
     '48x48']

.. hint:: Las listas por comprensión son una herramienta muy potente y nos ayuda en muchas ocasiones, pero hay que tener cuidado de no generar **expresiones excesivamente complejas**. En estos casos es mejor una *aproximación clásica*.

.. admonition:: Ejercicio
    :class: exercise

    Utilizando listas por comprensión, cree una lista que contenga el resultado de aplicar la función :math:`f(x) = 3x + 2` para :math:`x \in [0, 20)`.

    **Salida esperada**: ``[2, 5, 8, 11, 14, 17, 20, 23, 26, 29, 32, 35, 38, 41, 44, 47, 50, 53, 56, 59]``

    .. only:: html
    
        |solution| :download:`comprehension.py <files/comprehension.py>`

.. _sys-argv:

************
``sys.argv``
************

Cuando queramos ejecutar un programa Python desde **línea de comandos**, tendremos la posibilidad de acceder a los argumentos de dicho programa. Para ello se utiliza una lista que la encontramos dentro del módulo ``sys`` y que se denomina ``argv``:

.. figure:: img/sys-argv.png
    :align: center

    Acceso a parámetros en línea de comandos

Veamos una aplicación de lo anterior en un programa que convierte un número decimal a una determinada base, ambos argumentos pasados por línea de comandos:

:download:`dec2base.py <files/dec2base.py>`

.. literalinclude:: files/dec2base.py
    :linenos:

Si lo ejecutamos obtenemos lo siguiente:

.. code-block:: console

    $ python dec2base.py 65535 2
    1111111111111111

*********************
Funciones matemáticas
*********************

Python nos ofrece, entre otras [#more-math]_, estas tres funciones matemáticas básicas que se pueden aplicar sobre listas.

**Suma de todos los valores**:
    Mediante la función ``sum()``::

        >>> data = [5, 3, 2, 8, 9, 1]
        >>> sum(data)
        28

**Mínimo de todos los valores**:
    Mediante la función ``min()``::

        >>> data = [5, 3, 2, 8, 9, 1]
        >>> min(data)
        1

**Máximo de todos los valores**:
    Mediante la función ``max()``::

        >>> data = [5, 3, 2, 8, 9, 1]
        >>> max(data)
        9

.. admonition:: Ejercicio
    :class: exercise

    Lea :ref:`desde línea de comandos <sys-argv>` una serie de números y obtenga la media de dichos valores (*muestre el resultado con 2 decimales*).

    La llamada se haría de la siguiente manera::

        $ python avg.py 32 56 21 99 12 17

    Plantilla de código para el programa::

        import sys

        # En values tendremos una lista con los valores (como strings)
        values = sys.argv[1:]

        # Su código debajo de aquí

    **Ejemplo**
        * Entrada: ``32 56 21 99 12 17``
        * Salida: ``39.50``
    
    .. only:: html
    
        |solution| :download:`avg.py <files/avg.py>`

****************
Listas de listas
****************

|intlev|

Como ya hemos visto en varias ocasiones, las listas son estructuras de datos que pueden contener elementos heterogéneos. Estos elementos pueden ser a su vez listas.

A continuación planteamos un ejemplo del mundo deportivo. Un equipo de fútbol suele tener una disposición en el campo organizada en líneas de jugadores. En aquella alineación con la que España `ganó la copa del mundo <https://es.wikipedia.org/wiki/Espa%C3%B1a_en_la_Copa_Mundial_de_F%C3%BAtbol_de_2010>`_ en 2010 había una disposición *4-3-3* con los siguientes jugadores:

.. figure:: img/world-champions.png
    :align: center

    Lista de listas (como equipo de fútbol)

Veamos una posible representación de este equipo de fútbol usando una lista compuesta de listas. Primero definimos cada una de las líneas::

    >>> goalkeeper = 'Casillas'
    >>> defenders = ['Capdevila', 'Piqué', 'Puyol', 'Ramos']
    >>> midfielders = ['Xavi', 'Busquets', 'X. Alonso']
    >>> forwards = ['Iniesta', 'Villa', 'Pedro']

Y ahora las juntamos en una única lista::

    >>> team = [goalkeeper, defenders, midfielders, forwards]

    >>> team
    ['Casillas',
     ['Capdevila', 'Piqué', 'Puyol', 'Ramos'],
     ['Xavi', 'Busquets', 'X. Alonso'],
     ['Iniesta', 'Villa', 'Pedro']]

Podemos comprobar el acceso a distintos elementos::

    >>> team[0]  # portero
    'Casillas'

    >>> team[1][0]  # lateral izquierdo
    'Capdevila'

    >>> team[2]  # centrocampistas
    ['Xavi', 'Busquets', 'X. Alonso']

    >>> team[3][1]  # delantero centro
    'Villa'

.. admonition:: Ejercicio
    :class: exercise

    Escriba un programa que permita multiplicar únicamente matrices de 2 filas por 2 columnas. Veamos un ejemplo concreto:

    .. code-block::
    
        A = [[6, 4], [8, 9]]
        B = [[3, 2], [1, 7]]
    
    El producto :math:`\mathbb{P} = A \times B` se calcula siguiendo la `multiplicación de matrices`_ tal y como se indica a continuación:

    .. math::

        \mathbb{P}
        =
        \begin{pmatrix}
        6_{[00]} & 4_{[01]}\\
        8_{[10]} & 9_{[11]}
        \end{pmatrix}
        \times
        \begin{pmatrix}
        3_{[00]} & 2_{[01]}\\
        1_{[10]} & 7_{[11]}
        \end{pmatrix}
        =\\
        \begin{pmatrix}
        6 \cdot 3  + 4 \cdot 1 & 6 \cdot 2  + 4 \cdot 7\\
        8 \cdot 3  + 9 \cdot 1 & 8 \cdot 2  + 9 \cdot 7
        \end{pmatrix}
        =
        \begin{pmatrix}
        22 & 40\\
        33 & 79
        \end{pmatrix}

    .. only:: html
    
        |solution| :download:`matrix2x2.py <files/matrix2x2.py>`
    
        · Solución generalizada para matrices de cualquier dimensión: :download:`matrix.py <files/matrix.py>`

----

.. rubric:: EJERCICIOS DE REPASO

1. pycheck_: **max_value**
2. pycheck_: **remove_dups**
3. pycheck_: **flatten_list**
4. pycheck_: **remove_consecutive_dups**
5. pycheck_: **all_same**
6. pycheck_: **sum_diagonal**
7. pycheck_: **powers2**
8. pycheck_: **dec2bin**
9. pycheck_: **sum_mixed**
10. pycheck_: **n_mult**
11. pycheck_: **remove_second**
12. pycheck_: **nth_power**
13. pycheck_: **name_initials**
14. pycheck_: **non_consecutive**
15. pycheck_: **mult_reduce**
16. pycheck_: **digit_rev_list**
17. pycheck_: **time_plus_minutes**
18. pycheck_: **sum_positive**
19. pycheck_: **add_inverse**
20. pycheck_: **descending_numbers**
21. pycheck_: **merge_sorted**
22. pycheck_: **min_value**
23. pycheck_: **trimmed_sum**
24. pycheck_: **wolves**
25. pycheck_: **maxmin_values**
26. pycheck_: **cascading_subsets**
27. pycheck_: **diff_cuboid**
28. pycheck_: **fl_strip**
29. pycheck_: **logical_chain**
30. pycheck_: **smallest_unused_id**
31. pycheck_: **find_odds**
32. pycheck_: **reagent_formula**
33. pycheck_: **whats_next**
34. pycheck_: **npartition**
35. pycheck_: **add_length**
36. pycheck_: **reversing_words**
37. pycheck_: **barycenter**

.. rubric:: AMPLIAR CONOCIMIENTOS

* `Linked Lists in Python: An Introduction <https://realpython.com/linked-lists-python/>`_
* `Python Command Line Arguments <https://realpython.com/python-command-line-arguments/>`_
* `Sorting Data With Python <https://realpython.com/courses/python-sorting-data/>`_
* `When to Use a List Comprehension in Python <https://realpython.com/list-comprehension-python/>`_
* `Using the Python zip() Function for Parallel Iteration <https://realpython.com/python-zip-function/>`_
* `Lists and Tuples in Python <https://realpython.com/courses/lists-tuples-python/>`_
* `How to Use sorted() and sort() in Python <https://realpython.com/python-sort/>`_
* `Using List Comprehensions Effectively <https://realpython.com/courses/using-list-comprehensions-effectively/>`_

.. --------------- Footnotes ---------------

.. [#wishlist-unsplash] Foto original de portada por `Mike Arney`_ en Unsplash.
.. [#destructive] Cuando hablamos de que una función/método es "destructiva/o" significa que modifica la lista (objeto) original, no que la destruye.
.. [#return] Más adelante veremos el comportamiento de las funciones. Devolver o retornar un valor es el resultado de aplicar una función.
.. [#more-math] Existen multitud de paquetes científicos en Python para trabajar con listas o vectores numéricos. Una de las más famosas es la librería `Numpy`_.

.. --------------- Hyperlinks ---------------

.. _Mike Arney: https://unsplash.com/@mikearney?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText
.. _Numpy: https://numpy.org/
.. _producto escalar: https://es.wikipedia.org/wiki/Producto_escalar
.. _multiplicación de matrices: https://www.superprof.es/apuntes/escolar/matematicas/algebralineal/matrices/producto-de-matrices.html
.. _pycheck: https://pycheck.es
