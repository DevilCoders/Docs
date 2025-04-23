# EntityLists Shooter

Тулза для обстрела беты **entitysearch** списочными (и не только!) контекстами.

## Собираем контексты
Для обстрела необходимы патроны! О том, как их нагенерировать, можно прочитать [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/search/wizard/entitysearch/tools/evlogdump/README.md).
Если вам по какой-то причине не подходит схема с вылавливанием логов из прода, есть альтернатива -- прострелять свою бету корзинкой с метрикса (при условии, что бета поднята с опцией `--log {file}`), а затем прогнать дампер на получившемся небольшом логе. Главное условие -- чтобы в итоговой табличке на YT присутствовала колонка `Base64Context`.

## Стреляем
Предположим, что вы подняли две беты (неудобно, но что ж делать) по адресам `test_host:apphost_port` и `prod_host:apphost_port` (сами контесты будут отправляться в ручку `host:port/serp`). Тогда стрельбу можно запустить так:
`./entity_lists_shooter {mode} --input-table {table} --output-table {table} --test-address test_host:apphost_port --prod-address prod_host:apphost_port`. Более тонкие настройки можно найти [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/search/wizard/entitysearch/tools/entity_lists_shooter/lib/shooting_options.h?rev=r7600853#L42). Советую добавлять флаг `--dump-context`, чтобы иметь возможность перезадавать запросы, вызывающие дифф.

## Хочу свой кастомный компаратор карточек
Создайте наследника для [TComparisonOperator](https://a.yandex-team.ru/arc/trunk/arcadia/search/wizard/entitysearch/tools/entity_lists_shooter/lib/compare.h?rev=r7779539#L27). Примеры можно найти в `lib/operators`.
