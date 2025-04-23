# Плагин для подгрузки внешних словарей ClickHouse из YT

## Описание
Плагин представляет собой динамическую библиотеку, которая реализует интерфейс
для плагинов [внешних словарей ClickHouse](https://clickhouse.yandex/docs/ru/dicts/external_dicts/).
Поддерживает все типы внешних словарей, кроме `complex_key_cache и ip_trie`.
Для cached словарей используется YT-команда LookupRows, для прочих YT-команда SelectRows.
Вызовы делаются через rpc-proxy кластеров YT, поэтому
источником словарей для плагина могут быть только кластера, на которых есть
rpc-proxy.

## Конфигурационный файл
Данные для каждого словаря заполняются в секции `<dictionary>`, специфичные
настройки для YT-словаря задаются в секции `<source>`. Доступные настройки:
* `<path>` -- путь к .so файлу с плагином
* `<settings>` -- здесь указываются настройки для YT-таблицы
 * `<cluster>` -- имя YT-кластера на котором находится словарь, без точек.
Допускается несколько кластеров, при недоступности одного, будет использоваться
следующий по скиску. Пример `<cluster>hahn</cluster>`.
 * `<key>` -- ключевые поля справочника.

Для cache допускается только один ключ, при этом целочисленный,
Знаковость/беззнаковость не важна. Также он должен совпадать с одним из ключей таблицы в YT,
т.к. он будет использоваться в LookupRows. У прочих типов подобных ограничений нет. Пример `<key>OrderID</key>`.
 * `<table>` -- путь к таблице на YT-кластере, должен быть одинаковым для всех
   указанных YT-кластеров. Пример `<table>//home/yabs/dict/OrderInfo</table>`.
 * `<token>` -- YT-токен пользователя, имеющего read-права в указанную `<table>`.
 * `<user>` -- имя пользователя имеющий read-права в указанную `<table>`.
 * `<force_read_table>` -- форсировать использование функции ReadTable в SelectRows.
   При этом запрос `<query>` к словарю игнорируется. Может быть полезно, если
   нужно прочитать более 5 миллионов строк за раз из динамической таблицы.
 * `<field>` -- Поле словаря, которое требуется получить из таблицы. Допускается
   множество значений. Используется для `cached` и `hashed` словарей. Можно использовать alias через |.
   При указании alias'а поле доступно только по нему. Пример `<field>UpdateTime</field>`,
   с alias'ом `<field>GroupOrderID|GroupID</field>`.
   Если `<field>` указан для `hashed` -- словаря то подразумевается работа со статической YT-таблицей,
   которая вычитывается построчно, а не запросом.
   (!новая возможность!) Можно указывать `<date_field>` и `<datetime_field>`
   вместо `<field>`. Позволяет в атрибутах словаря указывать типы `Date` и
   `DateTime` и работать с датами с помощью запросов `dictGetDate` или
   `dictGetDateTime`.
 * `<query>` -- Запрос к словарю, который необходимо выполнить, чтобы получить
   из него все записи. Актуально для всех словарей. Но чтобы работало для
   `cached` нужно указать дополнительный параметр
   `<use_query_for_cache>true</use_query_for_cache>`.
   Имя таблицы указывать не нужно, но можно. Пример `<query>PageID, TargetType,
   OptionsMainSerp as IsMainSerp</query>`. Для всех полей с выражениями должны
   быть указаны алиасы, иначе либа даже не загрузится.

Остальные настройки, например в блоке `<structure>`, ничем не отличаются от
конфигураций словарей из других источников.

## Примеры для конфигурационных файлов

### Для `hashed`
```xml
    <dictionary>
        <layout>
            <hashed />
        </layout>
        <lifetime>
            <max>3600</max>
            <min>1800</min>
        </lifetime>
        <name>PageDictYT</name>
        <source>
            <library>
                <path>/usr/lib/libclickhouse_dictionary_yt.so</path>
                <settings>
                  <cluster>hahn</cluster>
                  <cluster>banach</cluster>
                  <key>PageID</key>
                  <query>PageID, TargetType, OptionsMainSerp as IsMainSerp</query>
                  <table>//home/yabs/dict/Page</table>
                  <token>XXX</token>
                  <user>someuser</user>
                </settings>
            </library>
        </source>
        <structure>
            <attribute>
                <name>TargetType</name>
                <null_value>0</null_value>
                <type>Int32</type>
            </attribute>
            <attribute>
                <name>IsMainSerp</name>
                <null_value>0</null_value>
                <type>Int8</type>
            </attribute>
            <id>
                <name>PageID</name>
            </id>
        </structure>
    </dictionary>
```
Со статической таблицей:
```xml
    <dictionary>
        <layout>
            <hashed />
        </layout>
        <lifetime>
            <max>180</max>
            <min>120</min>
        </lifetime>
        <name>StaticPageDictYT</name>
        <source>
            <library>
                <path>/usr/lib/libclickhouse_dictionary_yt.so</path>
                <settings>
                  <cluster>hahn</cluster>
                  <key>PageID</key>
                  <field>TargetType</field>
                  <field>OptionMainSerp|IsMainSerp</field>
                  <table>//home/yabs/dict/StaticPage</table>
                  <token>XXX</token>
                  <user>someuser</user>
                </settings>
            </library>
        </source>
        <structure>
            <attribute>
                <name>TargetType</name>
                <null_value>0</null_value>
                <type>Int32</type>
            </attribute>
            <attribute>
                <name>IsMainSerp</name>
                <null_value>0</null_value>
                <type>Int8</type>
            </attribute>
            <id>
                <name>PageID</name>
            </id>
        </structure>
    </dictionary>
```

### Для `cached`
```xml
    <dictionary>
        <layout>
            <cache>
              <size_in_cells>3000000</size_in_cells>
            </cache>
        </layout>
        <lifetime>
            <max>3600</max>
            <min>1800</min>
        </lifetime>
        <name>OrderInfoDictYT</name>
        <source>
            <library>
                <path>/usr/lib/libclickhouse_dictionary_yt.so</path>
                <settings>
                  <cluster>hahn</cluster>
                  <cluster>banach</cluster>
                  <key>OrderID</key>
                  <field>GroupOrderID|GroupID</field>
                  <field>BaseNo</field>
                  <field>UpdateTime</field>
                  <table>//home/yabs/dict/OrderInfo</table>
                  <token>XXX</token>
                  <user>someuser</user>
                </settings>
            </library>
        </source>
        <structure>
            <attribute>
                <name>GroupID</name>
                <null_value>0</null_value>
                <type>Int32</type>
            </attribute>
            <attribute>
                <name>BaseNo</name>
                <null_value>0</null_value>
                <type>Int8</type>
            </attribute>
            <attribute>
                <name>UpdateTime</name>
                <null_value>0</null_value>
                <type>Int64</type>
            </attribute>
            <id>
                <name>OrderID</name>
            </id>
        </structure>
    </dictionary>
```
### Для `complex_key_cache`
```xml
    <dictionary>
        <layout>
            <complex_key_cache>
              <size_in_cells>3000000</size_in_cells>
            </complex_key_cache>
        </layout>
        <lifetime>
            <max>30</max>
            <min>10</min>
        </lifetime>
        <name>SSPPageMappingDictYt</name>
        <source>
            <library>
                <path>/usr/lib/libclickhouse_dictionary_yt.so</path>
                <settings>
                  <cluster>hahn</cluster>
                  <key>SSPID</key>
                  <key>PageTokenMD5</key>
                  <field>PageToken</field>
                  <table>//home/yabs/dict/SSPPageMapping</table>
                  <token>XXX</token>
                  <user>someuser</user>
                </settings>
            </library>
        </source>
        <structure>
            <attribute>
                <name>PageToken</name>
                <null_value>0</null_value>
                <type>String</type>
            </attribute>
            <key>
              <attribute>
                <name>SSPID</name>
                <type>Int64</type>
              </attribute>
              <attribute>
                <name>PageTokenMD5</name>
                <type>UInt64</type>
              </attribute>
            </key>
        </structure>
    </dictionary>
```

## Текущие версии
* trusty - yandex-clickhouse-dictionary-yt=8388415
* xenial - yandex-clickhouse-dictionary-yt=8389625
