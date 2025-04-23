### Как заводится новый токен каунтер

Токен каунтер это уникальный счётчик, те два инкремента с одним идентификатором увеличат значение счетчика только на
один

Пример – [Токен Каунтер на current_shows](https://st.yandex-team.ru/VSINFR-2149)

1) Для начала добавляешь счётчик в конфиг ```token-counters.conf```

   Если счётчик создается для нового сервиса, то сервис нужно добавить в ```application.conf``` в *cassandra3.services*,
   и прописать ему конфиг для кассандры.

2) Каждый счётчик - это таблица в C*

   Для упрощения генерации классик не завезли. Можно посмотреть на таблицу из примера

3) В тестинге накатываешь схему сам (можно запустить прям из машины C*):

   ```cqlsh cassandra-hydra-rt-01-sas.test.vertis.yandex.net -u test -p test```

   Там ```use hydra_profile_bozon``` и скрипт

4) Выкатываешь в тестинг, проверяешь
   в [сваггере](http://hydra-profile-api-http.vrts-slb.test.vertis.yandex.net/swagger/?url=/api/v2/), что живое

5) Потом заходишь на один из хостов группы %vertis_vprod_cassandra_hydra_rt, пароль для пользователя
   в [секретнице](https://yav.yandex-team.ru/secret/sec-01fbkdrcfza5w9z7wbwmbnr7x9/explore/versions)

   ```cqlsh cassandra-hydra-rt-01-sas.prod.vertis.yandex.net -u hydra_profile -p <REDACTED>```

   и там тоже самое, ```use hydra_profile_bozon``` и скрипт

