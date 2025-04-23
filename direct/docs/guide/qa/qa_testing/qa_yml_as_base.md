##  Yml для QA

# Важные ссылки: { #qa_yml_links }
Проект dna: [https://a.yandex-team.ru/arc_vcs/adv/frontend/services/dna](https://a.yandex-team.ru/arc_vcs/adv/frontend/services/dna)

Все ямлы по проекту лежат в директории `/dna/tests/hermione/suites/functional`

Документация arc: [https://docs.yandex-team.ru/devtools/src/arc/workflow#workflow](https://docs.yandex-team.ru/devtools/src/arc/workflow#workflow)

Palmsync: [https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync/docs/quick-start.md](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync/docs/quick-start.md)

Дока palmsync: [https://github.yandex-team.ru/tools/palmsync-unit](https://github.yandex-team.ru/tools/palmsync-unit)

Кейсы в TestPalm: [https://testpalm.yandex-team.ru/dna](https://testpalm.yandex-team.ru/dna)


# Что такое Ямлик { #qa_yml_wit }
Ямлы - это файл формата *.yml, содержащие тестовые сценарии проверок (действия и проверки их результата), язык разметки [yaml](http://www.yaml.org/)

Сценарии из этого файла синхронизируются в дальнейшем с [Testpalm](https://testpalm.yandex-team.ru/dna) при помощи [palmsync](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync/docs/quick-start.md)

Palmsync валидирует правильность разметки файлов .yml с тест-кейсами, правила разметки описаны [ в доке palmsync](https://github.yandex-team.ru/tools/palmsync-unit#содержимое-файлов)

 
# Написание Yml { #qa_yml_write }
1. Если нет тикета на написание ямлов, то завести на себя тикет по [шаблону](https://st.yandex-team.ru/createTicket?template=6066&queue=DIRECT), перевести тикет в работу/In progress

2. Открыть [проект dna](https://a.yandex-team.ru/arc_vcs/adv/frontend/services/dna) в IDE

3. Отвести ветку по ключу тикета (например, `DIRECT-123456`)

4. Внести изменения в существующие ямлы или создать новые

4.1. Создание нового файла:

- В директории `\dna\tests\hermione\suites\functional\` находим папки имеющие логическое и функциональное отношение к вашим тест-кейсам и создаем там файл с расширением `*.hermione.yml`.
 
- Если подходящих папок нет, то надо их создать
 
- Название файла должно называться единообразно, учитывая смысл проверки

Например, кейсы на создание РМП будут находиться в папке `campaign` в файле `createRmpCampaign.hermione.yml`

4.2. Содержание файла:

- Основные поля, которые мы используем: `feature`, `specs`, `do`, `assert`, `tags`, `beforeEach`, `afterEach`

Описание содержимого файлов и как они синкаются в TestpPalm описано [ в доке](https://github.yandex-team.ru/tools/palmsync-unit#содержимое-файлов)

Пример хорошего ямла: [клик](https://a.yandex-team.ru/arc_vcs/adv/frontend/services/dna/tests/hermione/suites/functional/campaign/createTgoCampaign.hermione.yml)

4.3. Теги

- Все используемые в нашем проекте теги хранятся в файле `whitelist-tags.js`

- Регрессионным кейсам для асессоров проставляем тег `regression`

- Добавить необходимые теги фичи, страницы или роли для быстрого поиска кейсов в TestPalm

- по соглашению о тегах, в yml-файлах dna теперь пишем их вверху файла

4.4. Тестовые данные
 
- В начале каждого кейса создаем кампанию/группу/объявление необходимые для дальнейших проверок

- В конце каждого кейса все созданные в начале объекты нужно удалить

- Если для написания кейсов вам понадобилось создать новую кампанию/группу/объявление (!!не рекомендовано!!!), то нужно **защитить данные от удаления скриптом**

Занести их в [таблицу](https://wiki.yandex-team.ru/users/l-jul/tablica---kampanijj-asessora-ts---prod/) (отметить только принципиальные данные)
 
Занести их в [скрипт](https://a.yandex-team.ru/arc_vcs/direct/qa/direct-web-tests/src/main/java/ru/yandex/autotests/direct/web/cleandata/CleanTestDataForAssessorsTest.java) для защиты от очистки данных

И подготовить аналогичные данные в проде для переналивки баз

4.5. Можно запустить локально команду валидации ямлов, подробнее [в доке palmsync](https://github.yandex-team.ru/tools/palmsync-unit#readme)


5. Создать PR, перевести тикет в статус "в код ревью", призвать ревьювера посмотреть изменения
