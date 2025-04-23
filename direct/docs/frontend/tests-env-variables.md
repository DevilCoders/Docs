## Переменные окружения

Доступные для переопределения переменные окружения перечислены в таблице:

Переменная окружения | Назначение | Доступные значения | Значение по умолчанию
--- | --- | --- | ---
LOG_LEVEL | Установка уровня логирования | `emerg`, `alert`, `crit`, `error`, `warning`, `notice`, `info`, `debug` | `info`
BETA_PORT | Если вам требуется указать порт, отличный от `TS`, возможно вы что-то делаете не так | `<number>`, `TS` | `TS`
BETA_HOST | Например, `BETA_HOST="https://dna.yandex.ru:3000"`, чтобы прогнать тесты на локальных изменениях | `<string>` ,`''` | `''`
RETRY | Число перезапусков тестов | `<number>` | 4
SESSION_PER_BROWSER | Число сессий для одно браузерного окна | `<number>` | 10
OVERRIDE_FEATURES | Дефолтный список фичей для тестов указан [тут](https://github.yandex-team.ru/direct/dna/blob/master/.config/hermione/lib/overrideFeatures.js#L7-L55). Чтобы включить фичу укажите `<feature_name>`. Чтобы выключить фичу укажите `-<feature_name>`. Например: `b2b_balance_cart, -ab_segments` | `<feature_name>,-<feature_name>` | `''`
OVERRIDE_HASHSUMS | Требуется ли переопределить статику DNA. [В каких случаях может потребоваться.](tests-how-to.md#run-with-dumps) | `1`, `''` | `''`
