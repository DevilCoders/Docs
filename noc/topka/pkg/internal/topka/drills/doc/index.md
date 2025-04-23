# Что это за сервис

Topka.Drills – сервис для управления учениями на датацентрах.

Что можно делать:
* [искать](trainings/general.md) и [просматривать](trainings/edit.md) учения
* [создавать](trainings/create.md) учения
* [редактировать и отменять](trainings/edit.md) учения
* работать с [пресетами](presets/general.md)

Документацию по API можно найти на [странице документации API топки](https://firewall.yandex-team.ru/api) в разделе ***Trainings*** и  ***Trainings Presets***

Для того, чтобы пользоваться API учений, нужно на [сайте регистрации приложений](https://oauth.yandex-team.ru/client/new) выдать своему приложению
права на скоуп учений (Доступы → HBF.Drills):

1. *drills:read* для получения списка учений

1. *drills:write* для создания и редактирования учений
