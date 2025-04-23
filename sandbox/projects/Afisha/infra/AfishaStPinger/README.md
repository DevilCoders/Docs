# St-Pinger

Sandbox задача, которая помогает призывать ответственных в стартрек тикеты по которым давно не было активности

Документация и описание того, как можно заехать:
https://wiki.yandex-team.ru/mediaservices/sre/adp-public/tools/stpinger/

Структура проекта:
- \__init__.py -> код самой задачи
- helpers
  - \__init__.py -> различные вспомогательные функции, в т.ч. функции для призыва людей и закрытия тикета
  - autoclose.tpl -> шаблон сообщения при закрытии тикета
  - last_call.tpl -> шаблон последнего сообщения перед закрытием тикета
  - summon_critical.tpl -> шаблон для призыва в проверке check_outdated_critical
  - summon_task.tpl -> шаблон для обычного призыва в проверке check_outdated_normal
- config.yaml -> дефолтный конфиг
