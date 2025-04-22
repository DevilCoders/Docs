---
title: Seo-страницы поездов
---

## Организация данных в танкере

### Ветки
В танкере шаблоны лежат в двух ветках:
- [trains-testing](https://tanker.yandex-team.ru/project/travel-backend?branch=trains-testing) - для разработки и тестирования
- [master](https://tanker.yandex-team.ru/project/travel-backend?branch=master) - production ветка

Редактируем и добавляем шаблоны всегда в ветке trains-testing, после проверки мержим ветку trains-testing в master.

### Кейсеты
Предполагается 1 кейсет для текстовых констант trains.common и по 2 кейсета для каждой seo-страницы: кейсет с шаблонами и кейсет с тестами.

- [trains.common](https://tanker.yandex-team.ru/project/travel-backend/keyset/trains.common?branch=trains-testing) - текстовые константы 
- [trains.direction-landing](https://tanker.yandex-team.ru/project/travel-backend/keyset/trains.direction-landing?branch=trains-testing) - шаблоны страницы направлений
- [trains.direction-landing.tests](https://tanker.yandex-team.ru/project/travel-backend/keyset/trains.direction-landing.tests?branch=trains-testing) - тесты шаблонов страницы направлений

### Ключи кейсета seo-страницы
Кейсет seo-страницы может содержать произвольное количество django-шаблонов, они все будут рендериться с набором данных, который формируется на бекенде. Схема данных и доступные шаблонам поля уникальны для каждой seo-страницы, но одинаковые для всех шаблонов одной seo-страницы.
Кейсет seo-страницы содержит корневой ключ в формате json "response.scheme" - он описывает структуру ответа ручки seo-страницы, в нем вместо текстов содержатся ключи этого же кейсета с шаблонами.

Некоторые блоки seo-страницы могут не выводится итоговом ответе бекенда, если шаблонизатор отрендерил пустую строку, например это используется для блока [faq.prices.text](https://tanker.yandex-team.ru/project/travel-backend/keyset/trains.direction-landing/key/faq.prices.text?branch=trains-testing) когда на направлении нет цен.

На примере direction-landing:
- [response.scheme](https://tanker.yandex-team.ru/project/travel-backend/keyset/trains.direction-landing/key/response.scheme?branch=trains-testing) - корневой ключ в формате json
- [header.title](https://tanker.yandex-team.ru/project/travel-backend/keyset/trains.direction-landing/key/header.title?branch=trains-testing) - шаблон "header.title", будет подставлен в "response.scheme" вместо "header.title"
- [response.scheme.empty.direction](https://tanker.yandex-team.ru/project/travel-backend/keyset/trains.direction-landing/key/response.scheme.empty.direction?branch=trains-testing) - корневой ключ для рендера страницы, когда на выбранном направлении нет поездов

### Тесты шаблонов
Чтобы тестирование шаблонов не зависило от внешних факторов, полный набор данных для рендера шаблонов задается в танкере. 

В тестах шаблонов возможны следующие ключи:
- "data-{{dataset.name}}" - набор данных для тестирования, например "data-full".
- "{{template.name}}-{{dataset.name}}" - ожидаемый результат рендера шаблона {{template.name}} при использовании набора данных {{dataset.name}}, например "info.text-full".
- "response.scheme-{{dataset.name}}" - ожидаемый результат ответа бекенда при использовании набора данных {{dataset.name}}, например response.scheme-full.

В кейсете может быть несколько наборов данных, с кажым из них можно тестировать разные шаблоны. 

## Синтаксис шаблонов

Шаблоны поддерживают синтаксис [django-templates](https://docs.djangoproject.com/en/1.8/ref/templates/language/). 
Реализация на go - [pongo2](https://github.com/flosch/pongo2).

**Особенности**
Все переносы строки удаляются при рендеринге шаблонов, при этом все пробелы сохраняются.

### Основы языка шаблонов
Все очень шохоже на jinja2, кроме вызова фильтров - [отличия от jinja2](https://jinja2docs.readthedocs.io/en/stable/switching.html#django)

Условие: если есть пользователь, то здороваемся по имени, иначе просто "Привет!"
```
{% if User %}
Привет {{User.Name}}!
{% else %}
Привет!
{% endif %}. 
```

Применение фильтра: join с параметром ", " к полю Users. Например для списка ["Вася", "Женя", "Юра", "Макс"] получится "Вася, Женя, Юра, Макс"
```
{{Users|join:", "}}
```

Применение нескольких фильтров: join_last и join. Чтобы получилось "Вася, Женя, Юра и Макс"
```
{{Users|join_last:" и "|join:", "}}
```

Цикл: перечисляем пользователей из спаска Users. Например "Вася Женя Юра Макс "
```
{% for user in Users %}
{{user}} 
{% endfor %}.
```

Цикл: здороваемся со всеми пользователями из списка Users. Например "Привет Вася, Женя, Юра и Макс!"
```
{% for user in Users %}
{% if forloop.First %}
Привет {{user}}
{% elif forloop.Last %}
 и {{user}}
{% else %}
, {{user}}
{% endif %}
{% endfor %}!
```

### Названия станций и городов
Фильры для форм городов и станций:
- nominative: имя города в именительном падеже, например Москва
- genitive: имя города в родительном падеже, например Москвы
- dative: имя города в дательном падеже, например Москве
- accusative: имя города в винительном падеже, например Москву
- prepositional: имя города в предложном падеже, например Москве
- preposition_in: предлог в/во/на (в значении где?)
- preposition_to: предлог в/во/на (в значении куда?)
- locative: то же самое что и "{{city|preposition_in}} {{city|prepositional}}", например "в Москве"
- directional: то же самое что и "{{city|preposition_to}} {{city|accusative}}", например "в Москву"
- ablative: то же самое что и "из {{city|genitive}}", например "из Москвы"


## Выкатка изменений шаблонов

### TRAINS_DUMP_TEMPLATES

Таск в sandbox TRAINS_DUMP_TEMPLATES проверяет шаблоны в танкере и подготавливает их для использования в выбранном окружении. Окружение задается параметром Environment=testing/production.
После выполнения задачи в ней пишется лог выполнения тестов. 
Если провалена валидация шаблона, то будет выведен текст ошибки. 
Если в тесте ожидаемый результат не соответствует рендеру, будет выведен diff.

### Порядок выкатки шаблонов

1) правим шаблоны в танкере в ветке trains-testing
2) запускаем таск TRAINS_DUMP_TEMPLATES с параметром Environment=testing, смотрим что он выполнился успешно
3) ждем 5 минут, пока search-api перечитает шаблоны
4) ходим по seo-страничкам в тестинге, любуемся результатом
5) если в тестинге все ок, то в танкере мержим ветку trains-testing в master
6) запускаем TRAINS_DUMP_TEMPLATES с параметром Environment=production
7) ждем 5 мин search-api
8) проверяем шаблоны в проде


## Сборка и выкатка кода

[search_api:README](https://a.yandex-team.ru/arc_vcs/travel/trains/search_api/README.md)
