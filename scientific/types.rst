.. _python-built-in-types-and-operations:

Python Types and Operations
===========================

Python supports a number of built-in types and operations. This tutorial covers the most common types, but information about additional types is available `here <http://docs.python.org/library/stdtypes.html>`_

Basic numeric types
-------------------

The basic data numeric types are similar to those found in other languages, including:

* Integers (``int``)::

    >>> i = 1

* Floating point values (``float``)::

    >>> f = 4.3

* Complex values (``complex``)::

    >>> c = complex(4., -1.)

Manipulating these behaves the way you would expect, so an operation (``+``, ``-``, ``/``, ``*``, ``**``, etc.) on two values of the same type produces another value of the same type, while an operation on two values with different types produces a value of the more 'advanced' type:

* Adding two integers gives an integer::

    >>> 1 + 3
    4

* Multiplying two floats gives a float::

    >>> 3. * 2.
    6.0

* Subtracting two complex numbers gives a complex number::

    >>> complex(2.,4.) - complex(1.,6.)
    (1-2j)

* Multiplying an integer with a float gives a float::

    >>> 3 * 9.2
    27.599999999999998  # int * float = float

* Multiplying a float with a complex number gives a complex number::

    >>> 2. * complex(-1.,3.)
    (-2+6j)  # float * complex = complex

* Multiplying an integer and a complex number gives a complex number::

    >>> 8 * complex(-3.3,1)
    (-26.4+8j)  # int * complex = complex

However, there is one case where this happens but is not desirable, and that you should be aware of, which is the division of two integer numbers::

    >>> 3 / 2
    1

This behavior is widely regarded as a huge design mistake and Python 3.x has been fixed to behave like you would expect (more on Python 3.x later). A way to prevent this is to cast at least one of the integers in the division to a ``float``::

    >>> 3 / float(2)
    1.5

or::

    >>> 3 / 2.
    1.5

Lists
-----


Lists are sequences that can contain inhomogeneous data types:

    >>> l = [4, 5.5, "spam"]
    >>> l[0]
    4
    >>> l[1]
    5.5
    >>> l[2]
    'spam'

One useful operation with lists is ``+``, which can be used for concatenation::

    >>> [1,2,3] + [4,5,6]
    [1, 2, 3, 4, 5, 6]

    >>> ('spam', 'egg') + ('more spam','!')
    ('spam', 'egg', 'more spam', '!')

Lists can be *sliced*, meaning that we extract a chunk from the list::

    >>> a = ['spam', 'egg', 'bacon']
    >>> a[0:2]
    ['spam', 'egg']
    
Appending items to a list is also easy::

    >>> a = [1, 4, 3]
    >>> a.append(5)
    >>> a
    [1, 4, 3, 5]

Strings
-------

Strings (``str``) will be familiar from other programming languages::

    >>> s = "Spam egg spam spam"

You can use either single quotes (``'``), double quotes (``"``), or triple quotes (``'''``) to enclose a string (the last one is used for multi-line strings). To include single or double quotes inside a string, you can either use the opposite quote to enclose the string::

    >>> "I'm"
    "I'm"

    >>> '"hello"'
    '"hello"'

or you can *escape* them::

    >>> 'I\'m'
    "I'm"

    >>> "\"hello\""
    '"hello"'

You can access individual characters or chunks of characters::

    >>> s[5]
    'e'

    >>> s[9:13]
    'spam'

Note that strings are immutable, that is you cannot change the value of certain characters without creating a new string::

    >>> s[5] = 'r'
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    TypeError: 'str' object does not support item assignment

As for lists, concatenation is done with ``+``::

    >>> "hello," + " " + "world!"
    'hello, world!'

Finally, strings have many methods associated with them, here are a few examples::

    >>> s.upper()
    'SPAM EGG SPAM SPAM'  # An uppercase version of the string

    >>> s.index('egg')
    5  # An integer giving the position of the sub-string

    >>> s.split()
    ['Spam', 'egg', 'spam', 'spam']  # A list of strings

Dictionaries
------------

One of the remaining types are dictionaries (``dict``) which you can think of
as look-up tables::

    >>> d = {'name':'m31', 'ra':10.68, 'dec':41.27}
    >>> d['name']
    'm31'
    >>> d['flux'] = 4.5
    >>> d
    {'flux': 4.5, 'dec': 41.27, 'name': 'm31', 'ra': 10.68}

A note on Python objects
------------------------

Most things in Python are objects.  But what is an object?

Every variable or function in Python is actually a object with a
type and associated attributes and methods. An *attribute* is a property of the
object that you get or set by giving the <object_name> + dot +
<attribute_name>, for example ``img.shape``. A *method* is a function that the
object provides, for example ``img.argmax(axis=0)`` or ``img.min()``.

Use tab completion in IPython to inspect objects and start to understand
attributes and methods. To start off create a list of 4 numbers::

    l = [3, 1, 2, 1]
    l.<TAB>

This will show the available attributes and methods for the Python list
``a``.  **Using <TAB>-completion and help is a very efficient way to learn and later
remember object methods!**
::

    In [17]: a.<TAB>
    a.__add__           a.__ge__            a.__iter__          a.__repr__          a.append
    a.__class__         a.__getattribute__  a.__le__            a.__reversed__      a.count
    a.__contains__      a.__getitem__       a.__len__           a.__rmul__          a.extend
    a.__delattr__       a.__getslice__      a.__lt__            a.__setattr__       a.index
    a.__delitem__       a.__gt__            a.__mul__           a.__setitem__       a.insert
    a.__delslice__      a.__hash__          a.__ne__            a.__setslice__      a.pop
    a.__doc__           a.__iadd__          a.__new__           a.__sizeof__        a.remove
    a.__eq__            a.__imul__          a.__reduce__        a.__str__           a.reverse
    a.__format__        a.__init__          a.__reduce_ex__     a.__subclasshook__  a.sort

For the most part you can ignore all the ones that begin with ``__`` since
they are generally internal methods that are not called directly.  At
the end you see useful looking functions like ``append`` or ``sort`` which
you can get help for and use::

    a.sort
    a.sort?
    a.sort()
    a
