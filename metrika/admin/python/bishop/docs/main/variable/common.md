## Переменная (Variable)

Переменные создаются с привязкой к окружению. Используются в тексте шаблона

Бывают четырёх типов.
Так как значения в форме передаются в строковом виде, система преобразует значения в зависимости от типа по следующим правилам:
- `STRING`
```python
str(value)
```
- `INTEGER`
```python
int(value)
```
- `BOOLEAN`
```python
metrika.pylib.utils.str_to_bool(value)
```
- `JSON`
```python
json.loads(value)
```

Тип переменных может быть важен при работе с Jinja шаблонами.
Переменная может быть ссылкой на переменную в другом окружении (см. Создание ссылки)
[Примеры созданных переменных](https://bishop.mtrs.yandex-team.ru/environment/metrika.playground.example)
[Использование их в шаблоне](https://bishop.mtrs.yandex-team.ru/template/example.xml)
[Готовый конфиг, в котором использованы эти переменные](https://bishop.mtrs.yandex-team.ru/config/1793)
