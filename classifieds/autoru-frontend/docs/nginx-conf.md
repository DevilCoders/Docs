# Конфиги nginx

## development

В деве мы сами управляем конфигами nginx. В `dev-configs/auto.ru.nginx.conf` находится шаблон для генерации конфига.

Это именно шаблон, а не сам конфиг. Скрипт `tools/deploy-configs build` берет hostname, папку с репой, другие переменные окружения и генерирует из него настоящий конфиг для домена `<pathname>.<hostname>`

Сгенерированные конфиги лежат в `/etc/nginx/sites-enabled`. После изменения шаблона его надо перегенерировать `tools/deploy-configs build` и перезапустить nginx `sudo service nginx restart`.

## testing/production

Документация от админов: https://wiki.yandex-team.ru/vertis-admin/howtochangenginxconfig/   
