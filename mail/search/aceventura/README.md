# Поиск по контактам
* Чатик abook-search-support - линка нет, просите Влада @tabolin
#### Cервисы в няне:
* Сало + Продюсер [aceventura_salo_prod](https://nanny.yandex-team.ru/ui/#/services/catalog/aceventura_salo_prod/)
* Прокся [aceventura_proxy_prod](https://nanny.yandex-team.ru/ui/#/services/catalog/aceventura_proxy_prod/)
* Бекенд [aceventura_backend_prod](https://nanny.yandex-team.ru/ui/#/services/catalog/aceventura_backend_prod/)
* Msal совпадает с почтовым [mail_msal_prod](https://nanny.yandex-team.ru/ui/#/services/catalog/mail_msal_prod/)
* Корповый Msal совпадает с почтовым [mailcorp_msal_prod](https://nanny.yandex-team.ru/ui/#/services/catalog/mailcorp_msal_prod/)
* QA proxy [aceventura_proxy_prod_qa](https://nanny.yandex-team.ru/ui/#/services/catalog/aceventura_proxy_prod_qa/)
* Очередь общая для PS [ps_search_queue_prod_1](https://nanny.yandex-team.ru/ui/#/services/catalog/ps_search_queue_prod_1/)
#### Графики и логи
* [Прокси/общая панель](https://yasm.yandex-team.ru/panel/vonidu.aceventura-proxy-prod)
* [Сало](https://yasm.yandex-team.ru/template/panel/aceventura_salo/ctype=prod/)
* [Бекенд](https://yasm.yandex-team.ru/template/panel/ps_search_backend/prj=aceventura;ctype=prod,prestable/)
* [Шивака](https://yasm.yandex-team.ru/template/panel/Shivaka/project=personalsearch-main/)
* [Панель алертов](https://yasm.yandex-team.ru/template/panel/pssearch_service_alert_template/abc=pssearch;prj=aceventura/)
* [Дашборд качества](https://stat.yandex-team.ru/Dashboard/User/vonidu/MailComposeQuality?tab=10001)
* Логи в yt [//logs/pssearch-aceventura-access-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//logs/pssearch-aceventura-access-log/1d)

## Описание
### Поставка данных
Данные поставляются из pg по аналогии с почтой но из таблички `contacts.change_log`. В [msal](https://a.yandex-team.ru/arc/trunk/arcadia/mail/search/mail/msal/main/java/ru/yandex/search/msal/contacts) 
есть специальные ручки для работы с контактами. Каждый пользователь это `uid` + `user_type`. Для обычного пользвателя`user_type` = `passport_user` для организации `connect_organization`.<br>
В базе у каждого пользователя есть список книг. В каждой книге есть список контактов. 
У каждого контакта есть мета + список email, список тегов. У каждого емейла в свою очередь может быть несколько тегов.
В поисковом индексе это превращается в следующую структуру: есть несколько типа записей с разным полем `av_record_type`: `contact`/`email`/`tag`/`shared` ...
Префиксы строковые вида `uid$тип_аккаунта` - обычный пользователь будет иметь `prefix`=`227356512$passport_user` 
Полный список [AceventuraRecordType](https://a.yandex-team.ru/arc/trunk/arcadia/mail/search/aceventura/aceventura_base/main/java/ru/yandex/ace/ventura/AceVenturaRecordType.java)
Список полей можно посмотреть [здесь в конифге](https://a.yandex-team.ru/arc/trunk/arcadia/mail/search/aceventura/aceventura_backend/files/aceventura_search_backend_fields2.conf) либо в [маппинге в коде](https://a.yandex-team.ru/arc/trunk/arcadia/mail/search/aceventura/aceventura_base/main/java/ru/yandex/ace/ventura/AceVenturaFields.java) 
там же про формирование первичного ключа -  поле `id`. В общем случае `id = av_{record_type}_{uid}_{userType}_*` 

Помимо индекса пользователя, для пользователя могут быть расшарены общие книги организаций или других пользователей. Список пошаренных дляпользователя - в записях с `av_record_type`=`shared`
Большинство имеет префиксные алиасы `_p` имейте ввиду

### Ручки
`/api/suggest` - основная ручка и самая важная, дерагется при саджесте в компоузе почты/выборе участников в календаре
`/api/search`  - в основном это поиск внутри адресной книги при переходе на вкладку контакты
### Памятка дежурному
#### Общее
* Чтобы посмотреть что лежит в базе, нужно зайти в контейнере msal / corpmsal подключаемся к базе ./ace_connect.sh {uid} для обычного пользователя. Для организации ./ace_org_connect.sh {org_id}. Дальше стандартным SQL смотрим в нужных табличках contacts.change_log/contacts.contacts/contacts.emails.
* Чтобы проверить нет ли различия с базой в индексе, в webtools java api есть ручка `/check/index/full?uid={uid}&shared={default=true}&all_replicas={default=true}`
#### Доставка
* Если сработал  мониторинг доставки, нужно сделать вдох, от простоя доставки в 5 минут никто не умирал еще, есть время аккуратно разобраться что происходит. Проверь oom / лаги рестартани сало.
* Ключевой график - график сала. Transfer lag - (время обработки события - change_date у события) - ключевая метрика лага обработки события относительно появления его в базе
* Mdb add/delete/error - график показывает добавление/удаление шардов, в норме там пусто, если есть активность - проверьте не падают ли демоны с ООМ. Если падают уменьшайте select-length
* Мониторинг `Bp / corp max lag minutes` часто фолсит, признаки что все действительно плохо: 1) lag minutes монотонно растет 2) есть много ошибок msal 3) график трансфер лага синий частично / полностью - значительная доля сообщений доставляется с лагом. Первая помощь - попробуйте рестартануть сервис, если не поможет - надо разбираться  
* Сработал мониторинг на размер очереди - возможно кто то закинул много данных, проверить жива ли очередь, есть ли кворум. Если все ок до наблюдать, если в течении 30 мин продолжает расти - разбираться
#### Поиск
* Ключевое что смотрим, если есть ошибки поиска / плохие тайминги - троттл cpu на проксе/бекендах, что с местом под логи, жива ли очередь
* Если есть троттл, проверяем нет ли копирований индекса - возможно его стоит остановить временно. Сервис в генкфг, если все плохо можно добавить овверайдом цпу чтобы продышалось, перенастроить лимиты 