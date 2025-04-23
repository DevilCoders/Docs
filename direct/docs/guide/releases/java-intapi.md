# Релиз java-Intapi

{% include [этот релиз собирается в Newci](_includes/java-newci.md) %}

{% include [этот релиз собирается в Newci](_includes/newci-auto.md) %}

Для релиза, собранного автоматикой — переходи сразу к разделу [{#T}](#after-create).

{% include [inform](_includes/java-prepare-inform-colleagues.md) %}

### Запусти сборку
{% include [этот релиз собирается в Newci](_includes/java-newci.md) %}

#### Обнови пакеты
После сборки релиза NewCI обновит стейджи, если этого не произошло или нужна особая сборка для обновления разработческих сред следуем [инструкции](../../jeri/guide/update-yadeploy-stage.md#apply-new-spec). Стейджи для dev7/devtest:
- dev7: <https://deploy.yandex-team.ru/stages/direct-intapi-dev7>
- devtest: <https://deploy.yandex-team.ru/stages/direct-intapi-devtest>

{% include [update-stable-footer](_includes/java-update-stable-footer.md) %}


## Тестирование { #testing }

Раз в 15 минут [автоматика](../../reference/qa/regression-java-intapi.md#automation):

- переводит релиз в статус **Тестируется**
- создает и привязывает к релизу тикеты:
   - на регрессию ([пример](https://st.yandex-team.ru/TESTIRT-13217))
   - на юнит-тесты ([пример](https://st.yandex-team.ru/DIRECT-130139))
- запускает [автотесты](../../reference/qa/regression-java-intapi.md#autotests)
- прикладывает в тикет на регрессию ссылки на запуски в AQuA
- запускет [юнит-тесты](../../reference/qa/regression-java-intapi.md#unit-tests)

{% note info "Если автоматика сломалась" %}

Действуй по обстоятельствам — создай тикеты вручную, запусти [регрессию](../../reference/qa/regression-java-intapi.md).

{% endnote %}

{% include [Юнит-тесты](_includes/java-unit-tests.md) %}

После успешного разбора юнит-тестов добавь значение **intapi** в поле **Tested&nbsp;apps** тикета на их запуск и закрой его.

### Автотесты { #auto-tests }
Убедись, что регрессионные тесты прошли или перезапусти упавшие.

После успешного прохождения тестов —
добавь значение **intapi** в поле **Tested&nbsp;apps** тикета на регрессию и закрой его.


{% include [tasks-in-release](_includes/java-tasks-in-release.md) %}


{% include [заголовок "Хотфикс в релиз"](_includes/java-hotfix-head.md) %}

{% include [примечание про ОК от Леши](_includes/new-tasks-hotfixing.md) %}

Хотфиксы собираются по той же [инструкции](./release-newci.md)


{% include [wait-testing-header](_includes/java-wait-testing-header.md) %}

Убедись, что этим тикетам не забыли добавить значение **intapi** в поле **Tested&nbsp;apps**, иначе попроси тестировавшего это исправить.


{% include [testing-done-header](_includes/java-testing-done-header.md) %}

{% include [testing-done-footer](_includes/java-testing-done-footer.md) %}



{% include [accept](_includes/java-accept.md) %}


{% include [deploy](_includes/java-deploy.md) %}
