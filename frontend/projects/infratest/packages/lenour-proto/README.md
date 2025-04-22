# lenour-proto

Скомпилированные [proto файлы lenour][proto-files] (на момент [r8617026][r8617026]). За основу взят пакет [arcanum-proto][arcanum-proto], но используется официальная версия pbts.

## Установка

```console
npm i @yandex-int/lenour-proto --registry=https://npm.yandex-team.ru
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

[proto-files]: https://a.yandex-team.ru/arc/trunk/arcadia/serp/lenour/src/proto
[r8617026]: https://a.yandex-team.ru/arc/trunk/arcadia/serp/lenour/src/proto?rev=8617026
[arcanum-proto]: https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/arcanum-proto?rev=8556762
