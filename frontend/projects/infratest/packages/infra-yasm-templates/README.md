# Шаблоны алертов и панелей yasm команды FEI

**Конфиги из этого пакета сейчас не деплоятся автоматически, вам нужно запускать синхронизацию нужных файлов вручную.**

Не пугайтесь: сейчас шаблоны по старинке написаны на jinja и деплоятся bash-скриптами.

Раньше они жили в [arcadia/serp/yasm-templates](https://a.yandex-team.ru/arc/trunk/arcadia/serp/yasm-templates/?rev=7484100), если вам нужно старый блейм посмотреть, приходите туда.

Сейчас эти шаблоны переехали в infratest, чтобы все мониторинги fei-сервисов лежали в одном репозитории, и вы могли легко за один коммит поправить и сервис, и его алерты, и панели с графичками.

Эта директория оформлена в виде пакета для того, чтобы избежать сборки всего репозитория при изменениях в мониторингах.

Новые алерты рекомендуем заводить на [monitorado](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/monitorado) в папке monitorado. Возможно в будущем мы и панели научимся делать на нём.

## Monitorado

[Документация monitorado](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/monitorado).

* исправляем или добавляем yml-файлы в `monitorado`
* для удаления алертов нужно положить в алертсет пустой объект и синхронизировать файл, лишь затем его можно удалить. Подробнее в доке monitorado
* `npm run monitorado monitorado/file.yml` синхронизирует алерты из file.yml
* `npm run monitorado:all` синхронизирует алерты из всех файлов в monitorado

Не забудьте указать в конфиге `settings_defaults.abc`, и сможете видеть все ваши алерты на панели [fei-alerts](https://yasm.yandex-team.ru/template/panel/fei-alerts/), добавив в контекст `abc=ваш-сервис`. Например: [abc=webhook-handler](https://yasm.yandex-team.ru/template/panel/fei-alerts/abc=webhook-handler/).

## Алерты

`cd alerts` – обязательно.
`TEMPLATE_ID` - имя папки, в которой лежит шаблон (template.jinja2). Можно указывать со слешом на конце.
* исправляем шаблон в <TEMPLATE_ID>/template.jinja2;
* смотрим дифф с текущим загруженным шаблонов при помощи `diff.sh <TEMPLATE_ID>`, убеждаемся, что есть только наши изменения;
* смотрим на результат рендера `render.sh <TEMPLATE_ID>` или просто проверяем `check.sh`; адекватную ошибку можно увидеть только при помощи `render.sh`;
* заливаем `upload.sh <TEMPLATE_ID>`, новый шаблон будет сразу применен;
* второй запрос скрипта может упасть, смотри [Отваливается заливание алертов infra-yasm-templates](https://st.yandex-team.ru/FEI-23914)
* не забываем закомитить и запушить изменения.

## Панели

`cd panels` – обязательно.
`TEMPLATE_ID` - имя папки, в которой лежит шаблон (template.jinja2). Можно указывать со слешом на конце.
* исправляем шаблон в <TEMPLATE_ID>/template.jinja2;
* заливаем `upload.sh <TEMPLATE_ID>`;
* не забываем закомитить и запушить изменения.

----

Related links:

- [YASM: Документация](https://wiki.yandex-team.ru/golovan/userdocs/)
- [YASM: Типы агрегации](https://wiki.yandex-team.ru/golovan/userdocs/aggregation-types/)
- [Monitorado](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/monitorado)
