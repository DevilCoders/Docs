# Релизы Левитана

В данном документе описаны договоренности по релизам левитана для поддержания стабильного релизного цикла.

### Как договорились выпускать релизы левитана:

1) Для тикета из очереди MARKETFRAMEWORK реализуем изменения в отдельной ветке.
2) Проходим code review пулл реквеста.
3) Выпускаем canary версию сборки левитана из ветки, созданной в пункте 1. [Подробнее](https://a.yandex-team.ru/arc_vcs/market/front/apps/levitan/CONTRIBUTING.md#canary-релиз), как собрать canary версию. 
4) Создаем тикет MARKETPARTNER с внедрением новой версии левитана, проставляя в зависимостях package.json канареечную версию, выпущенную в пункте 3.
5) Доводим тикет MARKETPARTNER до статуса "Проверено" (ПР готов к релизу, code review пройдено, регресс разобран, стенд протестирован).
6) Вмердживаем ПР Левитана в trunk и выпускаете новую версию левитана. Подробнее выпуске новой версии левитана можно узнать [здесь](https://a.yandex-team.ru/arc_vcs/market/front/apps/levitan/CONTRIBUTING.md#reliz-versii-levitan-v-npm).
7) Меняем версию с канареечной на выпущенную версию левитана в ветке тикета MARKETPARTNER в package.json.
8) Релизим MARKETPARTNER тикет.

### Какую проблему это решает:
**Как было**: После успешного код ревью пулл реквеста в левитан, этот пулл реквкест сразу мерджился в trunk левитана, и выпускалась новая версия левитана.

**В чем была проблема**: В отсутствии проверки на интеграцию выпущенной версии Левитана с ПИ, существует вероятность что-то сломать, что заблокирует обновление Левитана в ПИ.
