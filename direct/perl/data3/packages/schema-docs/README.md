# schema-docs
Библиотека для построение документации использующая в качестве данных schema.json

### Использование

Сперва необходимо подключить библиотеку к проекту, это можно сделать двумя способами
 - Склонировать
````js
    git clone git://github.yandex-team.ru/belyanskii/schema-docs.git
````

 - Подключить в make.js файле
````js
    getLibraries: function() {

        return {
            'schema-docs': {
                type: 'git',
                url: 'git://github.yandex-team.ru/belyanskii/schema-docs.git',
                branch: 'master'
            }
        };

    }
````

Далее создадим файл GNUmakefile или же добавим правило в существующий

````js
    .PHONY: schema-docs
    schema-docs::
    	node schema-docs/schema-docs-builder.js
````
<blockquote> P.S. - перед строкой - node schema-docs/schema-docs-builder.js - обязательно должен быть TAB! </blockquote>

После чего нам будет доступна команда make schema-docs.

### Принцип работы
#### Скрипт `schema-docs-builder.js`
 - Ищет все schema.json файлы
 - Создает папку с названием исходного schema.json файла ( прим. block.schema.json > block )
 - Преобразует schema.json данные по шаблону в bemjson
 - Строит bemjson добавляя ссылки на css/js и контент полученный из schema.json
 - Запускает создание декларации и последующую сборку страницы документации блока
 - Далее по аналогии со сборкой документации собирается страница каталога всех документаций по блокам и ложится в папку catalog

#### Блоки
 - Содержат блоки для отображения документации

#### package.json
 - Q - библиотека промисов для node.js
 - walk - рекурсивный обход папок и файлов
 - custom-logger - библиотека для вывода сообщений в консоль

#### GNUmakefile
 - Пример файла для работы с библиотекой
