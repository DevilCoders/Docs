# Выключаем анонс аваксовых балансеров 

## Что это такое

Прекращение получения трафика **L7 балансерами** в определенном ДЦ. Поды с балансерами перестают отвечать 200 на ручку анонса и L3 перестает лить трафик в эти балансеры. Трафик в приложение при этом продолжает распределяться в соотвествии с весами в [ITS](./howto-dc-l7.md)

## Для чего бывает нужно
* Закрытие перед работами/учениями, чтобы не просыпать запросы при пропадании сети на балансерах.
* При раскатке конфигов балансера, чтобы проверить, что работает ожидаемо новый конфиг, притушив старый до полной раскатки
* Во время проблем с балансерами в каком-то ДЦ

## Снятие анонсов дежсменой(Marty)
Сейчас на наших балансерах включена настройка "Create announce handlers for marty", что означает, что дежурная смена поиска может снять анонс при каких-то глобальных авариях. Делают они это предварительно скидывая оповещение через martycast, на который подписан чат app-duty. Происходит такое только при глобальных прогрузках, подготовкам к работам в ДЦ или при проблемах с ДЦ. Это влияет только на анонс самих балансеров в локации, т.е. возможность захода трафика из вне через определенный ДЦ. Веса трафика при этом они не трогают и необходимо вручную закрываться при проблемах по [инструкции](./howto-dc-l7).

## Процесс выключения

Необходимо понять у каких балансеров нужно будет снять локацию, т.к. они живут не во всех ДЦ. Основные:
[direct.yandex.ru](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/direct.yandex.ru/) - MYT SAS VLA
[api.direct.yandex.ru](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/api.direct.yandex.ru/show) - IVA SAS VLA
[intapi.direct.yandex.ru](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/api.direct.yandex.ru/show) - IVA SAS VLA
SAS - ДЦ Сасово
VLA - ДЦ Владимир
MYT - ДЦ Мытищи
IVA - ДЦ Ивантеевка
Исторически сложилось, что для Поиска IVA и MYT это локация MSK, что отображается в интерфейсе. Если необходимо закрыть IVA или MYT в дальнейшем при выборе локации используйте MSK.

* Смотрим по графикам в неймспейсе - вкладка Monitoring ссылка service_total, что трафик идет в соседние локации балансеров и мы не закрываем последнюю
* Находим нужный неймспейс в интерфейсе по [ссылке](https://nanny.yandex-team.ru/ui/#/list-l7heavy/) или переходим напряму по ссылкам нужных нам сервисов [web](https://nanny.yandex-team.ru/ui/#/l7heavy/direct.yandex.ru/) [api](https://nanny.yandex-team.ru/ui/#/l7heavy/api.direct.yandex.ru/) [intapi](https://nanny.yandex-team.ru/ui/#/l7heavy/intapi.direct.yandex.ru/) (ТС управляется дежсменой, но можно закрыться самостоятельно: [web и logviewer](https://nanny.yandex-team.ru/ui/#/l7heavy/awacs.test.direct.yandex.ru), [api](https://nanny.yandex-team.ru/ui/#/l7heavy/api.test.direct.yandex.ru))
* Нажимаем кнопку "Open ITS location" ![alt text](https://jing.yandex-team.ru/files/pe4kin/2021-10-19T07:33:30Z.f51ced0.png "Переход в ITS"), попадаем в еще один интерфейс
* В открывшемся интерфейсе скроллим, попутно проверив, что мы в нужной секции выбранностью таба ![alt text](https://jing.yandex-team.ru/files/pe4kin/2021-10-19T07:46:23Z.ac86d97.png "локация"), до самого низа и видим интерфейс изменения настроек балансера ![alt text](https://jing.yandex-team.ru/files/pe4kin/2021-10-19T07:44:15Z.db9fb9c.png "ITS")
* Выбираем таб с нужной локацией ![alt text](https://jing.yandex-team.ru/files/pe4kin/2021-10-19T07:49:43Z.292e042.png "vla") 
* В строке "Shutdown announce" нажимаем синюю кнопку "+Apply", получаем картину вида ![alt text](https://jing.yandex-team.ru/files/pe4kin/2021-10-19T07:52:40Z.c89f306.png "SHTDWN") 

 **Для возвращения трафика надо нажать на появившуюся корзину.**
