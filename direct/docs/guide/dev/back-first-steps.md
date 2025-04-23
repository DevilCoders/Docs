# Первые шаги для бэкенд-разработчика Директа

## Чаты

Попросите руководителя или курирующего ментора, чтобы вас добавили во все релевантные командные и продуктовые чаты.

## Сгенерировать и разложить ssh-ключи

[Инструкция по настройке ssh](../../dev/ssh)

## Запросить роли в сервисах

Для бэкенд-разработчика часто необходима роль **Разработчик**.

[Инструкция по получению ролей](../qa/qa_kmb/qa_roles#create-roles)

## Установить общеяндексовые инструменты для разработки

Система контроля версии `arc`, утилита `ya`.

- [Установить утилиты и прочитайте общую документацию по разработке](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)
- Примонтировать единый репозиторий в директорию `~/arcadia`

## Установить Idea

- Установить Idea через Self-Service (предустановлен на маках)
  или [Ultimate версию с сайта](https://www.jetbrains.com/idea/download/)
- [Настроить лицензию](https://wiki.yandex-team.ru/aefimov/HowToUseLicenseServers/)

## Настроить Idea

[Инструкция по настройке Idea для разработки Директа](https://wiki.yandex-team.ru/Direct/Development/Java/IdeaFaq/)

## Получить токен YT

Токен YT позволит использовать распределённый кеш сборки для ya-idea, чтобы его получить нужно

- перейти на страницу [https://oauth.yt.yandex.net](https://oauth.yt.yandex.net)
- нажать "Give my token"
- выполнить в консоли выведенную команду

## Установить ya-idea

`ya-idea` это надстройка для удобной генерации Idea-проекта для Директа.

{% note info %}

Обратите внимание, что `ya-idea` следует запускать из каталога direct. Работоспособность для дочерних каталогов
(libs, jobs, прочие) - не гарантируется.

{% endnote %}

```sh
mkdir -p ~/bin && svn export svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/direct/bin/ya-idea ~/bin/ya-idea
which ya-idea || echo 'export PATH="'$HOME'/bin:$PATH"' >>~/.bash_profile
```

**Если компиляция в Idea падает с ошибкой** `.. class file has wrong version 55.0, should be 52.0..` - нужно обновить
Java

**Если в `~/.{bash,zsh}{_profile,rc}` прописана функция `ya-idea`** - сотрите её и перезапустите терминал. Проверить
можно командой ```type ya-idea```

## Настроить адрес для локального http-сервера

```sh
sudo bash -c 'echo "127.0.0.1 local-direct.yandex.ru" >> /etc/hosts'
```

После локального запуска API гридов можно будет открыть, например, так
`https://local-direct.yandex.ru:8443/grid/`

Обойти проблему с сертификатом можно открыв в ЯБро и набрав `thisisunsafe` (да, прямо просто печатаем с клавиатуры
вникуда, когда видим предупреждение про сертификат)

## Получить секреты для локального запуска приложений { #download-tvm-secrets }

Для получения необходимых секретов и токенов нужно запустить скрипты:
```
~/arcadia/direct/bin/download_secret_for_local_use.py
~/arcadia/direct/bin/get_oauth_token.sh
```
Скрипты положат полученные секреты в директорию `$HOME/.direct-tokens/`.

{% note info %}

Перед запуском ssh-ключи уже должны быть [настроены](../../dev/ssh) и лежать в папке `ENV{HOME}/.ssh/`. Возможно, так
же, перед запуском придётся выполнить команду `ssh-add`. Подробнее
в [DIRECTKNOL-47](https://st.yandex-team.ru/DIRECTKNOL-47)

{% endnote %}

## Настройка Docker (используется в тестах)

Docker используется для запуска тестов с БД. В яндексовом docker-registry хранятся готовые образы для тестов. Если
Docker'а нет, брать его следует с [официального сайта](https://www.docker.com/products/overview#/install_the_platform).

## Авторизация в яндексовом docker-registry

[Инструкция по настройке авторизации](https://wiki.yandex-team.ru/docker-registry/#authorization)

{% cut "Если docker-registry не настроен, при запуске тестов будут ошибки" %}

```
Unable to find image 'registry.yandex.net/direct/dbschema:db133619-gen2666536-percona-5.6.24-34f0300553e921c3ca6c986d25a53fde' locally
Pulling repository registry.yandex.net/direct/dbschema
docker: Error: image direct/dbschema:db133619-gen2666536-percona-5.6.24-34f0300553e921c3ca6c986d25a53fde not found.
See 'docker run --help'.
```

Ещё в очень редких случаях такие ошибки случаются, если указан tag неопубликованного образа. Проверить наличие образа
можно, посмотрев список доступных tag'ов как
указано [тут](https://wiki.yandex-team.ru/cocaine/docker-registry-distribution/#polucheniespiskategovvrepozitorii).

Пример команды и вывода

```sh
$ curl -H "Authorization: OAuth $TOKEN" https://registry.yandex.net/v2/direct/dbschema/tags/list | jq .
{
"name": "direct/dbschema",
"tags": [
"r132664-percona-5.6.24",
"db132664-gen2601079dirty-percona-5.6.24-742beb6fa6e72713cf5cf3387acea531",
"db135662-gen2711551-percona-5.6.24--3f4eaf11cd54cd304f1b8b7c3e7b74c7",
"db139534-gen2796055-percona-5.6.24--3a35aa56f3e5a95b0751f3a590021c66",
"db145131-gen2977818-percona-5.7.16--6ad89d15a0b58eda462fd7d290210032"
]
}
```

В списке должен быть tag, указанный в
файле `direct/libs/test-mysql/src/main/resources/ru/yandex/direct/test/mysql/dbschema_docker_image.txt`.

{% endcut %}

## Вспомогательные консольные утилиты под Мак

В некоторых вспомогательных скриптах используются консольные команды, которых по-умолчанию в MacOS нет. Потому стоит их
установить:
`$ brew install coreutils`
Иначе возможна, например, такая ошибка:
`./bin/create_library.sh: line 24: realpath: command not found`

## Зарезервировать для себя беты

Для разработки бывает нужно создавать отдельные экземпляры Директа, на которых удобно отлаживать и проверять свой код.
Стоит узнать у руководителя на каком [ppcdev](../../glossary/glossary#ppcdev) лучше
создавать [беты](../../glossary/glossary#beta)
и зарезервировать по инструкции.

[Инструкция по резервированию портов на бете](../../dev/betas/betas#beta-ports)

---

В случае вопросов или неактуальности информации на данной странице можно обращаться
к [Захару Зибарову](https://staff.yandex-team.ru/zakhar)
