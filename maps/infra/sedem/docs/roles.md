## Ролевая модель

### Виды ролей  { #roles }

Sedem выделяет 4 абстрактных роли, привязанных к скоупам ролей ABC:
- `responsible` - ответственные за сервис:
  - участники ABC, привязанного к sedem-сервису, со скоупом ролей `devops`;
- `devops` - супер-юзеры:
  - ответственные за сервис (см. предыдущий пункт);
  - участники ABC [`maps-duty` со скоупом ролей `devops`](https://abc.yandex-team.ru/services/maps-duty?scope=devops).
- `duty` - дежурные;
  - участники [duty-сервиса](monitorings/duty#glossary) (если он есть), привязанного к sedem-сервису, со скоупом ролей `dutywork`;
  - участники ABC [`maps-duty` со скоупом ролей `dutywork`](https://abc.yandex-team.ru/services/maps-duty?scope=dutywork).
- `developers` - разработчики сервиса:
  - участники ABC, привязанного к sedem-сервису, со скоупом ролей `development`;
  - участники ABC [`maps-infra` со скоупом ролей `development`](https://abc.yandex-team.ru/services/maps-infra?scope=development).

Данные роли могут по-разному маппиться на ролевую модель целевой системы: Nanny, AWACS и т.п. Подробнее см. в соответствующем разделе документации.

{% note warning %}

На текущий момент правила маппинга ролей Sedem'а в ABC-сервисы и скоупы ролей захардкожены из соображений безопасности, и не могут быть изменены с помощью конфига сервиса, но в будущем мы планируем это исправить.

{% endnote %}
