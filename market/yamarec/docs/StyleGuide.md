# Руководство по стилю кода

- [Python](#python)
- [YQL](#yql)

## Python

### Модули

```python
# This guide is based on PEP 8.
# Additional suggestions are given in the comments and illustrated in the code.
# If your issue is not covered by the guide, follow PEP 8.
#
# Comments should contain well-formed English sentences.
# Put a single space right after the # mark.
# Limit the length of each line to 99 characters. Wrap words normally if you reach this limit; for
# example, like this.
# Favour docstrings over comments.
#
# Provide a docstring for each module, describing its purpose.
# It is a good place to give an quick overview of how this module integrates with other modules.
"""
The first phrase should be short and descriptive.

Separate it from the rest of the text with a blank line.
Also, leave the first line of a docstring blank to align all the text with the quotes.
When writing text, follow the same rules as for comments.
You can reference declared entities using $, e.g. $ExampleClass, $SOME_CONSTANT, $guide.tools.
Unlike comments, docstrings may also contain sections, e.g. Examples.
Class/method docstrings have their own specialized sections.

Examples:
    Don't put any blank lines after a section declaration.
    Use 4 spaces to indent the content of a section.
    You can create lists of items like this:
        - start each item with a lowercase letter
        - don't put commas/semicolons/periods at the end of list items

    - You can create a list at the top level of the section as well
    - In this case, start each item with an uppercase letter instead
    - Avoid mixing top-level lists with a regular text

    You can add some code snippets using the following syntax:

        >>> example = "indent the code block, show the output"
        >>> print(example.capitalize() + "!")
        Indent the code block, show the output!

    Separate such snippets from the text with blank lines.
"""
# Separate the module docstring from the code with two blank lines.


# Start your code by importing all required modules/packages.
# Split imports into 4 groups (as shown below), and keep each group sorted lexicographically.
# Never use the `from X import Y` statement to import from outside your package.
# Import one thing at a time (i.e. no commas are allowed in import statements).
#
# First, import standard libraries.
import os
import re
import sys  # Use inline comments only if necessary, separate them with 2 spaces.

# Then, import third-party libraries.
import bottle
import numpy
import numpy.linalg
import pytest

# Then, import your local package modules.
# Using full modules names will save you from any name conflicts.
# You can give them meaningful and distinguishable aliases if you will.
import guide.tools

# And then, import local package classes, decorators, and beans.
# Other kinds of "from" imports are not allowed.
# It is safe to use the `from X import Y` statement, since other items will be prefixed with
# the module name, e.g. ExampleClass won't clash with some.thirdparty.package.ExampleClass.
# This allows to simplify the code a bit.
from guide.example_class import ExampleClass
# Separate imports from the rest of the code with 2 blank lines.


# Declare constants first.
SOME_CONSTANT = 0
ANOTHER_ONE = "another one"

# Group declarations by putting blank lines between the groups.
UNRELATED_CONSTANT = {}
# Put two blank lines after constant declarations.


# Declare all classes.
# Choose an appropriate declaration order based on their importance.
# For example, here Guide is the main class of the module, while Helper is a secondary class, so
# it is declared after the Guide class.
class Guide(object):
    # No blank line between the declaration and the docstring.
    """
    An example class.

    Covers class-related issues.

    Class docstrings can have a special Attributes section.
    It uses Google-style-like variable definition to specify public attributes of the class.
    See below for details on the variable definition.

    Attributes:
        message (String) - some message
        transposition (String) - its reverse

    Examples:
        This is a good place to give a couple of usage examples.
    """
    # A blank line right after the docstring.

    # Methods should be separated with a single blank line.
    # They should be listed in the following order:
    #  - special
    #  - public
    #  - protected
    #  - private
    # Sort them lexicographically within each group.
    def __getitem__(self, index):
        return index

    # Method definitions follow exactly the same rules as function definitions.
    # Again, see below for details.
    def __init__(self, message=""):
        # Constructors DO NOT require a description in the docstring.
        # You can start the docstring with an "Args" section.
        """
        Args:
            message (String) - a message
        """
        self.message = message

    # Public methods and attributes should have meaningful names.
    # Please, provide a docstring for every public method.
    def split(self):
        """
        Split the message into several parts.

        Returns:
            Sequence[String] - message parts
        """
        return self.message.split("\t")

    # Use properties where applicable; it is a powerful mechanism.
    # Using protected properties is also a good idea.
    # Cache them if needed to get performance boost (via a decorator).
    # Document properties in the Attributes section of the class docstring.
    @property
    def transposition(self):
        return self.message[::-1]

    # Methods and attributes considered protected (i.e. non-public, but still can be used in
    # subclasses) should be prefixed with a single underscore.
    def _do_something_important(self):
        return [].append("done")

    # Methods and attributes considered private (e.g. implementation details) should use name
    # mangling in order to avoid conflicts in subclasses.
    # However, if the class is not intended to be extended by other classes, you better treat them
    # as protected (see above). It simplifies the code a lot.
    def __do_nasty_things(self):
        sys.exit(1)
# Put two blank lines after each class declaration.


class Helper(object):
    pass  # There is no need to put an extra blank line if there is no body.


# Then, declare functions in lexicographical order (public before private though).
def do_first_stuff():  # See below for details on how to declare/write/call a function.
    pass
# Put two blank lines after each function declaration.


# Do not shorten words; find a short synonym instead.
# It is okay to use `args`, `kwargs`, and `cls`, though.
@stack
@decorators({"like": "this"})
def do_some_stuff(  # Start wrapping arguments only if the declaration exceeds 99 characters.
        # If it still takes more than 99 characters, put each argument on a separate line. 
        required_argument,  # Notice the 8-space indentation.
        some_callback,  # It distinguishes arguments from the function body.
        optional_argument=(123456780 + 9),  # Surround complex default values with parentheses...
        crazy_argument=ExampleClass(),  # only if they are complex enough.
        default_url="https://market.yandex.ru"):  # Put ): here to emphasize your sadness.
    """
    Do some really important stuff.

    The first phrase should be imperative.
    The rest of the docstring should be in the present simple tense.

    Function docstrings can have special Args, Returns, and Raises sections.

    The Args section defines input arguments in Google-style-like form, i.e.
        [name] ([type hint according to PEP 484]) - [short description]
                [optional continuation of the short description]
            [more elaborate description if needed]

    Args:
        required_argument (Sequence[String]) - a list of strings
        some_callback(Callable[[Integral], String]) - some callback
        optional_argument (Integral) - the number of some things
        crazy_argument (Optional[ExampleClass]) - an instance of $ExampleClass or None
        default_url (String) - some URL

    The Returns section defines the type of the output and (optionally) its semantics.

    Returns:
        Iterable[String] - a stupid string generator

    The Raises section lists exceptions that might be thrown by the function with optional
    scenario description.

    Raises:
        ValueError if $crazy_argument is None
        RuntimeError
        NotImplementedError if $default_url != "https://market.yandex.ru"
    """

    # Declare nested functions before the function body.
    def nested_function(*args, **kwargs):  # Separate nested functions with blank lines.
        return "nested"

    # It is a good idea to put TODO marks if something needs to be fixed/refactored, e.g.
    # TODO: update the docstring.
    if crazy_argument is None:  # Always use `is None` to compare to None (to avoid confusion).
        # Start the message with a lowercase letter.
        # Do not put a period at the end of the message. Keep it simple.
        raise ValueError("the crazy argument must not be None")
    if default_url != "https://market.yandex.ru":
        raise NotImplementedError("custom URLs are not supported yet")
    short_list = ["keep", "short lists", "on one line"]
    long_list = [
        "this list",  # Use 4-space indentation here.
        "is too long",
        "we need to split it into several lines",
        "like this",  # Notice the comma. It simplifies further editing.
    ]
    short_dictionary = {"same": "thing"}
    long_dictionary = {
        "key": "value",
        "pairs": "are called items",
        "dictionary items": "follow similar rules as list items",
    }
    # Avoid putting blank lines in the function body; consider refactoring the function or using
    # nested functions as building blocks instead.
    yield nested_function(
        "this argument list doesn't fit in one line",  # Notice the 4-space indentation.
        "so we split it just like in a function definition",  # Use it in function calls.
        short_list,
        long_list,
        embedded_list=[  # Consider giving it a name rather than inlining it.
            "we can even use embedded long list definitions",
            "as we pass arguments to a function",
        ],
        embedded_dictionary={
            "or embedded long dictionary definitions": "like this",
            "even though it looks a bit weird and begs to be refactored": "later",
        },
        **long_dictionary)
    yield another_nested_function(
        "these args fit in one line", "so new line per argument is not necessary")
    # Extensively use list/dict/set comprehensions unless it blows the asymptotic complexity.
    # You can wrap long comprehensions like this:
    long_list_comprehension = [
        (key[:-1], value[:-1])  # Transformation.
        for key, value in long_dictionary.items()  # Iteration.
        if key != value  # Filtering.
    ]
    # Try to keep the main code branch at the lowest nesting level as possible, as long as it
    # improves readability. Processing corner cases first often helps.
    if not required_argument:
        for element in required_argument:
            if not element:
                # Feel free to use `continue` and `break` statements in such cases.
                continue
            # Keep the main code branch at the highest level possible.
            yield some_callback(len(element))
    yield required_argument[0]
    # And remember: the shorter, the better.
```

### Пакеты

```python
"""
Initialization files (like this one) serve only for publishing internal classes/functions and preloading
submodules. Thereby, it is highly recommended to use explicit relative imports here.
It is okay to use *-imports here, but only if really intended.

Putting every worth class into a separate file is a good practice, since it simplifies code
navigation and refactoring.
It is also recommended to put all exceptions into a separate submodule "exceptions".
"""

from . import preloaded
from .example_class import ExampleClass
from .guide import Guide
```

### Обозначения типов

```
This is the list of standard type hints (from PEP 484, slightly modified):
- None
    None is None
- Any
    any type at all
- Union[T1, T2, T3, ...]
    one of the listed types (T1, or T2, or T3, and so on)
- Optional[T]
    shortcut for Union[T, None] (always use it where appropriate)
- Tuple[F1, F2, F3, ...]
    a tuple with typed fields
    use ... to describe uncertainties
- Callable[[A1, A2, ...], R]
    a function that accepts arguments of types {Ai} and returns a result of type R
    Callable[..., R] accepts any arguments
- String
    shortcut for Union[bytes, str]
- Text
    unicode in Python 2, str in Python 3
- Number, Complex, Real, Rational, and Integral
    numeric types
- Boolean
    shortcut for bool
- DateTime
    date and time
- TimeDelta
    time interval
- Container
    implements __contains__
- ContextManager
    implements __enter__ and __exit__
- Hashable
    implements __hash__
- Reversible
    implements __reversed__
- Sized
    implements __len__
- Iterable[T]
    implements __iter__
    provides Iterator[T]
- Iterator[T]
    inherits from Iterable
    implements __next__
    iterates over elements of type T
- Set[T]
    inherits from Sized, Iterable[T], Container
    contains elements of type T
    basically, a read-only set
- MutableSet[T]
    inherits from Set[T]
    implements add, discard
    basically, a set
- Sequence[T]
    inherits from Sized, Iterable[T], Container
    implements __getitem__
    contains elements of type T
    basically, a read-only list
- MutableSequence[T]
    inherits from Sequence[T]
    implements __delitem__, __setitem__, insert
    basically, a list
- Mapping[K, V]
    inherits Sized, Iterable[K], Container
    implements __getitem__
    maps keys of type K to values of type V
    basically, a read-only dict
- MutableMapping[K, V]
    inherits from Mapping[K, V]
    implements __delitem__, __setitem__
    basically, a dict
- IO
    file-like object
- BinaryIO
    file-like object (binary mode)
- TextIO
    file-like object (text mode)
- DBConnection
    database connection (PEP 249-compliant)
- DBCursor
    database cursor (PEP 249-compliant)
- Module
    built-in module type

Refer to https://www.python.org/dev/peps/pep-0484/ for details.
```

## YQL

```sql
-- This is a YQL style guide.
--
-- Provide a short comment at the beginning of a YQL query if desired.
--
-- Try to limit the length of each line to 99 characters.
--
-- Use uppercase letters for statements and built-ins, e.g. SELECT, GROUP BY, IF, COALESCE, etc.
-- In general, follow naming conventions used here: https://wiki.yandex-team.ru/yql/userguide.
--
-- Separate the comment from the code with a single blank line.

PRAGMA MyCoolPath = "./cool.py";  -- Put a semicolon right at the end of each definition.
-- Separate distinct definitions from each other with a single blank line.

$my_cool_variable = (  -- Surround = with spaces here.
    -- Split your queries into functional "sections".
    -- Sections usually start with a keyword, like SELECT, GROUP BY, etc.
    -- Stick to the following order of sections in your queries: INSERT-SELECT-FROM.
    SELECT single  -- Do not wrap section content if it consists of just one item...
    FROM [nowhere]  -- or doens"t contain a subquery...
    WHERE day = "2017-08-06"  -- or consists of just one condition.
);

INSERT TABLE [regular_table] WITH TRUNCATE
-- Wrap multi-line section contents as follows:
SELECT
    MIN(time) AS time,
    user,
    query
FROM (  -- Wrap and indent multi-line subqueries like this.
    SELECT *
    FROM (
        --
    ) AS l  -- It's OK to use one-letter subquery aliases.
    JOIN (  -- Put the `JOIN` on a separate line.
        --
    ) AS m
    USING (user)  -- Prefer USING to ON.
    JOIN (
        --
    ) AS r
    ON  -- Wrap and indent long conditions; parenthesize only if necessary.
        r.user = l.user  -- Right table"s field goes first.
        AND r.query = m.query
    JOIN t ON t.time = l.time
    UNION ALL  -- Put the `UNION ALL` on a separate line.
    SELECT *
    FROM (
        --
    )
)
WHERE
    day = "2016-05-21"  -- Break lines before logical operators when you wrap long conditions.
    AND (  -- Use parentheses only when needed.
        user RLIKE "noo+b"
        OR query = "/index"
    )
    AND 1 = 1
GROUP BY
    user,
    query
ORDER BY
    user,
    time
LIMIT 100
```
