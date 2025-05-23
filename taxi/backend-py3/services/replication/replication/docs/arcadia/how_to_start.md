# Быстрый старт

## Прочитайте вводную информацию
Сначала [ознакомьтесь](concepts.md) c коцепциями и требованиями к источникам и о способах репликации.

## Получите базовые доступы к сервису
Если вы еще не пользовались репликацией, проверьте наличие нужных [доступов](access.md).

## Чеклист создания правила
1) Настройте доступы для вашего правила.
    - Стоит получить доступы к источнику и добавить секреты: [подробнее](secrets.md)
    - Проверить доступы к таргетам: [инструкция для YT](yt_prefixes.md)

2) Заведите новые yaml-правила.
    - Правила расположены в аркадии. [Инструкция по создание правил](create_rule.md). Нужно сгенерировать правило генератором, либо создайте его вручную
    - Дождитесь зеленых тестов

3) Протестируйте ваши правила и запустите релиз
    - Проверьте правило в тестинге
    - [Выкатите](deploy.md) правило в **production**

4) [Включите ваше правило](drafts.md)

## Подпишитесь на мониторинги и получите доступы на изменение правил
Для новых правил обязательно стоит [завести мониторинги на них и настроить доступы](responsible.md), если
ранее этого не было сделано.

## Диагностика
[Ознакомьтесь с документацией](diagnostic.md) и c [FAQ](faq.md).

## Удалите ваше правило
Если правило вам более не нужно, то его нужно [удалить](delete-rule.md).
