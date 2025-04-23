# Клиент к Аватарнице

Полное описание АПИ Аватарницы [тут](https://wiki.yandex-team.ru/mds/avatars).

## Создание клиента
```python
avatars_client = await AvatarsClient(
    url="http://avatars-int.mdst.yandex.net:13000",
    namespace="adv-clients-mailing",
    tvm_client=tvm_client,
    tvm_source="scenarist",
    tvm_destination="avatars",
)
```


## Загрузка изображения по url
[Ручка](https://wiki.yandex-team.ru/mds/avatars/#put) АПИ Аватарницы

```python
    got = await avatars_client.put_image_by_url(
        image_url="http://path-to-image.png",
        image_name="test-yandex-logo",
    )

    assert got == {
        "group-id": 603,
        "meta": {
            "Faces": [[492, 134, 413, 413]],
            "OldPornoProbability": 0.5294117647058824,
            "PortraitType": "PT_MAIN_PORTRAIT",
            "orig-size": {"x": 1024, "y": 640}
        },
        "sizes": {
            "orig": {
                "height": 640,
                "path": "/get-avatars-namespace/603/green-leaves/orig",
                "width": 1024
            },
            "sizename": {
                "height": 200,
                "path": "/get-avatars-namespace/603/green-leaves/sizename",
                "width": 200
            }
        }
    }
```