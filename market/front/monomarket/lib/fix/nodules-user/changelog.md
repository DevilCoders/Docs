# 7.1.0

**PR:** [#2775370](https://a.yandex-team.ru/review/2775370)
**Author:** @robot-metatron **Date:** 2022-07-27

Перенос [@yandex-int/nodules-user](https://gitlab.yandex-team.ru/nodules/user) с дополнениями.
Внуть добавлены `nodules-blackbox` и `yandex-mycookie`, чтобы не тащить ещё и их.
Зачем: у пакета зависимости стявятся с закрытого внутреннего гитхаба, в аркадию он не переехал, поддержки нет.

### Usage

В клиентских библиотеках заменить использование `@yandex-int/nodules-user` на `@yandex-market/user`.