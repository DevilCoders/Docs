# Разработка плагина hermione-debug

Для работы плагина нужен клиент noVNC. Его адрес зашит в `lib/commands/create-vnc-url.js`. Сейчас адрес клиента залит в виде sandbox-ресурса.
Если необходимо обновить версию noVNC, нужно скачать [клиент](https://github.com/novnc/noVNC), убрать лишние файлы, залить при помощи `ya upload -T=SANDBOX_CI_ARTIFACT --ttl=inf --owner=SANDBOX_CI_SEARCH_INTERFACES ./noVNC` и обновить ссылку в коде команды vncUrl.
