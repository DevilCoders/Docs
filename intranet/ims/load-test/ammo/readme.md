### Генерация паторонов для нагрузочного тестирования

Для генерации патронов, требуется выполнить команду ``` go run ammo.go ``` и передать туда аргументы

##### Необходимые аргументы:

- count (числа патронов, которое будут сгенерировано)
- method (целевой метод патронов)
- identitySource (путь к csv файлу стартовых сущностей)
- groupSource (путь к csv файлу стартовых групп)
- identityTypeSource (путь к csv файлу стартовых типов сущностей)

Примеры csv файлов можно посмотреть в директории:
``` ~/arcadia/intranet/ims/load-test/ammo/generator/sources ```

##### Доступные методы (method) для генерации патронов:

- createIdentity (дополнительно требует аргумент identityTypeSource)
- deleteIdentity (дополнительно требует аргумент IdentitySource)
- listIdentities (дополнительно требует аргумент groupSource)
- getIdentity (дополнительно требует аргумент IdentitySource)
- moveIdentity (дополнительно требует аргумент IdentitySource, groupSource)
- addToGroup (дополнительно требует аргумент IdentitySource, groupSource)
- removeFromGroup (дополнительно требует аргумент IdentitySource, groupSource)
- listIdentityGroups (дополнительно требует аргумент IdentitySource)
- existsInGroup (дополнительно требует аргумент IdentitySource, groupSource)

##### Пример вызова генерации патронов getIdentity

```
go run ammo.go -count 10000 -method getIdentity -identitySource ./generator/sources/identity.csv > ammo.txt
```
