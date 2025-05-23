## Про взаимодействие с Коммандером
Чтобы минимизировать усилия на поддержку изменений в Коммандере договорились не создавать задачи в DIRECTCLIENT в тех случаях, когда "изменения не затрагивают Коммандер" (например изменяется/добавляется стратегия которой нет в Коммандере).
В тех случаях, когда изменения затрагивают Коммандер, призывать [Андрея Иванова](https://staff.yandex-team.ru/prof), он возьмёт на себя все необходимые в Коммандере действия.


## Требования к блокам
* Отсутствие проектоспецифичных деталей: от фреймворков (например, `react`), от серверсайда (формат данных), от платформы (`ajax`, `ipc` и т.п.), от блоков не из этой библиотеки
* Допускается зависимость от `i-bem`, `BEMHTML`, `lodash`, `moment`, `jquery`, `iget`, `bem-mvc` (только `view`-модели)
* Должен работать во всех поддерживаемых браузерах
* Должны присутствовать тесты
* Должна присутствовать документация
* Должен быть указан мейнтейнер
* Блок-визард должен быть без контейнера (попапа, диалогового окна и тд), так как в разных проектах блок может быть размещен в произвольных контейнерах, с собственным оформлением

Библиотека предполагает использование совместно с `islands v4.1.0`

## Требования к изменениям
* Вносимые изменения не должны ломать обратную совместимость
* Для всех вносимых изменений должен быть оформлен changelog
* Каждому релизу библиотеки должен соответствовать тег в git

## Процесс разработки
* Создаем отдельные задачи для проектов `direct`, `commander`. Устанавливаем связи между ними. Ставим им тег Direct&DC
* Создаем ветки под задачу в каждом проекте (`bricks`, `direct`, `commander`)
* Выбираем проект в котором будет происходить разработка (`direct`, `commander`)
* Вспоминаем, что есть и второй проект, и выясняем, что по этому поводу должно в нем произойти (должно ли изменение затронуть второй проект и как именно)
* В выбранном проекте подменяем выкаченную библиотеку `bricks` на полноценный репозиторий с новосозданной веткой.
* Вносим изменения одновременно в `bricks` и в выбранный проект. **Если в задаче требуется перенести блоки из `direct` - то нужен первый отдельный коммит с переносом блоков без изменений**
* После того как все готово, заполняем `CHANGELOG.md`, коммитим и пушим изменения в `bricks` (хотя коммитить можно и в процессе) и копируем hash последнего коммита
* В `package.json` **обоих проектов** вместо тега указываем hash последнего коммита в `bricks` (в `коммандере` можно указывать название ветки) и коммитим изменения в ветки проектов
* Создаем ревью в проекте (если там были изменения) и PR в `bricks`. Если были перенесены блоки из `direct` - то помимо PR нужно создать ревью в `upsource` в котором будет исключен первый коммит с переносом блоков, для того чтобы можно было посмотреть честный `diff`
* При внесении изменений по ревью нужно каждый раз менять hash последнего коммита `bricks` в `package.json` проектов (Если это не `commander` и в `package.json` не указано название ветки). **Если есть ревью в `upsource` - то ветку нельзя ребейзить, потому что после `rebase` у всех коммитов новый hash и в `upsource` потеряются коммиты добавленные в ревью**
* После того как ревью прошло коммитить в `bricks` не нужно, отдаем в тестирование в **двух проектах**

В коммандере это делается так:
1. Меняем версию брикс в app/package.json
2. npm install в корне проекта (ВНИМАНИЕ! не в app)
3. Коммитим
4. Отправляем PR (https://github.yandex-team.ru/direct/commander#pr) - появится ссылка на teamcity Details (https://jing.yandex-team.ru/files/alkaline/DIRECT-58271_pomenyala_versiyu_bricks_by_evolkowa__Pull_Request_357__directcommander_2017-01-16_14-24-09.png)
5. Пройдя по ссылке находим табик Artifacts - там ссылка на установщик, который нужно прикрепить к задаче и отдать в тестирование

* После успешного тестирования ребейзим ветку в `bricks`, просим принять PR, создаем новый `тег`. В проектах вместо hash коммита (либо название ветки) указываем новый тег

## Как добавить новый тег
* После принятия PR переключаемся в ветку `master` и подтягиваем новые изменения
* `npm version patch` - Поднимает версию в package.json (создает новый коммит) и создает новый тег
* `git push origin master` - Отправляем коммит с package.json
* `git push origin --tags` - Отправляем новый тег

## Makefile

```sh
make help                                   Выводит справку по командам makefile
make test                                   Запускает тесты на все блоки
make teamcity-test                          Запускает тесты на все блоки (выводит результаты в консоль в формате teamcity)
make dev-server-sandbox block=<BLOCK NAME>  Запускает песочницу для разработки указанного блока
make dev-server-tests block=<BLOCK NAME>    Запускает тесты для разработки указанного блока
make fixcss                                 Исправление css файлов в соответствии с принятым стилем
make fixsvg                                 Оптимизация svg
```
