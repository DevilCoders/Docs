# Robot switcher

Скрипт переключения дежурств: роботного телефона и темы в Slack.

Для работы требует обязательные параметры окружения:
+ SLACK_TOKEN - токен доступа в Slack
+ SLACK_CHANNEL `<channel_id>` канала дежурств
+ STAFF_TOKEN - токен доступа к staff
+ ROBOT_PHONE - номер бота
+ TELEGRAPH_TOKEN - токен доступа к [Telegraph API](https://wiki.yandex-team.ru/VladimirPiskun/Telefonija-na-telegrafe/)

Если SLACK_PREFERRED=yes, читает логин дежурного из темы в слаке, иначе - смотрит в календарь дежурств и сам прописывает тему в Slack:
+ CALENDAR_PRIVATE_TOKEN - приватный токен календаря
+ ADMIN_DEPARTMENT - урл отдела


# Sandbox

+ disk admin: https://sandbox.yandex-team.ru/scheduler/15154
+ disk admin second: https://sandbox.yandex-team.ru/scheduler/15143
+ disk dev: https://sandbox.yandex-team.ru/scheduler/15155
+ disk mpfs (aka dev second. STOPPED): https://sandbox.yandex-team.ru/scheduler/15156
+ disk front: https://sandbox.yandex-team.ru/scheduler/15159
+ disk testing: https://sandbox.yandex-team.ru/scheduler/15157
