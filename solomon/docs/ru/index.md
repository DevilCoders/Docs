# Оглавление

**Solomon** (Yandex Monitoring) — распределенная и высокодоступная система количественного мониторинга: сбор, агрегация, хранение и визуализация метрик (временных рядов) с возможностью алертинга через Email, SMS, Телефонный звонок, Telegram, Yandex.Messenger, Webhook и Juggler.

## Основные разделы документации

### [Что такое Solomon](overview/about.md) {#about}

В разделе содержится общее описание системы, помогающие получить представление об основных возможностях Solomon, а также о сценариях для которых она подходит или не подходит.

### Начало работы {#quickstart}

В разделе приведена пошаговая инструкция, помогающая быстро познакомиться с системой Solomon, создать свой проект и настроить передачу метрик.

- [Инструкция для большого Яндекса](howtostart/quickstart-yateam.md)
- [Инструкция для Яндекс.Облака](howtostart/quickstart-cloud.md)

### [Глоссарий](concepts/glossary.md) {#glossary}

Раздел содержит термины и определения, использующиеся в документации. В разделе можно узнать о том, что такое [алерт](concepts/glossary.md#alert), [гистограмма](concepts/glossary.md#histogram), [метрика](concepts/glossary.md#metric), [шард](concepts/glossary.md#shard) и другое.

### [Модель данных](concepts/data-model.md) {#data-model}

В разделе описана модель данных, использующаяся в Solomon: чем являются [метрики и метки](concepts/data-model.md#definitions), а также описаны [типы метрик](concepts/data-model.md#metric-kinds).

### [Язык запросов](concepts/querying.md) {#querying}

Данный раздел является справочником по языку запросов Solomon, который используется для преобразования и агрегации метрик при построении графиков и вычислении [алертов](#alerting).

### [Алертинг](concepts/alerting/index.md) {#alerting}

Раздел содержит описание механизма алертинга, позволяющего получать уведомления об изменениях в в метриках, собирающихся в Solomon.


## Полезные ссылки {#links}
* [Веб-интерфейс](http://solomon.yandex-team.ru/)
* [Клуб в Этушке](https://clubs.at.yandex-team.ru/solomon/)
* [Рассылка solomon@](https://ml.yandex-team.ru/lists/solomon/)
* [Телеграм-чат](https://t.me/joinchat/AWy4SEK1sYQoq4Ign2oINQ)
* [Как сообщить о проблеме](problems/howtoreport.md)

{% if version > '0' %}
Собрана версия: {{version}}
{% endif %}

<!-- Тестовая правка, чтобы проверить новый релизный процесс -->
