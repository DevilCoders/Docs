= `factor_check` на нескольких пулах
Программа multitask упрощает запуск проверки фичей на нескольких пулах.
Сейчас есть два таска:
- `any_features.yml` им пользоваться для проверки фичей, которые зависят в том числе от баннера. Среди пулов pclick-и и bid correction.
- `hit_features.yml` -- этот таск включает в себя всё из `any_features.yml` и еще некоторые другие пулы, которые расчитываются для хита целиком: cpm, медиация итп

Пример запуска: `./multitask user_features.yml --timestamp $(date -d 2018-10-02 +%s)`
