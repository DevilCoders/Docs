# providers_data
Здесь находится набор скриптов, необходимых для сборки сниппета с информацией о провайдерах, доступных для подключения в выбранном доме. [Таск на создание сниппета](https://st.yandex-team.ru/MAPSPRODUCT-846). Данные о провайдерах берутся из логов крипты, в которых есть *ip*, широта и долгота.

## Описание процесса сборки
### Получение и обработка исходных данных
Основные источники данных для сниппета - логи, которые находятся [здесь](https://yt.yandex-team.ru/hahn/navigation?path=//logs/crypta-rt-geo-v2-log/1d), и файлы-фиды с адресами, которые принесли нам провайдеры. В логах для нас наиболее интересны широта, долгота и *ip*. По координатам мы впоследствии сможем определить адрес дома, а по *ip* - провайдера. Существует *UDF*-функция *Geo::GetIspNameByIp*, позволяющая получить *id* провайдера по его *ip*, и файл с дополнительными данными о провайдерах, с помощью которого по *id* можно определить имя.
Логи фильтруются: не берутся строки с пустым *ip*, строки, геопозиция которых имеет слишком большую погрешность и строки, в которых данные о геопозиции получены из ненадежных источников. Поскольку после создания таблица с сырыми логами еще некоторое время модифицируется, в качестве входной берется таблица, созданная несколько дней назад.

### Вспомогательные таблицы
Перед тем, как строить сам сниппет, необходимо построить вспомогательные таблицы:

#### Таблица со списком офисов для каждого *id* сети, где офис описывается пермалинком, координатами и рейтингом
Строится из [экспорта организаций Справочника](https://yt.yandex-team.ru/hahn/navigation?path=//home/sprav/altay/prod/export/exported/company). *Protobuf*, который лежит в таблице, описан [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/sprav/protos/export.proto). Для каждой организации берутся координаты, *id* сети и рейтинг, который нужен для сортировки, после чего делается *reduce* по *id* сети. Таким образом, результат работы этой таблицы - это списки офисов, представленных в виде `{permalink, lon, lat, rating}`, сгруппированные по *id* сети.

#### Таблица с маппингом *id* сети - лого
Строится из [экспорта сетей Справочника](https://yt.yandex-team.ru/hahn/navigation?path=//home/sprav/altay/prod/export/exported/chain), *protobuf* см. там же, где и для первой таблицы. Основная особенность этой таблицы в том, что она ставит в соответствие *id* сети не только лого, но и фавиконку. Если к пермалинку подклеилась реклама, то в сниппете используется лого, поскольку оно больше и лучше смотрится с выделенным объявлением, а если нет, то используется фавиконка.
Лого берется из аватарницы по следующему пути: `https://avatars.mds.yandex.net/get-altay/GROUP/NAME/S`, где `GROUP` и `NAME` берутся из экспорта сети, а фавиконка берется из сервиса `https://favicon.yandex.net/favicon/v2/URL?size=32&stub=0`, где `URL` также берется из экспорта сети. При этом сети, *id* которых не указан в дополнительных данных, не берутся.

Также для построения сниппета используются готовые данные об этажности домов из [сниппета с информацией о доме](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/geoapp/snippets/building_info/result/latest).

#### Таблица для оффлайн-геокодера
Оффлайн-геокодер - это самодельный аналог настоящего геокодера, выполняющий только задачу обратного геокодирования, т.е. поиска дома, которому соответствует заданная точка. Использование оффлайн-версии позволяет не создавать на настоящий геокодер лишний *rps*, а главное - обойтись без дорогих сетевых взаимодействий. Результат его работы несколько отличается от настоящего - больше всего отличий, при которых оффлайн-версия находит дома, а онлайн-версия не находит. Было решено, что для данного сниппета такое поведение приемлемо и точности самодельного геокодера достаточно.
Оффлайн-геокодер для работы использует данные настоящего геокодера, которые [лежат на *YT*](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/geocoder/geosrc/latest_state). Интерес представляют таблицы с домами, именами топонимов и адресами. Перед использованием в оффлайн-геокодере их нужно поджойнить по *id* топонимов и домов, оставить только дома для интересующих нас городов и положить результат во вспомогательную таблицу.

### Дополнительные данные
Помимо вспомогательных таблиц существует еще файл с дополнительными данными *providers_info.json*, который заполняется вручную. В нем для каждого провайдера указывается имя, список его *id* и *id* сети, к которой он принадлежит. Также здесь можно руками указать пермалинк провайдера, ссылку на сайт или "забанить" его, то есть не учитывать его при построении списка провайдеров.
Возникают ситуации, когда в каком-то регионе провайдер называется по-другому, или нужно указать другой пермалинк. Переопределить эти параметры можно в полях *regional_names* и *regional_permalinks*, поставив новые значения в соответствие нужным *geoid*.
В поле `feeds_subdir` указывается поддиректория, где лежат фиды данного провайдера. Подробнее про то, как подключать фиды от пользователей, смотри ниже.
Существует ограничение, что имена *id* провайдера должны быть уникальны в рамках всего файла. Т.е. не может быть двух секций с одинаковым полем `name`, а любое значение из поля `ids` не может повториться ни в том же поле, ни в аналогичных полях других секций. Кроме того, список в `ids` не может быть пустым.

Для каждого провайдера в поле `adverts` можно добавить рекламу. Реклама в разных регионах может отличаться, поэтому в этом поле лежит массив объектов, для которых указаны списки *geoid* регионов в поле `geoids`. Если хотим включить рекламу для всех регионов, поле `geoids` не указываем. Объявление, у которого есть подходящий данному региону *id*, более приоритетно. Элементы `geoids` для каждого провайдера должны быть уникальны, и не может быть более одного объявления с отсутствующим `geoids`. Также нельзя указывать пустые списки рекламных объявлений и *id* регионов.
Каждый рекламный объект содержит текст рекламного объявления (не более 60 символов, рекомендуем не более 40). Еще в нем может быть указана минимальная цена, имя провайдера, которое нужно показывать в объявлении (не более 30 символов, рекомендуем не более 25), ссылка, по которой мы должны перейти по клику и небольшой текст, который будет показан в самом низу объявления (не более 17 символов). Ограничения по длине связаны с особенностями отображения этого текста в интерфейсе, более длинные тексты могут отображаться некорректно.
**Важно:** механизм позволяет добавлять рекламу только конкретным провайдерам, а не всей сети сразу. Теоретически может возникнуть ситуация, когда разные провайдеры с разным названием находятся в одной сети (т.е. имеют одинаковый `chain_id`). Поэтому если реклама добавляется для сети, необходимо сделать поиск по файлу и убедиться, что нужные данные добавлены для всех провайдеров, которые ей соответствуют.
От старого механизма рекламы в наследство досталось поле `advert_id`, которое использовалось для чего-то вроде сбора статистики по кликам. Сейчас каждому объявлению будет автоматически присваиваться уникальный *id*, который будет соответствовать имени провайдера и списку *geoid*. Посмотреть его можно в директории сниппета в таблице `advert_ids`.
#### Пример файла *providers_info.json*:
```json
[
    {
        "name": "ЭР-Телеком — Дом.ru", // имя провайдера (обязательное поле)
        "ids": [                       // список id провайдеров (обязательное поле)
            "digital-service llc",
            "dom.ru",
            "er-telecom",
            "ricentr llc",
            "teleset llc"
        ],
        "chain_id": 2575181646,        // id сети, которой принадлежит провайдер
        "permalink": 15174227114,      // пермалинк провайдера
        "url": "https://dom.ru/",      // ссылка на сайт провайдера
        "regional_names": {            // имена провайдера в заданных регионах
            "213": "Ринет"
        },
        "regional_permalinks": {       // пермалинки провайдера в заданных регионах
            "213": 1141789686
        },
        "banned": true,                // если выставлено в true, провайдер забанен
        "feeds_subdir": "domru",       // поддиректория в общей директории с фидами
        "adverts": [                   // рекламные объявления
            {
                "provider_name": "Домашний интернет Дом.Ру",      // имя провайдера, показываемое в рекламном объявлении
                "geoids": [                                       // регионы, в котором показывается данная реклама
                    213
                ],
                "advert": "Подключить домашний интернет выгодно", // рекламное объявление (обязательное поле)
                "url": "https://dom.ru/offers",                   // ссылка, по которой будем переходить по клику
                "postscript_text": "Посмотреть тарифы",           // дополнительный текст, показываемый внизу объявления
                "min_price": 420                                  // минимальная цена
            },
            ...
        ]
    }
    ...
]
```

При создании провайдера выбор пермалинка и создание иконки будет происходить в следующем порядке:
- Если удалось найти пермалинк по *geoid*, берется он
- Если не удалось найти пермалинк по *geoid*, то ищем глобальный пермалинк
- Если и глобальный пермалинк не удалось найти и задан *id* сети, то ищем ближайший офис

- Если есть рекламное объявление и провайдер сетевой, то берем лого по *id* сети
- Если нет объявления провайдер сетевой, то иконку строим по *id* сети
- Если провайдер не сетевой и нашелся пермалинк (либо по *geoid*, либо глобальный), то иконку строим из него
- Если нет ни пермалинка, ни сети, а задан только *url*, то берем иконку из *url*

### Фиды, принесенные провайдерами
Информация в сниппете будет наиболее точной, если провайдеры будут сами приносить нам списки адресов, по которым есть их подключения.
Ожидается, что провайдер приносит список адресов, где есть его абоненты. Удобнее, если это будет *excel*-файл, в котором адреса пречислены в одной колонке. Полный список требований можно найти здесь: https://wiki.yandex-team.ru/users/msmirnov91/trebovanija-k-fidam-s-adresami-provajjderov/.
Корневая директория для загрузки фидов указана в соответствующем параметре конфига. В ней у каждого провайдера есть своя (очевидно, уникальная) поддиректория, которая указывается в соответствующей секции файла с дополнительными данными *providers_info.json*. Принесенный файл с фидом нужно загрузить в эту поддиректорию через интерфейс *YT* как таблицу. Название таблицы должно соответствовать дате загрузки и иметь формат `%d-%m-%Y` (например, `03-02-2022`, если фид загружается второго февраля 2022 года). Колонка с адресами должна называться `address`.
Пошаговая инструкция, как загрузить фид через веб-интерфейс *YT*, лежит вот тут: https://wiki.yandex-team.ru/users/msmirnov91/kak-dobavljat-fidy-provajjderov-na-yt/, а инструкция, как обновить существующий фид, вот тут: https://wiki.yandex-team.ru/users/msmirnov91/kak-obnovljat-fidy-provajjderov-na-yt/.

Регулярный процесс сделает следующие шаги:
- Проверит по названию, не появился ли для провайдера новый фид
- Если появился, перенесет его во внутреннюю директорию, выполнив геокодирование
- Рядом появится таблица, в которой окажутся строки, не прошедшие геокодирование, с результатом ошибки
- Полученная таблица пройдет приемку, т.е. процесс упадет, если слишком много строк не удалось геокодировать
- Из внутренней директории будут взяты самые последние геокодированные фиды для всех провайдеров и объединены в одну общую выходную таблицу

Выходная таблица будет использована основным процессом построения сниппета как входной источник данных. Внутренняя директория нужна для безопасности: это позволит разграничить доступ и минимизировать риск порчи таблицы при ее изменении вручную.

### Формирование списка провайдеров
#### Схема построения сниппета
![](https://jing.yandex-team.ru/files/msmirnov91/provider_data-8.png)
#### Описание
За построение сниппета отвечают три регулярных процесса, в каждом из которых запускается свой бинарник. Это **build_logs**, **build_provider_feed** и **build_snippet**.

**build_logs**:
- Из исходной таблицы с логами берутся строки, координаты которых соответствуют одному из заданных в конфиге городов. Для каждой выбранной строки по *ip* определяется *id* и имя провайдера, результат записывается в промежуточную таблицу.
- Из строк таблицы, полученной на предыдущем шаге, берутся координаты, и делается попытка преобразовать их к адресу дома с помощью оффлайн-версии геокодера. Если оказывается, что координаты не соответствуют дому, строка отбрасывается. К строкам, которые удалось успешно геокодировать, добавляются адреса и *geocoder_id*.
- Результат вместе с таймстемпом сохраняется в выходную таблицу с кэшом.

**build_provider_feed**:
- Для всех провайдеров, у которых указана поддиректория с фидом, берется последняя загруженная таблица
- Проверяется, была ли она уже обработана
- Если нет, то адреса из нее геокодируется, проводится приемка, и содается таблица во внутренней директории.
- Для всех провайдеров, у которых указана директория с фидом, берутся последние обработанные таблицы и объединяются в предварительно очищенную выходную таблицу.

**build_snippet**:
- Строятся вспомогательные таблицы.
- В общую таблицу объединяются данные из выходных таблиц процессов **build_logs** и **build_provider_feed**. По специальному полю можно определить, откуда к нам попала данная строка - из логов или из фида.
- Если для провайдера есть фид, то данные, полученные из логов, будут игнорироваться.
- Строки, полученные на предыдущем шаге, объединяются по *geocoder_id*. Для каждого *geocoder_id* (т.е. для каждого адреса) строится список провайдеров, при этом сетевые провайдеры будут объединяться по *id* сети. Для полученных провайдеров будет предпринята попытка подобрать пермалинк ближайшего офиса.
- Провайдеры будут отфильтрованы и отсортированы. Если данные получены только из логов, то будут применены эвристики, чтобы отбросить заведомо ненадежные данные (Например, число подключений, число этажей в доме и т.д.). Если данные получены из фида, то они считаются достоверными и эвристики к ним не применяются.
- На этом этапе построение сниппета будет завершено, сниппет будет сохранен во временную таблицу.
- Временная таблица будет принята, т.е. проверено, что все адреса из объединенной таблицы с фидами попали в сниппет, все провайдеры из этой таблицы присутствуют в сниппете по указанным адресам и до всех провайдеров доехала правильная реклама. Если что-то из этого не выполнено, процесс упадет.
- Перед тем, как окончательно завершить построение сниппета, старый вариант сниппета бэкапится, после чего он обновляется данными из временной таблицы, построенной на предыдущем шаге. Под обновлением понимается процесс, при котором адреса, для которых не было получено нового списка провайдеров, не удаляются, а сохраняют свое старое значение, чтобы общее число сниппетов не уменьшалось.
После того, как описанные выше шаги будут пройдены, все вспомогательные и промежуточные таблицы будут не нужны, их можно удалить.
#### Ограничивающие параметры
В процессе построения сниппета задаются следующие параметры, вводящие определенные ограничения:
- **Количество этажей.** Для некоторых домов есть информация о количестве этажей. Чтобы улучшить качество данных, было решено не строить список провайдеров для малоэтажных домов (таким образом можно исключить, например, частные дома, для которых список провайдеров выглядел бы странным).
- **Количество подключений.** Мы считаем, что можем надежно сказать, что данный провайдер есть в данном доме, если набралось какое-то минимальное количество подключений этого провайдера. Если это не так, мы отбрасываем такого провайдера как ненадежного, чтобы повысить точность данных. При подсчете числа подключений *ip* не обязательно должны быть уникальными - т.е., например, если у нас есть три строки с одинаковыми *ip* и координатами, счетчик подключений увеличится на три.
**ВАЖНО:** если провайдер попал к нам из фида, то мы автоматически считаем его надежным и не выкидываем, даже если число уникальных пользователей окажется меньше порогового.
- **Максимальное расстояние до офиса.** При поиске ближайшего пермалинка существует ограничение на спан, в котором ищется офис, чтобы отсечь черезмерно удаленные варианты. Было принято решение, что лучше не показывать пермалинк совсем, чем показывать ближайший пермалинк в соседнем городе.
Сложно дать рекомендации по выбору этих параметров - их значения лучше всего подбирать методом проб и ошибок.
#### Сортировка
Список провайдеров сортируется по следующему принципу:
- В начале списка всегда находятся провайдеры, у которых есть рекламные объявления
- Если ситуация с рекламными объявлениями у двух провайдеров одинаковая, то первым будет тот, у которого выше рейтинг
- Если и рейтинги оказались одинаковыми, то первым будет тот, у которого больше подключений в данном доме

### Статистика
В процессе построения сниппета собирается статистика по городам и общая для всего сниппета. Они выгружаются в отдельные таблицы. Удобнее всего ее посмотреть на [дашборде](https://datalens.yandex-team.ru/uhcc5tj8y0cyp-provaydery?tab=aw).

#### Статистика по городам
Показывает количестве сниппетов с данным провайдером в срезе одного города. В таблицу записывается в следующем виде:

| city_geoid | date | provider_name | snippet_count |
| ---------- | ---- | ------------- | ------------- |
| Geoid города | Дата построения сниппета | Имя провайдера | Число сниппетов с данным провайдером |

#### Общая статистика
Позволяет определить, из какой таблицы варился сниппет, для каких городов и сколько времени было потрачено на каждый этап варки. В таблицу записывается в следующем виде:

| date | input_table | geoids | selecting_time | helper_tables_building_time | snippet_building_time |
| ---- | ----------- | ------ | -------------- | --------------------------- | --------------------- |
| Дата построения сниппета | Входная таблица | Список Geoid городов | Время, потраченное на выборку логов из входной таблицы | Время, потраченное на построение вспомогательных таблиц | Время, потраченное на построение сниппета |

### Как добавлять провайдеров вручную
Может возникнуть ситуация, когда необходимо добавить в данные нового провайдера или изменить информацию об уже существующем (например, в связи с тем, что сеть была продана другому провайдеру). Для этого нужно:
- Получить у саппортов `ip` этого провайдера.
- По `ip` получить техническое название проавйдера (его `id`) [вот так](https://yql.yandex-team.ru/Operations/YHf8dCyLNYPb7pMZG7xsiQs-zl21xwx4WVNeoxqATtI=).
- Добавить в *providers_info.json* соответствующую новому провайдеру секцию, в которой указать его имя, список *id*, пермалинки, *url* и т.д. Формат файла описан выше.
Для этих целей удобно править файл прямо в аркадии, нажимая на значок карандаша в правом верхнем углу.

### Конфиг
Часть параметров, необходимых для работы скриптов, передаются аргументами командной строки, а часть задается в едином для всех скриптов конфиге. Он имеет формат *JSON*. Корневой объект, содержащий параметры, называется `providers_data_snippet`.

#### Пример конфига:
```json
{
    "providers_data_snippet": {
        "cities": [                    // список городов, для которых берутся данные из логов. Каждый город описывается параметрами, указанными ниже
            {
                "geoid": 213,          // GeoId города
                "min-connections": 2,  // порог числа подключений уникальных пользователей для одного провайдера, по умолчанию 2
                "max-dist": 1,         // максимальное расстояние до ближайшего офиса, в градусах (как параметр 'spn' в геопоиске), по умолчанию 1
                "min-floors-count": 3, // минимальное количество этажей дома, для которого строим сниппет, по умолчанию 3
            },
            ...
        ],
        "cluster": "hahn",                                                    // YT-кластер
        "tmp-dir": "//home/maps/geoapp/tmp/provider_data_tmp",       // директория, в которой создаются временные таблицы
        "snippet-dir": "//home/maps/geoapp/snippets/provider_data",  // директория, в которой будут лежать таблицы со сниппетом и статистикой
        "logs-dir": "//logs/geolocation-united-geolog/1d",                    // директория, в которой находятся сырые логи крипты, с помощью которых стоится сниппет

        "logs-rows-limit": 4500000000,  // лимит количества строк, которые будут случайным образом взяты из логов
        "input-row-limit": 250000000,   // лимит количества строк, которые попадут на вход оффлайн геокодеру
        "user-id-column": "yandexuid",  // название колонки с уникальным *id* пользователя
        "precision": 100,               // ограничение по точности определения координат в логах, указывается в метрах

        "sources": ["GT_UNKNOWN", "GT_GPS", "GT_LBS", "GT_PLATFORM_LBS", "GT_IP", "GT_IPGEO"], // "вайтлист" источников информации о координатах

        "selected-logs-table-name": "selected_logs",     // имя таблицы, в которой будут лежать выделенные из входной таблицы логи
        "snippet-table-name": "provider_data",           // имя таблицы, в которой будет находиться построенный сниппет
        "days-ttl": 14,                                  // время, которое будет храниться сгенерированная таблица (в днях)
        "temp-output-table-name": "temp_provider_data",  // имя временной таблицы, в которой будет находиться построенный сниппет перед обновлением старого
        "error-table-name": "providers_err",             // имя таблицы, куда записываются ошибки операций map и reduce

        "feeds-dir": "//home/maps/geoapp/snippets/provider_data_feeds", // директория, в которую нужно складывать принесенные провайдером фиды

        "snippet-stat-table-name": "snippet_statistics", // имя таблицы со статистикой сниппетов по городам
        "common-stat-table-name": "common_statistics",   // имя таблицы с общей статистикой по построению сниппета

        "building-info-table": "//home/maps/geoapp/snippets/building_info/result/latest", // информация о доме (в т.ч. о количестве этажей)
        "exported-orgs-table": "//home/sprav/altay/prod/export/exported/company",                  // таблица с экспортом организаций из Алтая
        "exported-chains-table": "//home/sprav/altay/prod/export/exported/chain",                  // таблица с экспортом сетей из Алтая

        "days-interval": 3, // определяет, сколько дней назад была создана таблица с сырыми логами, которая будет использоваться при построении сниппета

        "geocoder-houses-table": "//home/maps/geocoder/geosrc/latest_state/houses",       // таблица геокодера с информацией о домах
        "geocoder-addresses-table": "//home/maps/geocoder/geosrc/latest_state/addresses", // таблица геокодера с информацией об адресах топонимов
        "geocoder-names-table": "//home/maps/geocoder/geosrc/latest_state/names"          // таблица геокодера с информацией об именах топонимов
    }
}
```

#### Города, для которых строится сниппет
Посмотреть соответствие города и его *geoid* можно [тут](https://geoadmin.yandex-team.ru/#region:41). Важно обращать внимание на тип - в текущей реализации это должен быть "город".

### Параметры, настраивающие запуск джобов в *YT*
Для того, чтобы варка сниппета не длилась слишком долго, важно правильно настроить параметры джобов в *YT*. Тогда планировщик сможет более оптимально их выполнять. Параметры, которые используются при настройке, и передаются как аргументы командной строки:

- `--mapper-memory-limit` - лимит памяти, выделяемый джобам, в гигабайтах
- `--mapper-memory-reserve-factor` - параметр, настраивающий резервирование памяти, по умолчанию `1`. Джобу гарантируется память в объеме `memory_limit *  memory_reserve_factor` (подразумевается, что `memory_reserve_factor < 1`), остальная память предоставляется только при наличии свободной. При неправильном выборе этого параметра может возникнуть ситуация, когда слишком много джобов абортится. Более подробно можно почитать [тут](https://yt.yandex-team.ru/docs/description/mr/operations_options#memory_reserve_factor)
- `--mapper-data-size-per-job` - рекомендованный объём данных на входе у одного YT-джоба в мегабайтах
- `--yt-pool` - пул, в котором выполняются джобы, по умолчанию `MAPSAPI`

## Описание скриптов
| Название | Реакция, запускающая процесс | Описание |
| -------- | ---------------------------- | -------- |
| build_logs | https://reactor.yandex-team.ru/browse?selected=11253573 | Селектит логи крипты, геокодирует и кэширует результат |
| build_provider_feed | https://reactor.yandex-team.ru/browse?selected=11184660 | Загружает фид, принесенный провайдерами, на YT и делает обратное геокодирование, находя для домов их внутренние id. |
| build_snippet | https://reactor.yandex-team.ru/browse?selected=7919127 | Строит вспомогательные таблицы, объединяет данные из логов и из фидов, строит сниппет, пишет статистику. |
| get_city_names | Запускается вручную | Возвращает список названий городов из конфига и их *geoid* |
| get_error_addresses | Запускается вручную | Возвращает список адресов из фида заданного провайдера, которые не удалось геокодировать, в виде excel-файла. |
| get_provider_addresses | Запускается вручную | Позволяет найти в заданном городе адреса и *geocoder_id* зданий, где есть провайдер с заданным *id* или именем. |
| remove_provider | Запускается вручную | Удаляет провайдера с заданным названием по адресу или *geoid* региона. |
| restore_backup | Запускается вручную | Восстанавливает бэкап из заданной таблицы. |
