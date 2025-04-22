# Что это?

Скрипт для генерации [дашборда Setcar comparison](https://grafana.yandex-team.ru/d/2L23CW6Mk/setcar-comparison-autogen-dont-edit-manually?orgId=1)

# Как пользоваться?

1. Открыть [JSON дашборда в графане](https://grafana.yandex-team.ru/d/2L23CW6Mk/setcar-comparison-autogen-dont-edit-manually?editview=dashboard_json&orgId=1), промотать вниз и запомнить поле version
2. В файле **generator.py** добавить новый процессинг и его метрики в **PROCESSINGS**, а в **VERSION** задать текущую версию дашборда
3. Запустить скрипт, скопировать содержимое полученного файла (generated.json) в grafana и сохранить дашборд
4. Закоммитить свои изменения

## NB

После названия процессинга можно указать процент, на который он включён сейчас на проде. Например, такой синтаксис говорит о том, что ``awesome_processing`` включён на 100%

```python
PROCESSINGS = {
    'awesome_processing #100': [...]
}
```
