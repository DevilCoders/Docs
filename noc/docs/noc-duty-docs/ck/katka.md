# Процедуры обновления ЦК

### Деплой ЦК

1.  Ставим тег в [репозитории ЦК](https://noc-gitlab.yandex-team.ru/nocdev/noc-ck/-/tags)
2.  Дожидаемся завершения [пайплайна](https://noc-gitlab.yandex-team.ru/nocdev/noc-ck/-/pipelines)
3.  Создаём тикет в кондукторе:
    1.  Переходим в кондуктор в [тикеты пакета noc-ck](https://c.yandex-team.ru/packages/noc-ck/tickets)
    2.  Нажимаем "клонировать" у последнего (верхнего) тикета
    3.  В открывшейся форме указываем:
        - Версия: номер новой версии ЦК
        - Комментарий: краткий changelog в свободной форме с описанием изменений
    4. Нажимаем "Сохранить"
4. У созданного тикета нажимаем "Выложить", начнётся деплой
5. Дожидаемся завершения и при необходимости смотрим логи выкладки

### Обновление cli на noc-sas

У нас нет автоматической выкладки noc-ck-cli на noc-sas, и поэтому обновление клиента происходит спонтанно по
необходимости

Для обновления noc-ck-cli нужно:

1.  Найти последнюю версию в [тегах репозитория ЦК](https://noc-gitlab.yandex-team.ru/nocdev/noc-ck/-/tags) (для примера
    дальше будем считать, что мы обнаружили версию `v0.80-1`)
2.  Зайти на noc-sas под рутом и выполнить:

    ```bash
    cd /usr/share/noc-ck
    git fetch
    git checkout v0.80-1
    source /usr/share/noc-ck/venv/bin/activate
    python setup.py bdist_egg
    easy_install dist/noc_ck-0.1-py3.7.egg
    ```

### Обновление Аннушки в ЦК

Аннушка обновляется руками по необходимости (планы по автоматизации есть в
[NOCDEV-4616](https://st.yandex-team.ru/NOCDEV-4616)). Старая Аннушка может приводить к тому, что
сценарии с
[ann_deploy action](https://docs.yandex-team.ru/ck/plugins/ann_deploy_action) будут катить конфиги
из неактуальной Аннушки. Чтобы обновить Аннушку, нужно обновить сабмодуль в склонированном
[репозитории ЦК](https://noc-gitlab.yandex-team.ru/nocdev/noc-ck/):

```bash
# инициализируем и выставляем сабмодуль Аннушки в изначальное (старое) состояние
git submodule update --init

# создаём новую ветку с изменением
git checkout -b update-annushka

# переходим в директорию с сабмодулем Аннушки
cd modules/annushka/

# выставляем сабмодуль Аннушки в состояние актуального мастера
git checkout master
git pull

# возвращаемся в корень проекта
cd ../..

# фиксируем изменение ссылки на сабмодуль Аннушки
git add modules/annushka

# коммитим и создаём ветку
git commit -m "Update Annushka"
git push -u origin update-annushka
```

Затем отправляем Merge Request (пример
[тут](https://noc-gitlab.yandex-team.ru/nocdev/noc-ck/-/merge_requests/321)), получаем OK,
вмерживаем и выкатываем ЦК по инструкции выше
