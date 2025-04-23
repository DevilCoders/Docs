## [CD] Облачный рантайм
Каждый 1 час шедулер пытается задеплоить `stable` конфиги:
- https://sandbox.yandex-team.ru/scheduler/703853/view
- ресурс конфигов: https://sandbox.yandex-team.ru/resources?type=MARKETFRONT_MONITORINGS_CONFIG

## [CI] В New CI

https://arcanum.yandex-team.ru/projects/yandexmarketfrontend/ci/releases/timeline?dir=market%2Fsolo_monitorings%2Fmarketfront&id=stable-release

После мержа в `trunk` собирается ресурс с бинарником и переводится в состояние `stable`, шедулер подхватывает его и запускает

## Локальный запуск

1) Внести изменения в `registry`.
2) В директории `arcadia/market/solo_monitorings/marketfront/creator/` запустить `ya.make`.
3) Запустить бинарник командой `./creator`, ознакомиться с изменениями

```
 ~/Documents/Arcadia/arcadia/market/solo_monitorings/marketfront/creator/ ./creator --apply-changes
solo - solomon and juggler configurator
Using LocalFileState state class!
Local state file "./solo.state" does not exist, using default state
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

4) Если изменения выглядят валидно - запустить бинарник с флагом `./creator --apply-changes`

## [Juggler] Все сгенерированные агрегаты

https://juggler.yandex-team.ru/aggregate_checks/?project=market.front&ignore_project=true&query=tag%3Dmarketfront%26tag%3Darc-generated

## Все сгенерированные сущности

https://arcanum.yandex-team.ru/arc_vcs/market/solo_monitorings/marketfront/creator/solo.state

## Секреты

Секрет, содержащий `Juggler` и `Solomon` токены:
https://yav.yandex-team.ru/secret/sec-01fv9zdsyegf8mmjfjer89zy3b/explore/versions
