Обнаруженные проблемы:


{%- if !instanceMismatches.isEmpty() %}
Расхождение в следующих инстансах:
------------------------------------

{% for instanceMismatch in instanceMismatches -%}
**Сервис {{instanceMismatch.getConfId().getService()}}, confId: {{instanceMismatch.getConfId().getId()}} (host: {{instanceMismatch.getHost()}})**

{%- if !instanceMismatch.getChangedFiles().isEmpty() %}
<{Измененные файлы:

#|
|| **Файл**| **Ожидаемая версия файла**| **Ожидаемая контрольная сумма**| **Фактическая контрольная сумма**||
{% for changedFile in instanceMismatch.getChangedFiles() -%}
|| {{changedFile.getPath()}}| ((https://sandbox.yandex-team.ru/task/{{changedFile.getExpectedVersion()}}/view {{changedFile.getExpectedVersion()}}))| {{changedFile.getExpectedChecksum()}}| {{changedFile.getActualChecksum()}}||
{% endfor %}

{%- if instanceMismatch.isChangedFilesOverflow() %}
...
Всего измененных: {{instanceMismatch.getTotalChangedFiles()}} (Показываются первые {{MAX_FILES_IN_REPORT}})
{%- endif %}
|#}>

{%- endif %}

{%- if !instanceMismatch.getNotFoundFiles().isEmpty() %}
<{Не найденные файлы:
{% for notFoundFile in instanceMismatch.getNotFoundFiles() -%}
* {{notFoundFile}}
{% endfor %}

{%- if instanceMismatch.isNotFoundFilesOverflow() %}
...
Всего не найденных: {{instanceMismatch.getTotalNotFoundFiles()}} (Показываются первые {{MAX_FILES_IN_REPORT}})
{%- endif %}}>

{%- endif %}

{% endfor %}

{%- endif %}


{%- if !unknownConfIds.isEmpty() %}
В ЦУМе отсутсвует информация о ресурсах для инстансов:
-----------------------------------
    {% for unknownConfId in unknownConfIds -%}
* Сервис {{unknownConfId.getService()}}, confId: {{unknownConfId.getId()}}
    {% endfor %}
{%- endif %}

