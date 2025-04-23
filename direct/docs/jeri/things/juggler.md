# Juggler

Самое главное, что надо знать о Juggler.

Juggler -- это яндексовый сервис событийного мониторинга ("лампочки").  

Живет здесь: <https://juggler.yandex-team.ru>

Делает две главные штуки:

- агрегирует события, то есть собирает из одних сигналов/лампочек другие
- отправляет нотификации

Документация: <https://docs.yandex-team.ru/juggler/>

Главные понятия, которые надо осознать:

- сырое событие
- проверка/агрегат (настройки)
- полное событие (результат работы проверки)
- правило нотификации

В Директе есть несколько пайплайнов заведения проверок:

- [directadmin-make-juggler.py](../howto-directadmin-juggler.md)
- TODO: из кода
- TODO: по событиям из Соломона
- TODO: по событиям из Голована

Правильные выборки проверок:

- чат со звонящими мониторингами (TODO ссылка)
- чат Direct.AppDuty.Monitoring (TODO ссылка)
- чат Direct.Monitoring (TODO ссылка)
- дашборд <https://solomon.yandex-team.ru/?project=direct&dashboard=direct-group-sre-tv>, блоки Direct Health и juggler

