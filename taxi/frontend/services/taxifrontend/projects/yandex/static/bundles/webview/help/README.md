# Вебвью: служба поддержки
Адрес: /help

**Тестовые параметры**
- Для тестирования истории переписок
`/help?authToken={AUTH}&helpType=Yandex&id={ID}`

_AUTH и ID достаём из логов админки_

- Тестирование последней поездки и чека
`/help?id=3e9313c5ca9643269fb1cfda1f8443ca&authToken=AQAAAADu4EeyAAAIgVjV1QZXc0bCjoMUlz4V-bU&helpType=Yandex&tripId=1512567229%3Adf506d52e4d54957a2e127456e8045f5`

**Чат**

Как показать чат описано [тут](https://wiki.yandex-team.ru/users/arefyev/Kak-sozdat-chat-v-testinge/)

/get_user_messages mock с CSAT
```(json)
{
    'ask_csat': true,
    'avatar_url': '2',
    'chat_open': true,
    'chat_visible': true,
    'csat_options': [{
        'option_key': 'horrible',
        'option_name': 'Ужасно',
        'reasons': [{'reason_key': 'long_answer', 'reason_name': 'Долгий ответ'}, {'reason_key': 'template_answer', 'reason_name': 'Ответ шаблоном'}, {
            'reason_key': 'disagree_solution',
            'reason_name': 'Не согласен с решением'
        }]
    }, {
        'option_key': 'bad',
        'option_name': 'Плохо',
        'reasons': [{'reason_key': 'long_answer', 'reason_name': 'Долгий ответ'}, {'reason_key': 'template_answer', 'reason_name': 'Ответ шаблоном'}, {
            'reason_key': 'disagree_solution',
            'reason_name': 'Не согласен с решением'
        }]
    }, {
        'option_key': 'normal',
        'option_name': 'Нормально',
        'reasons': [{'reason_key': 'long_answer', 'reason_name': 'Долгий ответ'}, {'reason_key': 'template_answer', 'reason_name': 'Ответ шаблоном'}, {
            'reason_key': 'disagree_solution',
            'reason_name': 'Не согласен с решением'
        }]
    }, {
        'option_key': 'good',
        'option_name': 'Хорошо',
        'reasons': [{'reason_key': 'thank_you', 'reason_name': 'Спасибо'}, {'reason_key': 'all_clear', 'reason_name': 'Всё понятно'}, {
            'reason_key': 'fast_answer',
            'reason_name': 'Быстро ответили'
        }, {'reason_key': 'helped_me', 'reason_name': 'Мне помогли'}]
    }, {
        'option_key': 'amazing',
        'option_name': 'Отлично',
        'reasons': [{'reason_key': 'thank_you', 'reason_name': 'Спасибо'}, {'reason_key': 'all_clear', 'reason_name': 'Всё понятно'}, {
            'reason_key': 'fast_answer',
            'reason_name': 'Быстро ответили'
        }, {'reason_key': 'helped_me', 'reason_name': 'Мне помогли'}]
    }],
    'messages': [{'author': 'user', 'body': 'тестовый отзыв', 'timestamp': '2018-08-14T11:38:53+0000', 'type': 'text'}, {
        'author': 'support', 'body': 'тестовый ответ'}],
    'new_messages': 2,
    'support_name': 'Павел'
}
```
