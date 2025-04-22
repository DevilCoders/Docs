# Как собрать пакет в Директе
За долгие годы мы наработали много способов собирать пакеты с кодом приложений или конфигам.
В этой инструкции описаны команды для сборки и признаки, по которым можно выбрать подходящий способ.

## Аркадийная сборка { #arcadia-ya-package }
Как узнать?
- файл `pkg.json`, `package.json`, `package-*.json` или `package/*.json`; внутри начинается с раздела `meta`
- все пакеты из [direct/packages](https://a.yandex-team.ru/arc/trunk/arcadia/direct/packages)
- большинство java-приложений Директа

### в Sandbox { #sandbox-ya-package }
**Рекомендуемый способ** — через наш скрипт—помощник `sandbox-ya-package.pl`,
который создает с нужными параметрами задачу в Sandbox и дожидается её выполнения.
Установлен на всех [ppcdev'ах](../../glossary/glossary.md#ppcdev).

Пакет будет собран с версией `1.<revision>-1`,
подписан GPG—ключом пользователя [robot-direct-debsign](https://staff.yandex-team.ru/robot-direct-debsign)
и залит на dist в репозиторий **direct-trusty**.

Команда для сборки:
```sh
sandbox-ya-package.pl --package <path/to/package.json> --revision <revision>
```
Обязательных параметра два:
- `--package` — путь от корня аркадии до json—файла с описанием пакета
- `--revision` — ревизия аркадии, из которой нужно собрать пакет

{% note tip "Узнать текущую ревизию транка" %}

Можно вот этой командой
```sh
svn info svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia | grep Revision
```

{% endnote %}

Примеры:
- собрать [пакет с конфигами push-client](https://a.yandex-team.ru/arc/trunk/arcadia/direct/packages/yandex-direct-send-logs-to-logbroker) для заливки логов:
    ```sh
    sandbox-ya-package.pl --package direct/packages/yandex-direct-send-logs-to-logbroker/pkg.json --revision 7327917
    ```
- собрать JobsApp с патчем из [ревью PR](https://a.yandex-team.ru/review/1689019/details)
    ```sh
    sandbox-ya-package.pl --patch arc:1689019 --package direct/jobs/package/package-jobs.json --revision 7958400
    ```
- вывести справку:
    ```sh
    sandbox-ya-package.pl --help
    ``` 

### вручную { #ya-package }
Для этого способа нужен настроенный GPG-ключ ([инструкция](../initial-setup/gpg-key.md)).

Команда для сборки (последним аргументом нужно указать путь к json-описанию пакета):
```sh
ya package --checkout --debian --publish-to=direct-trusty <package.json>
```

Пакет будет собран с версией `1.<ревизия в рабочей копии>-1` и подписан вашим ключом.

{% note warning "Используйте свежую утилиту `ya`" %}

Обязательно используйте `ya` из рабочей копии, обновив её!  
Старые версии утилиты ya могут не поддерживать некоторые параметры и в результате собрать некорректный пакет.

{% endnote %}

Примеры команд, для запуска из корня аркадии:
- собрать пакет yandex-du-solomon-agent:
    ```sh
    svn up && ./ya package --checkout --debian --publish-to=direct-trusty direct/packages/yandex-du-solomon-agent/pkg.json
    ```
- собрать yandex-direct-send-logs-to-logbroker:
    ```sh
    svn up && ./ya package --checkout --debian --publish-to=direct-trusty direct/packages/yandex-direct-send-logs-to-logbroker/pkg.json
    ```

## debosh
Как узнать?
- в каталоге есть два файла: `meta.yaml` и `changes`
- большинство старых пакетов из [direct-utils](https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/)

Это [наша](https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/debosh/bin/debosh) утилита для сборки по простому описанию и фиксированному расположению файлов. Работает на [ppcdev'ах](../../glossary/glossary.md#ppcdev), требуется настроенный GPG-ключ.

Команды:
```sh
debosh
dupload debian
```

Первая — соберёт (и подпишет) пакет с последней версией из changes, вторая — загрузит его на dist.

## стандартная debian—сборка {#debian}
Для этого способа нужен настроенный GPG-ключ ([инструкция](../initial-setup/gpg-key.md)).

Как узнать?
- папка `debian` с файлами control, rules
- структура папок вида `packages/yandex-что-то-там/debian`
- в packages лежит `Makefile`

Обычный набор команд (из packages):
```sh
make clean
make co
make
dupload
```
Такой способ чувствителен к локальным изменениям, поэтому очистки командой `make clean` может оказаться недостаточно.

## Как выложить на ppcdev
Пакеты yandex-direct, yandex-du-*, yandex-dau-* можно поставить, используя следующий команды:
- На все ppcdev-ы:
    ```sh
    beta-update --ppcdev-all yandex-du-blackbox-perl=0.01-1 
    ```
- Только на текущий ppcdev:
    ```
    beta-update yandex-du-blackbox-perl=0.01-1 
    ```
- Выложить новый пакет (если раньше такого не было установлено):
    ```
    beta-update yandex-du-blackbox-perl 
    ```
- Для пакетов директа указываем только версию:
    ```
    beta-update 1.164254-1 
    ```    

## Ссылки
- документация на [ya package](https://wiki.yandex-team.ru/yatool/package/)
- инструкция по [настройке GPG—ключа](../initial-setup/gpg-key.md)
