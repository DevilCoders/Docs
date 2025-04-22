## Запуск разработческой версии (на примере webmaster3-viewer)
* На машине `webmaster.dev.search.yandex.net` создать в домашнем каталоге каталог `mvn-dist`
* На своей машине в корне проекта создать файл `application.development.json`:
```
{
    "deployment": {
        "host": "webmaster.dev.search.yandex.net",
        "root-path": "mvn-dist"
    }
}
```
* Cоздать файл webmaster3-viewer-assembly/application.development.json (в качестве номеров портов надо указать порты, которые еще никем не заняты на `webmaster.dev.search.yandex.net`):
```
{
    "http": {
        "port": 33500 
    },
    "debug": {
        "enabled-by-default": false,
        "port": 35987
    }
}
```
* Важно, чтобы порт был в диапазоне 33000-34999, если его использует фронт 
* `svn checkout svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/wmconsole/backend/packaging-tools`
* `./packaging-tools/bin/application_deploy.py webmaster3-viewer` (тут предполагается, что мы в папке java и установлен `maven`)
* Зайти по ssh на `webmaster.dev.search.yandex.net:/mvn-dist/webmaster-viewer` и выполнить `./restart.sh`

## Автоборка deb пакета для релиза
* Находясь в корне каталога `xxxx-assembly`, добавить новую строчку в debian/changelog: `dch --distributor=debian -i 'Some comment about this release, like ticket number'`
* `svn ci -m "SKIP_CHECK New version"`
* Дальше запуститься автосборка, по окончании которой на почту придет письмо от Кондуктора
