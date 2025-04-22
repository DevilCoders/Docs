# Расширения

## Второй экран

Приложение позволяет работать одновременно с двумя мониторами: первый — это основной монитор, с которым оператор
взаимодействует по основным сценариям; на втором отображается вспомогательная информация к основному монитору. Например,
на основном мониторе отображается обращение обрабатываемое оператором, а на втором в это время отображается заказ,
который привязан к обращению.

Для настройки второго экрана предназначено расширение secondView, которое указывается для метакласса объекта основного
экрана.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<m:config xmlns:m="urn:jmf:metaclass:config:1.0"
          xmlns:de="urn:jmf:module:default:extension:config:1.0"
          xmlns:cie="urn:jmf:catalog:items:extension:config:1.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

    <m:metaclass>
        <m:fqn>ticket$firstLine</m:fqn>
        <!-- ... -->
        <m:extensions>
            <!-- Здесь указано, что отображаемый объект для второго экрана брать из атрибута с кодом order -->
            <m:extension xsi:type="de:secondView" attribute="order"/>
        </m:extensions>
    </m:metaclass>
</m:config>
```

## Каталоги

Для системных бизнес-объектов, с которыми оператор не работает напрямую, часто удобно иметь простой CRUD-интерфейс:
место, где можно посмотреть список всех объектов, создать объект, отредактировать его, удалить. Для построения такого
простого интерфейса служит расширение catalog.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<m:config xmlns:m="urn:jmf:metaclass:config:1.0"
          xmlns:de="urn:jmf:module:default:extension:config:1.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

    <m:metaclass>
        <m:fqn>customerMarker</m:fqn>
        <!-- ... -->
        <m:extensions>
            <!-- Здесь category - категория справочника -->
            <m:extension xsi:type="cie:catalog" category="order"/>
        </m:extensions>
    </m:metaclass>
</m:config>
```

## Управление идентификатором объектов метакласса

В системе есть возможность конфигурировать правила формирования идентификаторов (id) объектов. Для этого предназначено
расширение entityId

```xml
<?xml version="1.0" encoding="UTF-8"?>
<m:config xmlns:m="urn:jmf:metaclass:config:1.0"
          xmlns:hb="urn:jmf:hibernate:extension:config:1.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

    <m:metaclass>
        <m:fqn>customerMarker</m:fqn>
        <!-- ... -->
        <m:extensions>
            <!-- Идентификатор - строка. Его всегда необходимо указывать вручную. -->
            <m:extension xsi:type="hb:entityId" type="string"/>

            <!-- Идентификатор - число (используется по умолчанию) -->
            <!-- Дополнительно можно указать имя последовательности, которая будет использоваться для генерации -->
            <!-- идентификаторов. Если не указана, то используется id_sequence -->
            <!-- m:extension xsi:type="hb:entityId" type="integer" -->
            <!-- hb:generator xsi:type="hb:sequenceEntityIdGenerator" sequence="seq_name"/ -->
            <!-- /m:extension -->
        </m:extensions>
    </m:metaclass>
</m:config>
```

## Управление сериализацией атрибутов объекта

```xml
<?xml version="1.0" encoding="UTF-8"?>
<m:config xmlns:m="urn:jmf:metaclass:config:1.0"
          xmlns:u="urn:jmf:ui:extension:config:1.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

    <m:metaclass>
        <m:fqn>customerMarker</m:fqn>
        <!-- ... -->
        <m:attributes>
            <m:attribute>
                <m:code>title</m:code>
                <!-- ... -->
                <m:extensions>
                    <!-- Указываем, что значение атрибута всегда отдавать в DTO, при этом права на получение значения -->
                    <!-- атрибута -->
                    <m:extension xsi:type="u:dto" required="true" permission="false"/>
                </m:extensions>
            </m:attribute>
        </m:attributes>
    </m:metaclass>
</m:config>
```

## Управление логированием изменения значения атрибута

Все действия с объектами метаклассов с логикой entityHistory логируются и всегда можно восстановить кто и что делал с
объектом. Расширение entityHistory позволяет управлять логированием изменений отдельных атрибутов.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<m:config xmlns:m="urn:jmf:metaclass:config:1.0"
          xmlns:lde="urn:jmf:logic:default:extension:config:1.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

    <m:metaclass>
        <m:fqn>customerMarker</m:fqn>
        <m:logics>
            <m:logic>entityHistory</m:logic>
        </m:logics>
        <!-- ... -->
        <m:attributes>
            <m:attribute>
                <m:code>title</m:code>
                <!-- ... -->
                <m:extensions>
                    <!-- Отключаем логирование значения атрибутов -->
                    <m:extension xsi:type="lde:entityHistory" enabled="false"/>
                </m:extensions>
            </m:attribute>
        </m:attributes>
    </m:metaclass>
</m:config>
```
