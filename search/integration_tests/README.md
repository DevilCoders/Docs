
### Интеграционные тесты поиска TSoY

Интеграционные тесты генерируют HTTP запросы в указанный в переменной окружения **BETA\_HOST** тестовый стенд и проверяют полученные HTTP ответы. Никаких тестовых стендов и вспомогательных демонов тесты не запускают.

Тесты непокоммитные и не запускаются в CI.


### Запуск тестов

Тесты интегрированы в систему сборки ya make и запускаются с ее помощью.

Тесты расположены в Аркадии по адресу: https://a.yandex-team.ru/arc/trunk/arcadia/search/integration_tests


#### Секреты

Тестам необходимо передавать через переменные окружения секретные данные, так как производится тестирование авторизации с помощью тестовых аккаунтов.

Все данные, необходимые для запуска тестов вручную, хранятся в [Секретнице](https://yav.yandex-team.ru/secret/sec-01f3dnxszdxw71xyv8fszr22hy)

> **ПРОВЕРЬТЕ СВОИ ПРАВА НА СЕКРЕТ !!!**

Если у вас нет прав на секрет, и вы хотите только локально проверить какой-либо тест, которому не нужны секреты, то можно запускать тесты без них, обнулив переменную окружения:

    SECRET_VERSION= ./run.sh ...

#### SoY

Тесты можно запустить в SoY режиме, когда сгенерированные HTTP запросы в тестовый стенд задает SoY, и в обычном режиме, когда HTTP запросы в тестовый стенд задают сами тесты с помощью модуля requests.

SoY режим включается с помощью переменной окружения **SOY\_MODE=1**.

При ручном запуске тестов рекомендуется не включать режим SoY

#### Команда запуска тестов

Для ручного запуска тестов рекомендуется воспользоваться BASH скриптом [run.sh](run.sh) (рекомендуется прочесть сам скрипт для лучшего понимания механизма запуска тестов):

    cd ~/arcadia/search/integration_tests && ./run.sh -F test_xml.py:: * ::test_func*

#### Как запустить часть тестов
* Можно отредактировать ya.make файл
* Можно воспользоваться опцией -F в ya make -t команде [см gtest\_filter синтаксис](https://github.com/google/googletest/blob/master/googletest/docs/advanced.md):

    ./run.sh -F * :: * :: test\_name*

#### Checkout из Аркадии

    svn cat svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/ya | python - clone ~/integration_tests_arcadia
    cd ~/integration_tests_arcadia && ./ya make -j0 --checkout search/integration_tests
    cd ~/integration_tests_arcadia/search/integration_tests && ./run.sh

### Переменные окружения

**BETA\_HOST='hamster.yandex.ru'** - Хост тестируемого стенда (доменное имя или IP адрес). Стенд должен работать по HTTPS протоколу.

**SECRET\_VERSION** - id секрета в секретнице

**OAUTH\_TOKEN** - токен для авторизации в секретнице. Пользователь должен иметь доступ на чтение секрета **SECRET\_VERSION**. При локальном запуске берется из ssh сессии.

**SOY\_MODE=1** - Включить режим работы через SoY. По умолчанию **SOY\_MODE=0**.

**SOY\_MAP\_OP\_TYPE** - режим soy скачки. Поддерживается http - скачка без валидации и scraper - скачка с валидацией. По умолчанию **SOY\_MAP\_OP\_TYPE=http**

**LOGGING\_MODE=X** - Переменная окружения, управляющая режимом логирования библиотеки logging. Если не указано, то используется INFO. Поддерживаются значения: DEBUG, INFO, ERROR. Выхлоп направлен в STDERR

**TEST\_ID=0**, **EXP\_CONFS='testing'** - test-id и exp\_confs, которые нужно передавать в тестовый стенд при каждом запросе

**SOY\_POOL** - этот пул используется для soy скачки

**PATH\_TO\_SOY\_BATCH** - путь к директории, где хранятся файлы с id скачкой soy. Используется для отмены soy скачки в случае проблем.

**SOY\_RESULT** - Для отладки тестов. Путь к **output\_table**. Когда задана эта переменная, пропускаются операции записи тестовых HTTP запросов в input\_table и вызов SoY на исполнение. Тестовая система сразу считывает результат из указанной таблицы. **Экспериментальная функциональность.**

### Ключи [секрета](https://yav.yandex-team.ru/secret/sec-01f3dnxszdxw71xyv8fszr22hy)

**SOY\_PUBLIC\_KEY** - публичный ключ SoY, необходимый для шифрования HTTP хедеров с сессионными куками. Взять в [Секретнице](https://yav.yandex-team.ru/secret/sec-01e242n5v1bac4ccf2cdzhn4hv/explore/versions)

**SOY\_TOKEN** - Токен для SoY API. Взять [на странице QLoud авторизации](https://auth.qloud.yandex-team.ru/), кликнув по ссылке **OAuth token**

**TEST\_USER\_LOGIN** - Логин тестового пользователя, под которым проводится тестирование авторизации

**TEST\_USER\_PASSWD** - Пароль тестового пользователя

**TEST\_USER\_XML\_IP** - IP адрес тестового пользователя, используемый для тестирования XML авторизации

**TEST\_USER\_XML\_KEY** - Ключ тестового пользователя, используемый для XML авторизации

**TEST\_XML\_BANNERS\_NEW\_PARTNERS** - аутентификационные данные XML партнеров, получающих баннеры в новом формате

**TEST\_XML\_BANNERS\_OLD\_PARTNERS** - аутентификационные данные XML партнеров, получающих баннеры в старом формате

**TEST\_XML\_PARTNERS** - аутентификационные данные XML партнеров, работоспособность аккаунтов которых проверяют тесты

**YT\_TOKEN** - Токен для YT. Взять [на странице YT авторизации](https://oauth.yt.yandex.net/), кликнув по кнопке **Give me my token!**

### Специальныя директория crashed

Все тесты которые могут привести к крешу нужно помещать в директорию search/integration_tests/test_suits/crashed
Потому что в случае креша, останавливаются все тесты. Если же тест положить в отдельную директорию, то остановятся только тесты из этой директории, а остальные продолжат выполнятся.
Это позволяет экономить время на тестирование.


### Ограничения

Валидация в soy не работает:
* если код ответа 3xx SCRAPEROVERYT-418
* для внешних запросов SCRAPEROVERYT-430
* если в графе нет вершин TUNNELLER и SCRAPER_MAPPER или они настроены неправильно

### Таски в Sandbox
Есть таска [SEARCH_INTEGRATION_TESTS](https://sandbox.yandex-team.ru/tasks?children=true&type=SEARCH_INTEGRATION_TESTS&hidden=true&limit=20&created=14_days) которая умеет запускать тесты.
Так же есть [SEARCH_INTEGRATION_TESTS_WITH_RETRIES](https://sandbox.yandex-team.ru/tasks?children=true&type=SEARCH_INTEGRATION_TESTS_WITH_RETRIES&hidden=true&limit=20&created=14_days) эта таска запскает SEARCH_INTEGRATION_TESTS и перезапускает только упавшие тесты
[SEARCH_INTEGRATION_TESTS_FLAKY](https://sandbox.yandex-team.ru/tasks?children=true&type=SEARCH_INTEGRATION_TESTS_FLAKY&hidden=true&limit=20&created=14_days) выдает флапающие тесты в N последних запусках SEARCH_INTEGRATION_TESTS
