## Виртуальный диск статического ресурса {#virtual-disk-ref}

В случае, если у вас больше одного диска, необходимо указать `virtual_disk_id_ref`, чтобы статический ресурс скачивался в place нужного диска. Данный `virtual_disk_id_ref` должен совпадать с аналогичным полем в боксе, к которому этот ресурс линкуется, и в вольюме, к которому ресурс монтируется. Иначе спека не пройдет валидацию.

```yaml
static_resources:
- id: 'my_resource'
  ...
  virtual_disk_id_ref: 'disk-0'
```

[Пример полной спеки с использованием нескольких дисков.](https://deploy.yandex-team.ru/docs/concepts/pod/diskvolumerequests#primer-speki-s-ispolzovaniem-neskolkih-diskov)
