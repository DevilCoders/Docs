# Обновление документации через WEB

Обновлять документацию в docs можно через web-интерфейс [arcaria:noc:docs](https://a.yandex-team.ru/arc/trunk/arcadia/noc/docs/nocdocs).

## Инструкция

### Шаг 1

Выберите файл, который хотите изменить. Например, в файл [glossary.md](https://a.yandex-team.ru/arc/trunk/arcadia/noc/docs/nocdocs/glossary.md) мы добавим термин `Router`.

### Шаг 2

Открываем файл:
  - либо через arcadia: [glossary.md](https://a.yandex-team.ru/arc/trunk/arcadia/noc/docs/nocdocs/glossary.md)
  - либо в web: [glossary](https://docs.yandex-team.ru/nocdoc/glossary)

{% cut "Если открыли через web, то нажимаем на "карандаш":" %}

![img.png](images/img.png)

{% endcut %}

### Шаг 3

Нажимаем на "карандаш" - Edit this file

![img_1.png](images/img_1.png)

### Шаг 4

Вносим изменения

![img_2.png](images/img_2.png)

### Шаг 5

Нажимаем `commit`

![img_3.png](images/img_3.png)

Добавляем комментарии к commit

![img_4.png](images/img_4.png)

Нажимаем "Send to review"

### Шаг 6

Попадаем на страницу с Pull Request.

Вы можете увидеть различную информацию:
- стадии тестирования
- reviewer
- логи
- и пр.

![img_5.png](images/img_5.png)

Тесты прошли успешно:

![img_7.png](images/img_7.png)

Можем на этом этапе нажать "Ship".

### Шаг 7

Если тесты завершились успешно, и мы нажали "Publish" и "Ship", то вы увидете такую картинку:

![img_8.png](images/img_8.png)

### Шаг 8

Далее добавленные контент окажется на стадии тестирования.

![img_9.png](images/img_9.png)

### Шаг 9

После публикации в prod, вы сможете увидеть изменения на портале документации.

| Было | Стало |
|------|-------|
|![img_6.png](images/img_6.png)|![img_10.png](images/img_10.png)|

## Плюсы и минусы такого подхода

### Плюсы
1. Просто и быстро сделать быстрые изменения
2. Низкий порог входа

### Минусы
1. Нет возможности сделать `ya make` - не получится проверить все ли хорошо с картинками, ссылками и прочим
