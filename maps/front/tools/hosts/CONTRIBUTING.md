# CONTRIBUTING

## Как поменять hosts или inthosts

Склонируйте себе репозиторий и внесите изменения:

```sh
cd maps/front/tools/hosts
make
```

Обновите `CHANGELOG`:

```sh
arc pull --tags
make hosts.patch # или make inthosts.patch
arc pr create
```

> Если вы добавляете новые хосты, то не забудьте указать их и в схеме (`schema.json`). Иначе у вас будут падать тесты.

### Sandbox ресурсы

Trendbox CI соберет новый ресурс:

* [MAPS_CONFIG_HOSTS](https://sandbox.yandex-team.ru/resources?type=MAPS_CONFIG_HOSTS)
* [MAPS_CONFIG_INTHOSTS](https://sandbox.yandex-team.ru/resources?type=MAPS_CONFIG_INTHOSTS)

Для каждого ресурса автоматически добавляется атрибут `version`, по которому можно искать соответствующий `id` ресурса.
