## Project layout

Используется [Arcadia-style](https://docs.yandex-team.ru/arcadia-java/java_library_guide#standartnoe-raspolozhenie-fajlov-layout):
```
ya.make
src/
  resources/
    [resource files if needed]
  [code without package-prefix]
  ut/
    src/
      ya.make
      [unit tests code without package-prefix]
```

{% include [Package](./_package.md) %}

{% include [YaMake](./_ya.make.md) %}

### External libraries

External libraries' version fixed in [/crm/library/kotlin/dependency_management.inc](https://a.yandex-team.ru/arcadia/crm/library/kotlin/dependency_management.inc)

{% include [Proto](./_proto.md) %}

