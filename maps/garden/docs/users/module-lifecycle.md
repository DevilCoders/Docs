# Жизненный цикл модуля

## Написание модуля

* [Руководство по написанию нового модуля](module-creation.md).
* [Garden Module Developer Guide](https://wiki.yandex-team.ru/maps/dev/core/garden/developers-guide).

## Тестирование модуля

* [Как писать тесты](tests.md).

## Деплой модулей {#sedem}

Модули деплоятся через Sedem.
Основная документация по релизам Sedem [здесь](https://docs.yandex-team.ru/docs/sedem/releases).

После успешной автосборки модуля, можно увидеть коммит в списке кандидатов на релиз через команду `sedem release info <module path>`.

Пример кандидатов на релиз для модуля ymapsdf:

![](img/ymapsdf_candidates.png)

Для релиза в `testing`: `sedem release start <module path> <revision>` (отправляет модуль в тестовый контур Огорода)

После успешного релиза в тестинг будет создана релизная версия, которую можно увидеть в первой таблице `sedem release info <module path>`.
Обычно создание версии может занимать до нескольких минут.

Пример таблицы текущих версий модуля ymapsdf:

![](img/ymapsdf_releases.png)

Для релиза в `stable`: `sedem release step <module path> <version> stable` (отправляет модуль в стабильный контур Огорода).

Во время деплоя модуля в релизном окружении обновляются также и настройки модуля.

{% note warning "Attention" %}

Для деплоя модулей требуется дырка до продакшен Огорода.
Нужно вписать свою дев-машину в [правило в Панчере](https://puncher.yandex-team.ru/?id=5e8c566c9f563a721ff69383).

{% endnote %}

Для выпуска релизов модуля и для манипуляции с билдами необходимо [назначить](auth.md) роли пользователям.

Роли в Огороде выдаются через [IDM](https://idm.yandex-team.ru/system/garden_roles).

При необходимости модуль можно откатить командой:  `sedem release rollback <module path> testing|stable`

### Как делать хотфиксы

Команда `sedem release start` создаёт новую релизную ветку в `arc` по шаблону `releases/maps/garden-<module>-<major-version>`. Чтобы сделать хотфикс, нужно добавить коммит в нужную релизную ветку.

Прямого доступа к релизной ветке нет. Перенести существующий коммит в релизную ветку можно только с помощью Седема командой `sedem release hotfix -b <major-version> -a <commit>`.

Самое простое - сделать коммит в транк, и потом указать хэш коммита из транка.

Но этот способ не всегда срабатывает: может возникнуть конфликт при переносе коммита из транка в релизную ветку, а некоторые коммиты вообще не должны быть в транке.

Сложный способ, как добавить в релизую ветку произвольный коммит:

```bash
# Переключить рабочую копию на релизную ветку (локальное имя ветки может быть произвольным):
arc fetch releases/maps/garden-<module>-<major-version>
arc checkout -b any-local-branch-name releases/maps/garden-<module>-<major-version>

# Проделать все нужные манипуляции с кодом, закоммитить и запушить на сервер (удалённое имя ветки может быть произвольным):
arc commit -m "Fix an urgent bug"
arc push --set-upstream users/<user>/any-remote-branch-name

# В терминал будет напечатан хэш коммита, его и нужно скормить Седему:
ya tool sedem release hotfix -b <major-version> -a <commit>
```

Далее нужно подождать несколько минут, пока соберётся бинарник модуля, и зарелизить его в стейбл:
```
ya tool sedem release step <version> stable
```

Подробнее в доках по Седему [здесь](https://docs.yandex-team.ru/sedem/releases#release-hotfix).

## Склеивание модулей

## Разделение модулей

## Удаление модуля

{% note warning %}

Удалить модуль сложно. Если вы сомневаетесь в своих силах, обратитесь к
разработчикам Огорода. Тем более, иногда вам **придётся** к ним обращаться, так как
некоторые шаги могут быть выполнены только с их участием.

{% endnote %}

Для удаления модуля необходимо выполнить следующие шаги:

- Грепаем Аркадию на предмет упоминания модуля: `ya grep -i 'module_?name'`.
  Если в результатах было обнаружено нечто не попадающее под пункты этого
  подраздела, то необходимо пересмотреть указанную последовательность действий.

- Ставим даунтайм на мониторинги модуля. Для этого
  [здесь](https://juggler.yandex-team.ru/downtimes/) создаём даунтайм
  по фильтрам `host=maps_garden_<module_name>_stable` и
  `host=maps_garden_<module_name>_testing`

- Отключаем автоматическое создание билдов для данного модуля в UI Огорода в контурах `stable` и `datatesting`.

- _(автоматическое создание билдов должно быть выключено)_ Удаляем все созданные
  ранее билды из `stable` и `datatesting` контуров Огорода руками или скриптом:

    ```python
    import requests

    builds_url = f"http://core-garden-server.maps.yandex.net/modules/{module_name}/builds"
    for build in requests.get(builds_url).json():
        print(requests.delete(f'{builds_url}/{build["id"]}', headers={"Authorization":"OAuth <token>"}).json())
    ```

- Проверяем что в документации Огорода нет ссылок на описание (например на файл README.md) модуля. Если есть, удалить:
  - В файле [ya.make документации](https://a.yandex-team.ru/arc_vcs/maps/garden/docs/ya.make) в секции `DOCS_INCLUDE_SOURCES` – пути до файлов модуля
  - В [конфигурации документации](https://a.yandex-team.ru/arc_vcs/maps/garden/docs/users/toc.yaml) в секции "Описание модулей" – имена соответствующих разделв и пути до файлов модуля

- Удаляем код модуля из Аркадии

- _(билды должны быть удалены, код должен быть удалён)_ Удаляем модуль из стабильного Огорода
  и просим разработчиков Огорода удалить модуль из тестового Огорода

    ```
    curl -X DELETE -H "Authorization: OAuth <token>" -H "Content-Type: application/json" http://core-garden-server.maps.yandex.net/modules/<module_name>/?contour=stable
    curl -X DELETE -H "Authorization: OAuth <token>" -H "Content-Type: application/json" http://core-garden-server.common.testing.maps.yandex.net/modules/<module_name>/?contour=testing
    ```

- _(модуль должен быть удален)_ Просим разработчиков Огорода удалить оставшиеся версии
  модулей из [Кипариса](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/prod/modules).

- _(модуль должен быть удален)_ Удаляем нотификации и проверки в Juggler.
  Проверки удаляются вручную, поэтому об этом необходимо попросить в чате [Geo Helpline](https://t.me/joinchat/EI5uVEKnO40EkXbvaD7qkA).

- _(модуль должен быть удален)_ Если это deployment-модуль, который публикует
  датасет экстатика:

   * удаляем код генерации датасета (зачастую в соответствующем release-модуле)
   * удаляем соответствующие секции из конфига экстатика `maps/config/ecstatic`

- _(модуль должен быть удален)_ Проверьте, не был ли ваш модуль единственным
  потребителем какого-либо источника данных. Если да — следует удалить этот
  источник вместе с данными

- Закрываем тикеты в очереди [MAPSGARDENBUILD](https://st.yandex-team.ru/MAPSGARDENBUILD) с компонентом `modules-{module_name}`, а затем просим разработчиков Огорода удалить компонент.
