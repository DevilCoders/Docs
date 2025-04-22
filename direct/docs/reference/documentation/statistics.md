# Статистика по документации
_Также эта страница известна как DIRECTKNOL-64._

Для просмотра отчётов в Метрике — нужно получить доступ по [инструкции](../../guide/analytics/how-to-get-access-to-metrika-counter.md).

{% note info %}

Если уже есть роль Метрики `yamanager` (Менеджер Яндекса) — отдельно доступ к счётчикам можно не запрашивать.

{% endnote %}

## Эта документация
На нашей документации установлен счётчик Метрики, его номер `67613293`.

Примеры отчётов:
- [сводка](https://metrika.yandex.ru/dashboard?period=month&id=67613293)
- [посещаемость](https://metrika.yandex.ru/stat/traffic?period=month&accuracy=1&id=67613293)
- [сводка по источникам](https://metrika.yandex.ru/stat/sources?period=month&accuracy=1&id=67613293)
- [популярные страницы](https://metrika.yandex.ru/stat/popular?period=month&accuracy=1&id=67613293&stateHash=5f89b25eaedca30041b9aa7f)


## Другие источники

### Вики
Исторически, документация накапливалась на вики.
Там тоже стоит счётчик метрики, его номер `153432`.

Пример отчёта: [посещаемость за квартал](https://metrika.yandex.ru/stat/titles?rows_limit=100&period=quarter&accuracy=1&id=153432&ulogin=ya-metrika&stateHash=5f89b4d49698fe001f715e82). Поскольку нас — мало, точность отчётов следует ставить 100%.

### Трекер
В трекере у нас экспериментальная база знаний в форме тикетов — очередь [DIRECTKNOL](https://st.yandex-team.ru/DIRECTKNOL).

Статистику по просмотрам в трекере тоже можно получить из Метрики. Счётчик трекера — `21059467`.

Пример отчёта: [популярность KNOL'ов за год](https://metrika.yandex.ru/stat/popular?group=day&period=year&accuracy=1&id=21059467&ulogin=ya-metrika&stateHash=5f89b5c15fbe5b003404122d).


### Документация до переезда из doc
#### Посещаемость
У старой версии документации (на doc.yandex-team.ru) был общий счетчик на всех потребителей, его номер `40617875`.  
Чтобы получить статистику только по нашей части, нужно накладывать фильтр `/direct-dev/*` на **URL** или аналогичный на параметр **Адрес страницы, ур. 2**.

Пример отчёта: [визиты за июнь—октябрь](https://metrika.yandex.ru/stat/traffic?period=2020-06-01%3A2020-10-01&accuracy=1&id=40617875&stateHash=5f898aaf51d2af0044cb192e).

#### Кнопки 👍 / 👎
На старой платформе в подвале каждой страницы есть голосовалка **Была ли статья полезна?**.
Статистику по голосам можно посмотреть в [Stat](https://stat.yandex-team.ru/Adhoc/Support/voters-feedback/?scale=m&max_distance=1&_incl_fields=dislikes&_incl_fields=likes&path__mode=subtree&path=%09R%09doc%09direct-dev%09&_period_distance=1).
