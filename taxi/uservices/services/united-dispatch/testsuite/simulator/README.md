# United dispatch simulator

Инструмент имитационного моделирования операций доставки.
[Вики](https://wiki.yandex-team.ru/taxi/backend/logistics/united-dispatch/simulator/)

## Использование

Для того, чтобы начать пользоваться симулятором, нужно инициализировать отдельный case - локальный каталог с файлами,
который содержит все нужные данные для запуска.

1. Перейти в каталог united-dispatch

    ```bash
    cd services/united-dispatch
    ```

2. Инициализировать case с нужным именем

    ```bash
    make create-simulator-case CASE=your_case_name
    ```

3. Изменить нужные конфиги/моки/данные в созданном каталоге `testsuite/simulator/cases/your_case_name`
4. Запустить симуляцию

    ```bash
    make simulate CASE=your_case_name
    ```

## Файлы в case

1. `mocks` - моки ответов АПИ внешних сервисов
    * `driver_trackstory.py` - ответ `/driver-trackstory/position`
    * `order_satisfy.py` - ответ сервиса candidates `/candidates/order-satisfy`
    * `order_search.py` - ответ сервиса candidates `/candidates/order-search`
    * `score_candidates.py` - ответ сервиса `/driver_scoring/v2/score-candidates-bulk`
2. `static` - статические файлы
    * `experiments3/*` - конфигурация экспериментов
    * `config.json` - конфигурация статических конфигов
3. `main.py` - основной файл запуска с шагами генерацией данных, запусков планеров и сбора статистики
4. `out` - результат запуска симуляции
    * `.output.log` - лог шагов симуляции
    * `.stats.log` - агрегированная статистика запуска симуляции в читаемом формате
    * `.stats.p` - агрегированная статистика запуска симуляции (для скрипта)
5. `.stats.log` - статистика по запускам симулятора, формируется вызовом скрипта cmd/analyze
