# Написание, просмотр и выкладка документации
Документация хранится в [аркадии](http://a.yandex-team.ru/arc/trunk/arcadia/direct/docs/).

Краткий алгоритм:

1. Отредактировать существующие или добавить новые Markdown файлы
2. Проверить получившийся результат одним из способов:
   - собрать локально (об этом [ниже](#build-local))
   - собрать [на ppcdev](docs-on-ppcdev.md)
   - отправить изменения на ревью и подождать [автоматику](../../concepts/dev/documentation-auto-update.md#from-review)
4. Закоммитить


## Что "под капотом"
`ya make` [умеет](https://wiki.yandex-team.ru/yatool/docs/) собирать Markdown в статический сайт с использованием `yfm-docs`.

Какие компоненты в этом участвуют:

- `*.md` файлы — страницы документации
- `toc.yaml` — файл оглавления
- `.yfm` — настройки сборщика

## Написание документации
Используйте любой привычный вам редактор.

[Шпаргалка](https://docs.yandex-team.ru/docs/docstools/examples) по Yandex Flavored Markdown.

{% note tip %}

Для переноса строки нужно:
- напишите в конце предыдущей строки два пробела
- или напишите в месте переноса `<br>`

Чтобы начать новый абзац — оставьте перед ним пустую строку.

{% endnote %}

{% note tip %}

Перед списками тоже нужно оставлять пустую строку.

{% endnote %}

### Добавление новых страниц
У новых файлов обязательно должно быть расширение `.md`.

Важно не забыть добавить ссылку на новый файл в `toc.yaml` (оглавление) или другие страницы документации.
Если этого не сделать, то страница не попадёт в результат сборки.



### Быстрое редактирование
Редактирование возможно прямо из браузера.

На каждой странице документации в правом верхнем углу есть иконка карандаша "Редактировать в Arcanum" — она откроет файл в Аркануме.
Там его можно отредактировать (значком карандаша в правой части длинной серой плашки, рядом со ссылками _Blame view_ и _Raw_).
Внесите изменения, включите режим Preview (кнопка в правой верхней части) и бегло проверьте,
что нет бросающихся в глаза опечаток и не "едет вёрстка".
После этого можно коммитить.


## Сборка документации { #build-local }
Собрать документацию можно командой `ya make` из папки `direct/docs`.

{% note warning "Для тех, кто использует SVN-чекаут аркадии" %}

Перед первой сборкой нужно выполнить из корня аркадии команду `ya make --checkout -j0 tools/mkdocs_builder`.

{% endnote %}


### Локальный просмотр
В результате сборки получится файл `docs.tar.gz`.
Распаковать его можно командой
```sh
mkdir -p result && tar -xvf docs.tar.gz -C result
```

Всё, можно открывать html-страницы в браузере и смотреть что получилось.
На MacOS это можно сделать прямо из консоли:
```sh
open result/index.html
```

Пересборка и открытие документацию "в одну строку":

```sh
rm -rf result && ya make && mkdir -p result && tar -xvf docs.tar.gz -C result && open result/index.html
```


## Обновление документации
Обновление [автоматизировано](../../concepts/dev/documentation-auto-update.md).

Залить собранную вручную документацию **нельзя**.
Возможно только [ручное переключение](https://docs.yandex-team.ru/docstools/#release) тестинга/прода на одну из уже залитых роботом версий.


## Коммит
Не забудьте добавить новые файлы в коммит.

Для коммита в документацию __не нужно__ указывать тикет в коммит-сообщении (если уже есть — _можно_ указать).

Вместо коммита — обычно создается PR, проверяющий корректность сборки документации.
При успехе — он вливается в транк автоматически.
В Аркануме и SVN такое поведение можно обойти и сделать коммит сразу.


## Полезные ссылки
- о [сборке документации в Аркадии](https://wiki.yandex-team.ru/yatool/docs/)
- [примеры](https://docs.yandex-team.ru/docs/docstools/examples) Markdown и YFM синтаксиса
- [макросы](https://wiki.yandex-team.ru/arcadia/svn/) для коммитов в SVN
- официальный репозиторий [yfm-transform](https://github.com/yandex-cloud/yfm-transform)
