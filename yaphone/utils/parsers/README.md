## Parsers
Набор регулярок для парсинга Android-специфичных данных и не только.
Можно расширять, создавая свои парсеры.

### Использование
```
UaParser.parse(user_agent).get('device_type')
```

### Расширение

```
class MyAwesomeParser(RegexpParser):
  regexp = re.compile(r'(?P<entrance>My A\we\some ?Regexp)')

...
MyAwesomeParser.parse(some_string).get('entrance')
```
