# SystemPackage

Поле в спеке юнита package. Позволяет вместе с юнитом приносить apt pkg.

Для условной выкладки пакета только на определенное подмножество хостов,
где запускается юнит можно указать версию <skip> для пропуска установки пакета.

Добавление пакета с версией <skip> не изменит id ревизии (если одновремененно не было других изменений), не будет рестартов сервиса/контейнера под юнитом.
Не будет похода в orly на разрешение применения ревизии.

```yaml
packages:
  - name: "yandex-hm-reporter"
    version: "{ver}"
  - name: "yandex-hm-reporter-old"
    version: "<skip>"
```
