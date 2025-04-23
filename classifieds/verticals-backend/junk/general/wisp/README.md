# WISP
Сервис чатов Яндекс.Объявлений.

[Design Doc](design.md)
[Продуктовые метрики](https://grafana.vertis.yandex-team.ru/d/l19orJ0Gz/wisp)

[Доклад про устройство мессенджера, причины и предпосылки](https://nda.ya.ru/t/y0h7f1aA4KNEmt)

## Public Api

[Release Job](https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_AutoRuExp_wisp_api_release?mode=builds) 
[Grpc API](https://github.com/YandexClassifieds/schema-registry/blob/0d68b795f5c0c88352da5ce9497c5ea77548ba45/proto/general/wisp/chat_api.proto#L8)

testing - `wisp-api-grpc.vrts-slb.test.vertis.yandex.net:80`
production - `wisp-api-grpc.vrts-slb.test.vertis.yandex.net:80`


[[Grpc метрики](https://grafana.vertis.yandex-team.ru/d/grpc/grpc-server?orgId=1&var-datasource=Prometheus&var-job=wisp-api&var-dc=All&var-service=&var-method=All&var-window=2m&refresh=30s)]
[[Системные метрики](https://grafana.vertis.yandex-team.ru/d/system-info/system-info?orgId=1&var-datasource=Prometheus&var-job=wisp-api&var-dc=All&var-window=2m&var-gc=All)]
[Логи](https://grafana.vertis.yandex-team.ru/s/t/ejOEH_T44KMrLg)

## Полезные контакты
- [Саппорт-чат Я.Мессенджера](https://q.yandex-team.ru/#/join/325bdb3e-c9db-4feb-a21a-8f04fea7541b) - по любым вопросам, отвечает дежурный
- [Сергей Мануйлов](https://staff.yandex-team.ru/manokk) - основной разработчик, помогавший и помогающий в интеграции мессенджера. Иногда удобнее написать ему, нежели в саппорт чат. Особенно, если Сережа - дежурный. Писать лучше в Мессенджере.
- [Саппорт-чат Чистого Веба](TODO)
- [Дмитрий Васильев](https://staff.yandex-team.ru/vdf) - по вопросам и доделкам, связанным с Чистым Вебом.


## Внешние интергации

### API Яндекс.Мессенджера
- [Ботплатформа - Meta API](https://bp.mssngr.yandex.net/docs/api/meta/) - мета-операции над ботами (создание ботов, настройка ботов, получение Oauth для ботов) <br>
  альфа - https://botplatform-internal.alpha.yandex.net:443
  прод - https://botplatform-internal.yandex.net:443
  `Необходимы доступы`: puncher, доступ по tvm к конкретным методам (через тикет в MSSNGRBCKND)
- [Ботплатформа - Bot API](https://bp.mssngr.yandex.net/docs/api/bot/) - операции от имени ботов (отправка сообщений в комнаты, получение обновлений из комнат) <br>
  альфа - https://alpha.bp.mssngr.yandex.net:443
  прод - https://bp.mssngr.yandex.net:443
  `Необходимы доступы`: puncher
- [Messenger Meta API](https://wiki.yandex-team.ru/messenger/api/registrymeta/) - создание чатов <br>
  альфа - https://messenger-internal.alpha.yandex.net:443
  прод - https://messenger-internal.yandex.net:443
  `Необходимы доступы`: puncher, доступ по tvm к конкретным методам (через тикет в MSSNGRBCKND)
- [Fanout API](https://wiki.yandex-team.ru/messenger/fanoutapi) - операции с историей сообщений (чтение истории, пометка сообщений как прочитанных, скрытие сообщений)
  альфа - https://alpha.l3.mssngr.yandex.net:31926
  прод - https://l3.mssngr.yandex.net:31926
  `Необходимы доступы`: puncher, доступ по tvm к конкретным методам (через тикет в MSSNGRBCKND)

У мессенджера есть три окружения
- тест - для тестирования самого мессенджера. Использует тестовый паспорт
- альфа - для тестирования интеграций с мессенджером. Использует продовый паспорт с отдельной базой чатов
- прод - дефолтный продакшн. Использует продовый паспорт и продовую базу чатов

Тестинг мессенджера не очень стабилен, поэтому из теста мы ходим в альфу, используя [blackbox mimino](https://wiki.yandex-team.ru/passport/mimino/)

### Яндекс.Паспорт
- [Blackbox](https://doc.yandex-team.ru/blackbox/concepts/about.xml) - получение user tvm ticket-а по oauth владельца ботов для доступа в сервисы с tvm-авторизацией <br>
  `Необходимы доступы`: Заказ scope-ов [Форма для заказа грантов в Черный ящик](https://forms.yandex-team.ru/surveys/4901/)

### Clean Web
- [Дока](https://wiki.yandex-team.ru/jandekspoisk/antispam/cleanweb)
  тест - http://dev.clean-web.yandex.net:80
  прод - http://prod.clean-web.yandex.net:80
  `Необходимы доступы`: puncher