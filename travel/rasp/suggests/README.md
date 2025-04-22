# suggests

Микросервис саджестов откуда/куда переписанный на go

* Расположение в Platform (QLoud): https://platform.yandex-team.ru/projects/rasp/suggests/
* Production домен: ***suggests3.rasp.yandex.net***
* Testing домен: ***suggests.tst.rasp.yandex.ru***

***ATTENTION***: suggests.tst.rasp.yandex.net - старые саджесты на Python

## Requirements

* Для возможности пушить новые версии контейнеров, нужны доступы в IDM к Docker-registry репозиторию rasp/suggests (роль contributor или owner)

Для локальной работы приложения необходимы индексные файлы `objs_data.msgpack` и `idconverter.msgpack`. Они генирируются автоматически в Sandbox. Для того что-бы скачать актуальные индексы, нужно:

* Зайти по ссылке - https://sandbox.yandex-team.ru/tasks?order=-updated&type=RASP_SUGGESTS_DISTRIBUTE_DATA&hidden=true&children=true&page=1&pageCapacity=20&forPage=tasks

* Выбрать самый последний выполненный таск
![Выбираем таск](https://jing.yandex-team.ru/files/corsac/Tasks__Sandbox_2017-11-15_20-09-56.jpg)

* Зайти к нему в ресурсы, найти HTTP урл сгенерированного файла ресурса и скачать файлы `objs_data.msgpack` и `idconverter.msgpack`, положив их в корень проекта
![Выбираем вкладку ресурсы](https://jing.yandex-team.ru/files/corsac/Task_174958506_RASP_SUGGESTS_DISTRIBUTE_DATA_2017-11-15_20-12-36.jpg)
![Скачиваем ресурсы](https://jing.yandex-team.ru/files/corsac/Task_174958506_RASP_SUGGESTS_DISTRIBUTE_DATA_2017-11-15_20-18-42.jpg)

## Запуск

Для локальной работы достаточно сбилдить бинарник и запустить его на порту:

```
ya make

./suggests -p 3030                       # production окружение
YENV_TYPE=testing ./suggests -p 3030     # testing окружение
```

## Разработка и отладка

Разрабатывать удобнее всего в среде GoLand от JetBrains. После открытия проекта в GoLand можно настроить конфигурацию запуска. Для этого нужно нажать Edit Configuration и добавить конфигурацию Go Build, указав Run kind: File, Files и Working Directory - каталог репозитория, module - suggests. Аналогично, запуска тестов добавить конфигурацию Go Test, только Test kind указать - Directory.
