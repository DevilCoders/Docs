# mbo-gwt

Устаревший сервис работающий на базе GWT.
Канет в лету как только все гвт странички будут переписаны на react.
Новый модуль лежит в модуле mbo-react-ui

## Запуск на aida
Для запуска на aida используется скрипт scripts/dev/run-mbo-gwt.py

## Особенности YA
Для реализации полноценной сборки на ya сделана хитрая генерация и разбиение на подмодули проекта mbo-gwt
- в модуле gwt-src генерятся исходники для mbo-gwt
- Основной конфиг прописан в корневом mbo-gwt/ya.make
- gwt-gen/ya.make необходим для билда jar файла с помощью команды ya package, который поедет в няня сервис

Я сам не до конца понимаю хитрость с SET(targetDir ${CURDIR}/gwt-out), но она работает, поэтому эту строку не сносить

## Devops

### Дашборды

#### Прод

[Тайминги](https://solomon.yandex-team.ru/?project=market-mbo&dashboard=mbo-gwt-production-timings)

#### Тестинг

TBD

## Разработка

### Подключение react-ui

Для подключения mbo-react-ui при разработке на dev-сервере нужно сначала запустить на dev-сервере mbo-react-ui используя scripts/dev/run-mbo-react-ui.sh, а потом выполнить на странице gwt следующий код, заменим домен на свой:
```javascript
ln = document.createElement('link');
ln.rel = 'stylesheet';
ln.href = 'https://mbo-gwt-alabr-aida-4840.user.derkoat.yandex.ru/ui/static/css/main.css';
document.body.appendChild(ln);
sc = document.createElement('script');
sc.src = 'https://mbo-gwt-alabr-aida-4840.user.derkoat.yandex.ru/ui/static/js/main.js';
document.body.appendChild(sc);
```
