## Подготовка патронов для личного кабинета

Для подготовки патронов используются данные из [feedback_api][feedback_api]: из бд достаём сколько-то последних задач и для них формируем contribution-ы, при этом удаляем все пользовательские данные: вместо них генерируем фейковые.

#### Патроны хранятся s3
* Добавление contribution-ов: https://s3.mds.yandex.net/maps-load-ammo/maps_core_ugc_backoffice_create_contributions
* Удаление contribution-ов: https://s3.mds.yandex.net/maps-load-ammo/maps_core_ugc_backoffice_delete_contributions
* Получение ленты contribution-ов: https://s3.mds.yandex.net/maps-load-ammo/maps_core_ugc_account_get_contributions
* Добавление assignment-ов: https://s3.mds.yandex.net/maps-load-ammo/maps_core_ugc_backoffice_create_assignments
* Получение ленты assignment-ов: https://s3.mds.yandex.net/maps-load-ammo/maps_core_ugc_account_get_assignments

Подготовка патронов в ленту живёт в [junk-е](https://a.yandex-team.ru/arc/trunk/arcadia/junk/likynushka/ugc/prepare_account_ammo): для обстрела ленты нужно генерировать user-тикеты, а паспорт не разрешает ссылаться на свой код генерации тестовых тикетов.

#### Особенности подготовки патронов
1. Патроны для contribution-ов/assignment-ов генерируются по базе [feedback-api][feedback_api]. Т.е. это данные для вкладки "Исправления" в личном кабинете. Генерация патронов устроена почти так же, как и [генерация](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/libs/ugc/ugc_client.cpp?rev=r7857987#L94) самих contribution-ов в feedback-api. Но вместо всех http-запросов во внешние сервисы стоят заглушки, которые делают фейковые данные.
2. В запросах на добавление contribution-ов/assignment-ов внутри upsert, а не простой insert. Запросы на обновление данных работают быстрее, чем запросы на добавление. Поэтому повторные стрельбы одной и той же лентой патронов не показательны: надо зачищать бд прежде, чем повторять стрельбу. Или подменять uid-ы пользователей/id contribution-ов.
3. Запросы в пустую бд работают быстрее, чем в заполненную. Для показательных стерельб на добавление данных нужна непустая бд. Или же нужно делать долгую стрельбу, которая сама заполняет бд.
4. Патроны для получения ленты генерируются по базе ugc в лоаде. Поэтому их генерацию надо запускать, когда эта база заполнена.
5. Патронам для получения ленты нужен user-тикет.
6. Для стрельб по ленте нужно, чтобы в патронах были user-тикеты пользователей, для которых в базе есть данные.


#### Как пострелять
1. Перед началом стрельбы чистим бд ugc account-а в load-е
2. Генерируем патроны для бекофиса (опционально)
3. Стреляем по бекофису патронами на создание contribution-ов/assignment-ов:
  * на разладку
  * с постоянной нагрузкой
4. Получили, что бд ugc account-а уже заполнена данными
5. По этим данным генерируем патроны для стрельбы в ленту (опционально, если в патронах на создание были новые данные)
6. Стреляем в ленту:
  * на разладку
  * с постоянной нагрузкой
7. Запускаем параллельно стрельбу на добавление данных (ugc_backoffice) и получение данных (ugc_account). Смотрим, как себя ведёт бд
7. Опционально можно пострелять патронами на удаление contribution-ов. Если делать стрельбы на разладку и с постоянной нагрузкой, то вторая может быть не показательной: там будут запросы на удаление тех contribution-ов, которые были удалены предыдущей стрельбой.

#### Примеры запусков стрельб
* [Добавление contribution-ов](https://sandbox.yandex-team.ru/task/894791881/view) - стрельба по backoffice
* [Запросы в ленту contribution-ов](https://sandbox.yandex-team.ru/task/894858189/view) стрельба по account
* [Удаление contribution-ов](https://sandbox.yandex-team.ru/task/893461787/view) - стрельба по backoffice

Во всех стрельбах использованы конфиги не из аркадии, конфиги заданы прямо в sb-тасках, поэтому их можно настраивать прямо из таски. В том числе и настраивать формат нагрузки: постоянную или возрастающую. Ссылка на файл с патронами задана в том же конфиге.

#### Планировщики стрельб в sandbox:
* Получение ленты contribution-ов на разладку: https://sandbox.yandex-team.ru/scheduler/44612
* Получение ленты contribution-ов с постоянной нагрузкой: https://sandbox.yandex-team.ru/scheduler/44617
* Получение ленты assignment-ов на разладку: https://sandbox.yandex-team.ru/scheduler/44610
* Получение ленты assignment-ов с постоянной нагрузкой: https://sandbox.yandex-team.ru/scheduler/44616

#### Ссылки
* [Инструкция по настройке стрельб и заливке патронов](https://wiki.yandex-team.ru/maps/dev/core/instrukcija-po-sozdaniju-servisov-v-rtc/#nastroitreguljarnoeregressionnoetestirovanie).
* [Инструкция по подготовке патронов](https://wiki.yandex-team.ru/load/guides/ammo/?from=%2FNagruzochnoeTestirovanie%2Fguides%2Fammo%2F#3.uripost)
* [Тикет](https://st.yandex-team.ru/NMAPS-13013) c конспектом результатов

[feedback_api]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api
