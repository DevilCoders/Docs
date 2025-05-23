# Как катить бегемот через Морти

В чат `Morty Releases` приходит сообщение о релизе с кнопкой **Подтвердить**

{% cut "Пример сообщения" %}

![msg_morty](_screenshots/msg.png "msg_morty" =400x200)

{% endcut %}

После прихода сообщения у Марти есть 10 минут, чтобы нажать **Подтвердить**.
Если по каким-то причинам прожать кнопку в эти 10 минут не успели - релиз будет перешедулен (сдвинут на час в будущее).

### Возможные ошибки при выкатке

{% cut "Релиз начал катиться, но прилетела ошибка ValidationError" %}

![msg_morty](_screenshots/except_msg.png "msg_morty" =700x200)

В этом случае нужно нажать в сообщении **Перейти к событию** и в гуе прожать **Skip validation errors**

{% endcut %}

{% cut "Релиз так и не начал катиться в течении 5 минут от запланированного времени" %}

Скорее всего произошел перешедулинг.
Для починки нужно перейти в гуй релиза (через кнопку **Перейти к событию**), в событии нажать **Reschedule event** и повторить инструкцию по новой

{% endcut %}

{% cut "Релиз начал катиться, но прилетела ошибка ValueError_SB_task" %}

![msg_morty](_screenshots/except_msg_2.png "msg_morty" =700x200)
В этом случае можно только погрустить и лайкнуть [тикетос](https://st.yandex-team.ru/SPI-21130) на починку.
Катить нужно руками, **А РЕЛИЗ В МОРТИ ЗАКЕНСЕЛИТЬ**

{% endcut %}

## В любой непонятной ситуации будить ответственных за Морти - [pufit@](https://staff.yandex-team.ru/pufit)
