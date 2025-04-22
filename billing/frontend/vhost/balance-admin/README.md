## Страница в эксперименте UI

В xml-файле добавить перед легаси-методами
В тэг `page` добавить атрибут `is-experiment-page="true"`

```xml
<block threaded="no" timeout="35000">
    <nameref>MuzzleServantRef</nameref>
    <method>check_admin_ui_experiment</method>
    <param type="StateArg" as="Long" default="1">skip</param>
    <param type="State"/>
</block>
```

## Страница не в эксперименте, но старый UI еще нужен для java-тестов

В xml-файле добавить перед легаси-методами

```xml
<block threaded="no" timeout="35000">
    <nameref>MuzzleServantRef</nameref>
    <method>check_old_ui_user</method>
    <param type="StateArg" as="Long" default="1">skip</param>
    <param type="StateArg" as="LongLong">passport_id</param>
    <param type="State"/>
</block>
```