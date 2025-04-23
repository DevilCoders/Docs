# Использование курьера в nanny

## Ресурс с курьером

Курьер релизится в ресурсах [COURIER_BUNDLE](https://sandbox.yandex-team.ru/resources?type=COURIER_BUNDLE&limit=20&attrs=%7B%22released%22%3A%22stable%22%7D).

В списке файлов добавить новый sandbox-ресурс. Предполагаем, что рядом есть бандл с renderer, будем использовать ynode из него.

## Конфиг курьера

Предполагается, что конфиг курьера – ресурс нединамический и при его изменениях будут переналиты контейнеры. Курьер не умеет правильно обрабатывать ситуации, когда после изменения конфига не был перезапущен контейнер – например, если вы поправили конфиг на горячую.

Пример конфига приведен в [корневом readme](../README.md#пример-работы).

## Files

Во всех файлах с шаблонами и данными нужно отметить галочку "Is dynamic?":

![How to reach is_dynamic flag](./is_dynamic.png)

Теперь при обновлении только динамических ресурсов будет сделано действие, описанное в `Actions to be taken on dynamic resources update` вместо сборки нового контейнера.

## Instance init containers 

До курьера в prepare-скрипте могла быть распаковка архивов с шаблонами, например
```shell script
tar -xzf templates-desktop.tar.gz
tar -xzf templates-touch.tar.gz
```

Эту распаковку нужно удалить, она будет делаться самим курьером.

В prepare-скрипте добавить
```shell script
tar -xf courier.tar.gz

DEBUG=* FS_DEBUG=1 ./ynode/bin/ynode ./courier/build/bin/courier --config ./courier.json prepare
```

## Instance containers (sections)

Предлагается запускать курьера под nice, чтобы он отдавал CPU рендереру под нагрузкой:
```shell script
nice ./ynode/bin/ynode ./courier/build/bin/courier --config ./courier.json watch
```

В переменных окружения рекомендуется включить debug:
```
DEBUG=*
FS_DEBUG=1
```

Дебажного вывода немного – не более 10кб на каждый вызов /update, он пишется в stderr.

Unistat-ручки у курьера нет, есть планы на нее: https://st.yandex-team.ru/FEI-12481

Reopenlog action не поддерживается.

## Actions to be taken on dynamic resources update

Добавить новый action: HTTP_GET, порт из конфига, путь `/update`.

## Recipes

Рекомендуется оставить рецепт для безопасного деплоя – с `prepare_operating_degrade_level<1` и `operating_degrade_level<1` и добавить рецепт для деплоя только динамических ресурсов с `prepare_operating_degrade_level=1` и `operating_degrade_level=1`.

При обновлении динамических ресурсов в стадии prepare не происходит ничего. Соответственно, в рецепте на раскатку динамических ресурсов можно поставить `prepare_operating_degrade_level=1`.

Сами ресурсы начинают скачиваться на стадии activate. Поскольку при обновлении курьером инстанс остается в строю, можно катить изменение с `operating_degrade_level=1`.

## Tickets integration

Для ресурсов с шаблонами и данными выставить рецепт для динамических шаблонов.

**Если в сервисе в scheduling policy включен maintain active trunk, то использовать рецепты с degrade_level=1 нельзя**. Может получиться так, что два изменения – нединамических ресурсов, а затем динамических – покатятся рецептом с `degrade_level=1` и приведут к даунтайму сервиса. Сделать универсальный рецепт, который различал бы эти случаи, нельзя: https://st.yandex-team.ru/RTCSUPPORT-4826

