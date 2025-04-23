# basebot
telegram bot for deploy chats

#Конфиги:
Все конфиги лежат в файле
classifieds/basebot/basebot-scheduler/src/main/resources/properties.conf

Конфиги для аутетификации в телеграмм:

Для фонового обновления списков пользователей в чатах:
~~~
 telegram.api_id=${?API_ID}
 telegram.api_hash=${?API_HASH}
~~~

Для аутентификации в веб-апи:
~~~
telegram.host="api.telegram.org"
telegram.port=443
telegram.scheme=https
telegram.token=${?TELEGRAM_TOKEN}
~~~

#Секретница
https://yav.yandex-team.ru/secret/sec-01fhsxg8nyrk0jeqrdpjc4qqx5/explore/versions

#Устройство:

Состоит из основного компонента-Scheduler

tc: https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_Basebot_Docker
admin: https://admin.vertis.yandex-team.ru/services/basebot

Scheduler реализует в себе как периодические таски (Например, походы в апи телеграмм для получения новых сообщений), так и GRPC апи, для получения хуков от шивы.

Процесс получения апдейтов из апи запускается каждые несколько секунд, реализация в **TelegramPollWorker**
Процесс сбора списка пользователей реализован в **TdLibUpdatesProcessor**

Вся логика с обработкой апдейтов реализована в **UpdatesProcessor**, который перенаправляет запрос в **CallbackProcessor**, если это колбек(нажатие на кнопку) либо в MessageProcessor, если это появление нового сообщения в чате.
Обработка сообщений связана с т.н. триггерами, описанными в трейте **Trigger**, соответственно вся обработка сообщений реализует  его.
Триггеры обрабатываются последовательно.

При работе используется база даных YDB.
Сервис живет в тестовой коммуналке, [ссылка](https://yc.yandex-team.ru/folders/foo2qvhfq9b2r709olo5/ydb/databases/etn03ekqkhvsli0mtmh1/browse?path=%2Fbasebot)

Для каждого триггера, как правило, используется отдельная табличка
например, в таблице **abc_config** содержатся конфиги для триггера **show_duty**,
а в таблице **service_config**-описания сервисов для сбора аппрувов.

[WIKI ботика](https://wiki.yandex-team.ru/users/fripe/basebot/)


#Локальный запуск:

1) Внести креды в конфиге для доступов в аркадию/удб/etc
2) Указать токен тестового ботика (@usher_backend_test_bot) в telegram.token=${?TELEGRAM_TOKEN}
3) В строчках [ноды зукипера](https://a.yandex-team.ru/arc_vcs/classifieds/basebot/basebot-scheduler/src/main/scala/ru/yandex/vertis/basebot/workers/WorkersSupport.scala?rev=r9403142#L87-88) и  [Диструбьюции токенов](https://a.yandex-team.ru/arc_vcs/classifieds/basebot/basebot-scheduler/src/main/scala/ru/yandex/vertis/basebot/workers/WorkersSupport.scala?rev=r9403142#L101-102) указать новый путь (можно добавить -t в конец)
3a) На mac OS закомментировать [строчку в tdlib](https://a.yandex-team.ru/arc_vcs/classifieds/basebot/basebot-scheduler/src/main/scala/ru/yandex/vertis/basebot/components/processors/td/TdLibUpdatesProcessor.scala?rev=r9362646#L33-34)
4) запустить ботика и написать в личку @usher_backend_test_bot команду, которую хочется дебажить
