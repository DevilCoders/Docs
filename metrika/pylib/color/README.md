# Модуль metrika.pylib.color

Простейший модуль для раскраски текста. Содержит функцию colorize, поддерживается 3 цвета: red, yellow, green

### Пример использования
```py
>>> from metrika.pylib.color import colorize
>>> colorize('Hello, World!', 'red')
'\x1b[91mHello, World!\x1b[0m'
>>> print(colorize('Hello, World!', 'red'))
Hello, World!
```
