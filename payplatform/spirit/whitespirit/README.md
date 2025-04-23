# Whitespirit
Сервер печати чеков. Управляет ККТ

Общая документация расположена тут: https://wiki.yandex-team.ru/balance/spirit

Документация по фискализации чеков: https://wiki.yandex-team.ru/balance/spirit/ReceiptGeneration/

Заметки про тестовую среду: https://wiki.yandex-team.ru/balance/spirit/TestKKTs/

Смотри также: https://wiki.yandex-team.ru/balance/spirit/Starrus/

Адрес тестовой среды: `https://whitespirit-test.paysys.yandex.net:8080`, `https://whitespirit-test1e.paysys.yandex.net:8081`

Адрес девелоперской среды: `https://whitespirit-dev.balance.os.yandex.net:8080`, `https://whitespirit-dev1e.paysys.yandex.net:8081`

Автоматически сгенерированная документация на основе описания swagger.yaml в `docs` (доступна по URL `/apidoc`), описание генерации в `docs/compile.cmd`

Бинарный протокол `kkt_srv/cashmachine/kktproto/starrus/starrus_proto.py` сгенерирован из исходника `proto_grammars/starrus.ksy`. Компиляция с помощью [kaitai](http://kaitai.io/), смотри `proto_grammars/compile.cmd`

Получить чек (и любой другой документ) из налоговой: смотри `dev_utils/check_docs_fns.py`

# Ежедневный отчет (временные форма и адрес)
За предыдущие сутки
https://s3.mdst.yandex.net/spirit/report/today.html

Или по датам
https://s3.mdst.yandex.net/spirit/report/report20181206.html

# Виртуальные кассы
В `qemu_fr`.

# Балансировщик Hudscuker
В `hudsucker`.
Описание https://wiki.yandex-team.ru/balance/spirit/Hudsucker/

# Скрипты для проверки ККТ
В `nmap`.
Описание https://wiki.yandex-team.ru/balance/spirit/Starrus/malfunction

# TVM
[TVM описание и пример](https://github.yandex-team.ru/Billing/whitespirit/blob/master/dev_utils/tvm.py)
Конфигурация через salt https://github.yandex-team.ru/ps-admin/salt/blob/testing/pillar/stack/environment/testing/role/whitespirit/init.yml

# Разное полезное
Сейчас основной (и единственной) поддерживаемой кассой является РП-Система 1ФА. [Описание API](https://github.yandex-team.ru/Billing/whitespirit/blob/master/proto_docs/Starrus_protocol.pdf)

Сборка https://teamcity.yandex-team.ru/project.html?projectId=Billing_Spirit_Whitespirit&tab=projectOverview
Тесты https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Billing_Autotesting_PythonTests_Cashmachines

Патчи, которые могут понадобиться перед использованием:

Патч | Назначение
------------ | -------------
[FR.3.5.30.bin](https://github.yandex-team.ru/Billing/whitespirit/blob/master/patches/starrus/FR.3.5.30.bin) | Обновление софта до последней версии, если требуется, начиная с версии 3.5.30 поддерживается НДС 20% и ИНН поставщика в строках чека
[to_FS.bin](https://github.yandex-team.ru/Billing/whitespirit/blob/master/patches/starrus/to_FS.bin) | Отключает поиск принтера. После этого касса не лагает на старте (для касс 1ФА)
[chpassold.bin](https://github.yandex-team.ru/Billing/whitespirit/blob/master/patches/starrus/chpassold.bin) | Смена ssh-пароля на известный нам
[resize.bin](https://github.yandex-team.ru/Billing/whitespirit/blob/master/patches/starrus/resize.bin) | Патч-убийца. Перекраивает разделы и высвобождает свободное место (для старого вида прошивок)

## Технические советы

### Отладка Whitespirit в IDE под MacOS

Проблема состоит в том, что на маке нет доступа с хостовой машины к адресам из сети контейнера (причина описана тут: https://github.com/docker/for-mac/issues/2670), поэтому нет возможности иметь докеризированные кассы доступными с хостовой машины по разным ip и одному порту, а ws ожидает именно такого поведения. И даже если можно через конфиг переопределить порт 4444 для json api касс, то порт 3333 для binary api так переопределить не выйдет.

Основная идея состоит в том, чтобы WS-ом, запущенным под дебаггером, подключиться к кассам, поднятым на linux-машине. Для этого:
1. На линуксовой виртуалке поднимаем кассы в докере:
   ```bash
   cd it_tests
   ./gradlew run
   ```
   Сконфигурированные кассы поднимутся и будут доступны на виртуалке в подсети `171.42.42.0/24`. Рядом с ними поднимутся WS и Hudsucker, но нас они не интересуют.
2. Запускаем отладку WS на этой же виртуалке:
   * можно что-то наколдовать с pycharm-ом для запуска удалённого интерпретатора, но
   * проще воспользоваться VS Code с Remote over SSH.

   В любом случае, запускаем отладку `kkt_srv_run.py` с `environment='tests'` (описание окружения см. в `kkt_srv_run.yaml`).
3. Если не удаётся достучаться до swagger, можно пробросить его через ssh tunnel:
   ```bash
   ssh -L 18080:127.0.0.1:8080 -N <my_linux_dev_machine>
   ```
   Swagger будет доступен на локальной машине по адрес/у `localhost:18080`.
