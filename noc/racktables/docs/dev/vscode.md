## Настройка VSCode для Racktables
Эта страница посвящена настройке VScode для удобства локальной разработки Racktables на MacOS.  
Часть знаний, которые могут пригодится расположена в инструкции [{#T}](contribution.md) в этом же разделе документации и может ее дублировать и дополнять.  

## Подготовка
Предварительно лучше поставить **php7.4**
```bash
brew install php@7.4
brew unlink php
brew link php@7.4
```

## Настройка Репы RT локально

Для разработки и удобного запуска RT нам понадобятся следующие репозитории:
1) Racktables-upstream
2) rt-yandex
3) rtapi2rr
4) alexandria-php-client

{% note warning %}

alexandria-php-client в скором времени должна стать deprecated, проверьте этот момент, в любом случае хуже от клона этой репы не станет.

{% endnote %}

Склонируем все эти репы к себе в `~/projects/rt/`
```bash
mkdir -p ~/projects/rt && cd ~/projects/rt
git clone -b yandex-prod git@noc-gitlab.yandex-team.ru:nocdev/racktables-upstream.git racktables
git clone git@noc-gitlab.yandex-team.ru:nocdev/racktables.git rt-yandex
git clone git@noc-gitlab.yandex-team.ru:nocdev/rtapi2rr.git
git clone git@noc-gitlab.yandex-team.ru:nocdev/alexandria_php_client.git
```

Сделаем симлинки до нужных частей RT:
```bash
sudo ln -s ~/projects/rt/racktables /usr/local/racktables-production
sudo ln -s ~/projects/rt/alexandria_php_client /usr/local/alexandria_php_client
```

Или, теперь есть возможность использовать пути через ENV:
```bash
export RT_INIT_PATH="~/projects/rt/racktables/wwwroot/inc/init.php"
export RT_PLUGINS_PATH="~/projects/rt/rt-yandex/plugins"
export RT_GATEWAY_PATH="~/projects/rt/racktables/gateways"
export RT_STATIC_PATH="~/projects/rt/racktables/wwwroot"
export RT_SCRIPT_PATH="~/projects/rt/rt-yandex/plugins/scripts"
```

## Настройка плагинов VSCode
В VSCode открываем папку ~/projects/rt  

!После всех манипуляций можно будет сохранить текущий воркспейс на будущее.

Из полезных плагинов VSCode можно поставить:
#### 1) PHP Intelephense (Ben Mewburn)
Тут из настроек только личная вкусовщина.

#### 2) PHP Debug (Xdebug)
Для настройки нужно поменять в плагине настройку **"cwd"** на **"${cwd}"** или выполнить:
```bash
mkdir -p ~/projects/rt/.vscode && cd ~/projects/rt/.vscode
cat >launch.json <<END
{
    "configurations": [
        {
            "name": "Launch currently open script",
            "type": "php",
            "request": "launch",
            "program": "\${file}",
            "cwd": "\${cwd}",
            "port": 0,
            "runtimeArgs": [
                "-dxdebug.start_with_request=yes"
            ],
            "env": {
                "XDEBUG_MODE": "debug,develop",
                "XDEBUG_CONFIG": "client_port=${port}"
            }
        }
    ]
}
END
```

#### 3) php cs fixer (junstyle)
Чтобы удобно делать autofixtyle при сохранении файла.  
Для корректной работы **php-cs-fixer** нужно его поставить, причем второй версии для совместимости конфига:
```bash
brew install php-cs-fixer@2
brew link php-cs-fixer@2
```
Можно в настройках плагина накликать пункты "PHP-cs-fixer: Config" и "PHP-cs-fixer: On Save"
Или добавить конфиг vscode для этого Workspace:
```bash
mkdir -p ~/projects/rt/.vscode && cd ~/projects/rt/.vscode
cat >settings.json <<END
{
    "php-cs-fixer.config": "~/projects/rt/rt-yandex/.php_cs",
    "php-cs-fixer.onsave": true
}
END
```

#### 4) Плагин GitLens — Git supercharged (GitKraken)
Просто удобный плагин для git blame внутри


## Работа с staging
При локальном запуске кода можно использовать данные из БД стейджинга для удобства и тестов.
Как было сказано в других инструкциях следует добавить secret.php в репу апстрима в wwwroot/inc/ или выполнить:
```bash
cd ~/projects/rt/racktables/wwwroot/inc
cat >secret.php <<END
<?php

\$script_mode = TRUE;

global \$pdo_dsn, \$db_username, \$db_password, \$debug_mode, \$yandex_db_password, \$yandex_repo, \$racktables_plugins_dir, \$local_gwdir, \$instance;
\$yandex_repo                  = __DIR__ . '/../../../rt-yandex';
\$upstream_repo                = __DIR__ . '/../../../racktables';
\$yandex_db_password['master'] = [];
\$instance                     = 'master';

require_once \$yandex_repo . '/secret_common.php';
\$stagingmode = TRUE;
if (\$stagingmode) {
	\$branch = trim(\`cd \$yandex_repo && git branch --show-current\`);
	if (\$branch) {
		\$ansj = \`rttctl ps -j --branch="\$branch"\`;
		if (FALSE != \$ans = json_decode(\$ansj, TRUE)) {
			foreach (\$ans as \$n) {
				foreach (\$n['Envs'] as \$e) {
					\$pdo_dsn     = "mysql:host={\$e['endpoints']['mySQLHost']};port={\$e['endpoints']['mySQLPort']};dbname=racktables";
					\$db_username = 'racktables';
					\$db_password = \$e['endpoints']['mySQLPwd'];
					break 2;
				}
			}
			error_log("\$branch - \$pdo_dsn\n");
		} else {
			throw new RackTablesError('Can not found staging');
		}
	}
}

\$debug_mode = TRUE;

\$yandex_db_password = [
	'master' => [
		'db_username' => \$db_username,
		'db_password' => \$db_password,
	],
	'backup' => [
		'db_username' => \$db_username,
		'db_password' => \$db_password,
	],
];

\$racktables_plugins_dir = \$yandex_repo . '/plugins';
\$local_gwdir            = \$yandex_repo . '/safe_scripts';

END
```

{% note warning %}

Стейджинг создается после первого push в ветку. Подробнее про стейджинг в [доке стейджинга](https://docs.yandex-team.ru/racktables-staging/).

{% endnote %}

Теперь можно локально запускать части RT используя БД из запущенного стейджинга для бранча.
