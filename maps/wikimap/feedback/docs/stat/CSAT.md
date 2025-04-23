# Customer Satisfaction

В рассылках об изменении статуса фидбэка (публикация изменений, отклонение и т. д.) пользователь имеет возможность оставить отзыв о взаимодействии с системой фидбэка -- оценку, комментарий, что (не) понравилось из закрытого списка. Эту информацию хотим отображать на дашбордах.

## Пайплайн обработки данных

### Дополнительная информация о письмах пользователям

Датасет дашборда Рассылятора: [all_logs_sent_dttm](https://datalens.yandex-team.ru/datasets/g1qyuj88lvbad-all-logs-sent-dttm)

Оттуда нам нужно только число доставленных писем из рассылок, в которых есть данная CSAT-форма.

Для справки, общий дашборд Рассылятора на основе этого датасета: https://datalens.yandex-team.ru/7nwf8knshtrk4-novyy-dashbord-rassylyatora. Инфо на [вики](https://wiki.yandex-team.ru/sender/emailstatistics/).

### Исходные данные оценок

YT-таблица с оценками: [hahn.//home/forms/answers/forms_ext/production/10029783/data](https://yt.yandex-team.ru/hahn/navigation?path=//home/forms/answers/forms_ext/production/10029783/data)

### Регулярный процесс преобразования сырых оценок ([описание далее](#preobrazovanie-syryh-ocenok))

YQL-скрипт (здесь): [parse_form_answers.yql](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/stat/feedback_csat/parse_form_answers.yql)

Nirvana workflow: [CSAT Parse form answers](https://nirvana.yandex-team.ru/flow/705ae688-080a-432a-823c-8991d094997e)

Реакция: [CSAT parse form answers auto](https://reactor.yandex-team.ru/browse?selected=9730390)

YT таблица-результат: [hahn.//home/maps/core/nmaps/analytics/feedback/csat/data_parsed](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/feedback/csat/data_parsed)

Датасет на основе результата: [csat_data_parsed_dataset](https://datalens.yandex-team.ru/datasets/69rnqjgiiwcmz-csat-data-parsed-dataset)

## Визуализация

Страницы на дашбордах:
* на старом: [CSAT](https://datalens.yandex-team.ru/71ela79srnhq3-fidbek-iz-form?tab=Okv)
* на новом: [CSAT](https://datalens.yandex-team.ru/ywy6v7i0ywjyr-feedback-metrics?tab=Okv)

## Преобразование сырых оценок

[1]: В исходной таблице с оценками содержится json ответа пользователя для каждого заполнения формы из письма. В столбцах самой таблицы содержатся метаданные об ответе. В json-столбце answer содержится:
* оценка от 1 до 5 (`data/rating`);
* набор лайков (при положительной оценке, `data/like`);
* набор дизлайков (при отрицательной оценке, `data/dislike`);
* комментарий (`data/comment`);
* автоматически заполняемое поле `email_template_id` для связи ответа с рассылкой (`data/email_template_id`).

Используемые средства визуализации не могут работать с json напрямую, поэтому требуется операция, которая переложит данные из json в отдельные столбцы. Для этого налажен регулярный процесс на основе YQL-скрипта.

В результате получаем YT-таблицу и ChYT-датасет на её основе. Такой датасет уже напрямую используется графиками с дашбордов.

## Поддержка набора рассылок

Известные рассылки с формой оценки:
* [Заявка создана](https://sender.yandex-team.ru/maps/campaign/239945)
* [Заявка обработана](https://sender.yandex-team.ru/maps/campaign/237720)
* [Заявка не принята](https://sender.yandex-team.ru/maps/campaign/238874)
* [Не соответствует правилам](https://sender.yandex-team.ru/maps/campaign/508867)

При изменении набора рассылок с формой (на примере добавления новой) требуется обновить списки в артефактах визуализации.
* Селектор рассылки с дашбордов: [campaign_id_selector](https://datalens.yandex-team.ru/editor/25o2lzg04a62v-campaign-id-selector). На вкладке `Controls` требуется добавить `campaign_id` и описание рассылки.
* График доставленных писем: [csat_delivery_day](https://datalens.yandex-team.ru/wizard/aevi5bxhx0zi3-csat-delivery-day). Нужно обновить фильтр `campaign_id` -- добавить новую рассылку в список.

### Препятствия для автоматизации

* Обновляется редко
* Автоматические селекторы не дают задавать отдельное описание
* Нет средства автоматизации обращения к стороннему датасету

## Дополнительная информация

Письма в рассылки отправляются автоматизировано через sender-API в [feedback/api/src/notifications](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/notifications) ([место вызова клиента](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/notifications/lib/send_notifications.cpp?rev=r8272388#L137)).
