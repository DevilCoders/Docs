Пожалуйста, ознакомьтесь с [правилами разработки переранжирований](https://wiki.yandex-team.ru/jandekspoisk/kachestvopoiska/rearrange/codereview/) и [документацией переранжирований](https://wiki.yandex-team.ru/jandekspoisk/kachestvopoiska/rearrange/documentation/)

Вопросы про разработку переранжирований можно задать в [чате](https://t.me/joinchat/AAAAAEFgd-1cJ4ASIruPhg)


Про фреймворк юнит-тестов переранжирований
==========================================

Здесь приведён фрагмент письма velavokr@ начала января 2018 года, соответственно, со временем часть ссылок может устареть.

Недостатки: не хватает возможности читать канонизированные входные данные из файла,
это нужно будет добавить. Сейчас входные данные хардкодятся в юнит-тесты, и это не очень удобно.

https://a.yandex-team.ru/arc/trunk/arcadia/search/web/util/ut_mocks/meta_mock.h

Примеры использования
=====================

Вот тут эмулируются запросы в источники:

https://a.yandex-team.ru/arc/trunk/arcadia/search/web/core/querysearch/ut/querysearch_request_ut.cpp

Вот тут тестируется работа двух переранжирований в связке:

https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/querysearch/ut/querysearch_ut.cpp

Вот так переопределяется конфиг переранжирований. Полезно, например, когда несколько переранжирований должны работать в связке,
либо нужно тестировать разные варианты инициализации (например, зависящие от типа метапоиска, локали, устройства или изнаночности):

https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/querysearch/ut/ya.make
https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/filterbanned/web/bans/ut/ya.make

Вот тут тестируется работа сложных переранжирований, состоящих из большого числа простых правил:

https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/filterbanned/web/bans/ut/apply_bans_web_ut.cpp
https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/filterbanned/web/snippets/ut/apply_snippets_web_ut.cpp

Вот тут коллеги использовали фреймворк и написали годные тесты:

https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/blender_dssm_features/apply_dssm_ut.cpp
https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/dumper/extraction_ut.cpp
https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/fconsole/manual_fixer_ut.cpp
https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/saas_snippets/ut/saas_snippets_ut.cpp
https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/turbo_page_checker/lib/ut/turbo_page_checker_ut.cpp
