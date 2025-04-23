# Jupiter Viewers

Описание ролей для IDM системы [Jupiter Viewers](https://idm.yandex-team.ru/system/jupiter_viewers).

## Как выдать права на новый ClusterMaster

1. Описываем новую роль ```example-cm.in.yandex-team.ru``` в файле jupiter_viewer.yaml по аналогии с существующими записами, коммитаем. В принципе, можно описывать роли и без коммита, но для порядка храним историю в VCS
2. Копипастим jupiter_viewer.yaml полностью в https://paste.yandex-team.ru/
3. Заходим в [настройки системы](https://idm.yandex-team.ru/system/jupiter_viewers/settings/options), во вкладку "Параметры", в поле "Ссылка на дерево ролей" вставляем ссылку на полученный paste, с "/text" на конце, сохраняем настройки
4. Заходим на [страницу синхронизации системы](https://idm.yandex-team.ru/system/jupiter_viewers/sync), синхронизируем узлы. Можно нажать на кнопку "Посмотреть что изменилось"
5. Запрашиваем новую роль ```Вьюверы Юпитера > example-cm.in.yandex-team.ru``` для нужных пользователей и/или групп через кнопку "Запросить роль" в IDM
6. В конфиге ClusterMaster'а указываем ```IdmRole: "jupiter_viewers/example-cm.in.yandex-team.ru"```, выкатываем
7. Profit
