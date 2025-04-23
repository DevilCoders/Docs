## Обновление конфига

В Deploy конфиг поставляется через Sandbox ресурс. Чтобы конфиг раскатился, нужно:
1. Залить ресурс командой `make sandbox-update-unified-agent-config`
2. Заменить ссылку и хеш-сумму ресурса в `deploy/yandexpay-*.deploy.yaml`
3. Раскатить спеку в Deploy
