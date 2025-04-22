# Taxi ML в Нирване
Здесь собран vh3 код регулярных процессов Taxi ML в Нирване. Архитектура основана на ml/zeliboba/nirvana.

# common
Различные константы и общие вещи об инфре и моделях.

## Как обновить операцию
1. Меняем версию операции (если этого не сделать, то в нирване поведение не изменится). Это строка вида:
```python
@vh3.decorator.autorelease_to_nirvana_on_trunk_commit(
    version='https://nirvana.yandex-team.ru/alias/operation/get_maneuvers_yql/0.0.2', <------ CHANGE VERSION HERE
    nirvana_quota="taximl",
    ya_make_folder_path="taxi/ml/telemetry/operations",
)
```
2. Меняем код самой операции, т.е. обновляем ее поведение.
3. Открываем PR, ждем тесты. Посмотреть прогресс графа тестов можно в CI->sandbox->stderr.log. Если граф долго не шедулится и sandbox упал по таймауту или по каким-либо другим причнам CI красный, а граф на самом деле зеленый - можно просто приложить его в коммент PR.
4. Теперь можно релизить графы. Для этого нужно на [странице релизов графов](https://a.yandex-team.ru/projects/taximl/ci/releases/timeline?dir=ml%2Ftaximl%2Ftaximl_graphs&id=release-graphs) прожать `Run Release`. 

# graphs

Описания графов, которые выкатываются в нашу [библиотеку](https://nirvana.yandex-team.ru/browse?selected=11171388). 
[Страница релизов](https://a.yandex-team.ru/projects/taximl/ci/releases/timeline?dir=ml%2Ftaximl%2Ftaximl_graphs&id=release-my-graphs)

## Как обновить графы?
1. Обновляем код нужных графов
2. Проверяем, что графы все еще собираются командой 
```bash
cd taxi/ml/nirvana/graphs/autopack
ya make -r -j32
VH3_DEV=1 ./graphs draft-all
```
3. Мерджимся
4. Идем на [страницу релизов](https://a.yandex-team.ru/projects/taximl/ci/releases/timeline?dir=ml%taximl%2Ftaximl_graphs&id=release-my-graphs) и прожимаем `Run Release`

**NB** При добавлении нового графа его нужно обязательно добавить в `taxi/ml/nirvana/graphs/conf.yaml`

## graphs/*
Код графов на vh3. Тут можно поменять старые графы и добавить новые (про новые см. предыдущий пункт)

Собирает бинарь, который отвечает за релиз графов. С помощью него можно драфтить графы. Пример:
```bash
VH3_DEV=1 ./graphs draft telemetry_daily_predictions
```

## Пеерезд на vh3
Пример переезда графа на vh3, а также некоторые полезные команды по запуску и тестированию графа собраны здесь:
https://wiki.yandex-team.ru/taxi/ml/valhalla3-regular-processes-migration/
