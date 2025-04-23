## Тесты на статистику в API5

Чтобы запустить, нацелившись на бету, надо написать в `direct.test.run.properties`:

```ini
direct.stage=<номер беты>
direct.api.stage=<номер беты>
```

Если бета смотрит на `devtest` окружение, тесты могут падать из-за того,
что клиенты сидят в шардах 16+, или не хватает каких-то данных с прода.
За ТС окружением более пристально ухаживают, поэтому можно попробовать
переключить бету на `test`: `mk conf-test`.
Но необходимо дополнительно пропатчить бету так, чтобы она всегда строила
отчёты онлайн. Иначе офлайн отчёты будет генерить не бета а ТС.
Для этого нужно подправить две строки в `API::Service::Reports`:
```perl
#NO_PRODUCTION
# return $chosen_processing_mode if blessed($chosen_processing_mode) && $chosen_processing_mode->isa('Direct::Defect');

#NO_PRODUCTION
if (0 && $chosen_processing_mode == API::Service::Reports::ProcessingModeChooser::PROCESSING_MODE_OFFLINE ) {
```

Текстовые сообщения ошибок хранятся в монге

Чтобы получить их все, можно пройтись постранично:

```bash
curl -i 'https://direct-qa-restheart.qart.yandex-team.ru/BeanTemplates/TextResources?pagesize=1000&page=0'
```

Поискать одиночные сообщения по ключу можно в _Рукояточнике_: https://direct-handles.qart.yandex-team.ru/index.html

### Запуск back-to-back тестов локально

```ini
# Использовать эталонное хранилище
direct.api5.reports.backtoback.responses.in.indefinite.storage=true
# Если хочется проверить набор только из конкретного txt-файла, а не всё сразу
direct.api5.reports.backtoback.testfiles=CRITERIA_PERFORMANCE_REPORT
```

и запускать `CompareReportsTest`.

### Добавление новых сэмплов в back-to-back'и

1) Добавить сэмплы в txt-файлы
2) Протестировать получение отчётов по этим сэмплам
3) Добавить эталонные результаты в Elliptics

#### Добавить сэмплы в txt-файлы

Выполняется по аналогии с тем, как сейчас записано в файлах
`resources/backtoback.requests/report_types`. Нужно обратить внимание на то, что
`ReportName` указывать не нужно, а в `ACCOUNT_PERFORMANCE_REPORT.txt` нужно указать
логин клиента перед запросами, например:

 ```
 #login artboldyrev
 ```

#### Протестировать получение отчётов по этим сэмплам

 Чтобы протестировать работоспособность сэмплов, можно добавить пару строчек в property-файл:

 ```ini
direct.api5.reports.backtoback.result.directory=test001
direct.api5.reports.backtoback.testfiles=CUSTOM_REPORT
```

, закомментировать отправку в Elliptics в коде теста `GenerateReportsTest` и
запустить этот тест. А в логах проверить, правильные ли данные приходят. Чтобы не ждать
прогона по старым записям, можно их закомментировать через `//`.

#### Добавить эталонные результаты в Elliptics

Если все данные приходят ок, то можно их залить в Elliptics. Для этого нужен конфиг:

```ini
# Указываем конкретный файл, который будем заливать
direct.api5.reports.backtoback.testfiles=CRITERIA_PERFORMANCE_REPORT
# Использовать эталонное хранилище
direct.api5.reports.backtoback.responses.in.indefinite.storage=true
# Можно ли записывать в idefinite storage -- для первичной генерации эталонов
direct.api5.reports.backtoback.allowed.write.responses.in.indefinite.storage=true
```

Старые строчки в txt-файле комментируем, и запускаем тест `GenerateReportsTest`.

### Перезапуск в Aqua

https://wiki.yandex-team.ru/direct/api/duty/restart-reports-b2b/
