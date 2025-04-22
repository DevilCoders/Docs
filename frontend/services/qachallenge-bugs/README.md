# Примеры

Приложение запущено на продакшен стенде по ссылке https://qachallenge-bugs.si.yandex-team.ru/

Приложение запущено на тестовом стенде по ссылке https://test-qachallenge-bugs.si.yandex-team.ru/

# Деплой:
Лучше использовать форму

### В прод (с помощью формы):
1) открыть форму по ссылке: https://forms.yandex-team.ru/surveys/50569/
2) выбрать репозиторий: search-interfaces/frontend
3) выбрать ветку: master
4) вписать в название сервиса: qachallenge-bugs
5) выбрать причину: Внеплановый релиз 
6) нажать кнопку запуска релиза

### В прод (руками):
перед тем как пушить надо подключить наш docker registry. по факту сделать просто docker login ...
(инструкция про наш докер - https://wiki.yandex-team.ru/qloud/docker-registry/)

Переходим в папку с проектом 
1) `docker build . -t qachallenge-bugs:v<номер версии типа 0.0.3, обязательно надо поменять чтобы yd ее подхватил> --network=host --no-cache`
2) `docker tag qachallenge-bugs:v0.0.3 registry.yandex.net/shri/bundleteam-bugs:v0.0.3`
3) `docker push registry.yandex.net/shri/bundleteam-bugs:v0.0.3`

последнюю версию смотрим в yd - и делаем +1
аналогично для проекта админки qachallenge
докер обновлен, идем менять версию в yd → config → edit → меняем версию образа → save → deploy

yd qachallenge-bugs: https://yd.yandex-team.ru/stages/qachallenge-bugs-prod


### В тестовый стейдж:
Происходит автоматически при мердже pr в основную ветку

### Автособранные беты

доступны по адресу https://shri-```{НАЗВАНИЕ ПРОЕКТА НА BB}```-{{```ИМЯ ВЕТКИ```}}.ui-development-school.yandex-team.ru

***Например:***

https://shri-bundleteam-bugs-master.ui-development-school.yandex-team.ru


## Команды

***npm run fix***
Исправляет файлы в папке или файл (путь к к папке или файлу передаётся в аргументе и указывается относительно папки templates) согласно правилам указанных в файле src/fixInit.js
