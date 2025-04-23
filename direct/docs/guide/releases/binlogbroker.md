# Релиз binlogbroker

{% include [inform](_includes/java-prepare-inform-colleagues.md) %}

## Автоматическая сборка { #auto-release }

Автоматическая сборка проиходит раз в 2 недели в пятницу, если релиз не собирался в течение 2х недель. В пятницу, потому что релизу binlogbroker стоит полежать пару дней. После сборки стоит посмотреть, что релиз ничего не разломал в целом по [дашборду](https://solomon.yandex-team.ru/?project=direct-test&cluster=app_binlogbroker&service=java-monitoring&env=testing&dashboard=ess-test&b=1d&e=). Как минимум, проверить, что приложение не перезапускается постоянно, и пишет данные
Тестировать релиз нужно начинать в понедельник по инструкции ниже

## Ручная сборка { #manual-release }

Если нужно собрать релиз не дожидаясь автоматическую сборку: см. [инструкцию](./release-newci.md) по сборке в NEWCI. Работает долго: минут 25—45.

## После сборки релиза { #after-create }

#### Стейджи в Deploy
Приложение `binlogbroker` в Deploy, непрод обновляется при сборке релиза, для ручного обновления разработческих сред следуем [инструкции](../../jeri/guide/update-yadeploy-stage.md#apply-new-spec). Стейджи для dev7/devtest:
- dev7: <https://deploy.yandex-team.ru/stages/direct-java-binlogbroker-dev7>
- devtest: <https://deploy.yandex-team.ru/stages/direct-java-binlogbroker-devtest>

{% include [update-stable-footer](_includes/java-update-stable-footer.md) %}

## Тестирование { #testing }

- Робот [придет и сделает](./autochecklist.md) в тикете чеклист и будет периодически его обновлять

- создаются и привязываются к релизу тикеты:
    - на юнит-тесты ([пример](https://st.yandex-team.ru/DIRECT-160386))

- Когда релиз готов к проверке, выставить у тикета тег `binlogbroker_health_check`, в течение пары минут робот напишет комментарий с графиками и проверками. Нужно просмотреть все графики согласно инструкцим из комментария и, если все ожидаемо, выставить галку в чеклисте, что проверка сделана

{% note info "Если автоматика сломалась" %}

Действуй по обстоятельствам — создай тикет и запуск юнит-тестов вручную

{% endnote %}

{% include [Юнит-тесты](_includes/java-unit-tests.md) %}

{% include [tasks-in-release](_includes/java-tasks-in-release.md) %}

{% include [заголовок "Хотфикс в релиз"](_includes/java-hotfix-head.md) %}

{% include [примечание про ОК от Леши](_includes/new-tasks-hotfixing.md) %}

Хотфиксы собираются по той же [инструкции](./release-newci.md)

{% include [wait-testing-header](_includes/java-wait-testing-header.md) %}

{% include [testing-done-footer](_includes/java-testing-done-footer.md) %}

{% include [accept](_includes/java-accept.md) %}

{% include [deploy](_includes/java-deploy.md) %}
