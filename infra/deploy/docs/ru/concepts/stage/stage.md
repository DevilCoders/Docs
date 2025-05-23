# Stage

**Stage** — это группа [Deploy Unit](../deploy-unit/deploy-unit.md), выкладка которых оркестрируется между собой. Служит, например, для разделения окружений (testing, pre-stable, stable) или объединения разных, но связанных логически Deploy unit (backend + frontend).

Stage обозначается значком ![stage-icon](../../_assets/icons/stage.png).

Помимо списка deploy_unit, доступны следующие поля:

* `revision` — должно инкрементироваться при каждом изменении, dctl/GUI делают это за пользователя автоматически.
* `account_id` — ABC-сервис, из квоты которого будут браться вычислительные ресурсы для запуска Подов. С появлением проектов привязка к ABC-сервису переедет в них.
* `revision_info` — комментарий для отображения в истории

Все изменения в Деплой вносятся через спеку [YP-объекта stage](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/stage.proto?rev=r8782301#L44). Текущее состояние отображается [в статусе](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/stage.proto?rev=r8782301#L96).

{% note warning %}

Часть полей статуса относится к внутреннему состоянию и со временем будет удалена, перед использованием в скриптах проконсультируйтесь со специалистом

{% endnote %}

## Про ревизии {#revisions}

В Y.Deploy реализовано раздельное версионирование Deploy Unit'ов в рамках одного Stage. Это позволяет вносить изменения и управлять выкладкой более гранулярно — при изменении настроек Deploy Unit'а будет изменена только его ревизия, что приведет к обновлению подов только конкретного Deploy Unit'а, а не каждого пода у всех deploy unit'ов в стейдже.

При этом при внесении изменений в Deploy Unit стейджа, его версия также будет инкрементироваться — это полезно для отображения и отслеживания изменений, в том числе напрямую не связанных с изменениями в спецификации Deploy Unit'а. К таким изменениям можно отнести, например, удаление deploy unit'а или установку/снятие флага `Sox service`. Однако, в отличие от ревизии deploy unit'a, к ревизии стейджа неприменимо понятие "целевая" ревизия, только текущая актуальная, в то время как для deploy unit'ов еще присутствует этап приведения подов deploy unit'а из состояния "ревизия N" в "ревизия N+1".

### Особенности изменения ревизий {#revisions-details}

- В данный момент у пользователя есть возможность задать любое значение как для [Stage.revision](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/stage.proto?rev=r8189952#L50), так и для [DeployUnit.revision](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/stage.proto?rev=r8189952#L205). Единственное ограничение: новое значение ревизии не может быть меньше предыдущего. При попытке пользователем задать значение меньше текущего, такое значение будет проигнорировано, а фактически будет установлено current_revision + 1.
- В случае, если пользователь не заполнил поле с ревизией, автоматика выставит current_revision + 1 для тех DeployUnit, в которых были изменения. Для Stage заполнение ревизии на стороне YP работает аналогичным образом.
- Планируется убрать возможность ручного заполнения Stage.revision / DeployUnit.revision: [DEPLOY-4514](https://st.yandex-team.ru/DEPLOY-4514).
- Отсчет ревизий для новых Stage/DeployUnit начинается с 1.

### Пример {#sample}

Текущая версия ревизии DeployUnit = 100

1. Пользователь обновляет спеку и просит выставить DeployUnit.revision = 77 (т.е. просит выставить значение меньше текущего).

    Спека обновится (ошибки не возникнет), но в ревизии появится версия 101 (если содержимое DU поменялось) либо останется 100 (если содержимое DU не менялось). В обоих случаях данного примера будет **не та ревизия, которую просил пользователь** (просил 77, при текущей 100). Таким образом контролируется, что ревизия DU никогда не откатывается назад, а всегда только возрастает (не обязательно на 1).

2. Пользователь обновляет спеку и просит выставить DeployUnit.revision = 277.

    Спека обновляется, значение 277 будет записано независимо от того, менял он что-то в DU или нет.

3. Пользователь обновляет спеку, поле DeployUnit.revision отсутствует, либо имеет значение 100.

    Если в спеке DU есть изменения, запишется 101 (current_revision + 1). Если нет изменений, останется значение 100.