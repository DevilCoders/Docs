# Разработчику

## Настройка git

Чтобы история выглядела красиво и gitlab знал, куда засылать уведомления о событиях,
связанных с вашим изменением (например, кто-то его откомментрировал), вам нужно
настроить git, если ещё не. Ваш `Author` должен выглядеть так:

> Author: Alexey Andriyanov <alan@yandex-team.ru>

или так:

> Author: alan <alan@yandex-team.ru>

Для этого:

```sh
git config --global --add user.name 'Alexey Andriyanov'
git config --global --add user.email 'alan@yandex-team.ru'
```

## Настройка окружения разработчика RT

### Назначение

Данное руководство разработано с целью представить один из удобных вариантов окружения разработчика `Racktables` (далее *`RT`*) в NOCDEV.  
Быстрой/разовой альтернативой описанному решению является использование [среды rt-docker](https://noc-gitlab.yandex-team.ru/nocdev/rt-docker/-/blob/master/README.md) (далее *`стейджинг`*).  
Представленное в руководстве окружение обладает рядом преимуществ, не ограничивающихся следующим списком:

* Возможность использования локального IDE (в том числе инструменты откладки)
* Возможность использования Phpunit
* Удобное изменение и build кодовой базы, представленной на Golang 

## Необходимые репозитории

Для облегчения поиска по проектам (в т.ч. grep), рекомендуется держаться все проекты, связанные с RT рядом, в отдельной директории:

```bash
└─[√] $ tree -L 1
.
├── racktables
├── rt-yandex
├── rtapi2rr
└── alexandria-php-client
```

Данную структуру предлагается расположить в директории: `~/projects/rt`
Похоже именование директорий (`rt-yandex` и `racktables`) применяется на продакшен-серверах RT и в fpm-контейнерах стейджинга.

### racktables (upstream)

Является ненемного доработанной копией известной миру upstream-версии (aka racktables.org) Racktables.  
Репозиторий нашей версии [racktables-upstream](https://noc-gitlab.yandex-team.ru/nocdev/racktables-upstream/-/tree/yandex-prod) (далее *upstream/апстрим*).
Говорят, в старые времена был процесс переноса наших изменений в апстрим, но сейчас такое не происходит.

```bash
└─[√] $ git clone -b yandex-prod git@noc-gitlab.yandex-team.ru:nocdev/racktables-upstream.git racktables
```

### rt-yandex

Необходимые расширения к RT, зачастую полностью изменяющие поведение отдельных функциональностей.
Изменённые модули и плагины могут выполняться совместно с или даже вместо кода upstream-версии. Почти все изменения вносятся именно в этот проект.
[Репозиторий rt-yandex](https://noc-gitlab.yandex-team.ru/nocdev/racktables)

```bash
└─[√] $ git clone git@noc-gitlab.yandex-team.ru:nocdev/racktables.git rt-yandex
```

### rtapi2rr

Это код демона на go и phpшных воркеров RTAPI и InvAPI.
[Репозиторий rtapi2rr](https://noc-gitlab.yandex-team.ru/nocdev/rtapi2rr)
Не путать с клиентами RTAPI на [Go](https://a.yandex-team.ru/arc/trunk/arcadia/noc/go-rtrpc) и [Python](https://a.yandex-team.ru/arc/trunk/arcadia/noc/rtapi).

```bash
└─[√] $ git clone git@noc-gitlab.yandex-team.ru:nocdev/rtapi2rr.git
```

### alexandria-php-client

Автогенерированный клиент для [alexandria](https://a.yandex-team.ru/svn/trunk/arcadia/noc/alexandria/). Должен стать deprecated, но пока еще нет.

```bash
└─[√] $ git clone git@noc-gitlab.yandex-team.ru:nocdev/alexandria_php_client.git
```

## Локальная разработка

Обычно, в процессе работы над кодом, хочется проверять как что-то работает, запускать тесты. В силу того как устроен RT делать это без живой БД зачастую сложно или невозможно, вместе с тем трогать БД на проде - очень плохая идея. Поэтому стоит использовать возможности стейджинга.

Для использования базы стейджинга при локальной разработке в `racktables/wwwroot/inc/secret.php` складываем примерно следующее([rttctl](https://noc-gitlab.yandex-team.ru/nocdev/rt-docker/-/blob/master/README.md) должен быть установлен и сконфигурирован)


```php
<?php
global $pdo_dsn, $db_username, $db_password, $debug_mode, $yandex_db_password, $yandex_repo, $racktables_plugins_dir, $local_gwdir, $instance;
$yandex_repo = __DIR__.'/../../../../rt-yandex';
$upstream_repo = __DIR__.'/../../../../racktables';
$yandex_db_password['master'] = [];
$instance = "master";

require_once $yandex_repo . '/secret_common.php';
$stagingmode = TRUE;
if ($stagingmode) {
	$branch = trim(`git -C $yandex_repo branch --show-current`);
	if ($branch) {
		$ansj = `rttctl ps -j --branch="$branch"`;
		if (FALSE != $ans = json_decode($ansj, TRUE)) {
			foreach ($ans as $n) {
				foreach ($n['Envs'] as $e) {
					$pdo_dsn = "mysql:host={$e['endpoints']['mySQLHost']};port={$e['endpoints']['mySQLPort']};dbname=racktables";
					$db_username = 'racktables';
					$db_password = $e['endpoints']['mySQLPwd'];
					break 2;
				}
			}
			error_log("$branch - $pdo_dsn\n");
		} else {
			throw new RackTablesError("Can not found staging");
		}
	}
}


$debug_mode = TRUE;

$yandex_db_password = array (
    'master' => array (
            'db_username' => $db_username,
            'db_password' => $db_password,
    ),
    'backup' => array (
            'db_username' => $db_username,
            'db_password' => $db_password,
    ),
);


$racktables_plugins_dir = $yandex_repo . '/plugins';
$local_gwdir = $yandex_repo . '/safe_scripts';
?>
```

Сделаем симлинки до нужных частей RT:
```bash
sudo ln -s ~/projects/rt/racktables /usr/local/racktables-production
sudo ln -s ~/projects/rt/alexandria_php_client /usr/local/alexandria_php_client
```

И обновим зависимости alexandria_php_client с помощью composer:
```bash
cd ~/projects/rt/alexandria_php_client && composer up
```

В начале работы над фичей отводим ветку от master `git checkout -b YOURBRANCH`. После пуша в репозиторий можно будет создать стейджинг.
При работе над яндексовой RT (rt-yandex, rtapi2rr), Gitlab CI сделает это сам после git push.  
При работе над другими проектами пока приходится делать ветку RT (rt-yandex) и поддерживать ее живость самостоятельно через rttctl (смотри [быстрый старт](https://noc-gitlab.yandex-team.ru/nocdev/rt-docker/-/blob/master/README.md)).

После применения такой магии, наш локальный php-код будет обращаться к БД, которая развернута в контейнере стейджинга.
Для rtapi2rr/invapi возможно надо будет поправить пути импорта файлов.

### Основные ограничения описанного решения

Зачастую функциональностям RT необходима только база данных.  
Описанный в руководстве способ не открывает доступа к проверке и тестированию ряда манипуляций, часть ограничений возможно обойти, рецепты есть в документации стейджинга:  

* Опрос и изменение состояний оборудования
* Работа содержимым CVS
* Работа с Netmap
* Использование основных скриптов crontab

### Требования к окружению

* PHP 7.4.*
* Go (1.16.5+, уточнить)
* Composer (PHP) и php-cs-fixer

### Style

В rt-yandex (но не для upstream-версии) используется стиль, описанный в [rt-yandex/.php_cs](https://noc-gitlab.yandex-team.ru/nocdev/racktables/-/blob/master/.php_cs), применяется с помощью php-cs-fixer.  
Проверка стиля также запускается принудительно в рамках Gitlab CI pipeline, как на этапе обновления ветки в origin, так и при попытке Merge.  
Для локального использования понадобится установить Composer и php-cs-fixer.  
Пример вызова:

```bash
└─[√] $ php-cs-fixer fix -vv --diff --diff-format=udiff --config=.php_cs plugins/dynamic_dns.php
```

Можно настроить интеграцию с любимым редактором. Подружить с Windows не просто.
