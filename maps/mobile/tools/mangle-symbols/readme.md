https://swiftversion.net/ - соответствие версии xcode и swift

### Сборка с использованием swift-llvm

Для сборки запустить  ```./build_mangler.sh```. В результате по пути `maps/mobile/tools/mangle-symbols/tools-mangle-symbols` будет собран и протестирован манглер.

### Релиз новой версии
1. Открыть [релизы манглера в CI](https://a.yandex-team.ru/projects/maps-core-mobile-arcadia-ci/ci/releases/timeline?dir=maps%2Fmobile&id=release-mangler)
2. Запустить новый релиз
3. По окончанию открыть релиз, в задаче `Build mangle symbols` найти ресурс с собранным манглером
4. Обновить id ресурса в `maps/mobile/tools/packages_generator/lib/templates/constants.py`.

