lint
====

Хуки и линтеры для статического анализа JS/CSS кода.

* jshint
* jscs
* csscomb

Быстрый старт
====

```bash
npm install --save git://github.yandex-team.ru/nodules/lint.git
```

В корневую директорию проекта положите файлы настроек:
* `.jshintrc`
* `.jscs.json`
* `.csscomb.json`

В проектном мейкфайле:

```bash
NODE010 = "путь до бинарника node 0.10+"
PRJ_ROOT = $(PWD)
...
.PHONY: build
...
ifeq ($(wildcard $(PRJ_ROOT)/node_modules/lint),)
	$(MAKE) git.hooks
else
include node_modules/lint/lint.mk
endif
```

Цели
====

* `git.hooks` - установить pre-commit хуки.
* `test` - запустить все тесты на все JS/CSS файлы.
* `jshint [JSFILES=...]` - запустить линтер на все файлы или на файлы, переданные параметром.
* `jscs [JSFILES=...]` - запустить линтер на все файлы или на файлы, переданные параметром.
* `csscomblint [CSSFILES=...]` - запустить линтер на все файлы или на файлы, переданные параметром.
* `csscomb [CSSFILES=...]` - отформатировать css-файлы посредством csscomb.
