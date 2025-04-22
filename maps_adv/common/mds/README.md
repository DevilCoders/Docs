# Клиент к MDS

Полное описание АПИ MDS [тут](https://wiki.yandex-team.ru/mds/dev/protocol/).

## Создание клиента
```python
mds_client = await MDSClient(
    url="http://storage-int.mdst.yandex.net:1111",
    namespace="business",
    tvm_client=tvm_client,
    tvm_source="doorman",
    tvm_destination="mds",
)
```


## Загрузка изображения по url
[Ручка](https://wiki.yandex-team.ru/mds/dev/protocol/#put) АПИ MDS

```python
    got = await mds_client.upload_file(
        file_content=b'some file content',
        file_name="test_file.csv",
        expire="1d",
    )

    assert got == UploadFileResult(download_link="http://storage-int.mdst.yandex.net:1111/get-business/test_file.csv")
```
