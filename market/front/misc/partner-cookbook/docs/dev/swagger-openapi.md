# Бекенды просят описать/дополнить ручку в Swagger'е или OpenAPI, что дальше?

**Содержание**

-   [Разница между Swagger и OpenAPI](#разница-между-swagger-и-openapi)
-   [Знакомство с Swagger](#знакомство-с-swagger)
-   [Знакомство с OpenAPI](#знакомство-с-openapi)
-   [Каким должно быть хорошее API](#каким-должно-быть-хорошее-api)
-   [Пример плохо описанной ручки](#пример-плохо-описанной-ручки-)
-   [Пример хорошо описанной ручки](#пример-хорошо-описанной-ручки-)
-   [Советы](#советы)

## Разница между Swagger и OpenAPI

Обе являются схемами для описания API бекендов, и могут быть взаимозаменяемыми, но это заводит людей в заблуждение. Исторически сложилось что был один формат для описания схем API и назывался он Swagger. При обновлении мажорной версии с 2 на 3 был переименован из Swagger в OpenAPI.

Другими словами:

-   Swagger v2 и OpenAPI v2 одно и тоже
-   Swagger v3 не существует

Исторически сложилось что говоря:

-   **Swagger** имеют ввиду **v2** схемы
-   **OpenAPI** имеют ввиду **v3** схемы

Усиленно советую придерживаться такого наименования.

Так же обе схемы можно обычно описывают с помощью `json` или `yaml`.

Яндекс.Маркет движется в сторону OpenAPI со Swagger. Если перед вами стоит выбор между 2умя схемами - выбирайте OpenAPI.

## Знакомство с Swagger

Для описания сваггер схемы для бекенда не обязательно знать наизусть все сущности из swagger, но иметь представление об общей форме SwaggerObject стоит. Можно ознакомиться с официальной [документацией](https://swagger.io/specification/v2/).

Из особо важного стоит иметь представление как выглядят:

-   [ReferenceObject](https://swagger.io/specification/v2/#reference-object)
-   [PathItemObject](https://swagger.io/specification/v2/#path-item-object)
-   [OperationObject](https://swagger.io/specification/v2/#operation-object)
-   [ResponseObject](https://swagger.io/specification/v2/#response-object)
-   [ParameterObject](https://swagger.io/specification/v2/#parameter-object)
-   [SchemaObject](https://swagger.io/specification/v2/#schema-object) и обратить внимание на:
    -   **anyOf** как аналог `union type` из flow или typescript
    -   **required** для объявления обязательных полей, по умолчанию все поля опциональные

## Знакомство с OpenAPI

Если вы уже знакомы со Swagger то OpenAPI покажется очень знакомой, из особо заметных изменений `ParameterObject` был разбит на 2 сущности [`ParameterObject`](https://swagger.io/specification/#parameter-object) (для query, header, path и cookie) и [`RequestBodyObject`](https://swagger.io/specification/#request-body-object) (для тела запроса), а так же в [`SchemaObject`](https://swagger.io/specification/#schema-object) теперь помимо `allOf` теперь есть `oneOf` и `anyOf`.

Посмотреть [документацию](https://swagger.io/specification/) схемы можно на оф. сайте.

## Каким должно быть хорошее API

-   **Легким для понимания и работы**: Хорошо спроектированное API должно быть простым для освоения и легко запоминаемым для тех, кто с ним часто работает.
-   **Сложным для неправильного использования**: Работа с хорошо спроектированным API должна быть простой и прямолинейной, как итог написание плохого кода должно даваться с трудом.
-   **Завершенным и лаконичным**: Обычно API вырастает со временем, нужно прикладывать усилия для того чтобы содержать его совместимым и отмечать не поддерживаемые части приложения как `deprecated`.

## Пример плохо описанной ручки ❌

На примере Swagger

```json
{
    "swagger": "2.0",
    "info": {
        "title": "sample",
        "version": "1.0"
    },
    "paths": {
        "/entities/": {
            "get": {
                "consumes": ["application/json"],
                "produces": ["application/json"],
                "responses": {
                    "200": {
                        "description": "meh",
                        "schema": {
                            "type": "array",
                            "items": {
                                "$ref": "#/definitions/ApiResponse"
                            }
                        }
                    }
                }
            }
        }
    },
    "tags": [],
    "definitions": {
        "ApiResponse": {
            "type": "object",
            "required": ["status"],
            "properties": {
                "id": {
                    "type": "string"
                },
                "condition": {
                    "type": "string",
                    "enum": ["good", "bad", "alright"]
                },
                "Meta": {
                    "type": "boolean"
                }
            }
        }
    }
}
```

Что плохого в этом описании

-   ❌ Описан ответ только для положительного результата(200)
-   ❌ Отсутствует описание(`description`) у метода ручки
-   ❌ Отсутствует описание(`description`) у ответа ручки
-   ❌ URL заканчивается на `/`
-   ❌ Разный кейсинг у свойств объекта `ApiResponse`
-   ❌ Не задан тег для ручки
-   ❌ Не указано что вернется, если ручку вызвать неверно

## Пример хорошо описанной ручки ✅

На примере Swagger. Помимо ручки для получения сущностей, мы так же добавили ручки для обновления/добавления/удаления сущностей для наглядности как такой подход может скейлится.

На этом примере исправлены недостатки из плохого примера выше, а также:

-   Подняли `consumes` и `produces` на верхний уровень что бы не повторять во всех ручках одно и тоже.
-   Вынесли переиспользуемые сущности в отдельные `definition`'ы.
-   Добавили описания к полям, ручкам и параметрам(они отображаются в swagger UI, а так же инлайнятся как комментарии при генерации клиента для фронтов).
-   Вынести `enum` в отдельный `definition`, даже если он сейчас больше нигде не используется, он всегда один из первых кандидатов на переиспользование при заведении новых ручек для работы с сущностями, так же для фронтов генерятся типы по `definition`'ам.

```json
{
    "swagger": "2.0",
    "info": {
        "title": "Example schema",
        "version": "1.0"
    },
    "consumes": ["application/json"],
    "produces": ["application/json"],
    "paths": {
        "/entities": {
            "get": {
                "summary": "Ручка для получения состояния СУЩНОСТЕЙ",
                "tags": ["entity-tag"],
                "responses": {
                    "200": {
                        "description": "Успешно нашли кол-во сущностей",
                        "schema": {
                            "type": "array",
                            "items": {
                                "$ref": "#/definitions/Entity"
                            }
                        }
                    },
                    "404": {
                        "description": "invalid parameters",
                        "schema": {
                            "$ref": "#/definitions/InvalidParameterError"
                        }
                    }
                }
            },
            "put": {
                "summary": "Ручка для обновления состояния СУЩНОСТЕЙ",
                "tags": ["entity-tag"],
                "parameters": [
                    {
                        "in": "body",
                        "name": "entities",
                        "description": "Cписок сущностей для обновления",
                        "schema": {
                            "type": "array",
                            "items": {
                                "$ref": "#/definitions/EntityShape"
                            }
                        }
                    }
                ],
                "responses": {
                    "200": {
                        "description": "Успешно нашли кол-во сущностей",
                        "schema": {
                            "type": "array",
                            "items": {
                                "$ref": "#/definitions/Entity"
                            }
                        }
                    },
                    "400": {
                        "description": "invalid parameters",
                        "schema": {
                            "$ref": "#/definitions/InvalidParameterError"
                        }
                    }
                }
            },
            "post": {
                "summary": "Ручка для добавления новых СУЩНОСТЕЙ",
                "tags": ["entity-tag"],
                "parameters": [
                    {
                        "in": "body",
                        "name": "entities",
                        "description": "Cписок сущностей для добавления",
                        "schema": {
                            "type": "array",
                            "items": {
                                "$ref": "#/definitions/Entity"
                            }
                        }
                    }
                ],
                "responses": {
                    "200": {
                        "description": "Успешно нашли кол-во сущностей",
                        "schema": {
                            "type": "array",
                            "items": {
                                "$ref": "#/definitions/Entity"
                            }
                        }
                    },
                    "400": {
                        "description": "invalid parameters",
                        "schema": {
                            "$ref": "#/definitions/InvalidParameterError"
                        }
                    }
                }
            },
            "delete": {
                "summary": "Ручка для удаления СУЩНОСТЕЙ",
                "tags": ["entity-tag"],
                "parameters": [
                    {
                        "in": "body",
                        "name": "entities",
                        "description": "Cписок идентификаторов сущностей для удаления",
                        "schema": {
                            "type": "array",
                            "items": {
                                "$ref": "#/definitions/EntityId"
                            }
                        }
                    }
                ],
                "responses": {
                    "200": {
                        "description": "OK"
                    },
                    "400": {
                        "description": "invalid parameters",
                        "schema": {
                            "$ref": "#/definitions/InvalidParameterError"
                        }
                    }
                }
            }
        }
    },
    "tags": [
        {
            "name": "entity-tag",
            "description": "Все операции связанные с работой с СУЩНОСТЯМИ"
        }
    ],
    "definitions": {
        "Entity": {
            "type": "object",
            "required": ["id", "status"],
            "properties": {
                "id": {
                    "$ref": "#/definitions/EntityId"
                },
                "condition": {
                    "$ref": "#/definitions/EntityCondition"
                },
                "meta": {
                    "type": "string"
                }
            }
        },
        "EntityShape": {
            "type": "object",
            "required": ["id"],
            "properties": {
                "id": {
                    "$ref": "#/definitions/EntityId"
                },
                "status": {
                    "$ref": "#/definitions/EntityCondition"
                },
                "meta": {
                    "type": "string"
                }
            }
        },
        "EntityId": {
            "type": "string"
        },
        "EntityCondition": {
            "type": "string",
            "enum": ["good", "bad", "alright"],
            "description": "Состояние сущности"
        },
        "InvalidParameterError": {
            "type": "object",
            "required": ["error"],
            "properties": {
                "error": {
                    "type": "string",
                    "enum": ["INVALID-PARAM"]
                },
                "meta": {
                    "type": "string"
                }
            }
        }
    }
}
```

## Советы

1. Иметь хорошее представление о форме Swagger и OpenAPI
2. Все сущности описывать в `#/components/schemas` (OpenAPI) или `#/definitinos` (Swagger), поскольку они все равно буду переиспользованы в дальнейшем.
3. Не увлекаться anyOf и oneOf они работают только на уровне request response. Генератор бекендного кода с ними пока еще не хорошо дружит.
4. Использовать [Swagger Editor](https://editor.swagger.io/) для **написания** схем(для генерации используются другие инструменты). Он подсказывает если схема не совместима с спецификацией, а так же покажет первью Swagger UI. Пример ниже

 <p align="center"><img alt="swagger editor screenshot" src="https://media.github.yandex-team.ru/user/5825/files/78013f80-bd81-11ea-812f-ad0cd7b544d4" width="85%" alt="npm command"></p>

5. Использовать [Swaggerlint Playground](https://swaggerlint-playground.now.sh/) для проверки что написанная схема соответствует маркетным договоренностям.

 <p align="center"><img src="https://media.github.yandex-team.ru/user/5825/files/ffe94880-bd85-11ea-8fce-9490b549d4f2" width="85%" alt="swaggerlint playground screenshot"></p>
