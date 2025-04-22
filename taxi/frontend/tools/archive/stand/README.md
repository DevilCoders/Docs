# Стенды

[TeamCity Queue](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Infranaim_LavkaFrontend_Stand)

## Параметры package.json

- обязательная точная версия NodeJS:

```json
{
    "engines": {
        "node": "14.17.5"
    }
}
```

## Параметры service.yaml

- обязательный идентификатор сервиса в `tariff-editor`-е:

```yaml
serviceId: 354720
```

- опциональный пресет инстанса, по-умолчанию используется `piko` (0.5 CPU, 1GB RAM), можно указать более мощный `nano` (
  1 CPU, 4GB RAM), но злоупотреблять этим не стоит (стендов много, а ресурсы не бесконечные):

```yaml
pullRequestStand:
    preset: nano
```

- опциональный суффикс домена стенда, по-умолчанию используется `{project}.dev.yandex.net`
  (например: `lavka.dev.yandex.net`):

```yaml
pullRequestStand:
    fqdnSuffix: lavka.dev.yandex.ru
```

- по умолчанию выгрузка статики на s3 отключена, можно включить через флаг:
```yaml
pullRequestStand:
    s3: true
```

## Дата центр

По умолчанию стенд размещается случайным образом в одном из ДЦ: `man`/`sas`/`vla`. Чтобы разместить стенд в конкретном
ДЦ, можно добавить в PR соответствующую метку:

- `man` <- `dc:man`
- `sas` <- `dc:sas`
- `vla` <- `dc:vla`

При наличии нескольких ДЦ меток, будет выбран первый по алфавиту ДЦ.

## Статика

Стенды не используют s3 статику, поэтому для `unstable` окружения нужно отдавать статику из приложения