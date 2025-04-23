# Highlight.js

## Сборка

Счекаутить highlight-js с  [github](https://github.com/highlightjs/highlight.js)

**ВАЖНО:** Положить [yql](https://a.yandex-team.ru/arc/trunk/arcadia/yql/library/highlightjs_syntax/yql.js) в список языков, чтобы собрать с ним (так как его нет в коробке)

Далее есть несколько вариантов сборки:
- все языки и темы по отдельным минимизированным файлам, для этого выполнить
```sh
node tools/build.js -t cdn
```
- либо собрать билд для браузера с нужными языками
```sh
node tools/build.js -t browser yql lang2
```
## Заливка на статику

Можно с помощью [static-uploader](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/static-uploader).
Для авторизации можно взять креденшелы [робота](https://yav.yandex-team.ru/secret/sec-01cmj435me73jwafpxrqeqret8/explore/versions)
- Очистить папку ``build`` (иначе зальется все, что там)
- Cоздать папку ``build/_/highlight.js/<version>-<build>`` и положить туда все нужные для заливки файлы, сейчас так:
 ```
    <version>-<build>
        styles
            <name>.min.css
            ...
        highlight.min.js
```
``version`` - версия hl

``build`` - сборка (может отличаться набором языков)

- Выполнить 
```sh
YENV=production static-uploader
```

### Сборки

Сейчас есть:
- ``10.1.1-0`` - [common](https://highlightjs.org/download/) + дополнительные языки
```
node tools/build.js -t browser :common yql 1c actionscript applescript  clojure cmake csp d delphi dos django dockerfile erlang erlang-repl go haskell lisp matlab r scala smalltalk latex vbscript
```
- ``10.1.1-1`` - все доступные в hl языки + yql
