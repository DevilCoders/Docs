# Балансерные панели для Woland

## Обновление бинаря, генерирующего панели
```
cd bin
ya make
./balancer_panels_bundle upload --attr target=arcadia/BuildBalancerPanelsBundle/bin
```

После успешной загрузки проходим по сгенерированной ссылке в задачу:
```
2020-03-20 18:30:59 INFO Uploading task #123123123 created: https://sandbox.yandex-team.ru/task/123123123
```

Релизим: нажимаем на кнопку Release справа от названия задачи (HTTP_UPLOAD_2), а потом во всплывающем окне еще раз Release.

Когда задача зарелизится, изменения автоматически подхватятся, а итоговые панельки можно увидеть по ссылке:
```
https://woland.yandex-team.ru
```

## Локальный запуск для генерации панелей

Поднимаем локальный sandbox: https://wiki.yandex-team.ru/sandbox/local-sandbox/.

Нужно скопировать в локальный sandbox ресурс с типом BALANCER_GENCFG_CONFIGS_L7_TGZ -- их скрипт скачивает и парсит.

Также нужно скопировать таск BUILD_WOLAND_PANELS_BUNDLE -- он запускает пайплайн.

```
cd bin
ya make
sandbox upload_binary ./balancer_panels_bundle --attr target=arcadia/BuildBalancerPanelsBundle/bin
```

Релизим бинарь (как описано выше).

После релиза запускаем в локальном sandbox таск с типом BUILD_WOLAND_PANELS_BUNDLE -- он и сгенерирует панели, в которые можно заглянуть и убедиться, что они корректные.

Дальше можно эти панели подложить в search/tools/woland/panels_balancer и запустить воланда с ними.

Если через браузер получится все панели просмотреть, то все хорошо.
