# Параметризация метарецептов

Дашборд можно выкатить, используя два типа рецептов.

Первый тип — рецепты, конструируемые с помощью няниного UI (выпадушка **Actions → Recipes**). Они хранятся в базе данных Няни, и, зайдя в (**Actions → Deployments**), можно выбрать один из таких рецептов, указать снапшоты сервисов и покатить. Процесс выкатки можно наблюдать в удобном специально для этого созданном UI.

Второй тип — рецепты, представляющие собой шаблонизированную с помощью Jinja2 YAML-разметку. В данный момент [они хранятся в SVN](https://arc.yandex-team.ru/wsvn/robots/trunk/genconf/recepies). Их также можно использовать для выкладки сервисов дашборда. Рассмотрим, как это делать на примере [демонстрационного дашборда](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/demo/).

## Применение из UI {#ui}

Зайдя в [Actions → YAML Recipes](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/demo/yaml-recipes/), мы увидим список _всех_ рецептов, хранящихся в SVN. Это временное решение; в будущем появится возможность задать список рецептов в настройках дашборда.

Кликнем на [deploy_demo_dashboard.yaml](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/demo/yaml-recipes/deploy_demo_dashboard.yaml/). Этот рецепт написан специально для демонстрационного дашборда.

Контекст рецептов, использующихся для выкладки дашборда, должен содержать переменные `services` и `service_ids`, удовлетворяющие следующей JSON-схеме:

```json
{
    "type": "object",
    "required": ["services", "service_ids"],
    "properties": {
        "services": {
            "type": "object",
            "properties": {
                <service_id_*>: {
                    "type": "object",                
                    "required": ["runtime_attrs_id"],
                    "properties": {
                        "runtime_attrs_id": {
                            "type": "string"
                        },
                        "labels": {
                            "type": "object",
                            "patternProperties": {
                                 ".*": {"type": "string"}
                             }
                        }
                    }
                }
            }
        },
        "service_ids": {
            "type": "array",
            "items": {
                "type": "string"
            }
        }
    }
}
```

Как видно из схемы, переменная `services` должна содержать словарь, ключами которого являются идентификаторы сервисов, а значениями — словари вида `{"runtime_attrs_id": "..."}`. Переменная `service_ids` должна содержать список ключей `services` — такая «избыточность» делает возможным писать рецепты, совместимые с jinja2schema.

Вернёмся к deploy_demo_dashboard.yaml.
Сначала активируются `demo_service_1` и `demo_service_2`, затем для каждого из остальных сервисов дашборда происходит сначала prepare, а затем activate.

Нажав кпопку Apply на [странице рецепта](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/demo/yaml-recipes/deploy_demo_dashboard.yaml/), мы попадаем на [страницу с формой для контекста](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/demo/yaml-recipes/deploy_demo_dashboard.yaml/apply/), содержащую поля для заполнения «стандартных» `services` и `service_ids`, а также всех остальных переменных рецепта.

Нажав кнопку Apply ещё раз, мы попадаем на страницу порождённой рецептом таскгруппы.

## Применение через API alemate {#api-alermate}

Применить рецепт можно через [стандартную ручку apply](../alemate/alemate-api.md).

Получить переменные `services` и `service_id`, содержащие данные о всех сервисах дашборда и их текущих runtime-снапшотах, можно с помощью ручки
`/v2/services_dashboards/catalog/<dashboard_id>/state/`. Например:

```
GET /v2/services_dashboards/catalog/demo/state/ HTTP/1.1
Accept: application/json
Accept-Encoding: gzip, deflate
Content-Type: application/json; charset=utf-8
Host: nanny.yandex-team.ru

HTTP/1.1 200 OK
Content-Length: 618
Content-Type: application/json
X-Backend-Host: vsearch8-05.search.yandex.net
X-Backend-Version: 0.7.848

{
    "service_ids": [
        "demo_service_1",
        "demo_service_2",
        "demo_service_3",
        "demo_service_4",
        "demo_service_5",
        "demo_service_6"
    ],
    "services": {
        "demo_service_1": {
            "runtime_attrs_id": "19796f14f7b3bac228381724edbbf22b4e4dd645"
        },
        "demo_service_2": {
            "runtime_attrs_id": "adb4951845595efc459a9d028dc9ff34fffb8476"
        },
        "demo_service_3": {
            "runtime_attrs_id": "016124af0395c8b0cc5ef8652b5d47f5db44f618"
        },
        "demo_service_4": {
            "runtime_attrs_id": "62cf3a4ab7ed55793fb3fccb20df7e902caa160d"
        },
        "demo_service_5": {
            "runtime_attrs_id": "3daff107365c0d11fd32647405b2c3ed712d7e6a"
        },
        "demo_service_6": {
            "runtime_attrs_id": "5d65818a63c5bb344db40b403556bd2731d5f6a4"
        }
    }
}
```

## Применение через API Nanny {#api-nanny}

Задеплоить метарецепт можно с помощью POST-запроса на `https://nanny.yandex-team.ru/v2/services_dashboards/catalog/<dashboard_id>/deployments/`.

JSON запроса должен содержать `{"type": "yaml", "yaml_recipe_id": "<name>.yaml", "yaml_recipe_context": {...}}`, где `yaml_recipe_context` согласно соглашению должен содержать поля `service_ids` и `services` (см. предыдущий раздел), необходимые для рендеринга рецепта.

При успешном создании деплоймента POST-запрос вернёт его данные с кодом ответа `201 CREATED`.

Пример запроса: [https://paste.yandex-team.ru/574458](https://paste.yandex-team.ru/574458)

