# octopus

## Подтягиваем библиотеки
	git clone --recursive git@github.com:YandexClassifieds/octopus.git
	php -q build/tools/composer.phar install

## Сборка пакета
Перед сборкой необходимо настроить окружение:
  * https://wiki.yandex-team.ru/autoru-admin/packaging-and-deploy
  * http://doc.yandex-team.ru/Debian/deb-pckg-guide/concepts/About.xml

### Сборка
	git clone --recursive git@github.com:YandexClassifieds/octopus.git
	cd octopus
	make debuild
### Конфигурируем nginx (на примере пользователя alexreznikov и allteam сервера)
	vi /etc/nginx/devconf.d/alexreznikov.conf

	server {
	listen 84.201.136.230:443;
	listen [2a02:6b8:b010:36::27]:443;
	server_name octopus.alexreznikov.dev.autoru.yandex.net;
	keepalive_timeout    70;
	access_log /var/log/nginx/ssl.log;
	error_log /var/log/nginx/ssl_error.log;

	ssl on;
	ssl_certificate /etc/nginx/conf.d/certs/nginx.pem;
	ssl_certificate_key /etc/nginx/conf.d/certs/nginx.key;
	ssl_protocols SSLv2 SSLv3 TLSv1;
	ssl_ciphers ALL:!ADH:!EXPORT56:RC4+RSA:+HIGH:+MEDIUM:+LOW:+SSLv2:+EXP;
	ssl_prefer_server_ciphers on;

	location / {
		fastcgi_pass php-fpm;
		fastcgi_param SCRIPT_FILENAME /home/alexreznikov/octopus/src/index.php;
		fastcgi_param  AUTORU_CONFIG_PHP_LIB5  /home/alexreznikov/octopus/configs/development/lib5.php;
		fastcgi_param  AUTORU_CONFIG_PHP_LIB2  /etc/autoru-dev/alexreznikov/lib2.php;
		include fastcgi_params;
		}
	}
###Документация 
https://wiki.yandex-team.ru/autoru-dev/api-octopus/

### Работа с ветками
Каждая задача требует создания новой ветки, после решения задачи создается pull request.
Одобрить pull request должны как минимум 2 человека.
Обязательно прогоняем тесты при ревью кода, в соответствии с инструкцией:
https://beta.wiki.yandex-team.ru/autoru-dev/testing/run-api-tests/for-developers/
После этого исполнитель задачи принимает PR, при этом если требовались правки тестов, эти правки тоже необходимо принимать.
