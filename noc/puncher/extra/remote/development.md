

# Зависимости

-   docker на локальном хосте
-   ansible
-   ya
-   docker role
    Берем готовую

        ansible-galaxy install nickjj.docker


## ya tool qyp


### Для управления виртуалками надо поставить [QYP CLI](https://wiki.yandex-team.ru/qyp/cli/).

На вики есть [инструкция](https://wiki.yandex-team.ru/yatool/distrib/). Я ставил так:

    curl https://api-gotya.n.yandex-team.ru/ya > ~/bin/ya
    chmod +x ~/bin/ya


### Токен

-   Получаем токен [тут](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=d13a24721141492096c50ed35d33f8fd).
-   Кладем его себе в .bashrc/.zshrc и так далее по вкусу

    echo "export VMCTL_TOKEN=<token>" >> ~/.zshrc
    . ~/.zshrc


### Проверяем что получилось

    ya tool qyp list


## Проверяем работу клиента секретницы

    ya vault list secrets

    +--------------------------------+----------------------------------------------------------------+--------------------------------+-------+-------+--------+---------------------+
    | secret uuid                    | name                                                           | last version uuid              |   cnt |   tok | acl    | created             |
    |--------------------------------+----------------------------------------------------------------+--------------------------------+-------+-------+--------+---------------------|
    | sec-01dv2xjs5gd8zd1rdcjaaj8ada | puncher-test-s                                                 | ver-01dv2y3cmrha6e7vn5hp21wbzg |     2 |     0 | OWNER  | 2019-12-02 12:03:08 |
    | sec-01dth3s03eqg58x9bdgk849fjx | certificate_7F000A7D58B70FAB46B0690EF80002000A7D58_private_key | ver-01dth3s05nakeeh1qyenh78a0f |     1 |     0 | OWNER  | 2019-11-25 14:05:04 |
    | sec-01dth1s0gm78r8zrhybx4cmsz7 | certificate_7F000A7CEB34BD5430C648F9D40002000A7CEB_private_key | ver-01dth1s0j34a4zanqkt96xz3hm |     1 |     0 | OWNER  | 2019-11-25 13:30:07 |
    | sec-01dtgxrqsgxcf8vnh8jd6zph84 | certificate_7F000A7C14D2C244BF35E199EB0002000A7C14_private_key | ver-01dtgxrqved5dj46vbw49tmkhe |     1 |     0 | OWNER  | 2019-11-25 12:20:04 |
    | sec-01ds3987pdg92nb49m1emt3mcg | rt-key                                                         | ver-01ds3987pq9kh370jdb2xb03fe |     1 |     1 | READER | 2019-11-07 18:55:42 |
    | sec-01drxjckr3spg0tx9hk3thqya2 | tacplus-secret                                                 | ver-01drxrm658qkxkge5y54t9fnv3 |     1 |     0 | OWNER  | 2019-11-05 13:39:56 |
    | sec-01dpjr4jyjzzkhrwnfxd8ngksp | contest                                                        | ver-01dpjr4jyv313m45wx4w9zr2w9 |     1 |     0 | READER | 2019-10-07 12:17:22 |
    | sec-01dfdgdq0j9ps14amet875v6t8 | FIXME                                                          | ver-01dfdgdq11kkm5xekyrbvb1yqy |     1 |     5 | READER | 2019-07-10 11:36:28 |
    | sec-01dc1dxehkb9ehssp4tyytz29e | hermione-usage-stats-db                                        | ver-01dch2c94p0zvjn18fa1sq6p1x |     2 |     0 | READER | 2019-05-29 12:14:39 |
    | sec-01dazy4ygjxbnc94kjrj99hqn0 | fml_public_yt_token_test                                       | ver-01dazy4ygxhxnd9ea0q8j33hje |     1 |     1 | READER | 2019-05-16 12:04:11 |
    | sec-01daxgtnjnbwws9bty9jfqszze | valhallasecret2                                                | ver-01daxgtnk26fjqjb5yyy6rbcee |     1 |     4 | READER | 2019-05-15 13:32:54 |
    | sec-01daxgtn66mvmf75vhxcy11z0a | valhallasecret1                                                | ver-01daxgtn6gddnpt7345jcm34bh |     1 |     1 | READER | 2019-05-15 13:32:54 |
    | sec-01daxg33dmmp5skkh23816mb9n | catboost_public_rsa                                            | ver-01daxg33dzc5a04pxjbrtgksf4 |     1 |     5 | READER | 2019-05-15 13:20:02 |
    | sec-01daxg2g6v9ywgddypd8z6ya1x | valhallasecret0                                                | ver-01daxg2g75ghz1hd98v0gm7nv7 |     1 |     1 | READER | 2019-05-15 13:19:42 |
    | sec-01daxfwj9kedfz2a788dp0ra81 | robot-nirvana-prsops_scraper_token                             | ver-01daxfwja0am1k0ppr05epc1gh |     1 |     1 | READER | 2019-05-15 13:16:28 |
    | sec-01daxfwhz1ke654t1etvdkc9sh | robot-nirvana-prsops_yt_token                                  | ver-01daxfwhzec9ebs3skfq8ey9b4 |     1 |     1 | READER | 2019-05-15 13:16:27 |
    | sec-01daxf448xx57v60pgspmbvjcs | robot-klaus-fuchs_yt_token                                     | ver-01devrxzf63qvwszv51ekm25m4 |     2 |     1 | READER | 2019-05-15 13:03:07 |
    | sec-01daxdzmvnjxjas5jc65zkm2vf | zora_any                                                       | ver-01daxdzmvz56d4g4c8p64zaw2f |     1 |     2 | READER | 2019-05-15 12:43:11 |
    | sec-01daxdkranjvvfpb0dpw3vhck0 | robot-ml-engine-hahn-yt-token                                  | ver-01daxdkrb4v9yzyssxm2mg1n9e |     1 |     1 | READER | 2019-05-15 12:36:42 |
    | sec-01daxdkk3pphbds5d321hb5q2w | fml_public_yt_token                                            | ver-01daxdkk452wefx8a0cwfyhbb8 |     1 |     7 | READER | 2019-05-15 12:36:36 |
    | sec-01daxdgc61cepnxh5b9br7mbc5 | blender_stub_yt_token                                          | ver-01daxdgc6fz5sbz8sgwa7k44kw |     1 |     5 | READER | 2019-05-15 12:34:51 |
    | sec-01d60gxt0xyxjxp3h4prgtdxne | Root-ningbo                                                    | ver-01d60hykexehax8faegvf363x4 |     1 |     0 | OWNER  | 2019-03-15 14:13:51 |
    | sec-01cyrt1nseravt0ndndcnyydgk | VCS_BERLIN                                                     | ver-01cyrtanv1re7mh8b45k794mgn |     1 |     0 | READER | 2018-12-15 14:29:27 |
    | sec-01ckx62bkvpee201ks4d4a1g09 | ya-upload-mds                                                  | ver-01ckx62bm2j00f44sag2910hn4 |     1 |     4 | READER | 2018-08-02 14:23:50 |
    | sec-01chj6wrapfb43ck2xmv6fyaf6 | puncher-idm-oauth-token                                        | ver-01chj6wratfjp9gstjcj4c6ac4 |     1 |     0 | OWNER  | 2018-07-04 11:35:12 |
    | sec-01chj6q52bwa6x3bj7dkpqepjf | puncher-staff-api-token                                        | ver-01chj6q52sf698ga2efdfte7ns |     1 |     0 | OWNER  | 2018-07-04 11:32:09 |
    +--------------------------------+----------------------------------------------------------------+--------------------------------+-------+-------+--------+---------------------+

Обычно клиент авторизуется по ssh-ключу
Проверить список ключей

    ssh-add -l

    2048 SHA256:gEyXtMZemnzI6S7EN6F+uoWPZGvhZ31gBEIa5DrhJy4 moonug@yandex-team.ru (RSA)

Добавить все подряд

    ssh-add


## Доступ к сертификатору

Документация на [вики](https://wiki.yandex-team.ru/intranet/crt/api/)

-   Получаем токен [тут](http://oauth.yandex-team.ru/authorize?response_type=token&client_id=8b8ba6767850432b93d0442e4a38dcd6), потом его положим в секретницу рядом с oauth


# Разворачивание


## Подготовительные операции


### Исходный код

1.  Склонировать себе панчер
    -   Бекэнд

            git clone -b PUNCHER-804 https://github.yandex-team.ru/moonug/puncher
    -   Фронт

            git clone -b PUNCHER-804 https://github.yandex-team.ru/moonug/puncher-1 puncher-front
2.  Нужный нам ansible лежит в `extra/local` в репозитории бэкэнда


### Private данные

Все токены и секреты из `private` и `development.yml` я перенес в секрет `sec-01dv2xjs5gd8zd1rdcjaaj8ada`


### Определиться с именем для виртуалки

Сейчас в QYP у нас есть квота только в SAS, поэтому если виртуалку назвать `puncher-test-s`, например,
то итоговый FQDN получится `puncher-test-s.sas.yp-c.yandex.net`.
Этот FQDN надо будет вставить в свой `vms.yml`


## Авторизация

Тут есть 2 пути. Если мы разворачиваем панчер для работы с каким-то инстансом паспорта,
то надо идти и создавать в паспорте все запчасти. Начать можно, например, [отсюда](https://doc.yandex-team.ru/blackbox/?lang=ru)
Как развернуть это автоматически я не представляю. Пока этот вариант отложен.
Второй вариант это переключить авторизацию на oauth, именно это мы и сделаем.


### Зарегистрировать OAuth-приложение

Документация на [вики](https://wiki.yandex-team.ru/intranet/dev/oauth/)
Примерно так заполняем [форму](https://oauth.yandex-team.ru/client/new):

-   **Название приложения:** Тестовая установка панчера в QYP

-   **Платформы:** Веб-сервисы

-   **Callback URL:** <https://><fqdn vm>/oauth

-   **Доступы:** -   Изменение правил Puncher
    -   Просмотр правил Puncher
    -   Доступ к логину, имени и фамилии, полу

Примерно такой ответ получим
  ID: Тут будет ID
  Пароль: А тут пароль
  Callback URL: <https://puncher-test-s.sas.yp-c.yandex.net/>

Сделать это надо один раз, id и пароль сохранить и положить в [секретницу](https://yav.yandex-team.ru).
id должен лежать по ключу oauth<sub>id</sub>, пароль по oauth<sub>pass</sub>
А ID секрета в vms.yml
Не забываем в тот же секрет положить токен от сертификатора, который мы получили выше, по ключу crt<sub>token</sub>


## Правим переменные.

Копируем пример и правим, если еще не.

    cp vms.example.yml vms.yml

Стоит убедиться, что есть доступ к <span class="underline">PUNCHER<sub>TEST</sub><sub>NETS</sub></span>, если нет - получить его, либо перенести виртуалку в сетевой макрос, к которому доступ есть.

    cat vms.yml

    # Inventory file для ansible
    # Здесь же настраивается расположение кода, секреты
    vms:
      # Список управляемых виртуалок
      hosts:
        # Имя виртуалки
        # QYP создает FQDN по одной форме, <pod-id>.<cluster>.yp-c.yandex.net
        # pod-id - это имя виртуалки, cluster - sas,myt,man
        puncher-test-s.sas.yp-c.yandex.net:
          # Надо ли создавать виртуалку при ее отсутствии
          vm_create: true
          # ID секрета, в котором хранятся доступы к oauth и сертификат SSL
          # Для OAUTH доступы надо положить в секретницу руками
          # id должен лежать по ключу oauth_id, пароль по oauth_pass
          # Сертификат лежит по ключу cert.pem, руками класть не обязательно
          # если сертификата нет, скрипт попробует получить его и при удаче положит его сам в этот секрет
          vm_vault: sec-01dvbbwy2zs5633dyq9y4r19cx

      # Эти переменные применяются ко всем виртуалкам
      vars:
        # Параметры для создания новой виртуалки
        # Если виртуалка есть или vm_create для хоста false, то эти параметры никак не используются
        vm:
          # Сейчас у нас есть хоть какая-то квота только в Сасово
          cluster: SAS
          # Источник квот
          abc: personal
          # Базовый образ, на других тестирования не было
          image: bionic-dev
          # Размер диска, меньше 30 делать не стоит, будут проблемы с разворачиванием дампов
          size: 40G
          # Сетевой макрос, в котором будет создана виртуалка. Для тестового панчера _PUNCHER_TEST_NETS_
          # должен стать основным
          macros: _PUNCHER_TEST_NETS_
          # RAM
          memory: 8G
          # Ядер проца
          cpu: 2
        # Настройки фронтовой части
        front:
          # Расположение склонированного репозитория фронтенда
          path: "{{ lookup('env', 'HOME') }}/projects/puncher"
          # репозиторий и ветка фронта
          git: https://github.yandex-team.ru/moonug/puncher-1
          branch: PUNCHER-804
          # версия фронта, особо не на что не влияет
          version: 0.0.2
        # настройки путей
        path:
          # Директория на виртуалке, в которую будет скопирован бэкэнд и прочие запчасти
          puncher: ~/puncher
          # Через эту директорию будут копироваться docker-образы
          tmp: /tmp
          # Путь к директории бэкэнда на локальной машине
          local_puncher: "{{ playbook_dir }}/../../"
        private:
          # ID секрета, в котором хранятся токены, сертификаты и ключи для доступа панчера к внешним сервисам
          # Для девелоперских установок пока стоит использовать sec-01dv2xjs5gd8zd1rdcjaaj8ada
          vault: sec-01dv2xjs5gd8zd1rdcjaaj8ada
        # ID секрета, в котором по ключу crt_token лежит токен для работы с API сертификатора
        crt_token_vault: sec-01dvbbwy2zs5633dyq9y4r19cx


## Почти готово

Теперь надо проиграть playbook и мы получим виртуалку, которую указали в `vms.yml`.
Ansible может создать виртуалку в QYP, накатить на нее докер, скопировать в виртуалку
docker-образы, сгенерировать конфиги и запустить docker-compose

    ansible-playbook -i vms.yml docker.yml

QYP может не донастроить виртуалку сразу, и не будет работать sudo. Надо подождать минут 10 и повторить playbook.


## Синхронизируем состояние с ночным дампом

    make sync_from_prod


## Livereload

Сделал почти хорошо работающий livereload.
Для работы нужен fswatch
После успешной настройки:

    make livereload_all

Измененный файл будет скопирован на виртуалку, сервис перезапущен.
Если изменения были не в cmd/puncher-<daemon>, то будут перезапущены все демоны.
Если хочется отслеживать только один, то

    make livereload_<daemon>


## Что еще можно подпилить:

-   Автоматическое вытягивание кода фронта
-   Возврат на использование черного ящика
-   Рандомный выбор сервера, с которого тянуть дамп?
