## Как добавить балл пробок для новой станции метро

1. [Заходим](https://passport.yandex-team.ru/auth) под пользователем `zomb-podrick`, пароль [здесь](https://yav.yandex-team.ru/secret/sec-01cjz304eaxa8sgys9r4ddanyh/explore/versions).

2. Из [метростроя](https://metrostroy.c.maps.yandex-team.ru/release_editor) скачать xml-схему нужного города. Из ноды нужной станции взять значение поля `<nkId>id</nkId>` - это id станции в народной карте. Если его нет, попросить контент-менеджеров добавить. Там же взять координаты станции `<geoCoordinates latitude="xxx" longitude="yyy"></geoCoordinates>`.

3. Добавить в таблицу с порогами станцию и дефолтные пороги по ней. Создать на аналитиков тикет с тем чтобы оценить реальные пороги.
    <details>
        <summary>Открываем yql в режиме запросов к ydb.</summary>
        <img src="https://jing.yandex-team.ru/files/astandrik/2022-02-14_21-11-33.png" />
    </details>
    <details>
        <summary>SQL</summary>
        ```
            UPSERT INTO `metro-people-count-thresholds-latest`
            (
                avg_underground_device_count,
                station_id,
                station_name,
                threshold_2,
                threshold_3
            )
            VALUES
            (
                1, /* Любое значение. Аналитики исправят на реальное значение. */
                "4419552810", /* nkId */
                "Зюзино",
                24, /* Любое значение. Аналитики исправят на реальное значение. */
                70 /* Любое значение. Аналитики исправят на реальное значение. */
            );
        ```
    </details>

4. Выполнить скрипт и получить строки с значениями, которые будут использоваться для расчётов сигналов для новых станций. В массив `$new_stations` в скрипте положить новые станции.
    <details>
        <summary>SQL</summary>
        ```
            use hahn;
            PRAGMA yt.PoolTrees = "physical";
            PRAGMA yt.TentativePoolTrees = "cloud";

            -- Массив новых станций
            $new_stations = [{"id":"<nkId>","lat":"<lat>","lon":"<lon>"}];

            $R = 6371;
            $pi180 = Math::Pi()/180;

            $calc_geo = ($lat1, $lon1, $lat2, $lon2) -> {
                $dLat = ($lat2-$lat1) * $pi180;
                $dLon = ($lon2-$lon1) * $pi180;
                $a =
                            Math::Sin($dLat/2) * Math::Sin($dLat/2) +
                            Math::Cos(($lat1) * $pi180) * Math::Cos(($lat2) * $pi180) *
                            Math::Sin($dLon/2) * Math::Sin($dLon/2);
                $c = 2 * Math::Atan2(Math::Sqrt($a), Math::Sqrt(1-$a));
                $d = $R * $c;
                return $d;
            };

            $filter_stations = ($lat, $lon) -> {
                return ListMap(
                    ListFilter($new_stations, ($x) -> { return $calc_geo($lat, $lon, Cast($x["lat"] as Double), Cast($x["lon"] as Double)) < 0.1;  }),
                    ($x) -> {return $x["id"]});
            };

            Select "{" || "'station_id':'" || station_id || "', 'minLat':'"  ||
                Cast(ListMin(AGGREGATE_LIST(lat)) as String) || "', 'maxLat': '" ||
                Cast(ListMax(AGGREGATE_LIST(lat)) as String) || "', 'minLon': '" ||
                Cast(ListMin(AGGREGATE_LIST(lon)) as String) || "', 'maxLon': '" ||
                Cast(ListMax(AGGREGATE_LIST(lon)) as String) || "'}"
            from (
                select Math::Round(lat * 10000) as lat, Math::Round(lon * 10000) as lon, station_ids as station_id from (SELECT lon, lat, $filter_stations(lat, lon) as station_ids
                    from `home/maps/analytics/data/metro-jams/lon-lats`
                where ListLength($filter_stations(lat, lon)) > 0)
                Flatten by station_ids
            ) GROUP BY station_id;
        ```
    </details>

    Должна получиться жсонина с `id станций` и диапазонами точек по `lon` и `lat` для них, в которые будут падать сигналы из метрики.
    <details>
        <summary>Скрин</summary>
        <img src="https://jing.yandex-team.ru/files/zomb-podrick/2022-02-09_12-34-02.png" />
    </details>

5. Заходим в в [yql](https://yql.yandex-team.ru) и находим в сохранённых операциях `RTMR_VLA`.
    <details>
        <summary>Скрин</summary>
        <img src="https://jing.yandex-team.ru/files/zomb-podrick/2022-02-09_12-36-32.png" />
    </details>

6. Останавливаем процесс, если он ранится.
    <details>
        <summary>Скрин</summary>
        <img src="https://jing.yandex-team.ru/files/zomb-podrick/2022-02-09_15-08-35.png" />
    </details>

7. Убеждаемся на [графиках](https://solomon.yandex-team.ru/?project=yf&service=yf+functions&cluster=prod_vla&host=cluster&dashboard=yf-function-dashboard&l.version=Total&l.jobSetPath=yql_metro-jams&b=1h&e=), что процесс остановился.
    <details>
        <summary>Скрин</summary>
        <img src="https://jing.yandex-team.ru/files/zomb-podrick/2022-02-09_15-28-37.png" />
    </details>

8. Добавляем новую станцию в массив, сохраняем и запускаем rtmr-процесс.
    <details>
        <summary>Скрин</summary>
        <img src="https://jing.yandex-team.ru/files/astandrik/2022-02-09_15-58-12.png" />
    </details>

9. Убеждаемся, что процесс запустился.
    <details>
        <summary>Тык 1</summary>
        <img src="https://jing.yandex-team.ru/files/zomb-podrick/2022-02-09_16-03-25.png" />
    </details>
    <details>
        <summary>Тык 2</summary>
        <img src="https://jing.yandex-team.ru/files/zomb-podrick/2022-02-09_16-08-48.png" />
    </details>

10. Если по какой-то причине процесс не запустился - попробовать остановить, подождать и снова запустить.
    Если что-то совсем не получается - идти в поддержку [RTMR Support](https://t.me/joinchat/CmQ4RRRPWBrlfVgTCgb9fQ).

11. Проделать те же процедуры для `RTMR_SAS`.

12. Перейти на [карточку станции](https://yandex.ru/maps/213/moscow/stops/station__9858871/?ll=37.639867%2C55.732178&tab=overview&z=14.63) в картах и убедиться, что балл появился.
    <details>
        <summary>Скрин</summary>
        <img src="https://jing.yandex-team.ru/files/reshetnev-gb/%D0%91%D0%B5%D0%B7%20%D0%BD%D0%B0%D0%B7%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F.9367f60.png" />
    </details>

## Как обновить пороги для станции
После того как аналитки расчитают пороги в своей таблице https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/data/metro-jams/thresholds/last нужно обовить таблицу для расчёта пробок.

1. [Заходим](https://passport.yandex-team.ru/auth) под пользователем `zomb-podrick`, пароль [здесь](https://yav.yandex-team.ru/secret/sec-01cjz304eaxa8sgys9r4ddanyh/explore/versions).

2. Выполнить https://yql.yandex-team.ru/Operations/Yn4g3K5OD4EIK0DYkFxRGrvG7LcvO6Mkes9GntA-B68=
Тут создаётся пустая временная табличка в нашей базе для порогов

3. Выполнить https://yql.yandex-team.ru/Operations/Yn4hX7q3k0t8JSAxI5XdQZo0mXFj-xAttJTP_WIPQhc=
Тут мы льём из таблички аналитиков в нашу новую табличку эти пороги

4. Выполнить https://yql.yandex-team.ru/Operations/Yn4h_VZ1O6FkFEEO2uYFAkk_b1BxkIY8NCl-Q-dEjX4=
Тут мы льём из нашей таблички в ту, которая юзается для расчёта пробок
