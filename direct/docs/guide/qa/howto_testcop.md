# Тесткоп — ваш помощник в дежурстве

Сервис используется для облегчения дежурства по автотестам, с его помощью можно легко мьютить упавшие тесты, а задачи на починку будут созданы автоматически.
Подробнее о сервисе и его истории можно узнать из [документации.](https://doc.yandex-team.ru/si-infra/tests-stability/overview.html)

### FAQ по использованию
- [Как заскипать или замьютить тест через Тесткоп?](https://doc.yandex-team.ru/si-infra/tests-stability/testcop/testcop-how-to-skip-or-mute-test.html)
- [Как расскипать или размьютить тест?](https://doc.yandex-team.ru/si-infra/tests-stability/testcop/testcop-how-to-unskip-or-unmute-test.html)

#### В наших проектах ссылка на отчет находится в бэйджиках
![no alt](_assets/testcop_link.png)

### Подключен и используется в проектах:
 - [DNA](https://a.yandex-team.ru/arc/trunk/arcadia/adv/frontend/services/dna)
 - [UAC](https://a.yandex-team.ru/arc/trunk/arcadia/adv/frontend/services/uac)

### Состоит из:
 - Конфиг, пример. - https://testcop.si.yandex-team.ru/config/dna
 - Плагины на стороне сервиса:
    - `@yandex-int/frontend-hermione-config/plugins/json-reporter`
    - `@yandex-int/frontend-hermione-config/plugins/hermione-muted-tests`
 - Задача для `ci-flowgen` - [ссылка](https://a.yandex-team.ru/arcadia/adv/frontend/packages/ci-flowgen/docs/job-hermione.md)
