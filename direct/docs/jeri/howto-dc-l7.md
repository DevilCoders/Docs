# Увод локации через l7-heavy(ITS)

## Теория

Можем благодаря аваксу контролировать поток трафика в локации (MSK, SAS, VLA, MAN). Для каждого приложения(web, api, intapi) поднят свой балансер, поэтому рулится отдельно. Осуществляется через интерфейс [L7-heavy в няне](https://nanny.yandex-team.ru/ui/#/list-l7heavy/). Крутить надо с осторожностью, т.к. можно пролить трафик. После не забывать выставлять веса в дефолты.

## Как управлять весами

Находим нужный неймспейс в интерфейсе по ссылке выше или переходим напряму по ссылкам [web](https://nanny.yandex-team.ru/ui/#/l7heavy/direct.yandex.ru/) [api](https://nanny.yandex-team.ru/ui/#/l7heavy/api.direct.yandex.ru/) [intapi](https://nanny.yandex-team.ru/ui/#/l7heavy/intapi.direct.yandex.ru/). Внутри находим локацию с java/perl в имени. В левых полях "Current weight" выставляем нужные веса, чтобы суммарно получилось 100%, удобнее воспользоваться кнопками-ссылками "Close w/ current weights" на нужной локации. Получится картина вида  ![alt text](https://jing.yandex-team.ru/files/pe4kin/2021-09-23T13_45_51Z.93dbac1.597d4d2.jpeg "скрин увода SAS") После этого надо нажать кнопку с дискетой "Save section weights", вылезет дифф изменений ![alt text](https://jing.yandex-team.ru/files/pe4kin/2021-09-23T13:50:59Z.1212733.png "дифф весов"), для применения которого нужно нажать "Push to ITS". Если надо увести сразу все локации в ДЦ удобнее нажать на выпадушку "Bulk actions" и в ней нажать выставление весов ![alt text](https://jing.yandex-team.ru/files/pe4kin/2021-10-04T16:40:03Z.1858c64.png "Закрытие всего ДЦ") Применение асинхронное, будет заметно примерно в течение минуты.

## Возврат изменений

Для того, чтобы вернуть трафик на место, необходимо нажать кнопку "Reset weights to defaults" у необходимой локации ![alt text](https://jing.yandex-team.ru/files/pe4kin/2021-09-23T13_45_51Z.93dbac1.2ecc6e2.jpeg "Вернуть вес")  и нажать на "Save section weights" с подтверждением дифа(вдумчиво на него посмотрев=)). Можно также вернуть через балковые действия сразу везде ![alt text](https://jing.yandex-team.ru/files/pe4kin/2021-10-04T16:43:03Z.27a39c6.png "Вернуть веса") также с подтверждением сохранения.

## На почитать
[Подробности от команды балансера](https://wiki.yandex-team.ru/awacs/tutorial/l7heavy/)
