# How to stateless remove resource

Чтобы удалить ресурс (пакет, файл) из спеки hostctl юнита юнита при этом реально не удаляя ресурс с хоста.
Например, может быть полезно, в случаях когда в спеке управлялся файл из пакета,
чтобы перестать управлять файлом из нескольких мест можно воспользоваться такой схемой:
1. Выставить аннотацию skip-remove-phase с yaml значением в формате описаном ниже
https://a.yandex-team.ru/arc/trunk/arcadia/infra/hostctl/proto/hostctl.proto?rev=r8223708#L57
```proto
// Can be used as annotation in yaml format
message SkipRemovePhase {
    repeated string packages = 1;
    repeated string files = 2;
    bool daemon = 3;
}
```
Пример как положить yaml структуру внутрь спеки юнита
```yaml
meta:
  kind: "SystemService"
  version: "{ver}"
  name: "systemd-sysctl"
  annotations:
    stage: "{stage}"
    skip-remove-phase: |+
      packages:
        - pkgname
      files:
        - filename
      daemon: true
```
2. Выкатить изменения, после этого hostctl будет вырезать/пропускать все таски на удаление REMOVED ревизии
3. Следующим шагом удалить из спеки нужный ресурс, реально с хоста ничего не удалится, но произойдет переключение ревзии (может порестартится systemd сервис, port контейнер юнита)
4. Не забыть удалить skip-remove-phase аннотацию
