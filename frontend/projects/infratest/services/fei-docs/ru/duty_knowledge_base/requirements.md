# Требования к областям ответственности

При добавлении в дежурство новой области ответственности необходимо выполнить определенные условия.

## Требования к обращениям пользователей

### При приемке в дежурство

#### 🔴 Обязательно. Продукт должен быть добавлен в общую форму или иметь свою форму с созданием тикетов в очереди INFRADUTY. 

Для того чтобы обращения по продукту роутились в правильный контур и содержали необходимую для разбора информацию,
нужно либо добавить продукт (и при необходимости дополнительные вопросы) в общую форму,
либо создать форму специально для продукта.

При добавлении продукта в общую форму нужно [добавить новый продукт](https://wiki.yandex-team.ru/search-interfaces/infra/duty/infraduty-form/) в список инструментов 
и [настроить роутинг по инструменту](https://wiki.yandex-team.ru/search-interfaces/infra/duty/infraduty-form/#nastrojjkazerolinedljaroutingavkontur).

При создании отдельной формы в настройках интеграции обязательно добавьте тикету следующие поля: 

- компонент `source: form` (в созданные людьми тикеты без этого компонента приходит робот и говорит, что тикет надо создавать через форму),
- abc области ответственности (по abc области будет происходить роутинг после [FEI-22790: infraduty: научиться роутить тикеты с выставленным ABC области ответственности](https://st.yandex-team.ru/FEI-22790)),
- abc контура (по abc контура работает эскалация).

### На дежурстве

Если вы заметили, что обращения вашего контура роутятся zeroline неправильно, [исправьте правила роутинга](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/services/zeroline/docs/how-to.md). 

## Требования к мониторингам

### При приемке в дежурство

Перед тем, как направить уведомления от мониторингов на рассылку `infraduty`, убедитесь, что:

#### 🔴 Обязательно. Алерт должен быть обкатан хотя бы в течение одной-двух недель. 

Для обкатки оповещения настраиваются непосредственно на его создателя.
  
#### 🔴 Обязательно. Алерт должен иметь достаточную и лаконичную документацию по разбору в [базе знаний дежурства](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/services/fei-docs).

В частности документация должна отвечать на вопросы:

* что за алерт? на чем он основан?
* куда смотреть при его получении? 
* что делать при срабатывании алерта?

При этом документация должна быть понятна представителю любого контура.
  
#### 🔴 Обязательно. Алерт должен быть размечен ABC-сервисом области ответственности. 
  
* через правила [zeroline](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/services/zeroline).
* в `yasm` для удобного поиска всех алертов сервиса (например, [tun](https://yasm.yandex-team.ru/template/panel/fei-alerts/abc=tun/), [surfwax](https://yasm.yandex-team.ru/template/panel/fei-alerts/abc=surfwax/)).

#### 🔵 Опционально. Алерт должен быть в коде

* если сервис находится в `infratest`, то рекомендуется располагать алерты рядом с сервисом. Для этого надо поставить [monitorado](https://a.yandex-team.ru/arc_vcs/frontend/packages/monitorado) в `devDependencies`, настроить алерты и скрипты для их синхронизации по аналогии с `surfwax` ([скрипты запуска](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/services/surfwax/package.json?rev=r7830887#L59-60), [yaml-файл](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/services/surfwax/monitoring/router.awacs.yml?rev=r7830887))
* eсли сервис не в `infratest` - расположить в [infra-yasm-templates](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/infra-yasm-templates). И в данном случае лучше пользоваться [monitorado](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/infra-yasm-templates#monitorado).

Также хорошим тоном является обогащать алерты ссылками на документацию и окружение в Deploy при помощи поля `urls` ([пример](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/infra-yasm-templates/monitorado/zeroline.yml?rev=r7746566#L36-41))

### На дежурстве

#### 🔴 Обязательно. Алерты нужно перенастраивать после 2 ложных срабатываний.
