### Yandex.Directory документация

* [Документация разработчика](http://dir.yd-dev.cmail.yandex.net/docs/docs_dev.html)
* [Документация для потребителей API](http://dir.yd-dev.cmail.yandex.net/docs/index.html)

### Как писать документацию

Изменяем .md файлы и билдим html:

    $ make build_docs

Можно повесить вотчер на автоматическое обновление:

    $ sudo pip install watchdog
    $ make watch_docs

На забывать комитить в ветку `gh-pages`