# Ответ поиска по картинкам

API поиска по картинкам возвращает ответ в формате XML. Результаты представлены в виде XML-элементов.

XML-документы состоят из группирующих тегов [request]{% if audience == "internal" %}(../concepts/requestelement-internal.md){% endif %}{% if audience == "external" %}(../concepts/xmlanswer.md#requestelement){% endif %} (обобщенная информация о запросе) и [response]{% if audience == "internal" %}(../concepts/responseel-internal.md){% endif %}{% if audience == "external" %}(../concepts/xmlanswer.md#responseel){% endif %} (список результатов поиска по запросу).

Ниже приведена общая структура результирующего XML-документа.

```xml
<yandexsearch version="1.0">
   <request>
      <!--Атрибуты запроса в дочерних тегах-->
   </request>
   <response>
      <!--Обобщенная информация о полученных результатах поиска в дочерних тегах-->
      <reask>
         <!--Информация об автоматической замене текста запроса перед поиском. Добавляется только в том случае, если запрос исправлен-->
      </reask>
      <results>
         <!--Параметры группировки и результаты поиска в дочерних тегах-->
         <grouping attr="ii" mode="deep" groups-on-page="20" docs-in-group="1" curcateg="-1">
         <group>
         <!--Информация об одном результате поиска по картинкам. Содержит сведения о картинке, попадающей на выдачу, и о ее дубликатах. Негруппирующие дочерние теги содержат общую информацию о группе-->
            <doc>
               <!--Информация о найденной картинке и ее дубликатах в дочерних тегах-->
            </doc>  
               <image-properties>
                  <!--Свойства отображаемой в поисковой выдаче картинки в дочерних тегах-->
               </image-properties>
               <image-duplicates>
                  <!--Сведения о дубликатах отображаемой в поиосковой выдаче картинки. Информация о каждом дубликате содержится в дочерних тегах группирующего тега image-properties-->
               </image-duplicates>
               <image-duplicates-fitsize>
                  <!--Сведения о найденных дубликатах наибольшего размера. Информация о каждом дубликате содержится в дочерних тегах группирующего тега image-properties-->
               </image-duplicates-fitsize>
               <image-duplicates-preview>
                  <!--Сведения о найденных дубликатах уменьшенной копии картинки. Информация о каждом дубликате содержится в дочерних тегах группирующего тега image-properties-->
               </image-duplicates-preview>
         </group>
         <group>
         </group>
         ...
         <group>
         </group>
   </response>
```