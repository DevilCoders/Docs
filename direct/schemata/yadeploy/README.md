# Сущности в Я.Деплое


## Релизные правила

Автоматизации по массовому дампу, загрузке и сравнению файлов с Я.Деплоем пока нет.

Файлы желательно называеть `<id правила>.release-rule.yaml`

В интерфейсе релизные правила смотреть на вкладке Releases, например <https://deploy.yandex-team.ru/stage/direct-logviewer-test/releases>

Список релизных правил конкретного стейджа:
```
dctl list release_rule --stage direct-chassis-prod
```

Записать в yaml-файл определение релизного правила:
```
dctl get release_rule direct-chassis-prod-rule > direct-chassis-prod-rule.release-rule.yaml
```

Создать релизное правило по yaml-файлу:
```
dctl put release_rule direct-chassis-prod-rule-yapackage.release-rule.yaml
```

Документация по релизным правилам: <https://wiki.yandex-team.ru/deploy/docs/concepts/release-integration/#primerypolzovatelskixscenariev>

