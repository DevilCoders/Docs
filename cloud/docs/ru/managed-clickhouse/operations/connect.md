# Подключение к базе данных в кластере {{ CH }}

К хостам кластера {{ mch-short-name }} можно подключиться:

{% include [cluster-connect-note](../../_includes/mdb/cluster-connect-note.md) %}

К кластеру можно подключиться как с использованием шифрования — через порты `9440` для [clickhouse-client]({{ ch.docs }}/interfaces/cli/) и `8443` для [HTTP-интерфейса]({{ ch.docs }}/interfaces/http/), так и без него — через порты `9000` и `8123` соответственно.

## Настройка групп безопасности {#configuring-security-groups}

{% include [sg-rules](../../_includes/mdb/sg-rules-connect.md) %}

Настройки правил будут различаться в зависимости от выбранного способа подключения:

{% if audience != "internal" %}

{% list tabs %}

- Через интернет

  [Настройте все группы безопасности](../../vpc/operations/security-group-add-rule.md) кластера так, чтобы они разрешали входящий трафик с любых IP-адресов на порты 8443, 9440. Для этого создайте следующие правила для входящего трафика:

  * Диапазон портов — `8443`, `9440`.
  * Протокол — `TCP`.
  * Источник — `CIDR`.
  * CIDR блоки — `0.0.0.0/0`.
  
  На каждый порт создается отдельное правило.
  
- С ВМ в {{ yandex-cloud }}

  1. [Настройте все группы безопасности](../../vpc/operations/security-group-add-rule.md) кластера так, чтобы они разрешали входящий трафик из группы безопасности, в которой находится ВМ, на порты 8123, 8443, 9000, 9440. Для этого создайте в этих группах следующие правила для входящего трафика:

     * Диапазон портов — `8123` (или другой порт из перечисленных).
     * Протокол — `TCP`.
     * Источник — `Группа безопасности`.
     * Группа безопасности — если кластер и ВМ находятся в одной и той же группе безопасности, выберите значение `Текущая` (`Self`). В противном случае укажите группу безопасности ВМ.
     
     На каждый порт создается отдельное правило.
  
  1. [Настройте группу безопасности](../../vpc/operations/security-group-add-rule.md), в которой находится ВМ так, чтобы можно было подключаться к ВМ и был разрешен трафик между ВМ и хостами кластера.
  
     Пример правил для ВМ:
  
     * Для входящего трафика:
       * Диапазон портов — `22`.
       * Протокол — `TCP`.
       * Источник — `CIDR`.
       * CIDR блоки — `0.0.0.0/0`.

       Это правило позволяет подключаться к ВМ по протоколу SSH.

     * Для исходящего трафика:
        * Диапазон портов — `{{ port-any }}`.
        * Протокол — `Любой` (`Any`).
        * Назначение — `CIDR`.
        * CIDR блоки — `0.0.0.0/0`.
        
       Это правило разрешает любой исходящий трафик, что позволяет не только подключаться к кластеру, но и устанавливать на ВМ необходимые для этого сертификаты и утилиты.

{% endlist %}

{% else %}

{% list tabs %}

- Через интернет

  Настройте все группы безопасности кластера так, чтобы они разрешали входящий трафик с любых IP-адресов на порты 8443, 9440. Для этого создайте следующие правила для входящего трафика:

  * Диапазон портов — `8443`, `9440`.
  * Протокол — `TCP`.
  * Источник — `CIDR`.
  * CIDR блоки — `0.0.0.0/0`.
  
  На каждый порт создается отдельное правило.
  
- С ВМ в {{ yandex-cloud }}

  1. Настройте все группы безопасности кластера так, чтобы они разрешали входящий трафик из группы безопасности, в которой находится ВМ, на порты 8123, 8443, 9000, 9440. Для этого создайте в этих группах следующие правила для входящего трафика:

     * Диапазон портов — `8123` (или другой порт из перечисленных).
     * Протокол — `TCP`.
     * Источник — `Группа безопасности`.
     * Группа безопасности — если кластер и ВМ находятся в одной и той же группе безопасности, выберите значение `Текущая` (`Self`). В противном случае укажите группу безопасности ВМ.
     
     На каждый порт создается отдельное правило.
  
  1. Настройте группу безопасности, в которой находится ВМ так, чтобы можно было подключаться к ВМ и был разрешен трафик между ВМ и хостами кластера.
  
     Пример правил для ВМ:
  
     * Для входящего трафика:
       * Диапазон портов — `22`.
       * Протокол — `TCP`.
       * Источник — `CIDR`.
       * CIDR блоки — `0.0.0.0/0`.
       
       Это правило позволяет подключаться к ВМ по протоколу SSH.
  
     * Для исходящего трафика:
        * Диапазон портов — `{{ port-any }}`.
        * Протокол — `Любой` (`Any`).
        * Назначение — `CIDR`.
        * CIDR блоки — `0.0.0.0/0`.
        
       Это правило разрешает любой исходящий трафик, что позволяет не только подключаться к кластеру, но и устанавливать на ВМ необходимые для этого сертификаты и утилиты.

{% endlist %}

{% endif %}

{% note info %}

Вы можете задать более детальные правила для групп безопасности, например, разрешающие трафик только в определенных подсетях.

Группы безопасности должны быть корректно настроены для всех подсетей, в которых будут размещены хосты кластера. При неполных или некорректных настройках групп безопасности можно потерять доступ к кластеру.

{% endnote %}

Подробнее о группах безопасности см. в разделе [{#T}](../concepts/network.md#security-groups).

## Получение SSL-сертификата {#get-ssl-cert}

Чтобы использовать шифрованное соединение, получите SSL-сертификат.

{% list tabs %}

- Linux (Bash)

  Выполните команды:

  {% include [install-certificate](../../_includes/mdb/mch/install-certificate.md) %}

{% if audience != "internal" %}

- Windows (PowerShell)

  1. Скачайте и импортируйте сертификат:
      ```powershell
      mkdir -Force $HOME\.clickhouse; `
      (Invoke-WebRequest https://{{ s3-storage-host }}{{ pem-path }}).RawContent.Split([Environment]::NewLine)[-31..-1] `
        | Out-File -Encoding ASCII $HOME\.clickhouse\{{ crt-local-file }}; `
      Import-Certificate `
        -FilePath  $HOME\.clickhouse\{{ crt-local-file }} `
        -CertStoreLocation cert:\CurrentUser\Root
      ```

  1. Подтвердите согласие с установкой сертификата в хранилище «Доверенные корневые центры сертификации».

{% endif %}

{% endlist %}

{% include [ide-ssl-cert](../../_includes/mdb/mdb-ide-ssl-cert.md) %}

## Подключение из графических IDE {#connection-ide}

{% include [ide-environments](../../_includes/mdb/mdb-ide-envs.md) %}

Подключаться из графических IDE можно только к хостам кластера в публичном доступе с использованием SSL-сертификата. Перед подключением [подготовьте сертификат](#get-ssl-cert).  

{% list tabs %}

- DataGrip

  1. Создайте источник данных:
     1. Выберите в меню **File** → **New** → **Data Source** → **{{ CH }}**.
     1. На вкладке **General**:
        1. Укажите параметры подключения: 
           * **Host** — FQDN любого хоста {{ CH }} или один из [особых FQDN](#auto);
           * **Port** — `{{ port-mch-http }}`;
           * **User**, **Password** — имя и пароль пользователя БД;
           * **Database** — имя БД для подключения.
        1. Нажмите ссылку **Download**, чтобы загрузить драйвер соединения.
     1. На вкладке **SSH/SSL**:
        1. Включите настройку **Use SSL**.
        1. Укажите путь к файлу [SSL-сертификата для подключения](#get-ssl-cert).
  1. Нажмите ссылку **Test Connection** для проверки подключения. При успешном подключении будет выведен статус подключения, информация о СУБД и драйвере.
  1. Нажмите кнопку **OK**, чтобы сохранить источник данных.

- DBeaver

  1. Создайте новое соединение с БД:
     1. Выберите в меню **База данных** пункт **Новое соединение**.
     1. Выберите из списка БД **{{ CH }}**.
     1. Нажмите кнопку **Далее**.
     1. Укажите параметры подключения на вкладке **Главное**:
        * **Хост** — FQDN любого хоста {{ CH }} или один из [особых FQDN](#auto);
        * **Порт** — `{{ port-mch-http }}`;
        * **БД/Схема** — имя БД для подключения;
        * В блоке **Аутентификация** укажите имя и пароль пользователя БД.
     1. На вкладке **Свойства драйвера**:
        1. Нажмите **Скачать** в новом окне с приглашением скачать файлы драйвера.
        1. Укажите параметры [для SSL-соединения](#get-ssl-cert) в списке свойств драйвера:
           * `ssl:true`;
           * `sslrootcert:<путь к файлу SSL-сертификата для подключения>`.
  1. Нажмите кнопку **Тест соединения ...** для проверки подключения. При успешном подключении будет выведен статус подключения, информация о СУБД и драйвере.
  1. Нажмите кнопку **Готово**, чтобы сохранить настройки соединения с БД.

{% endlist %}

## Примеры строк подключения {#connection-string}

{% include [conn-strings-environment](../../_includes/mdb/mdb-conn-strings-env.md) %}

Вы можете подключаться к хостам кластера {{ CH }} в публичном доступе только с использованием SSL-сертификата. Перед подключением [подготовьте сертификат](#get-ssl-cert).

В примерах ниже предполагается, что сертификат `{{ crt-local-file }}`:
* расположен в директории `{{ crt-local-dir }}` — для Ubuntu;
* импортирован в хранилище доверенных корневых сертификатов — для Windows.

Подключение без использования SSL-сертификата поддерживается только для хостов, находящихся не в публичном доступе. В этом случае трафик внутри виртуальной сети при подключении к БД шифроваться не будет.

{% include [see-fqdn-in-console](../../_includes/mdb/see-fqdn-in-console.md) %}

{% include [mch-connection-strings](../../_includes/mdb/mch-conn-strings.md) %}

При успешном подключении к кластеру и выполнении тестового запроса будет выведена версия {{ CH }}.

## Автоматический выбор доступного хоста {#auto}

Чтобы вручную не подключаться к другому хосту, если текущий станет недоступен, можно использовать адрес вида:

* `c-<идентификатор кластера>.rw.{{ dns-zone }}` для подключения к доступному хосту кластера.

* `<имя шарда>.c-<идентификатор кластера>.rw.{{ dns-zone }}` для подключения к доступному хосту [шарда](../concepts/sharding.md).

Если хост, на который указывает этот адрес, станет недоступен, может быть небольшая задержка, прежде чем адрес начнет указывать на другой доступный хост.
