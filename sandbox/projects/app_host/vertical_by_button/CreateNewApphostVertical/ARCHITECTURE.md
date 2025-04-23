# Создание новой вертикали Apphost.

## Части процесса
Для новой вертикали Apphost'a нужно создать компоненту в [Release Machine](rm.z.yandex-team.ru/) ([документация по RM](https://wiki.yandex-team.ru/releasemachine/))
для управления релизами данной вертикали, сервисы в Nanny выкатки вертикали,
сетевые макросы в Racktables, необходимые сущности в awacs-балансере,
дашборд для деплоя, а также запустить все это и прокатить первый релиз новой компоненты.

## Составляющие процесса
Все вышеописанное реализуется при помощи Sandbox-задач:
* [`CreateNewApphostVertical`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/app_host/vertical_by_button/CreateNewApphostVertical)
* [`CreateNewRmForApphostVertical`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/app_host/vertical_by_button/CreateNewRmForApphostVertical)
* [`CreateNannyServicesForApphostVertical`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/app_host/vertical_by_button/CreateNannyServicesForApphostVertical)

Входной точкой является задача `CreateNewApphostVertical`, которая запускает другие две
задачи как подзадачи внутри себя. Так как после добавления новых макросов необходимо
дождаться их раскатки во все ДЦ при помощи HBF (а это процесс небыстрый),
примерное время выполнения всех задач составляет 4-6 часов.

В случае неудачного запуска, когда что-то упало на полпути можно просто
перезапустить упавшую задачу.

Если вдруг нужно подчистить все, что было создано для какой-либо вертикали,
можно воспользоваться задачей [`RemoveApphostVertical`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/app_host/vertical_by_button/RemoveApphostVertical),
она удалит все, что описано в параграфе "Части процесса".
