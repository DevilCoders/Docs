# Оглавление
2. [Общее описание](#general)
1. [Локальная проверка](#dev)
1. [CD - Облачный рантайм](#cd)
1. [CI - new CI](#ci)
3. [Мониторинги](#monitorings)
4. [Квоты](#monitorings)

## Общее описание <a name="general"></a>
Сервис мониторингов контура промо.
Главный дашборд контура https://juggler.yandex-team.ru/dashboards/promo_meta_dashboard?project=market-promo

## Локальная проверка <a name="dev"></a>

1) Внести изменения в `registry`.
2) В директории `arcadia/market/solo_monitorings/marketpromo/creator/` запустить `ya make`.
3) Запустить бинарник командой `./creator`, ознакомиться с изменениями
Можно запустить команду `./creator --apply-changes` и изменения накатятся на прод, чтобы их можно было отсмотреть визуально.
Эти изменения автоматически откатятся через час

```
 ~/Documents/Arcadia/arcadia/market/solo_monitorings/marketpromo/creator/ ./creator --apply-changes
======================================
Processing Check
Syncing resources state!
Calculating actions!
diff for: idx-production.promo-collected-valid-promos
--- before
+++ after
@@ -46,7 +46,7 @@
     "refresh_time": 300,
     "service": "promo-collected-valid-promos",
     "tags": [
-        "a_mark_nrmzpfwtbl",
+        "a_mark_solo_example_juggler",
         "market-promo"
     ],
     "ttl": 3000
Action MODIFY: 1 resources: ['idx-production.promo-collected-valid-promos']
Action SKIP: 4 resources: ['checkouter_production.promo_orders', 'market-main-report.market-generations-count', 'idx-production.promo-collected-invalid-promos', 'idx-production.fast-promo-collected-invalid-promos']
Executing actions!

```

### Секреты

Секрет, содержащий `Juggler` и `Solomon` токены:
https://yav.yandex-team.ru/secret/sec-01fsejq1esjyjxae751yw2kd2t/explore/versions

Если возникает ошибка `'code': 'access_error'`, проверь доступ к секретам

## [CD] Облачный рантайм <a name="cd"></a>
Каждый 1 час шедулер пытается задеплоить `stable` конфиги:
- https://sandbox.yandex-team.ru/scheduler/701819/view
- ресурс конфигов: https://sandbox.yandex-team.ru/resources?type=MARKETPROMO_MONITORINGS_CONFIG

## [CI] В New CI <a name="ci"></a>

https://arcanum.yandex-team.ru/projects/marketpromo/ci/releases/timeline?dir=market%2Fsolo_monitorings%2Fmarketpromo&id=stable-release

После мержа в `trunk` собирается ресурс с бинарником и переводится в состояние `stable`, шедулер подхватывает его и запускает

### [Juggler] Все сгенерированные агрегаты

https://juggler.yandex-team.ru/aggregate_checks/?project=market-promo&ignore_project=true&query=tag%3Dmarket-promo%26tag%3Darc-generated

### Все сгенерированные сущности

https://yt.yandex-team.ru/locke/navigation?path=//home/marketpromo/solo/solo.json
## Мониторинги <a name="monitorings"></a>
!!Пока нет мониторингов!!

## Квоты <a name="quotas"></a>
1. Ресурсы sandbox в квоте MARKETPROMO
2. Ресурсы YT в квоте promocoordinator

