### Как заводится новый лимитер

Лимитер это неуникальный счётчик (из 2х идентичных запросов будут учтены оба) с обратным отсчётом Бывают оптимистичными
и пессимистичными, оптимистичный не уходит в минус, те не учитывает в квоте запросы, которые были потроттлены.
Пессимистичный же при постоянном потоке запросов с рэйтом выше лимита полностью перестанет их пропускать.

Пример – [Лимитеры для Shark](https://st.yandex-team.ru/VSDATA-1399)

1) Для начала добавляешь лимитер в конфиг ```limiters.conf```

   Если лимитер создается для нового сервиса, то сервис нужно добавить в ```application.conf``` в *cassandra3.services*,
   и прописать ему конфиг для кассандры. Лимитер внешних запросов лучше вносить в секцию pessimistic, внутренних - в
   optimistic.

2) Каждый лимитер - это таблица в C*

   Для упрощения генерации есть классик ```ru.yandex.hydra.profile.dao.limiter.dao.impl.SchemaGen```

   Подставляешь свои значения и получаешь скрипт

3) В тестинге накатываешь схему сам (можно запустить прям из машины C*):

   ```cqlsh cassandra-hydra-rt-01-sas.test.vertis.yandex.net -u test -p test```

   Там ```use hydra_profile_bozon``` и скрипт

4) Выкатываешь в тестинг, проверяешь в [сваггере](http://hydra-profile-api-http.vrts-slb.test.vertis.yandex.net/swagger/?url=/api/v2/), что живое

5) Потом заходишь на один из хостов группы %vertis_vprod_cassandra_hydra_rt, пароль для пользователя в [секретнице](https://yav.yandex-team.ru/secret/sec-01fbkdrcfza5w9z7wbwmbnr7x9/explore/versions)

   ```cqlsh cassandra-hydra-rt-01-sas.prod.vertis.yandex.net -u hydra_profile -p <REDACTED>```

   и там тоже самое, ```use hydra_profile_bozon``` и скрипт

