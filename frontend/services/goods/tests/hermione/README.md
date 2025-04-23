# Гермиона-тесты

[Гермиона](https://github.com/gemini-testing/hermione) — это инструмент для интеграционного тестирования, использующий [webdriver](https://webdriver.io).

## Запуск

1. Посмотреть хелп
```
npx hermione --config .config/hermione/hermione.conf.js --help
```

2. Запустить тесты из указанного файла
```
# Запуск в терминале
npm run hermione -- [path/to/file.hermione.js]

# Запуск в GUI (можно будет посмотреть скриншоты и детали выполнения тестов)
npm run hermione:gui -- [path/to/file.hermione.js]
```

3. Часто востребованные опции
* `--play` или `--save` — первая опция устанавливает режим чтения дампов данных для вёрстки, а вторая режим записи
* `--retry 0` — количество попыток перезапуска упавших тестов до успешного выполнения
* `--grep '[description] [description] [it]'` — фильтр для запуска тестов по их названию
* `--browser linux-chrome` — браузеры, в которых нужно запускать тесты
* `--debug-enabled=true --debug-record-video 1` — записать видео выполнения теста (ссылка на видео будет выведена в терминале)
* `npm run hemrione:debug -- [path/to/file.hermione.js] -b [browser]` - запуск в vnc (дебаг с удаленным доступом)

4. Погонять тесты. Запустить каждый тест N раз (минимум 20), чтобы проверить стабильность
```
npm run hermione:gui -- [path/to/file.hermione.js] --test-repeater-enabled true --test-repeater-repeat 20
```

## Команды в тестах

- [стандартный список команд](https://webdriver.io/docs/api)
- [кастомный список команд монорепозитория](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/hermione-ya-commands?rev=r8680141#api-команд)
- [кастомный список команд для проверки счётчиков и метрик](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/hermione-get-counters#использование-4)
- [кастомный список команд нашего проекта](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/goods/tests/hermione/commands)

## Тесты на метрики

На сервере средствами [баобаба](https://wiki.yandex-team.ru/baobab/rfc/products/) мы отправляем дерево структуры страницы, которое записывается в blockstat-лог. В этом дереве у каждого узла есть уникальный идентификатор.
На клиенте так же средствами баобаба при возникновении интересующих нас событий мы отправляем счётчики, которые попадают в redir-лог. Все события привязаны к идентификаторам узлов исходного дерева, например, через поля `parent-id` или `id`. Далее на основании [записанных логов](https://wiki.yandex-team.ru/serp/counters/#kudapopadetsobrannajainformacija) формируется сессия и высчитываются метрики.

Для получения записанных в логи счётчиков и метрик мы используем команды из пакета [hermione-get-counters](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/hermione-get-counters#getallcounters-5). Он запрашивает по HTTP данные у [MetricsFetcher](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-metrics-fetcher#процесс-metricsfetcher), а тот в свою очередь у [calc_metrics_daemon](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/archon-calc-metrics-daemon) для [Archon](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon.html), который запускает [бинарник на C++](https://a.yandex-team.ru/arc/trunk/arcadia/quality/logs/calc_metrics/calc_metrics_daemon), строящий сессии и наконец считающий метрики.

Основные команды:
* [getAllCounters()](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/hermione-get-counters#getallcounters) — получить все записанные в лог счётчики в рамках текущего запуска теста
* [yaGetMetrics()](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/goods/tests/hermione/commands/yaGetMetrics.ts) — получить все посчитанные метрики
* [yaCheckMetrics()](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/goods/tests/hermione/commands/yaCheckMetrics.ts) — проверить соответствие рассчитанных метрик ожидаемым значениям

**Важно помнить, что все вышеприведённые команды для формирования результата используют логи, а в логи счётчики записываются с некоторой задержкой.** Если нужно для отладки просто получить список залогированных счётчиков (`getAllCounters()`) или метрик (`yaGetMetrics()`), то это нужно делать либо после вызова `yaCheckMetrics()`, либо после небольшой паузы.

Полный список наших метрик есть в [АБшнице](https://ab.yandex-team.ru/observation/459/calc/abt/20220409/20220409?metric_picker_key=m6df144429a76e09e8d2b5b2a70ae7c02#metrics=m16e5306c53562cbbcbd0514d58834184). Ключ метрики можно увидеть в попапе при нажатии на вопросик:
<img src="https://jing.yandex-team.ru/files/vladpotapov/Screen%20Shot%202022-04-13%20at%2011.43.50.png" width="500">

**Особенности:**
* Дозапросы следующих страниц выдачи в рамках одного поискового запроса не считаются новыми запросами в метриках.
* Изначально в тесте нужно открывать страницу так, чтобы не было редиректа. Иначе возникнет [проблема с отсутствием логов](https://st.yandex-team.ru/INFRADUTY-21695).
