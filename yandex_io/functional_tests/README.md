### Как запустить функциональные тесты на живом девайсе

[FAQ на WIKI](https://wiki.yandex-team.ru/quasar/software-requirements-documents-srds/functionaltesto/faq/#faq)

Чтобы запустить против настоящего настроенного железа нужно:

1) Подготовить конфиг с помощью утилиты yandex_io/tools/presmoke_groomer.

```presmoke_groomer --presmoke_mode``` самостоятельно спулит конфиг с девайса, подготовит новый конфиг, запушит конфиг, и перезапустит quasar, прокинет порты через adb forward tcp:port tcp:port

Собрать утилиту можно в самой папке functional_tests.

```
cd yandex_io/functional_tests 
ya make
./presmoke_groomer --presmoke_mode
```

2) Запустить тесты на устройстве (устройство должно быть соединено по adb)
```
ya make -tA -DREMOTE_TEST --test-threads=1 --test-param testing_mode=presmoke --test-param session_id="SESSION_ID" --test-param remote_test=true
```

```
--test-param testing_mode=TESING_MODE
```
На данный момент существует три множества кейсов: **regression**, **presmoke** и **station_presmoke**. 
Они соотвествуют множеству тест-кейсов из тестпалма.
Если параметр не указан, то запускается **regression**

По дефолту quasar.cfg девайса берется из yandex_io/functional_tests. Если хочется использовать кастомный конфиг необходимо добавить параметр
```
--test-param config_path=PATH_TO_CONFIG/quasar.cfg
```

Если по какой-то причине девайс недоступен по adb (или же функ тесты не работают корректно), но доступен по ip -- можно использовать параметр:
```
--test-param target_host=TESTED_HOST
```
FIXME: Есть известный баг, что TCPAudioDevice не успевает получить данные до закрытия сокета при использовании adb forward. В данном случае нужно использовать ```target_host``` параметр

Параметры:
   **target_host** - адрес в локальной сети, на котором сидит тестируемая железка

   **config_path** - путь до файлика конфига, идентичного тому что лежит на тестируемой железке (взятый с устройства/из smart_devices/platforms/%platform%/config/). Важно чтобы был указан правильный порт tcp-аудиодевайса

   **session_id** - кука Session_id от аккаунта, на который пропиликан девайс (взять можно в браузере с http://yandex.ru)

   **test-threads=1** - нужно чтобы тесты не запускались параллельно, т.к. устройства не умеют отрабатывать параллельные запросы

   **-DREMOTE_TEST** - флаг для сборки, отключающий зависимость на sample_app

#### Где брать session_id: 
- на текущий момент его можно достать из куки пользователя на yandex.ru https://nda.ya.ru/t/U1W20ew33YJkEW
- session_id выглядит так: `3:1601289662.5.0.1594066777175:AgABAAAAAAAiBoGwuAYCDg:b.1|387453088.0.302.0:3|223573.453592.wMrjWec1UWBi9cUKvmPAb9QctpQ`
- итоговый запрос выглядит так (пример):
```
ya make -tA -DREMOTE_TEST --test-param target_host=192.168.0.159 --test-param config_path=/Users/rudskoy/a/arcadia/yandex_io/tools/presmoke_groomer/quasar.cfg --test-param session_id="3:1601289662.5.0.1594066777175:AgABAAAAAAAiBoGwuAYCDg:b.1|387453088.0.302.0:3|223573.453592.wMrjWec1UWBi9cUKvmPAb9QctpQ" --test-threads=1
```

#### Как понять, что все запустилось:
- у вас бежит тест в консоли (показывается текст `[TS]`, название теста и таймер)
- миник отвечает на запросы, который задает в него тестовая система (если споттер триггерится, но алиса молчит, то что-то идет не так)

### Запуск тестов против не продового бэкенда

Тесты с sample_app можно запускать против бэкенда, отличного от продового, указав нужные урлы при запуске теста через `--test-param`. В настоящее время менять можно URL для VINS и Ya.Music websocket API.

Параметры:
   **vins-url** - URL для VINS, используемый в SpeechkitEndpoint
   **music-api-url** - URL для вебсокетного API Музыки, используемый в mediad

Пример запуска тестов с QA-бекендом Музыки:
```
ya make -tA music --test-param vins-url="http://vins-int.voicetech.yandex.net/speechkit/app/quasar/?srcrwr=BASS_SRCRWR_MusicQuasar:http://music-web-ext.music.qa.yandex.net/external-api" --test-param music-api-url="wss://ws-api.music.qa.yandex.net/quasar/websocket"
```

При запуске тестов на настоящем устройстве эти параметры будут проигнорированы. Если нужно поменять URL в тестах на устройстве, это можно сделать, подправив руками quasar.cfg на этом устройстве.

### Пресмоук для станции

Пресмоук для станции можно запускать через скрипт `station-presmoke.sh`.
В этом скрипте есть фильтр, чтобы в пресмоуке запускались не все функциональные тесты, а только кейсы из TestPalm.
Параметры `--test-param` нужно передавать скрипту в том же виде, как они были бы переданы в `ya make`.

Пример запуска:
```
./station-presmoke.sh \
    --test-param session_id="<your session_id cookie>" \
    --test-param target_host="172.21.237.226"
```
