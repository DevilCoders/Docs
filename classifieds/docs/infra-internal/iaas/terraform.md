# Terraform

## Настраиваем окружение
1. Terraform версии v1.0.3. Взять можно с [зеркала от Yandex Cloud](https://hashicorp-releases.website.yandexcloud.net/terraform/).
2. Скачиваем ключ от service account из [yav](https://yav.yandex-team.ru/secret/sec-01edxy4am1ke19n2k3tt6dcbxs/explore/versions). Путь до ключа нужно указать в `env YC_SERVICE_ACCOUNT_KEY_FILE`. Например, `YC_SERVICE_ACCOUNT_KEY_FILE=/Users/spooner/key.json`
3. Прописываем env-переменную `TF_VAR_YANDEX_USER=<логин со staff>`, например `TF_VAR_YANDEX_USER=spooner`.
4. Клонируем [репозиторий](https://bb.yandex-team.ru/projects/YANDEX-CLASSIFIEDS/repos/terraform/browse)
5. Инициализируем нужные модули и подключаем PG в котором хранится state:

    `cd compute/<group>`
    `terraform init -backend-config="conn_str=postgres://terraform_backend:${password}@c-mdbtgdr5496mfe56fkvh.rw.db.yandex.net:6432/terraform_backend?binary_parameters=yes"`

    Пароль можно взять [тут](https://yav.yandex-team.ru/secret/sec-01ecss4z95efs5vsedw9jqn0xr/explore/versions). Строка подключения будет храниться в .terraform, который не должен попадать в репозиторий.

6. Для установки terraform-provider-conductor пока привозятся бинари как описано в официальной [доке](https://www.terraform.io/docs/language/providers/configuration.html#third-party-plugins). Последний релиз провайдера лежит в s3 в бакете `terraform-provider-conductor`. Его можно скачать в UI облака по [ссылке](https://yc.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/storage/buckets/terraform-provider-conductor)

    После скачивания его необходимо положить на локальный ноут по пути:

    mac os (Intel): `~/.terraform.d/plugins/github.com/yandexclassifieds/conductor/0.1/darwin_amd64/terraform-provider-conductor`

    mac os (ARM): `~/.terraform.d/plugins/github.com/yandexclassifieds/conductor/0.1/darwin_arm64/terraform-provider-conductor`

    linux: `~/.terraform.d/plugins/github.com/yandexclassifieds/conductor/0.1/linux_amd64/terraform-provider-conductor`

7. Рекомендуем ознакомиться с Best Practices о том, как мы работаем с репозиторием `terraform` в [этой документации](cloud.md).
8. Добыть токен для кондуктора в соответствии с [докой](https://wiki.yandex-team.ru/conductor/API/#autentifikacija) и добавить в `.bash_rc` или `.bash_profile` строку `export CONDUCTOR_OAUTH_TOKEN=<token>`.

## Добавляем новую группу хостов
1. Создаём подкаталог по названию группы в каталоге compute
2. Создаем в нем файл variables.tf: `ln -s terraform/variables/variables.tf terraform/compute/<conductor_group_name>/variables.tf`;
3. Создаём в нём файл terraform.tf с содержимым:

    ```
    terraform {
      required_version = "v1.0.3"
      backend "pg" {
        schema_name          = "<название группы>"
        skip_schema_creation = false
      }
    }
   ```

3. Создаем файл `<название_группы>.tf` с нужными модулями (конфигами по которым создадутся машинки)
Пример:

```
	# myt
	module "<название модуля>" {
	  source = "../../modules/yandex_compute_instance"
	  # common
	  folder_id       = "<id каталога в облаке>"
	  env             = "<dev/test/prod>"
	  network_id      = "<id сети>"
	  addr_prefix     = "<буквенный префикс адреса>"
	  group           = "<имя группы>"
	  hostname_prefix = "<префикс иммени>"
	  YANDEX_USER     = var.YANDEX_USER // gets from local env, just set export TF_VAR_YANDEX_USER=<your-yndx login>

	  # count
	  compute_count = <count> // количество виртуальных машин в данном модуле

	  # network
	  network_subnet_id    = "<id подсети>"
	  network_prefix       = "<префикс IPv6 адреса>"

	  # compute
	  zone           = "<зона>" // ru-central1-[a,b,c]
	  dc             = "<датацентр>"
	  node_cores     = <число ядер>
	  node_memory    = <размер оперативной памяти>
	  node_disk_size = <размер диска>
      disk_type      = "<тип диска>"

      placement_group_id = "<id группы размещения>" // пока используется только для консул серверов
	}
```
Где:
- Название модуля: `<имя_группы>_<дц_в_котором_создаём>`, пример: `vertis_vtest_docker_myt`
- Переменные-id различных ресурсов берем из общего файла [variables.tf](https://bb.yandex-team.ru/projects/YANDEX-CLASSIFIEDS/repos/terraform/browse/variables/variables.tf) и обращаемся к ним как к переменным, например: `network_id = testing.vertisdev_network_id`
- Буквенный префикс адреса: префикс для разограничения разных групп в одной подсети. Такие как [(полный список используемых префиксов можно найти тут)](https://wiki.yandex-team.ru/vertis-admin/klaster-nomada-v-jandeksoblake/#proipv6adresa):
`a` - vertis_vprod_docker/vertis_vtest_docker
`b` - vertis_vprod_nomad/vertis_vtest_nomad
`c` - vertis_vprod_consul/vertis_vtest_consul
`aa` - ноды rundeck
`bb` - vertis_vdev_gh
Пример использования префиксов (тестинг, сасово, подсеть: `enp4k4stlkg3k3d0qi1q`, префикс сети: `2a02:6b8:c02:900:1:d:0:` ):
`2a02:6b8:c02:900:1:d::**c**01` - `consul-01-sas.test.vertis.yandex.net`
`2a02:6b8:c02:900:1:d::**b**01` - `nomad-01-sas.test.vertis.yandex.net`
`2a02:6b8:c02:900:1:d::**a**01` - `docker-cloud-01-sas.test.vertis.yandex.net`
- Префикс имени: префикс имени машинки (пример: **docker-cloud**-01-sas.test.vertis.yandex.net)
- Префикс IPv6 адреса: префикс `IP` адресов. Первые шесть блоков из IPv6 CIDR подсети + ":0:" (Пример: IPv6 CIDR="**2a02:6b8:c0e:500:1:d**::/96", префикс адреса="2a02:6b8:c0e:500:1:d:0:" )
5. Подключаемся к базе данных для хранения state, делаем первичную инициализацию и проверяем план выполнения.
	terraform init -backend-config="conn_str=postgres://terraform_backend:${password}@c-mdbtgdr5496mfe56fkvh.rw.db.yandex.net:6432/terraform_backend?binary_parameters=yes"
	terraform init
	terraform plan
Пароль можно взять [тут](https://yav.yandex-team.ru/secret/sec-01ecss4z95efs5vsedw9jqn0xr/explore/versions). Строка подключения будет храниться в .terraform, который не должен попадать в репозиторий.

## Полезные советы
1. Команда для быстрого создания пачки тачек (перед запуском не забываем смотреть "terraform plan")
   terraform apply -auto-approve -lock=true -parallelism=30
2. Большие пачки машинок лучше создавать постепенно увеличивая каунт на 50, иначе можно столкнуться с ошибкой `too many open files` ( VERTISADMIN-25522 ).
3. В modules содержатся общие модули для создания ресурсов. Используются как source в соответствующих директориях. Для проверки изменений можно использовать compute/terraform_dev.

## Создание дуалстек-виртуалок для CME

Виртуалки в Яндекс.Облаке для CME - дуалстечные. Заводятся в основном репозитории битбакета [terraform](https://bb.yandex-team.ru/projects/YANDEX-CLASSIFIEDS/repos/terraform/browse).

Чтобы создать необходимый кластер, нужно:
1. Создать директорию `<conductor_group_name>` в `terraform/compute`;
2. Сделать симлинк файла с переменными для кластера: `ln -s terraform/variables/variables.tf terraform/compute/<conductor_group_name>/variables.tf`;
3. Создать файл `terraform.tf` в соответствии с пунктом 3 [в разделе выше](#dobavlyaem-novuyu-gruppu-hostov)
4. Создать файл, описывающий конфигурацию кластера (приведен пример для одного ДЦ):

    ```
      module "<conductor_group>_dc" {
      source = "../../modules/cme_compute_instance"

      hostname_prefix = "<hostname prefix>"
      env             = "<prod/test/dev>"
      group           = "<conductor_group>"

      primary_secret_id = var.<prod/test>-cme.primary_secret_id

      # count
      compute_count = <count>

      # network
      addr_prefix_yandex = "<addr_prefix_yandex>"
      ipv4_addresses     = ["<cme_address_1>", "<cme_address_2>"]
      location           = var.location["<dc>"]

      # compute
      node_cores     = <cpu>
      node_memory    = <mem>
      node_disk_size = <disk size>
      disk_type      = "network-ssd"
   }
    ```

    где:
    * `<addr_prefix_yandex>` - один из свободных префиксов для формирования ipv6-адреса. Список занятых можно найти [здесь](https://wiki.yandex-team.ru/vertis-admin/infra.cm.expert/architecture/dualstackklastera/#prefiksyvipv6-adresax). **Не забудь добавить свой префикс в список во избежание проблем при создании следующих кластеров!**
    * `ipv4_addresses` - список ipv4-адресов в сетях CME для использования на интерфейсе `eth1`. Чтобы вписать его/их, необходимо в сети cme [в UI облака](https://console.cloud.yandex.ru/folders/b1gcubb60v40fve1scvd/vpc/network/enp9pidt4ifnl6tuglfd/overview) открыть страницу подсети необходимого ДЦ (`dmz-ru-central-a/b/c`), перейти на вкладку `IP-адреса` и вписать свободный ip-адрес этой подсети в конфиг терраформа. *Автоматизация планируется в [VERTISADMIN-28460](https://st.yandex-team.ru/VERTISADMIN-28460)*
    * `location` - данная переменная позволяет динамически прописывать идентификаторы сети без участия пользователя в корневой конфиг модуля, при использовании необходимо лишь указать датацентр.
