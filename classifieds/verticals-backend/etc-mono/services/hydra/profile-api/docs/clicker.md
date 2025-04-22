### Как заводится новый кликер

Кликер это неуникальный счётчик (2 идентичных запроса увеличивают значение счётчика на 2)
Он может быть вечным (eternal clicker), или работать в каком-то окне

Пример – [Новый кликер CARFAX](https://st.yandex-team.ru/VSINFR-3857)

1) Для начала добавляешь кликер в конфиг ```clickers.conf```, в список clickers или eternal

Если кликер создается для нового сервиса, то сервис нужно добавить в ```application.conf``` в *cassandra3.services*, и
прописать ему конфиг для кассандры.

2) Каждый кликер - это таблица в C*

   Для упрощения генерации есть классик ```ru.yandex.hydra.profile.dao.clicker.impl.SchemaGen```

   Подставляешь свои значения и получаешь скрипт

3) В тестинге накатываешь схему сам (можно запустить прям из машины C*):

   ```cqlsh cassandra-hydra-rt-01-sas.test.vertis.yandex.net -u test -p test```

    Там ```use hydra_profile``` и скрипт

4) Выкатываешь в тестинг, проверяешь в [сваггере](http://hydra-profile-api-http.vrts-slb.test.vertis.yandex.net/swagger/?url=/api/v2/), что живое 

5) Потом заходишь на один из хостов группы %vertis_vprod_cassandra_hydra_rt, пароль для пользователя в [секретнице](https://yav.yandex-team.ru/secret/sec-01fbkdrcfza5w9z7wbwmbnr7x9/explore/versions)

   ```cqlsh cassandra-hydra-rt-01-sas.prod.vertis.yandex.net -u hydra_profile -p <REDACTED>```

   и там тоже самое, ```use hydra_profile``` и скрипт

