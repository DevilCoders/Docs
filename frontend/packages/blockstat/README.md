# blockstat

Библиотека для формирования и записи blockstat-лога.

Описание формата: https://wiki.yandex-team.ru/jandekspoisk/dokumentacija/poiskovyelogi/#blockstatlog

## Если нужно поменять формат полей объекта

Полями `blocks` и `tree` могут обмениваться между собой объекты разных версий библиотеки. Поэтому важна совместимость функций сериализации/десериализации при изменении формата полей.
Подробности см. в коде и описании методов `BlockStat.prototype.serialize` и `BlockStat.prototype.restore`.

## Миграция на версию 1.4

- Передача в конструктор третьего аргумента `params` стала обязательной, если надо вызывать любой из методов `redirPrefixCore`, `redirFrom`, `clickHost`, `clickPrefix`
- Проверьте, что в вашем проекте не используются поля `BlockStat#blocksData`, `BlockStat#blocks_data`. В самом классе они не использовались и были удалены
- Замените в вашем проекте вызовы методов с подчёркиваниями `redir_prefix`, `redir_from`, `click_prefix`, `is_empty` на аналогичные в camelCase: `redirPrefix`, `redirFrom`, `clickPrefix`, `isEmpty` (в предыдущих версиях были оба варианта названия этих методов, теперь остался только camelCase)
