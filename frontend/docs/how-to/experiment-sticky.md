# Генерация эксперимента для залипания в шаблоны беты на продакшене

## Пререквизиты

Граф вашего сервиса в AppHost должен поддерживать передачу флагов.

Например, для работы `srcrwr` нужно [следовать рекомендации](https://st.yandex-team.ru/FEI-14707#5d4d2a22a2b79e001dedcf6d).

## Инструкция

Задача **Создание эксперимента на 0% для залипания**.
Задача создаёт выборку (testid) для всех затронутых сервисов, у которых указан конфиг.
Задача выполняется после задачи **Deploy**, так как информация для плейсхолдеров может быть доступна только после деплоя бет.

Требуется добавить в `devDependencies` пакет `@yandex-int/si.ci.testid-cli` и создать конфиг `services/{ID_сервиса}/.config/pr-experiment/config.json` со следующим содержимым:
```json
{
    "prDescription": {
        "title": "{название_сервиса}",
        "redirectTo": "{ссылка_куда_будет_произведён_редирект_после_перехода_по_ссылке_на_залипание}",
        "testingUrl": "{ссылка_куда_будет_подставлен_эксперимент_в_query_параметры}"
    },
    "template": {
        "title": "{{title}}",
        "type": "ABT",
        "queue_id": 1,
        "params": [
            {
                "HANDLER": "{хэндлер_сервиса}",
                "CONTEXT": {
                    "MAIN": {
                        "REPORT": {
                            "srcrwr": {
                                "TEMPLATES": "{{fqdn_list_srcrwr}}"
                            }
                        }
                    }
                },
                "TESTID": [
                    "__PLACE_TEST_ID_HERE__"
                ]
            }
        ],
        "replace_token": "__PLACE_TEST_ID_HERE__"
    },
    "appendTestids": "массив_служебных_выборок_который_будет_подмешиваться_в_ссылку_на_залипание",
}
```

В поле `template` содержится шаблон для конфигурации testid в AB. Подробнее см. в [документации](https://wiki.yandex-team.ru/serp/experiments/20/adminka/api/#/api/testid/).

Для шаблона доступны следующие переменные:

- **title** — название беты (например, `renderer-granny-pull-6673`)
- **fqdn** — один хост (слот) беты с портом (например, `renderer-betas-4-1.iva.yp-c.yandex.net:4010`)
- **timeout** — таймаут, берётся из конфига для беты rr (например, `5000`)
- **fqdn_list_srcrwr** - готовый список из всех слотов беты с установленными таймаутами в формате srcrwr, можно использовать вместо `{{fqdn}}:{{timeout}}`. Пример - `renderer-betas-4-1.iva.yp-c.yandex.net:4010:5000;renderer-betas-replica-7-1.sas.yp-c.yandex.net:4230:5000`

Из-за того, что для создания беты нужна информация о бете, задача сама обновляет свою секцию (`Тестирование в продакшене`) в описании пулл-реквеста.
Поля `prDescription.title` и `prDescription.redirectTo` нужны для подстановки ссылки на залипание с QR-кодом и ссылки на конфигурацию эксперимента в AB в описание пулл-реквеста.
Поле `prDescription.testingUrl` должно содержать ссылку, в query-параметры которой будут подставлен `test-id={id_созданного_эксперимента}`. Например, это может быть ссылка на hamster.

## FAQ

### Доступность статики из внешней сети

Если планируется использовать эксперименты и ссылки на залипание для раздачи заданий асессорами/толокерам, то проверьте, что ваша статика доступна из внешней сети.

Например, если вы пользуетесь `static-uploader`, то обратите внимание на опцию `usePublicUrl`.
