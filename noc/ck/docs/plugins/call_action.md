# call - вызвать python-функцию

Это надо использовать, если другие способы получить желаемое исчерпаны:

1. найти функциональность в остальных готовых экшенах,
2. если там не нашлось подходящего, успешно [заказать у NOCDEV реализацию недостающей](https://forms.yandex-team.ru/surveys/72658/?task_type=feature&task_priority=normal&project=_project_automation&title=%D0%A6%D0%9A%20%E2%80%93%C2%A0%D0%BD%D1%83%D0%B6%D0%B5%D0%BD%20%D1%8D%D0%BA%D1%88%D0%B5%D0%BD&problem=%D0%A0%D0%B5%D1%88%D0%B0%D1%8E%20%D0%B7%D0%B0%D0%B4%D0%B0%D1%87%D1%83%20%D1%82%D0%B0%D0%BA%D1%83%D1%8E-%D1%82%D0%BE%20%D0%B2%D0%BE%D1%82%20%D1%8D%D1%82%D0%B8%D0%BC%20%D1%81%D1%86%D0%B5%D0%BD%D0%B0%D1%80%D0%B8%D0%B5%D0%BC,%20%D0%BD%D0%BE%20%D0%BD%D0%B5%D0%BF%D0%BE%D0%BD%D1%8F%D1%82%D0%BD%D0%BE,%20%D0%BA%D0%B0%D0%BA%20%D1%81%D0%B4%D0%B5%D0%BB%D0%B0%D1%82%D1%8C,%20%D1%87%D1%82%D0%BE%D0%B1%D1%8B%20%D0%B4%D0%B6%D0%BE%D0%B1%D0%B0%20%D0%B4%D0%B5%D0%BB%D0%B0%D0%BB%D0%B0%20%D1%8D%D1%82%D0%BE) функциональности в нужный срок.

Ограничения:

1. нельзя реализовывать в сценариях, [отправленные](/ck/concept/cli) через `ck-cli create-declarative` – потому что пушить можно только yaml, но не питон, который придётся коммитить:
2. потому что все такие коллбеки, реализованные для сценария, должны находиться [**в репозитории ЦК**](https://noc-gitlab.yandex-team.ru/nocdev/noc-ck/-/tree/master/app/declarative) рядом с ямловым текстом сценария – но звать можно любые колбеки из любого в той директории.

Пример, как этим пользоваться [в сценарии](https://noc-gitlab.yandex-team.ru/nocdev/noc-ck/-/blob/master/app/declarative/huawei_spine_reboot.yml#L105):

```yaml
#...
actions_module: switch_upgrade
actions:
#...
      # if reboot was done as part of upgrade SW process actual SW version is set in RT
      - name: racktables update sw version
        call: rt_update_sw_version
#...
```

Пример, как реализацию для такого экшена написать в [питонячьем модуле](https://noc-gitlab.yandex-team.ru/nocdev/noc-ck/-/blob/master/app/declarative/switch_upgrade.py#L6) – с такой же сигнатурой:

```python
import typing

from app import config, models2, racktables

async def rt_update_sw_version(
    app: typing.Mapping[str, typing.Any], hostname: str, _ctx: models2.Context2
) -> bool:
    cfg = config.get(app)
    async with racktables.async_connect(
        cfg, mode=racktables.ConnectionMode.READ_WRITE
    ) as rt:
        object_id = await rt.call.findObjectByName(hostname)
        await rt.call.do_updateSwVersion(object_id)
    return True

#...
```

Иногда хочется работать с данными, лежащими в контексте сценария (именованных переменных, доступных в его тексте), это можно делать через прямую работу с `_ctx`:

```python
async def ruin_some_ctx_var(
    app: typing.Mapping[str, typing.Any], hostname: str, _ctx: models2.Context2
) -> bool:
    _ctx["ruinee"] = "100500"
    return True
```

Если хочется позвать более одного `actions_module`, можно импортировать в модуле соседние файлы.
