# Trendbox

[Документация trendbox](https://a.yandex-team.ru/arcadia/devtools/trendbox).

Написать в поддержку Trendbox CI можно через форму: https://nda.ya.ru/3UZzvU

## Коротко о главном

Trendbox - это CI, прародитель того CI, что используется в аркадии. Основной смысл в том, что он реагирует на изменения в репозитории с проектом (например новый ПР, изменение ветки master) и запускает скрипты, которые лежат в нашем проекте, на базе собранного нами LXC-контейнера. Сами скрипты пишутся на typeScript.

В данном проекте trendbox реагирует на:

-   Создание новых ПР и их изменение - в этом случае запускаются, тесты, собирается образ и выкатывается на стенд для тестирования ПР, пишет ссылку на него в задачу.
-   Изменение ветки master (новый коммит, мердж ПР и пр.) - в этом случае запускается создание нового релиза: запускаются тесты, добавляется релизный тэг, билдится образ и создается релизный тикет в YDeploy.

Подробнее о том как это выглядит при разработке описано в разделе [Процесс разработки](/docs/developmentProcess.md).

Сам конфиг trendbox лежит в корне проекта с названием `.trendbox.yaml`. О том как его редактировать можно почитать в документации к самому trendbox (ссылка выше).

Каждая задача trendbox (например билд образа) выполняется в sandbox.

## Управление задачами trendbox в sandbox

В каждую задачу можно попасть, кликнув по ссылке "Details" в ПР:
![trendboxTasksInPr](/docs/images/trendboxTasksInPr.png)
или в списке коммитов master:
![trendboxTasksInMaster](/docs/images/trendboxTasksInMaster.png)

Основные элементы управления sandbox-задачей: ![sandboxTask](/docs/images/sandboxTask.png)

Если задача сфэйлилась, как на картинке, то имеет смысл заглянуть в логи и там выбрать "step**script.log" - это и будут логи нашего скрипта. Если такого лога нет, значит задача сломалась где-то на этапе подготовки и нужно посмотреть в логи других шагов ("step**prepare.log", "step\_\_install.log" и пр.). Так же можно перезапустить задачу, скопировав ее.

## Сборка LXC-контейнера

Инструкция по созданию LXC-контейнера живет [здесь](https://a.yandex-team.ru/arcadia/devtools/trendbox/docs/formats/0.2/recipes/build-lxc.md?rev=r9761100).

-   Создать задачу в sandbox с типом TRENDBOX_CI_LXC_BETA
-   Выбрать "Advanced" -> "DNS" -> "dns64"
-   Выбираем "Components" Node.js и Docker.
-   В поле "Pre-install Node.js versions" вбиваем `[{ "node_js": "8.14.1", "npm": "6.4.1" }]`.
-   Выбрать "Ubuntu release" -> "xenial"
-   Заполнить Description как "LXC-контейнер для задач trendbox проекта rasp/morda_front"
-   В поле "Shell script to execute during final stage" вбиваем:

    ```bash
    apt-get update
    apt-get install -y yandex-fakeya \
                              python-pip

    mkdir ~/.pip
    echo "[global]" > ~/.pip/pip.conf
    echo "index-url = https://pypi.yandex-team.ru/simple/" >> ~/.pip/pip.conf
    echo "extra-index-url = https://pypi.python.org/simple" >> ~/.pip/pip.conf

    pip install awscli==1.19.112
    ```

-   Запускаем
