[Небольшая дока с описанием сервиса](https://docs.yandex-team.ru/travel/services/commode/components/user_search_intents/architecture
)

### Разработка локально в `GoLand`
0. Простая инициализация проекта
    ```shell
    cd ${ARCADIA}
    ya ide goland ${ARCADIA}/travel/avia/personalization/
    ```
_(подразумевается, что все последующие команды выполняются из директории проекта)_

1. Генерируем нужные proto через `ya make`
   ```shell
   ya make --yt-store --add-result=.go
   ```

2. Копируем конфиг-файл, заполняем необходимые переменные
    ```shell
    cp config/reader/config.development.yaml .
    vim config.development.yaml
    ```

3. Настраиваем `Build configuration`
    1. `Run -> Edit configurations -> Add New Configuration -> Go Build`
    2. `Run kind: Directory`
    3. `Directory: ${ARCADIA}/travel/avia/personalization/cmd/reader`
    4. `Working directory: ${ARCADIA}/travel/avia/personalization`
    5. `Environment variables`:
        - `CONFIG_PATH=config.development.yaml`

4. Для API отдельную конфигурацию, как в п3, только
   - Поменять `Directory` в п3.3 на `${ARCADIA}/travel/avia/personalization/cmd/api`
   - Проделать п2 с конфигом из `config/api`

5. Загружаем необходимые ресурсы
   ```shell
   bash dev/tools/download-resources.sh
   ```


### Ещё немного про запуск и разработку

#### YDB
*API* читает данные из БД (в которую пишет *reader*), поэтому нужно:
- Создать свою YDB базу
[локально](https://ydb.yandex-team.ru/docs/getting_started/create_db#self-hosted)
или во [внутреннем облаке](https://ydb.yandex-team.ru/docs/getting_started/create_db#yandex-team-cloud)
- [Создать таблицу](https://yql.yandex-team.ru/Operations/YPGKyAuEI3xk-TbIqRCBfRph6xNGh0FekNPhCadGHd0=)
- *Иногда бывает необходимо налить базу из YT, последний раз делали [так](https://yql.yandex-team.ru/Operations/YPGIF9K3DCAgw0JRsYPhqKgQa8KdwtB0h9roxI2Nlno=)

#### LogBroker
*Reader* читает данные из LogBroker топиков, поэтому если использовать свой токен нужно:
- Создать в [development](https://lb.yandex-team.ru/logbroker/accounts/avia/development) директории собственного консьюмера
- Добавить в конфигурации консьюмера read rules с необходимыми топиками
- Выдать права на чтение топиков пользователю токена

Возможно создать не получится из-за ограничения на кол-во консьюмеров в одном аккаунте.
Можно использовать уже [имеющегося](https://lb.yandex-team.ru/logbroker/accounts/avia/development/personalization/consumer)
_personalization_ консьюмера с [токеном робота](https://yav.yandex-team.ru/secret/sec-01e487k510yycfs1h6bepjsx07/explore/versions)

Заметки на полях:
- полечить 	`imports github.com/DataDog/zstd: invalid input file name "_cgo_gotypes.go"` при запуске мне помогал флаг CGO_ENABLED=0
- Работа с YT-кэшем таблицы отелей могла бы быть лучше

### Проверить API через grpcurl

В тестинге ходим на `personalization.testing.avia.yandex.net`

Список доступных функций: `grpcurl -plaintext localhost:9001 describe`

#### Получить данные GRPC
- Старая ручка для колдунщика
    ```shell
    grpcurl -d '{"YandexUid": "9538903851607506075", "GeoId": "213"}' -plaintext localhost:9001 NAvia.NPersonalization.PersonalSearchServiceV1/GetPersonalSearch
    ```
- Avia History
    ```shell
    grpcurl -d '{"YandexUid": "9538903851607506075"}' -plaintext localhost:9001 ru.yandex.travel.avia.personalization.personal_search.v2.PersonalizationServiceV2/GetAviaHistory
    ```
- Avia Suggest
    ```shell
    grpcurl -d '{"YandexUid": "9538903851607506075", "GeoId": "213"}' -plaintext localhost:9001 ru.yandex.travel.avia.personalization.personal_search.v2.PersonalizationServiceV2/GetAviaSuggest
    ```
- Hotels Suggest
    ```shell
    grpcurl -d '{"YandexUid": "9538903851607506075"}' -plaintext localhost:9001 ru.yandex.travel.avia.personalization.personal_search.v2.PersonalizationServiceV2/GetHotelsSuggest
    ```

#### (Deprecated) Получить данные HTTP
- deprecated avia/history: `curl 'http://localhost:80/personal-search?yandexUid=9538903851607506075&geoId=213'`
- avia/history: `curl 'http://localhost:80/personal-search/avia/history?yandexUid=9538903851607506075&geoId=213'`
- avia/suggest: `curl 'http://localhost:80/personal-search/avia/suggest?yandexUid=9538903851607506075&geoId=213'`
