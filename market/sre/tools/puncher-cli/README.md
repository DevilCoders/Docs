Утилита для массовой модификации правил в Puncher
-------------------------------------------------

Найти правила содержащие домен.

   ./puncher-cli find\_fqdn  test2.tst.vs.market.yandex.net 

Добавить домен `test3` в правила содержащие `test2`.

   ./puncher-cli add\_fqdn --comment 'puncher test'  test2.tst.vs.market.yandex.net test3.tst.vs.market.yandex.net

С опцией `--debug` - показывать запросы и ответы от сервера.

   ./puncher-cli --debug find\_fqdn|add\_fqdn ...
