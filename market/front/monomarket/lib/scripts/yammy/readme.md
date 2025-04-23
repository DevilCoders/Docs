[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/scripts/yammy)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/scripts/yammy) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-market/yammy)](https://oko.yandex-team.ru/pkg/@yandex-market/yammy)

Yammy
=====

_Yandex Monorepo Manager - is Yammy!_

Yammy - это пакетный менеджер для монорепозитория.

### Установка

```(bash)
yarn global add yammy
```

Использование и наличие yarn в системе является обязательным требованием - yammy построен поверх двух технологий: git и
yarn.

Yammy обладает очень умным и достаточно быстрым автокомплитом. Чтобы его включить надо добавить в скрипты `.bashrc`
или `.bash_profile` строчку `source <(yammy _autocomplete)`

Правилом хорошего стиля также является установка пакета в зависимости проекта с которым он будет работать. В этом случае
yammy автоматически будет использовать локально установленную версию, что позволит более точно управлять версиями самого
yammy.

### Конфигурация репозитория

Минимальная конфигурация - это настройка поля workspaces в корневом package.json (
см. https://yarnpkg.com/en/docs/workspaces)

Для того чтобы корректно работала сборка однако на данном этапе требуется сделать небольшую хитрость - настроить
workspaces на симлинк, а не настоящую директорию с пакетами. Например:

- создаём директорию `lib`, где размещаем все пакеты
- создаём симлинк `ln -s lib packages`
- настраиваем workspaces: `"workspaces": ["packages/*"]`

Это позволяет одновремено использовать воркспейсы в yarn и при необходимости устанавливать все зависимости конкретного
пакета в его собственную директорию `node_modules` - в противном случае при вызове `yarn install` из директории пакета
этого не произойдёт.

### Настройка git и yarn

Все настройки в этом разделе являются необязательными, но значительно упростят жизнь в монорепе.

#### Настраиваем yarn-offline-mirror

Нам потребуется 2 файла .yarnrc Первый файл будет жить в корне репозитория. В нём надо прописать что-то типа

```
prefer-offline true
yarn-offline-mirror "./modules"
yarn-offline-mirror-pruning true
```

Второй файл будет жить в каталоге с пакетами. В нём надо прописать

```
yarn-offline-mirror "../modules"
yarn-offline-mirror-pruning false
```

Смысл второго файла в том, что при сборке пакета в нём вызывается `yarn install`, который без такой настройки убьёт все
кешированные модули, которые не относятся к текущему пакету.

#### Настройки гита

Рекомендуемый файл .gitignore (в случае если пакеты живут в lib/)

```
node_modules/
yarn-error.log
.yarn-cache/
lib/**/yarn.lock

server.log
server.err
server.pid

**/.build/
.npm-bundle/
.stash/

**/debian/changelog
**/debian/files
**/debian/*.debhelper.log
**/debian/*.postinst.debhelper
**/debian/*.postrm.debhelper
**/debian/*.substvars
**/debian/*/

**/*.build
**/*.deb
**/*.changes
**/*.upload
```

### Настройка сборки пакетов

В настоящий момент yammy поддерживает сборку 3х типов пакетов:

- debian пакеты
- docker образы
- npm пакеты

Для настройки сборки пакета нужно

- записать в package.json скрипт build, который будет подгатавливать все файлы проекта. Простейший скрипт
  сборки `cp -r ./* .build/dist/`.

- записать в package.json конфигурацию каталогов
  сборки: `"config": {"build": { "root": ".build", "dist": "dist", "temp": "temp" } }`, где root - корень каталога
  сборки, temp - директория временных файлов в каталоге сборки, dist - директория с результатами сборки в каталоге
  сборки.

- для сборки в виде NPM-пакета убрать опцию `"private": true`

- для сборки в виде docker-образа добавить
  конфигурацию: `"config": {"docker": {"name": "prefix/repo", "template": "dockerfile.js"}}`, где name - это имя
  репозитория в registry, а template - это скрипт, который генерирует Dockerfile для сборки

- для сборки debian пакета требуется добавить конфигурацию: `config: {debian: {"name": "deb-package-name"}}`, где name -
  название debian пакета. Также требуется создать все необходимые скрипты сборки в директории `debian/` кроме ченжлога -
  он генерируется автоматически в процессе сборки.

#### Авторство

В корневом `package.json` файле можно настроить секцию owners для проставления прав на npm пакеты и корректного
определения авторства веток:

```
"owners": [
	"gheljenor",
	"goldfinch",
	...
	"robot-musfront-ci",
	"teamcity"
]
```

Чтобы исключить роботов из списка возможных авторов веток их нужно перечислить в секции robots:

```
"robots": [
	"teamcity",
	"robot-musfront-ci",
	"robot-potato",
	"robot-domino"
]
```

### Интеграция со Стартреком

Для интеграции со стартреком требуется добавить конфигурацию: `"config": {"st": { "cmd": "st" }}`, где cmd - команда с
помощь которой создаются и обновляются тикеты.

Сигнатуры вызовов:

```
 > st create <type> <pkg> <version> <branch> <user> --changelog "<changelog>"  -  Создание нового тикета
 > st update <type> <ticket> <pkg> <version> <branch> <user>  --changelog "<changelog>"  -  Обновить тикет
 > st comment <ticket> [--comment "comment"] [--tag "<tag1>,..."] [--untag "<tag2>,..."] [--status <status>]  -  Добавить комментарий, проставить теги и статус
```

Поле type - это тип тикета из списка `release, feature, hotfix`. Все остальные поля достаточно интуитивно-понятны, кроме
поля user - это предполагаемый автор ветки (вычисляется на основании наиболее раннего коммита в ветке)

При желании в качестве подобной команды можно использовать плагин `yammy-st`.

### Хуки

В настоящий момент поддерживается только precommit гит-хук. Для его установки в корневом репозитории нужно добавить
конфиг `"config": { "installPrecommit": true }`.

Также можно создать дефолтные настройки прекоммит-хуков:

```
"config": {
	"settings": {
		"precommit": {
			"eslint: {
				"title": "eslint",
				"command": "eslint",
				"include": "\\.js$",
				"exclude": "\\.min.js$"
				"types": [
					"changed",
					"created",
					"renamedto"
				]
			}
		}
	}
} 
```

А также указать какие прекоммит-хуки надо запускать во всех пакетах:

```
"config": {
	"settings": {
		"default-precommit": [
			"eslint"
		]
	}
} 
```

В каждом отдельном пакете также нужно настроить конкретные скрипты, которые будут обрабатывать прекоммит хуки:

```
"config": {
	"precommit": [
		{
			"title": "eslint",
			"command": "eslint",
			"include": "\\.js$",
			"exclude": "\\.min.js$"
			"types": [
				"changed",
				"created",
				"renamedto"
			]
		}
	]
} 
```

или использовать объявленные в корневом package.json хуки:

```
"config": {
	"precommit": [
		"eslint"
	]
} 
```

Каждый объект в precommit - это описание скрипта, где command - это команда которая будет запущена, include - фильтр
имён файлов, exclude - исключающий фильтр файлов, types - список типов
событий `changed, created, deleted, renamed, renamedto`. Все файлы, которые пройдут фильтрацию будут добавлены в
качестве аргументов в команду
