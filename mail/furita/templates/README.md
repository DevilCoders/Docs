
Скрипт для выкачивания шаблонов сообщений (автоответов, подтверждений правил итд) из танкера.

Использование:
```
$ cd ~/arcadia/mail/furita/templates
$ ya make --checkout
$ ./get-message-templates -t `ya vault get version sec-01d34s477p8fak79sq374swfqa -o tanker.oauth.token`
$ cd ~/arcadia/mail/furita/etc
$ svn ci -m 'update templates'
...
# собираем и релизим новую версию furita
```
