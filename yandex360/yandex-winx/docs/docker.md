## docker и arc

1. ставим docker по оф. инструкции
2. убираем sudo по инструкции https://docs.docker.com/engine/install/linux-postinstall/
3. далее у докера будут проблемы с монтированием из-за того что arc это fuse
	* добавить `user_allow_other` в `/etc/fuse.conf`
	* смонтировать arc так – `arc mount -S store -m arcadia -o allow_other --ssh-tokens`
4. далее нужна авторизация для нашего docker registry
	* выполняем `docker login -u `whoami` registry.yandex.net`
	* терминал замрет в ожидании токена, берем его тут - https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1
5. запросить доступ к базовому образу – https://idm.yandex-team.ru/#rf-role=rBvVWe4b#user:temasus@docker/distribution/mail%7Cmail-xenial-common/rbtorrent(fields:();params:()),rf-expanded=rBvVWe4b,rf=1
6. включаем ipv6 для докера иначе apt не сможет многое скачать и образ не соберется - https://wiki.yandex-team.ru/users/sivakov512/docker-and-ipv6
7. Возможно из-за фриза ( https://clubs.at.yandex-team.ru/tools/19953 ) при сборке образа magic некоторые pip пакеты не смогут установиться, включая транзитивные. Придется прибивать версии вручную в `requirements.txt`  как сделано для `SQLAlchemy`
