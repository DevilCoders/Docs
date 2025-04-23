{%- if (request.getGeneratedBy().contains("forecaster_") || !version.equals("Базовая версия")) %}
%%(wacko wrapper=shade border="2px dashed  red")
== //Внимание! Важная информация!//
{%- if request.getGeneratedBy().contains("forecaster_") %}
=== Заявка сгенерирована автоматически
!!Если вы хотите отредактировать заявку вручную — проконсультируйтесь предварительно с ((https://wiki.yandex-team.ru/Market/Projects/preorder/2021/responsibles/ ответственным за облако)), вероятно лучше алгоритм скорректировать и перегенерить заявку. Любые вопросы по расчету можно задать ответственному за облако.!!
{%- endif %}
{%- if !version.equals("Базовая версия") %}
=== Версия заявки отличается от базовой
!!Это заявка не базовой версии (Версия другой KPI), и, вероятно, на другой набор KPI (см. обоснование заявки)!!
{%- endif %}
%%
{%- endif %}

Запрос на предоставление ресурсов:

#|
|| **{{preorderId}}. {{version}}** ||
|| Имя | {{request.getName()}} ||
|| Облако | {{request.getCloud()}} ||
|| Группа | ((https://abc.yandex-team.ru/services/{{request.getAbc()}}/)) ||
|| Тип | {{requestType}} ||
{%- if requestType == "NEW_SERVICE" %}
|| Цель | {{goal}} ||
{%- endif %}
{%- if request.getGeneratedBy().contains("forecaster_") %}
|| Запрошено | !!автоматически!! {{request.getGeneratedBy()}} ||
{%- else %}
|| Запрошено | кто:{{request.getCreatedBy()}} ||
{%- endif %}
|| Дедлайн | {{request.getDeadline()}} ||
{%- if !request.getApprovedBy().isEmpty() %}
|| Подтверждено | кто:{{request.getApprovedBy()}} ||
{%- endif %}
|#

== Запрошенные ресурсы

!!++Внести изменения в заявку можно **__только через комментарии__**, см. Макросы --> Макрос MCRP++!!

%%
{{request.getResources().toPrettyJsonString()}}
%%

* Для редактирования запрашиваемых ресурсов напишите комментарий с использованием макроса "Макрос MCRP".
* Для изменения ABC сервиса поменяйте соответствующее поле в тикете.

{%- if !request.getReason().isEmpty() %}
===+ Обоснование заявки
<[{{request.getReason()}}]>
{%- endif %}

{%- if !request.getWhatifno().isEmpty() %}
===+ В случае отказа
<[{{request.getWhatifno()}}]>
{%- endif %}
