# Поиск по бизнес-объектам системы

В системе реализован полнотекстовый поиск по значениям атрибутов бизнес-объектов.

Для включения поиска необходимо в описании метакласса указать список атрибутов по которым должен осуществляться
полнотекстовый поиск в extension для поиска. Атрибуты, которые объявлены у родительского метакласса, автоматически
прорастают в потомков.

Логика withSearch делает объекты метакласса доступными для глобального поиска по объектам всей системы и позволяет
выдавать права на поиск разным ролям.

Пример:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<m:config xmlns:c="urn:jmf:common:1.0"
          xmlns:m="urn:jmf:metaclass:config:1.0"
          xmlns:mse="urn:jmf:module:search:extension:config:1.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

    <m:metaclass>
        <m:fqn>employee</m:fqn>
        <m:logics>
            <m:logic>withSearch</m:logic>
        </m:logics>
        <m:attributes>
            <m:attribute>
                <m:code>title</m:code>
                <m:title>
                    <c:value>ФИО</c:value>
                </m:title>
                <m:type code="string"/>
            </m:attribute>
            <m:attribute unique="true">
                <m:code>staffLogin</m:code>
                <m:title>
                    <c:value>login из staff.yandex-team.ru</c:value>
                </m:title>
                <m:type code="string"/>
            </m:attribute>
        </m:attributes>

        <m:extensions>
            <m:extension xsi:type="mse:search" globalSearchEnabled="true">
                <mse:search>
                    <mse:attribute code="title"/>
                    <mse:attribute code="staffLogin"/>
                    <mse:attribute code="uid"/>
                </mse:search>
            </m:extension>
        </m:extensions>
    </m:metaclass>

</m:config>
```

См. так же FulltextSearchFilter
