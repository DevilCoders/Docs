# Layer

Layer — это архив с произвольной частью файловой системы. Файловая система любого [volume](../../volume.md) (в том числе rootfs volume [box](../../box.md)) собирается последовательным наслоением содержимого всех архивов, которые заданы в спецификации конкретного `volume/box`.

Например, если в первом архиве лежит следующая файловая система:

```bash
fs
└── dir
    ├── file1
    └── file2

1 directory, 2 files
```

А во втором:

```bash
fs
├── dir
│   └── file2
└── dir_other
    └── file3

2 directories, 2 files
```

То итоговый результат будет:

```bash
fs
├── dir
│   ├── file1
│   └── file2
└── dir_other
    └── file3

2 directories, 3 files
```

При этом `/dir/file2` будет взят из того слоя, который наслаивался позже.
Порядок наслоения указывается в спецификации конкретного `volume/box` (в `layer_refs`). Слои наслаиваются **справа налево**, т.е. первый слой в списке будет наложен последним. Так сделано чтобы соответствовать `api porto`: `layers - layers, syntax: top-layer;...;bottom-layer`.

{% note warning %}

Но наложение не всегда работает так, на файлах могут стоять специальные атрибуты, [будьте внимательны](https://st.yandex-team.ru/RTCSUPPORT-5726#5e6fde9b41a0f221ddaabaac).

{% endnote %}

Если говорить более формально, то используется [Overlayfs](https://www.kernel.org/doc/Documentation/filesystems/overlayfs.txt). Layer, который вы указываете, скачивается ровно один раз, распаковывается в специальное место, а затем наслаивается на все `volume`, у которых он указан в спецификации.

Алгоритм мержа слоев (директорий, файлов, прав) описан на [https://www.kernel.org/doc/Documentation/filesystems/overlayfs.txt](https://www.kernel.org/doc/Documentation/filesystems/overlayfs.txt)

Подробнее про то, как собирать разные слои, можно прочитать [в документации porto](https://wiki.yandex-team.ru/porto/layers/).

В Деплое слой представлен следующей [proto схемой](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=7140819#L406-440):

## Примеры и частые ошибки {#examples}

### Основное {#main}

Layer чаще всего используется для того, чтобы приносить образ системы. Из-за того, что layer накладывается при помощи [Overlayfs](https://www.kernel.org/doc/Documentation/filesystems/overlayfs.txt), даже при наличии пяти [box](../../box.md), которые будут использовать этот слой, он скачается всего один раз и не будет пять раз скопирован, будут скопированы только файлы, который изменяются в run-time (по сути для всех файлов образа работает `CopyOnWrite`).

Также при помощи layer удобно приносить бинарники, который были собраны при помощи [ya package](https://wiki.yandex-team.ru/yatool/package/).

К сожалению, layer это **обязательно** архив, поэтому нельзя просто подставить ссылку на обычный файл или `rbtorrent` на много файлов. В противном случае система не опознает ваш файл и попробует его разархивировать как `.tar.xz` архив, и вы получите следующую ошибку:

```json
{
    "reason": "INVALID",
    "last_transition_time": {
        "nanos": 347243000,
        "seconds": 1585752003
    },
    "message": "InvalidValue(7):ImportLayer:/pod_agent/resources/default/layer/9c23f2c19c54f8ffd20184b126b1624f/downloaded/layer.tar.xz:InvalidValue:(Cannot detect archive /place/db/iss3/volumes/pod_wu7ehy72seipfeem_place/db/iss3/volumes/ISS-AGENT_cdNnM6hcS7T/pod_agent/resources/default/layer/9c23f2c19c54f8ffd20184b126b1624f/downloaded/layer.tar.xz compression by magic)",
    "status": "true"
}
```

Поэтому для "сырых" файлов надо использовать [static_resource](staticresource.md).

### Как указать в спеке {#url}

```yaml
# Через url
# Если вам не нужны никакие особые параметры запуска sky get (например deduplicate hardlink),
# то предпочтительно использовать этот метод
# Доступные протоколы: http, https, rbtorrent
layers:
- id: TestDownload
  url: rbtorrent:d57bb5d384702469a420e497ac67d8c14986277f
  checksum: MD5:195fbd0b6af168c26fcc67defabf8af5

# Через sky_get
# Этот формат еще не поддержан в UI (такие layer будет невозможно редактировать через UI)
layers:
- id: TestDownload
  sky_get:
    resid: rbtorrent:d57bb5d384702469a420e497ac67d8c14986277f
    deduplicate: no
  checksum: MD5:195fbd0b6af168c26fcc67defabf8af5
```

Также это можно сделать в UI, но есть небольшое отличие: в UI нельзя добавить layer отдельно от бокса, поэтому надо нажать `Add layer` в `Box`.

Тем не менее, все одинаковые layer из разных `Box` будут соединены в один layer.

При этом в UI для box вам всегда обязательно указывать `Base layer`, его можно выбрать из набора дефолтных, либо указать свой, либо указать ссылку на docker image, который будет преобразован в набор слоев.

## Связь с docker {#doker}

Под капотом [docker image](https://docs.docker.com/engine/docker-overview/#docker-objects) используется такой же алгоритм [Overlayfs](https://www.kernel.org/doc/Documentation/filesystems/overlayfs.txt).

Поэтому при подстановке docker ваш образ преобразовывается в набор слоев, и все они добавляются в спецификацию пода.

## Механизм сохранения исходного файла layer после импорта в порто {#save-layers}

На стороне pod-agent мы реализовали функциональность по сохранению исходных файлов (нераспаковыанных архивов) layers после импорта в porto.
Функциональность доступна с [релиза pod-agent  101](https://deploy.yandex-team.ru/docs/reference/pod-agent-releases#101-1).

Наверно многие из вас замечали следующую ошибку: ResourceDownloadError: Unable to receive resource info in 60 seconds.
Она вызвана тем, что сейчас layers в деплое доставляются следующим образом:
1. Скачивается пакет с ресурсом (.tar.gz/tar.zstd/etc файл)
2. Импортируется во внутреннее хранилище (при помощи porto)
3. Удаляется исходный файл
4. Далее из внутреннего хранилища доезжает до вас при помощи магии overlayfs

Удаление в пункте 3 вызывает проблему загрузки layers другими подами.
Сopier при помощи которого они загружаются при удалении исходного файла очень долго не снимает анонсы, а принудительно снять анонс дорогая операция, больше информации [тут](https://st.yandex-team.ru/SKYDEV-2333 ). Это приводит к проблеме с пропавшими пирами на раздачу torrent.
Единственным источником ресурсов в данном случае является sandbox/mds, что приводит к тому, что ресурсы дольше качаются на другие поды и идет большая нагрузка на sandbox/mds. В случае удаления ресурса из sandbox/mds его больше нельзя скачать и новые поды не могут подняться.

Поэтому для надежности было принято решение, что удаление исходных файлов layers это вредная оптимизация. И на текущий момент мы реализовали возможность отключения сохранения исходных файлов layers через UI.

Это позволит ускорить выкладку, так как torrent будут качаться с data locality и, то есть по возможности из максимально близкого соседа а не из хранилища где torrent хранится и ограничен на раздачу по IO.

Раздача копиром исходных файлов layers происходит в квоте хоста(disk io, net, cpu, mem), на котором располагается под

{% note warning %}

При сохранения исходных файлов layers есть минус в виде требования доп. места на диске для хранения layers.

{% endnote %}

### Дефолтная политика сохранения/удаления исходных файлов layers {#default-policy}

Политика применяется на все layer DeployUnit, где нет явного переопределения дефолтной политики.
![Пример](https://jing.yandex-team.ru/files/dkochetov/screenshot_21.png)
**None** - работает аналогично Remove. Является дефолтной политикой (политика которая не задана). Предназначена для миграции.
**Keep** - pod-agent не удаляет исходные файлы layer после импорта в porto.
**Remove** - pod-agent агент удаляет исходные файлы layer после импорта в porto.

### Переопределение дефолтной политики сохранения/удаления отдельного layer {#default-policy-update}

![Пример](https://jing.yandex-team.ru/files/dkochetov/screenshot_150.png)
**Default** - для layer применяется дефолтная политика сохранения/удаления layers (см.выше). 
**Keep** - pod-agent не удаляет исходный файл layer's после импорта в porto.
* Если в сервисе используется один пользовательский диск, то исходный файл layer сохраняется на этом диске.
* Если в сервисе используется несколько пользовательских дисков, то исходный файл layer сохраняется на диске, который прописан в virtual_disk_id_ref layer.

**Remove** - pod-agent удаляет исходные файлы layer после импорта в porto.

## Виртуальный диск слоя {#virtual-disk-ref}

В случае, если у вас больше одного диска, необходимо указать `virtual_disk_id_ref`, чтобы слой создавался в place нужного диска. Данный `virtual_disk_id_ref` должен совпадать с аналогичным полем в боксе и вольюме, из которого они собираются. Иначе спека не пройдет валидацию.

```yaml
layers:
- id: TestDownload
  ...
  virtual_disk_id_ref: 'disk-0'
```

[Пример полной спеки с использованием нескольких дисков.](https://deploy.yandex-team.ru/docs/concepts/pod/diskvolumerequests#primer-speki-s-ispolzovaniem-neskolkih-diskov)
