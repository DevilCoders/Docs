# Принципы построения домохозяйств

Домохозяйства представляют собой надстройку над склейкой в человека,
как объединение нескольких `crypta_id`.
Из этого следует что склейка может быть многоуровневой:  
`склейка в устройство (indevice_id)` &xrarr;
`склейка в человека (crypta_id)` &xrarr;
`склейка в домохозяйство (hh_id)`

### Данные

Связи между `crypta_id` строятся на основе ребер:

- (`crypta_id` -- `yandexuid`) -- из склейки в человека [vertices_no_multi_profile_by_id_type];
- (`yandexuid` -- `ip, date`) -- из [bs-watch-log] и [awaps-log];
- (`yandexuid` -- `GeoHash(predicted_home)`) -- из [homework_yuid], как строгое совпадение;

Потенциально возможные ребра для построения домохозяйств в будущем:

- (`crypta_id` -- `crypta_id`) -- `crypta_id` соседи по расклейке;
- (`device_id` -- `wifi ssid`) -- как общие точки доступа;
- (`login` -- `login`) -- из семейного такси, и семейного яндекс+;
- (`phone` -- `phone`) -- из звонков в АОН;
- (`yandexuid` -- `GeoHashNeighbours(predicted_home)`) -- из [homework_yuid], как соседние хеши;
- (`yandexuid` -- `private ip, date`) -- серые ip из browserinfo:pp [bs-watch-log];
- активность за одним `ip` адресом, без обязательного совпадения даты активности;
- мультиаккаунты в яндекс станции;
- персональные данные (совпадение фамилии) из яндекс паспорта и соц. сетей;
- друзья из соц. сетей;
- более сложное гео, регулярные совместные перемещения; 
- общие точки в маршрутах из навигатора (дом, гараж, дача...);

### Эвристики

Сейчас в построении домохозяйства используются следующие ограничения:

- В один день, за одним `ip` адресом, должно быть не более 10 различных
    `crypta_id` (защита от коллективных `ip`) [`$MAX_CRYPTA_ID_ON_IP`][hh_limits];
- На один `geo` регион, должно приходится не более 3k `crypta_id`
    (вынужденное техническое ограничение) [`$MAX_CRYPTA_ID_ON_GEO`][hh_limits];
- Один и тот-же `crypta_id`, не должен содержать в себе `yandexuid`-ы с более чем
    15 различных предсказанных домов (защита от переклейки) [`$MAX_GEO_PER_CRYPTA_ID`][hh_limits];
- Один и тот-же `crypta_id`, не должен содержать в себе более 750 `yandexuid`-ов
    (защита от переклейки) [`$MONSTER_CCID`][hh_limits];
- Совпадение по `ip` адресу, должно подтверждатся не менее 5 дней,
    при условии совпадение `GeoHash` [`$MIN_DAYS_GEO`][hh_limits];
- Совпадение по `ip` адресу, должно подтверждатся не менее 15 дней,
    при условии отсутствия `GeoHash` [`$MIN_DAYS_ONLY_IP`][hh_limits];

### Принцип работы

Для тех связей между криптаайди, которые соответствуют представленным выше ограничениям,
ищутся компоненты связности, и отбрасываются компонеты,
в которые входит более 10 различных `crypta_id`.

Оставшиеся компоненты признаются как домохозяйства и получаются соответсвующий `hhid`,
как минимальный `crypta_id` вошедший в данный компонент связности.
Стабильности идентификатора домохозяйства основана на стабильности идентификатора склейки в человека.

Для `yandexuid`-ов с юзерагентом `smart-tv` существует дополнительная, жадная,
доливка в домохозяйства. Выбирается наиболее частое `crypta_id`
совпадающее с данным `yandexuid`-ом по активности за одним `ip`.

После построения домохозяств дополнительным шагом строится
объединенный профиль домохозяйства, в котором учитывается соцдем и прочие атрибуты `yandexuid`-ов
вошедших в данное домохозяйство.

### Метрики

[Метрики домохозяйств][metrics].

# Построение домохозяйств

### Исходный код

Код лежит в аркадии в директории [`crypta/graph/households`][hh-src].
Состоит из отдельных задач для сбора данных (`data_import`),
построения домохозяйств (`hh_match`) и объединенного профиля (`hh_composition`).

Код сандбокс задач находится в директории [`sandbox/projects/crypta/graph/households`][hh-sndbx-src].

### Запуск

Домохозяйства работают в сандбоксе, задачи отмечены тегом [`HOUSEHOLD`][sandbox-task],
запускаются через [шедулеры][sandbox-sheduler] и связаны между собой через [`step`][step].

### Результат работы

Выходные таблицы домохозяйств хрянятся в директории [`//home/crypta/public/households`][hh-output].

- `composition` -- объединенный профиль домохозяйства,
    в этом историческом формате данные храняться в бб, как киворд 353.
    Для чтения можно использовать [decoder.py][decoder.py];
- `edges` -- искуственные суповые ребра `yandexuid-yandexuid`, для добавления телевизоров в отгрузку склейки;
- `hh_crypta_id` -- соотношение id домохозяйства, с id склейки в человека;
- `hh_crypta_id_reversed` -- та-же таблица, что выше, но сортировка по `crypta_id`; 
- `hh_match` -- соотношение id домохозяйства, с `yandexuid`-ом, без домохозяйств состоящих из единственного crypta_id.
- `hh_enrich` -- соотношение id домохозяйства, с `yandexuid`-ом.
    Может содержать `yandexuid`-ы не имеющие собственное `crypta_id`;
- `hh_reversed` -- та-же таблица, что выше, но с сортировкой по `yandexuid`;

### Метрики

[Дашборд][dashboard]

[vertices_no_multi_profile_by_id_type]: https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/production/state/graph/v2/matching/vertices_no_multi_profile_by_id_type
[bs-watch-log]: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/bs-watch-log
[awaps-log]: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/awaps-log
[homework_yuid]: https://yt.yandex-team.ru/hahn/navigation?path=//home/user_identification/homework/prod/homework_yuid
[hh_limits]: https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/households/hh_match/lib/query/prepare.sql?rev=5029282#L7-13
[hh-src]: https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/households
[hh-sndbx-src]: https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/crypta/graph/households
[sandbox-task]: https://sandbox.yandex-team.ru/tasks?all_hints=false&all_tags=false&children=true&hidden=true&tags=HOUSEHOLDS&limit=20&created=14_days
[sandbox-sheduler]: https://sandbox.yandex-team.ru/schedulers?all_hints=false&all_tags=false&owner=CRYPTA&tags=HOUSEHOLDS&limit=20
[step]: https://step-ui.qloud.yandex-team.ru/configs/?description=hh
[metrics]: https://stat.yandex-team.ru/Dashboard/UnifiedCryptaStats?tab=1003j
[hh-output]: https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/public/households
[decoder.py]: https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/households/hh_composition/lib/query/decoder.py
[dashboard]: https://datalens.yandex-team.ru/uj0m556sqfoir-unifiedcryptastats?tab=QQB
