# Скрытие рекламы
## Зачем

Хотим предоставить пользователю инструмент для скрытия рекламных объявлений
Такое может понадобиться для:
1. Скрытия нерелевантной рекламы
2. Скрытия объявлений, которые не интересуют пользователя
3. Другие причины, в том числе не рекламные

## Что это даст нам

1. Больше иформации о пользователе
2. Возможность дальнейшего расширения рекомендательной системы, что приведет к улучшению нашей рекламной выдачи

Данные можно дальше отправить в рекомендер для улучшения рекламной выдачи пользователям с подобнымой релевантностью

## Как делаем

В eats-user-reactions:
1. Расширяем базку реакций на дополнительное поле reaction_type, тем самым позволяем заводить новые пользовательские реакции
2. Заводим конфиг, в котором указываем все допустимые типы реакций
3. Заводим новые ручки для добавления, удаления и поиска реакций

В каталоге:
1. Зпрашиваем реакции для итера
2. Избранное так и остается избранным, дизлайки прокидываются в advert_context
3. в advert_context происходит фильтрация плейсов до отправки их в аукцион
    а) на данный момент фильтруем по времени, если последний дизлайк входит во временной промежуток (время скрытия берем из экспа)
    б) дальше планируем сделать отдачу данных в мл
4. добавлем в конструирование карточки feature dislike в которой передаем список причин и их id, которые будем брать из экспа

## Базка

```sql
begin;
    alter table favourite_reactions rename to reactions;
    create view favourite_reactions as select * from reactions;
commit;

ALTER TABLE eats_user_reactions.reactions ADD COLUMN type TEXT NOT NULL default 'favourite';

CREATE TYPE eats_user_reactions.reaction_v1 AS
(
    id                UUID,
    type              TEXT,
    eater_id          TEXT,
    subject_namespace TEXT,
    subject_id        TEXT,
    created_at        TIMESTAMP WITH TIME ZONE,
    updated_at        TIMESTAMP WITH TIME ZONE
);
```

Такжже нужно конкурентно создать индекс:
```sql
CREATE UNIQUE INDEX CONCURRENTLY ux__fr__eater_id__type__subject_namespace__subject_id on eats_user_reactions.reactions (eater_id, type, subject_namespace, subject_id);
```

И дропнуть индекс ux__fr__eater_id__subject_namespace__subject_id

!!! Уже после выкатки кода  ```drop view favourite_reactions;```

## Ручки добавления и удаления реакции

```yaml
/eats/v1/eats-user-reactions/v1/reaction/add:
        post:
            x-taxi-middlewares:
                eats: v1
            summary: Добавить реакцию.
            description: |
                Добавляет реакцию итера на субъект
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            $ref: "#/components/schemas/AddReactionRequest"
            responses:
                "204":
                    description: OK
                "400":
                    description: Бренд не найден
                    content:
                        application/json:
                            schema:
                                $ref: "#/components/schemas/ErrorResponse"

/eats/v1/eats-user-reactions/v1/reaction/remove:
        post:
            x-taxi-middlewares:
                eats: v1
            summary: Удаляет реакцию.
            description: |
                Удаляет реакцию итера на субъект
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            $ref: "#/components/schemas/RemoveReactionRequest"
            responses:
                "204":
                    description: OK
                "400":
                    description: Бренд не найден
                    content:
                        application/json:
                            schema:
                                $ref: "#/components/schemas/ErrorResponse"

AddReactionRequest:
            type: object
            additionalProperties: false
              - subject
              - type
            properties:
                eater_id:
                    $ref: "#/components/schemas/EaterId"
                subject:
                    $ref: "#/components/schemas/SubjectFrontIdentity"
                type:
                    type: string
                    description: тип реакции

RemoveReactionRequest:
            type: object
            additionalProperties: false
              - subject
              - type
            properties:
                eater_id:
                    $ref: "#/components/schemas/EaterId"
                subject:
                    $ref: "#/components/schemas/SubjectFrontIdentity"
                type:
                    type: string
                    description: тип реакции

SubjectFrontNamespace:
            type: string
            description: |
                Неймспейс субъекта оценки. Присылаемый фронтом. Необходим для того, что бы различать сущности оперируемые фронтом и сущностями внутри сервиса:
                К примеру фронт не должен знать id брэнда и оперирует только слагом, а на бэке слаг должен преобразовываться в id
            enum:
              - brand
              - menu_item

SubjectFrontIdentity:
            type: object
            additionalProperties: false
            description: |
                Полный идентификатор субъекта оценки, включающий в себя неймспейс и id
            required:
              - namespace
              - id
            properties:
                    $ref: "#/components/schemas/SubjectFrontNamespace"
                id:
                    $ref: "#/components/schemas/SubjectId"

ErrorResponse:
            type: object
            additionalProperties: false
            description: |
                Ответ при возникшей ошибке
            required:
              - code
              - message
            properties:
                code:
                    type: string
                    description: |
                        Машинночитаемый код ошибки
                message:
                    type: string
                    example: "Something request parameter is invalid"
                    description: |
                        Человекочитаемое сообщение об ошибке

```
## Заводим новую ручку для каталога, для получения всех реакций

```yaml
    /eats-user-reactions/v1/reactions/find-by-eater:
        post:
            summary: Найти реакции Итера
            description: |
                Возвращает список итемов, на которые реагировал итер.
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            $ref: "#/components/schemas/FindReactionsByEaterRequest"
            responses:
                "200":
                    description: |
                        OK
                    content:
                        application/json:
                            schema:
                                $ref: "#/components/schemas/FindReactionsByEaterResponse"
                "400":
                    description: |
                        Ошибка запроса
                    content:
                        application/json:
                            schema:
                                $ref: "#/components/schemas/BaseErrorResponse"


        FindReactionsByEaterRequest:
            type: object
            additionalProperties: false
            required:
              - eater_id
            properties:
                eater_id:
                    $ref: "#/components/schemas/EaterId"
                reactions:
                    type: array
                    items:
                        $ref: "#/components/schemas/ReactionsRequest"

        ReactionsRequest:
            type: object
            additionalProperties: false
            required:
              - reaction_type
            properties:
                reaction_type:
                    type: array
                    items: 
                        type: string
                subject_namespaces:
                    type: array
                    items:
                        $ref: "#/components/schemas/SubjectNamespace"
                    description: |
                        Неймспейсы субъектов, в которых надо найти оценки. Если не указано, то найдёт во всех неймспейсах.
                pagination:
                    $ref: "#/components/schemas/RequestPagination"

        FindReactionsByEaterResponse:
            type: object
            additionalProperties: false
            required:
              - reactions
              - pagination
            properties:
                reactions:
                    type: array
                    items:
                        $ref: "#/components/schemas/FoundReaction"
                pagination:
                    $ref: "#/components/schemas/ResponsePagination"
            description: |
                Найденные субъекты, оцененные пользователем

        FoundReaction:
            type: object
            additionalProperties: false
            description: |
                Найденная реакция добавления в избранное
            required:
              - reaction_type
              - subject
              - created_at
            properties:
                reaction_type:
                    type: string
                subject:
                    $ref: "#/components/schemas/SubjectIdentity"
                created_at:
                    type: string
                    format: "date-time"
                    description: |
                        Дата и время когда Итер добавил в избранное субъект
```

