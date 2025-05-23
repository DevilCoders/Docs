# Текущие ограничения

Сейчас в системе есть недоработки, которые мы закроем в ближайшее время. Одна их часть относится к базовой функциональности, другая к отдельным возможностям системы и UX. Ниже они перечислены с ожидаемым сроком закрытия.

## Добавление секретов {#secrets-delegation}

В стейдж нельзя добавить секрет, который ранее в нём не использовался. Уже вписанные в сервис через UI Yandex.Deploy или dctl секреты будут работать, а указать там новый нельзя. Возможность будет добавлена с наивысшим приоритетом, но это займёт от одного до двух месяцев. [Тикет](https://st.yandex-team.ru/INFRACTL-32).

## Гибкая выдача ролей на свои объекты {#roles}

Для группировки объектов в infractl используется сущность неймспейс, [инструкция по его созданию](https://docs.yandex-team.ru/infractl/howto#import). Один из обязательных атрибутов неймспейса это ссылка на ABC-сервис, все члены которого автоматически получают права на управление всеми входящими в неймспейс объектами. На данный момент это единственный штатный механиз выдачи прав на объекты в infractl. Нет штатной возможности выдать права кому-то, кроме членов указанного в неймспейсе ABC-сервиса, как и нет штатной возможности выдать права на свои объекты более гранулярно чем на весь неймспейс. На данный момент мы собираем требования к ролевой модели в [тикете](https://st.yandex-team.ru/INFRACTL-113), после чего приступим к её поддержке.
