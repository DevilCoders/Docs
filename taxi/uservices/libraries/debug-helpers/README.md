== Debug helpers ==
This library provides helper classes and templates, that can be used for
debugging purposes. Although it is ok to release service that uses
those classes to production, please do not forget to remove them eventually -
most of the classes and templates incure heavy penalty on performance.

Classes/templates:
* Countable - counts the number of alive instances of the given class
