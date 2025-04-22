### Ссылки

[Папка с проектом](https://datalens.yandex-team.ru/navigation/fr0eajjm1apy7-maps-core-mobile)

### Как добавить новый график

1. В папке с проектом нажать Создать/Чарт в editor/График (в задаче `UpdateDatalensChart` на текущий момент поддержаны только графики)
2. Сохранить
3. В `arcadia/maps/mobile/datalens/` создать папку для нового графика (имя может не совпадать) и создать в ней нужные .js файлы с кодом по именам вкладок
4. Добавить в `a.yaml` в `ci/actions/update-datalens-charts/flow-vars/charts` новый график. `chart_id` можно узнать из url графика в datalens - комбинация из 13 цифр и букв в конце url перед именем чарта
