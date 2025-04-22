# Static resource

Static resource — это файл или набор файлов, которые можно либо скачать из сети, либо захардкодить их содержимое прямо в спецификации, либо указать, что в этот файл надо записать значение секрета. Затем эти файлы можно смонтировать в заданный каталог любого [box](../../box.md).

У статических ресурсов нет последующей обработки после скачивания, поэтому нет возможности, например, скачать все одним архивом, распаковать его, и уже распакованные данные монтировать в бокс. Если вы хотите автораспаковку архивов, подумайте об использовании layer. Если вам нужна какая-то более сложная post обработка, ее можно сделать при помощи [init команд в box](../../box.md#init), но учтите, что вы, скорее всего, будете вынуждены скопировать ресурсы, что займет больше места на диске.

Каждый статический ресурс скачивается в отдельное специальное место в поде, а затем монтируется во все [box](../../box.md), где он указан в спецификации. Из-за того, что доставка ресурсов идет при помощи монтирования, есть некоторый набор ограничений на директорию `mount_point`. Нельзя монтировать в `"/"`, и `mount_point` не должны пересекаться. Поэтому, если у вас есть отдельный ресурс с бинарником приложения `app` и отдельный ресурс с конфигом `config.json`, вы не сможете смонтировать оба этих ресурса в одну директорию, более того, вы не сможете смонтировать `config.json` в поддиректорию приложения.

В качестве примера, вот такие пары `mount_point` **невалидны**: (`/my_app`, `/my_app`), (`/my_app`, `/my_app/config`).
Тем не менее, точки монтирования могут иметь общий префикс, поэтому вот эта пара **валидна**: (`/my_app/bin`, `/my_app/config`)

В деплое представлен следующей [proto схемой](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=5791549#L187-223):

##  Примеры использования {#examples}

### Основное {#main}

Чаще всего статические ресурсы используются для того, чтобы принести на под какие-то файлы с конфигами или какие-то данные в сыром виде.

Также статические ресурсы используются для записи секретов в файлы.

Статические ресурсы можно использовать для того, чтобы приносить бинарники своего приложения, но в таком виде это создает больше накладных расходов (в виде проверок целостности, которые можно отключить).

### Скачивание файлов {#download_files}

Чтобы скачать файлы, надо указать `download_method` для загрузки. Если `checksum` не пуста, содержимое будет верифицироваться каждые `check_period_ms`.

Есть несколько доступных методов загрузки:

#### Через произвольный url {#url}

Если вам не нужны никакие особые параметры запуска `sky get` (например `deduplicate hardlink`), то предпочтительно использовать этот метод.

Доступные протоколы: `http`, `https`, `rbtorrent`, `sbr`:

```yaml
static_resources:
- id: TestDownload
  verification:
    checksum: MD5:676b95c8c7b8c080c6725ac6fb1e014d
    check_period_ms: 180000
  url: rbtorrent:8b218e1e8a05c51864ef25ffb99df0d037ce91ad
```

`sbr:<sandbox resource id>` позволяет скачать ресурс из Sandbox, указав его ID с помощью торрентов. Время жизни ресурса будет продлеваться автоматически пока ресурс используется.

`rbtorrent:<torrent id>` позволяет скачать торрент по его ID, но следить за жизнью сидеров придётся самостоятельно.

`http`, `https` позволяет скачать произвольный файл, но нужно помнить, что:
* нужны соответствующие правила в firewall;
* более высокая нагрузка на сервер, раздающий файлы по http;
* нет гарантии (не указывая `checksum`) что разные скачивания файла не приведут к разному содержимому этого файла.

#### Через sky get с особыми параметрами {#sky_get}

Этот формат еще не поддержан в UI (такие static_resource будет невозможно редактировать через UI).

```yaml
static_resources:
- id: TestDownload
  verification:
    checksum: MD5:676b95c8c7b8c080c6725ac6fb1e014d
    check_period_ms: 180000
  sky_get:
    resid: rbtorrent:8b218e1e8a05c51864ef25ffb99df0d037ce91ad
    deduplicate: no
```

### Как указать ресурсы для загрузки через UI {#ui}

Ресурсы для загрузки можно указать через UI, но есть некоторый набор ограничений:

1. В UI нельзя добавить ресурс отдельно от бокса, поэтому надо нажать `Add resource` в `Box`. Все одинаковые ресурсы из разных `Box` будут соединены в один ресурс.
1. К сожалению, в UI пока нет тонкой настройки ресурса.

### Запись произвольного содержимого в файл {#raw_data}

Для записи произвольного содержимого в файл надо объявить static resource с опцией files:

```yaml
static_resources:
- id: TestFiles
  verification:
    checksum: 'EMPTY:'
    check_period_ms: 180000
  files:
    files:
    - file_name: raw_file1.txt
      raw_data: "raw_data1"
    - file_name: raw_file2.txt
      raw_data: "raw_data2"
```

### Запись секрета в файл {#secret}

Предварительно необходимо добавить секрет и delegation_token в спеку RS/MCRS.

Для записи секрета в файл надо объявить static resource с опцией files:

```yaml
static_resources:
- id: TestFiles
  verification:
    checksum: 'EMPTY:'
    check_period_ms: 180000
  files:
    files:
    - file_name: secret_file1.txt
      secret_data:
        id: MyPerfectSecret1
        alias: "<SECRET_UUID1>:<SECRET_VERSION1>"
    - file_name: secret_file2.txt
      secret_data:
        id: MyPerfectSecret2
        alias: "<SECRET_UUID2>:<SECRET_VERSION2>"
        decode_base64: true
```

Опция `decode_base64` позволяет декодировать значение из `base64` перед записью в файл.

Для указания пути, по которому должен быть виден файл, нужно [указать](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=r7652645#L827) в `TBox` ссылку на static resource и директорию [mount_point](../../static-resources.md).

### Запись всех значений секрета в файл как в ya vault get version {#multisecret}

Предварительно необходимо добавить секрет и delegation_token в спеку RS/MCRS:

Для записи всех секретов из одного alias надо объявить static resource с опцией files:

```yaml
- id: TestFiles
  verification:
    checksum: 'EMPTY:'
    check_period_ms: 180000
  files:
    files:
    - file_name: all_secrets.json
      multi_secret_data:
        format: json
        secret_alias: "<SECRET_UUID>:<SECRET_VERSION>"
```

Поддерживаются форматы: json, java (без перекодировки в latin1), yaml.

Примерный результат выглядит вот так:

```bash
root@sas3-7384-1:/$ cat all_secrets.json
{
    "MyPerfectSecret":"value",
    "MySecondPerfectSecret":"second_value"
}

root@sas3-7384-1:/$ cat all_secrets.java
MyPerfectSecret = value
MySecondPerfectSecret = second_value

root@sas3-7384-1:/$ cat all_secrets.yaml
MyPerfectSecret: value
MySecondPerfectSecret: second_value
```

## Виртуальный диск статического ресурса {#virtual-disk-ref}

{% include notitle [virtual-disk-static-resources](../../../../_includes/virtual-disk-static-resources.md) %}