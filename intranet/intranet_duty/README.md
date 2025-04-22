# Дежурство по Интранету

Здесь находятся утилиты сервисов Интранета, которые находятся в [дежурстве](https://abc.yandex-team.ru/services/intranetduty/). За консистентность содержимого этой директории и соблюдение всех правил перечисленных ниже отвечают [участники роли "Разработка" Дежурства по Интранету в АБЦ](https://abc.yandex-team.ru/services/intranetduty/?scope=development).

[Как мы дежурим](https://wiki.yandex-team.ru/content/duty/intranet-duty/)

## /alerts

Конфиги алертов для сервисов.

## /templates

Код JINJA шаблонов для дашбордов в головане. 

## /scripts
Код для автоматизации заведения алертов

# Чего мы ждем чтобы все заработало с минимумом ручной работы
* https://st.yandex-team.ru/JUGGLER-3610 - эскалация до звонка не по логинам, а по сервисным группам 
* https://st.yandex-team.ru/TOOLBOX-27 - алерты на уровень логов ERROR и WARN в кулауде
* https://st.yandex-team.ru/TOOLBOX-42 - поддержка Яндекс.Деплой. Обешают формат конфига совместимый с кулаудным.
* https://st.yandex-team.ru/TOOLBOX-56 - автозаведение в infra.yandex-team.ru
