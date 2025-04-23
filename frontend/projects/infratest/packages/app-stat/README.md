# AppStat 

Библиотека для сбора статистики приложений в отчёты на stat.yandex-team.ru. 
Подготовлены графики с обобщённым кодом для отображения основной информации, что делает создание своего дэшборда очень простым. 

Ключевые термины отчётов Statface:
1. Скейл(scale) - размер временного интервала, на которые разбиты данные. В библиотеке используется секундный(минимальный) скейл. 
2. Измерение (dimension) - поле, определяющее структуру куба. Группирует показатели набора данных.
Обязательным измерением в отчетах является измерение времени. 
Оно описывается в конфигурации с именем fielddate и типом date. 
Dimensions нельзя изменять(удалять, добавлять) после создания отчёта. 
3. Показатель (measure) - поле, содержащее значение ячейки куба. Каждому уникальному сочетанию измерений соответствует только одно значение показателя.
Нельзя менять тип measure, даже если удалить его и создать заново с новым типом.

Подробнее об отчётах в [документации](https://doc.yandex-team.ru/stat/report-overview/concepts/about.html).

## API

### constructor(reportId, version)

##### reportId  
Type: `string`

ID отчёта. Например, для отчёта 'https://stat.yandex-team.ru/Yandex/Infra/Castle/CastleUsageStatistics' ID будет '/Yandex/Infra/Castle/CastleUsageStatistics'.

##### version  
Type: `string`

Версия утилиты (или библиотеки) из package.json, для которой собираем статистику.

### emit(eventName, data)
Отправить запись в отчёт. Возвращает Promise. 

##### eventName
Type: `string`

Название события. Основной параметр, по которому будем делать отчёты.

##### data
Type: `string`

Default: `{}`

Дополнительные поля для записи в отчёт. Для каждого поля этого объекта должно быть создано поле в Measures отчёта.

Statface принимает строки и числа. Поэтому значения других типов конвертируем:
boolean приводим к числу, объекты преобразуем с JSON.stringify, остальное приводим к строке. Это нужно, чтобы сбор
статистики никогда не падал. Пользователь скорее всего ошибку проигнорирует.

## Переменные окружения

#### APP_STAT_DONT_TRACK
Отправка статистики отключается при наличии этой переменной окружения.
Это может быть полезно для задач в Sandbox.

#### STATFACE_HOST 
Изменить хост для отправки статистики. По умолчанию - 'https://upload.stat.yandex-team.ru'.

## Использование

1. Создайте отчёт на stat.yandex-team.ru.
1. В отчёте создайте обязательные поля в Dimensions (они будут передаваться всегда):
    * fielddate - date, дата-время регистрируемого события. Appstat формирует это поле с точностью до секунды.  
    * event - строка, регистрируемое событие,
    * username - строка, имя пользователя.
1. В отчёте создайте обязательные поля в Measures (они будут передаваться всегда):
    * nodejs - строка, версия node.js,
    * version - строка, версия пакета, для которого собираем статистику,
    * platform - строка, платформа, на которой бежит приложение.
1. В отчёте создайте дополнительные поля в Dimensions и Measures, если необходимо. Сохраните конфигурацию отчёта.
1. Настройте права на запись в отчёт - нужно разрешить запись всем. 
1. Добавьте в код приложения вызов библиотеки. Например, так:
    ```js
    const AppStat = require('@yandex-int/app-stat');
    const pkg = require('<путь до package.json>');
    
    const appStat = new AppStat('<ID отчёта>', pkg.version);
    
    appStat.emit('awesomeExampleEvent');
    
    //...
    
    appStat.emit('bestExampleEvent', {
        duration: 105,
        enableUsefulOption: true
    });
    ```

1. Создайте дэшборд на stat.yandex-team.ru, настройте права на просмотр.
1. Добавьте на дэшборд виджет "график". В простых случаях подойдут два графика:
    * https://charts.yandex-team.ru/editor/serp.infratest/app_stat_usage. График отображает количество уникальных пользователей и 
    количество событий (соответствует полю 'event' отчета). Принимает параметры:
        * report - ID отчёта, по которому строить график.  Слэши нужно заменять на "%2F";
        * scale - масштаб графика. Принимает 'day' (по дням) и 'month' (по месяцам);
        * date_min - минимальная дата для отображения в графике. Формат "YYYY-MM-DD";
        * date_max - максимальная дата для отображения в графике. Формат "YYYY-MM-DD".
    * https://charts.yandex-team.ru/editor/serp.infratest/app_stat_usage_by_users. График отображает количество пользователей
     для каждого уникального значения в столбце(поле) отчёта. Принимает параметры:
        * fieldName - поле отчета, по которому будет строится график;
        * report, scale, date_min, date_max - аналогично app_stat_usage.
    
    Параметры могут добавляться, проверить актуальность можно в [коде графиков](https://github.yandex-team.ru/search-interfaces/ci/tree/master/charts/SERP.infratest). 
    
    Примеры URL для виджетов:
    * https://charts.yandex-team.ru/editor/serp.infratest/app_stat_usage_by_users?report=%2FYandex%2FInfra%2FCastle%2FCastleUsageStatistics&fieldName=version
    * https://charts.yandex-team.ru/editor/serp.infratest/app_stat_usage?report=%2FYandex%2FInfra%2FCastle%2FCastleUsageStatistics

1. В меню дэшборда нужно его "сделать общим". Автоматически будет заведена задача в Startrack.


#### Изменить список dimensions или тип measure в отчёте
Это необходимо делать через пересоздание отчёта: 
1. Создайте новый отчёт.
1. Перелейте данные из старого отчёта в новый:
    1. Установите python-statface-client: 
       ```
       pip install -i https://pypi.yandex-team.ru/simple/ python-statface-client --user
       ```
    1. Получите OAuth токен по [инструкции](https://wiki.yandex-team.ru/statbox/statface/externalreports/#autentifikacija).
    1. Доработайте под ваши нужды следующий python код и выполните:
       ```python
       #!/usr/bin/env python
       # coding: utf-8
       
       import statface_client
       
       # прежде чем работать с отчётами в production, потестируйте код на отчётах в бета - stat-beta.yandex-team.ru
       # client = statface_client.StatfaceClient(host=statface_client.STATFACE_BETA, oauth_token=<токен>)
       client = statface_client.StatfaceClient(host=statface_client.STATFACE_PRODUCTION, oauth_token=<токен>)
       
       report_from = client_prod.get_old_report('<ID отчёта, из которого будем брать данные>')
       report_to = client_beta.get_old_report('<ID отчёта, в который будем загружать данные>')
       
       # возьмём данные за год
       period_distance=60*60*24*365
       
       data = report_from.download_data(scale=u's', _period_distance=period_distance)
       
       new_data = []
       for record in data:
           new_record = dict(record)
       
           # удалить поле
           new_record.pop('property_for_remove', None)
       
           # добавить/изменить поле
           new_record['property_for_change'] = 0
       
           new_data.append(new_record)
       
       report_to.upload_data(scale=u's', data=new_data)
       ```
       Другие примеры работы с python-statface-client можно посмотреть [тут](https://a.yandex-team.ru/arc/trunk/arcadia/statbox/python-statface-client/examples/basic_usage.py).

1. Переместите старый и новый отчеты - в настроках отчёта выбрать "Report control" -> "Move the report".






