## Задача

Необходимо добавить возможность задавать вопросы о качестве поездки.
На этапе MVP вопрос должен конфигурироваться экспериментом. 

Сейчас функциональность уже реализована, но:
- поддержан всего один вопрос;
- метод получения ответов был сделан как временное решение и нуждается в изменении.

## Дизайн

Нет изменений, если сравнивать с текущей реализацией.

Пример вопроса:

![](img/ride_survey_question.jpg)

Пример экрана:

![](img/ride_survey.jpg)

## Про текущую реализацию

Сейчас функциональность реализована без бэкенда. 
Вопрос приходит из эксперимента `check_car_number`.

Сейчас вопрос, который был задан пользователю, нигде не сохраняется, 
поэтому нельзя задавать разные вопросы. Статистика собирается по логам.

##  MVP

В MVP версии вопрос будем задавать через эксперимент по водителям. 
Нужна возможность задавать разные вопросы, поэтому теперь вопрос и ответ на него будем сохранять.

Фидбек о поездке собирается ручкой `/passenger-feedback/v2/feedback` сервиса 
`passenger-feedback`. Добавим в неё поля для сохранения вопроса и ответа на него:
```
V2SaveRequest:
    type: object
    properties:
        ...
        survey:
            $ref: "#/definitions/SurveyInfo"
    required:
        ...
    additionalProperties: false

SurveyInfo:
    type: array
    definition: список вопросов, которые можно задать пользователю
    items:
         $ref: "#/definitions/QuestionInfo"

QuestionInfo:
    type: object
    properties:
        question_id:
            type: string
            description: идентификатор вопроса, на который отвечал пользователь
        answer_id:
            type: string
            description: идентификатор ответа пользователя на заданный вопрос
    required:
      - question_id
      - answer_id
    additionalProperties: false
```

Для того, чтобы управлять показом эксперимента по водителям, 
нужно отправлять в эксперимент кварг водителя. 
На клиенте его нет, поэтому попадание в эксперимент будем проверять на бэкенде.

Для этого можно будет добавить новую ручку в `passenger-feedback`.
Она будет проверять эксперимент и возвращать вопросы.
После запуска mvp можно будет расширить ручку и возвращать в ней не только вопросы, 
но и другие данные, нужные для предложения оставить фидбек.
В запросе будет передаваться id заказа, чтобы по нему извлекать id водителя.

Ручку будет вызывать клиент при изменении статуса поездки. 
На этапе mvp будет достаточно вызывать ручку только для статуса `completed`.

```
paths:
    ...
    /4.0/passenger-feedback/v1/feedback-proposal:
        post:
            x-taxi-middlewares:
                api-4.0: true
            description: возвращает вопрос, на который пользователь отвечает в рамках опроса о качестве поездки
            parameters:
              - in: body
                name: body
                required: true
                schema:
                    $ref: '#/definitions/FeedbackProposalRequest'
            responses:
                200:
                    description: OK
                     schema:
                        $ref: '#/definitions/FeedbackProposalResponse'


definitions:
    FeedbackProposalRequest:
        type: object
        properties:
            order_id:
                description: id заказа
                type: string
        required:
          - order_id
        additionalProperties: false

    SurveyAnswerOption:
        type: object
        properties:
            id:
                type: string
                description: идентификатор ответа
            text:
                type: string
                description: текст ответа
        required:
          - id
          - text

    SurveyQuestion:
        type: object
        properties:
            question_id: 
                type: string
                description: идентификатор вопроса, на который отвечает пользователь
            question_text:
                type: string
                description: текст вопроса, на который отвечает пользователь
            answer_options:
                type: array
                    items:
                        $ref: '#/definitions/SurveyAnswerOption'   
        required:
          - question_id
          - question_text
          - answer_options
        additionalProperties: false

    FeedbackProposalResponse:
        type: object
        properties:
            survey_info:
                type: array
                items:
                    $ref: '#/definitions/SurveyQuestion'
        additionalProperties: false

    ErrorWithMessage:
        type: object
        additionalProperties: false
        properties:
            code:
                type: string
                description: error code
            message:
                type: string
                description: error message
        required:
          - code
          - message
```

Управлять показом вопросов можно новым экспериментом `ride_quality_surveys`:
```
SurveyAnswer:
    type: object
    description: данные ответа опроса
    properties:
        id: 
            type: string
            description: идентификатор ответа
        tanker_key:
            type: string
            description: танкерный ключ ответа
    required:
      - id
      - tanker_key
    additionalProperties: false

SurveyQuestion:
    type: object
    description: вопрос и ответы предлагаемого опроса
    properties:
        question_id: 
            type: string
            description: идентификатор вопроса
        question_tanker_key:
            type: string
            description: танкерный ключ вопроса
        answers: 
            type: array
            items:
                $ref: '#/definitions/SurveyAnswer'
    required:
      - question_id
      - question_tanker_key
      - answers
    additionalProperties: false

type: object
additionalProperties: false
properties:
    enabled:
      type: boolean
    survey_questions:
        type: array
        items:
            $ref: '#/definitions/SurveyQuestion'
required:
  - enabled
  - survey_questions
```

### Доработки на бэкенде

Информация о фидбеке хранится в монге `feedback`.
Можно дописать в ней в данные фидбека `data` информацию о вопросе и ответе. 

```
...
    # Данные фидбека
    'data': {
        ...
        # данные опроса о качестве поездки
        'survey': [ {
            # идентификатор заданного вопроса
            'question_id': 'car_state',
            # идентификатор ответа пользователя
            'answer_id': 'yes'
        }, ...]
    },
...
```

В `order_proc` ничего не дописывать.

Ручка `/passenger-feedback/v1/feedback` устарела, можно попробовать удалить старый код в рамках техно.

## После MVP

Если будет конверсия из показа в ответ 10%+, а также повторяемость в ответах, будем дополнять функциональность. 
Есть желание подключить алгоритмы, возможно ml, чтобы он задавал случайные вопросы, и если кто-то ответил Да - 
доуточнял точечно конкретный вопрос.

## Рефакторинг
Планируется сделать рефакторинг и перенести в ручку `/4.0/passenger-feedback/v1/feedback-proposal` 
получение полей фидбека, которые сейчас клиент получает из `/taxiontheway` и `/zoneinfo`.

Ответ ручки дополнится полями:

```
FeedbackProposalResponse:
    type: object
    properties:
       ...
       feedback:
            $ref: '#/definitions/Feedback'
       supported_feedback_choices:
            $ref: '#/definitions/SupportedFeedbackChoices'
    additionalProperties: false

Feedback:
    type: object
    properties:
        msg:
            type: string
            description: сообщение пользователя с комменнтарием о поездке
        rating:
            type: int
            description: оценка поездки
        call_me:
            type: bool
        choices:
            type: array
            items: 
                $ref: '#/definitions/FeedbackChoice'
    required:
      - rating
    additionalProperties: false

FeedbackChoice:
    type: object
    properties:
        type:
            type: string
            example: "badge"
        value:
            type: string
            example: "pleasantmusic"
    required:
      - type
      - value
    additionalProperties: false

SupportedFeedbackChoices:
    type: object
    properties:
        low_rating_reason:
            type: array
            items: 
                $ref: '#/definitions/LowRatingReason'
        cancelled_reason:
            type: array
            items: 
                $ref: '#/definitions/CancelledReason'
        feedback_badges:
            type: array
            items: 
                $ref: '#/definitions/FeedbackBadge'
        feedback_rating_mapping:
            type: array
            items:
                $ref: '#/definitions/FeedbackRelation'
    additionalProperties: false

LowRatingReason:
    type: object
    properties:
        name: 
            type: string
            example: "driverlate"
        label: 
            type: string
            example: "Водитель опоздал"
    required:
      - name
      - label
    additionalProperties: false

CancelledReason:
    type: object
    properties:
        name: 
            type: string
            example: "mistaken"
        label: 
            type: string
            example: "Передумал"
    required:
      - name
      - label
    additionalProperties: false

FeedbackBadge:
    type: object
    properties:
        label:
            type: string
        count:
            type: string
        images:
            type: object
            $ref: '#/definitions/BadgeImage'
    required:
      - label
      - count
      - images
    additionalProperties: false

BadgeImage:
    type: object
    properties:
        active_image_tag:
            type: string
        inactive_image_tag:
            type: string
    required:
      - active_image_tag
      - inactive_image_tag
    additionalProperties: false

FeedbackRelation:
    type: object
    properties:
        rating:
            type: int
        choice_title: 
            type: string
        badges:
            type: array
            items:
                type: string
    required:
      - rating
      - choice_title
      - badges
    additionalProperties: false
```

Схемы примерные, детали уточню на этапе рефакторинга.

Что войдёт в рефакторинг:
1. Перенос части ответа с фидбеком (оценка, сообщение) из монолита (из ответа `totw`)
 в `passenger-feedback`.
2. Перенос бейджей положительного фидбека из монолита (из ответа `totw`)
 в `passenger-feedback`.
3. Перенос вариантов выбора причин отрицательных оценок из монолита 
(из ответов `zoneinfo` и `totw`) в `passenger-feedback`.

Клиентские разработчики смогут перейти с получения полей фидбека из ручек монолита на новую ручку. 
Рассчитываю, что получение вариантов фидбека из монолита можно будет удалить.
