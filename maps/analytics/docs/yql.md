## Как создать постоянный расчет на YQL?

- Определить место в Аркадии, где будет лежать расчет
- Создать новую папку с файлами `query.sql` и `lama.yaml`
- В `YQL` можно передать инлайном параметры (часто это просто дата)

    ```sql
    DECLARE $date as String;
    ```
    Либо можно встреить старый способ (не рекомендуется к использованию)
    ```sql
    DECLARE $param_dict AS Dict<String, String>;
    $date = $param_dict['date'];
    ```
- Для того, чтобы тестировать и не перезаписать данные в продакш нужно завести флаг `debug` и все пути выходных табличкек заводить определенным образом(см пример ниже). Такой формат нужен чтобы можно было написать тесты на этот `YQL` и использовать команду `lama make_sample`
    ```sql
    $debug = True; -- False for trunk/production
    $some_output_table = '//home/maps/analytics/legacy/yql/output'; -- production name
    $some_output_table = if($debug, Re2::Replace('home/maps/analytics')($some_output_table, 'home/maps/analytics/tmp'), $some_output_table); -- tmp debug name
    ```
- Для обычных расчетов (почти все) `lama.yaml` используем [пресет](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/tools/lama/presets/README.md#projects/maps-analytics/yql) для `YQL`

    ```yaml
    preset: projects/maps-analytics/yql
    preset_options:
      path: /maps/analytics/YOUR__REACTOR_PATH
      trigger_artifacts:
        - /maps/analytics/YOUR_TRIGGER_PATH
    ```
    Если не подходит по каким-либо причинам этот пресет, можно воспользоваться полным конфигом или обратиться к [Руслану Кучерову](https://staff.yandex-team.ru/r-kucherov)
    
    В пресете используется шаблонный воркфлоу для `YQL`. Подробнее можно почитать [тут](https://a.yandex-team.ru/arc_vcs/maps/analytics#kubik-yql)


## Как внедрить тесты на YQL?

- Приводим query.sql к поддерживаемому виду (смотри [докуметацию](https://a.yandex-team.ru/arc_vcs/maps/analytics/tools/lama#make_sample) к `lama make_sample`)
- Вызываем команду `lama make_sample`. Если есть дата то `lama make_sample --date 2022-02-10`
    - Если все ок, то все семплы подготовятся
    - Если нужна дата, а вы ее не указали, то упадет с ошибкой и напишет об этом
    - Если не сможет понять какую-то переменную, то напишет об этом
- Вызываем команду `lama test -s` для сохранения выходного сэмпла
- Проверяем выходной семплы
    - Если пустой, то нужно изменить входные данные
- Запускаем `lama test` и убеждаемся что тесты проходят
- Пушим в репозиторий, проверяем как отработает `CI`
