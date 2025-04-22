# logging-setup-proto

Скомпилированные [proto файлы logging_setup][proto-files] (на момент [r9231804][r9231804]). За основу взят пакет [arcanum-proto][arcanum-proto], но используется официальная версия pbts.

## Установка

```console
npm i @yandex-int/logging-setup-proto --registry=https://npm.yandex-team.ru
```

## Обновление

Скачайте свежие обновления из аркадии:

```console
npm run fetch
```

Скомпилируйте для упаковки в npm-пакет:

```console
npm run proto
```

Закоммитьте всё, что получилось. Не забудьте обновить версию в этом README.

[proto-files]: https://a.yandex-team.ru/arc/trunk/arcadia/search/begemot/rules/init/logging_setup/proto/logging_setup.proto
[r9231804]: https://a.yandex-team.ru/arc/trunk/arcadia/search/begemot/rules/init/logging_setup/proto/logging_setup.proto?rev=9231804
[arcanum-proto]: https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/arcanum-proto?rev=8556762
