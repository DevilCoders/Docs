# Настройка датасета с пользовательскими данными

Для использования ecstatic в качестве транспорта для доставки датасетов с пользовательскими данными необходимо ограничить доступ к этим данным, 
ведь по дефолту ecstatic позволяет скачать без авторизации любой датасет, загруженный в него.

1. Настройка tvm для потребителей датасета

    Для всех сервисов-потребителей необходимо настроить tvmtool для работы с ecstatic и выкатить их. Пример:
   [конфиг tvmtool](https://a.yandex-team.ru/arc_vcs/maps/infra/ecstatic/storage/docker/install/etc/template_generator/templates/etc/tvmtool?rev=cad67b4b24f8b6a446477b446d3eea124c9da2aa), 
   [конфиг template-generator](https://a.yandex-team.ru/arc_vcs/maps/infra/ecstatic/storage/docker/install/etc/template_generator/config.d/ecstatic-storage.yaml?rev=cad67b4b24f8b6a446477b446d3eea124c9da2aa#L4),
   [sedem_config](https://a.yandex-team.ru/arc_vcs/maps/infra/ecstatic/storage/sedem_config/__all__.yaml?rev=cad67b4b24f8b6a446477b446d3eea124c9da2aa#L18)
    
    После выкатки сервиса, в конфиг ecstatic надо добавить следующую строчку:
    
    ```
   group rtc:my_deploy_group has tvm:12345
    ```

    {% note alert %}

    После коммита изменений в конфигах ecstatic начнет проверять tvm id и при неправильной конфигурации ecstatic client перестанет работать

    {% endnote %}

2. Запрет скачивания датасета

    После успешной настройки tvm id для всех потребителей необходимо запретить скачивание датасета без авторизации. 
Для этого в конфиги ecstatic необходимо закоммитить следующую строчку:
    ```
   restrict download my-secure-dataset
   ```

    После этого, датасет нельзя будет скачивать с помощью `ecstatic tool`, а также для него не будет работать репликация в другие окружения.
В остальном, взаимодействие с этим датасетом в ecstatic не поменяется. 
