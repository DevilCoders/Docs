# Docker image
Docker-образ для разработки и прода

## Как запустить
На машинах из https://wiki.yandex-team.ru/qyp/ уже стоит docker, но нужно сделать несколько подготовительных шагов.

### Получаем доступ к docker
sudo adduser <niknik> docker
Группа применится, когда вы перелогинитесь.
Если ждать не хочется, вводим в текущий шелл:
newgrp docker

### Сначала нужно залогиниться на registry.yandex.net

1) Получаем OAuth token [по ссылке [(https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1)]]
2) Добавляем токен в docker
echo "<token>" | docker login -u <login> --password-stdin registry.yandex.net

Подробности здесь:
https://wiki.yandex-team.ru/qloud/docker-registry/#authorization

### Скачиваем образ на машину
Достаточно запустить скрипт ./robot/blrt/docker_image/pull.sh

### Готово
