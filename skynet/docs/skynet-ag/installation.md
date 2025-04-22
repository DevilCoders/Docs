# Установка и настройка

На схеме ниже представлен порядок установки сервисов {{ serviceName }} на серверах.

![alt_text](./_assets/scheme.png "Skynet-setup" =600x700)

1. [Настройка серверных доступов](access.md).
    
    Для корректного функционирования и своевременного обновления {{ serviceName }} необходимо обеспечить доступы к серверам:
    
    * С которых осуществляется управление клиентскими экземплярами {{ serviceName }}. Требуется для получения актуальных сведений о версии, которая должна быть установлена, списка сервисов, которые должны быть запущены на группе серверов и т.п.
    * На которые устанавливается {{ serviceName }}. Требуется для последующей раздачи служебных файлов {{ serviceName }} с помощью сервиса [Copier](https://doc.yandex-team.ru/Search/skynet-desc/concepts/public-services_copier.html#public-services_copier).
    
1. (_Опц._) [Настройка параметров установки и функционирования](configuration.md).
    
    Выполняется, если для группы серверов, на которые устанавливается {{ serviceName }}, требуются настройки, отличные от используемых по умолчанию:
    
    * Версия {{ serviceName }}.
    * Список устанавливаемых сервисов.
    * Параметры сервисов.
    
1. Загрузка и установка Skynet.
    
    Способы загрузки и установки Skynet зависят от используемой [операционной системы](restrictions.md).
    
    {% cut "MacOS и Cygwin" %}
    
        Загрузите требуемую версию дистрибутива {{ serviceName }} (`skynet.bin`) [из сервиса Sandbox](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=SKYNET_BINARY&attrs=%7B%7D).
    
        Затем запустите дистрибутив на сервере.

    {% endcut %}
    
    {% cut "Linux" %}
    
        [Установите и запустите утилиту gosky](gosky-install.md). Утилита обеспечивает первичную установку и последующие обновления {{ serviceName }}.
    
        После запуска утилита загружает и запускает требуемую версию дистрибутива {{ serviceName }} (`skynet.bin`). Затем gosky переводит сервер в режим раздачи служебных файлов Skynet с помощью сервиса [Copier](https://doc.yandex-team.ru/Search/skynet-desc/concepts/public-services_copier.html#public-services_copier)

    {% endcut %}
    
    Отчет о результате установки требуемой версии Skynet и его сервисов автоматически отправляется в сервис [heartbeat](https://doc.yandex-team.ru/Search/skynet-desc/concepts/internal-services_heartbeat.html). Посмотреть отчет можно в веб-интерфейсе сервиса на [вкладке Lacmus](https://heartbeat.yandex-team.ru/lacmus).
    
    Дистрибутив `skynet.bin` содержит:
    
    * Скрипт, обеспечивающий установку сервисов, [определенных](configuration.md) в {{ deploy-and-configService }} для данной группы серверов.
    * Python для поддерживаемых операционных систем.
    * Архив всех сервисов {{ serviceName }}. Устанавливаются только те, которые определены для данной группы серверов.

        Для установки сервиса Skynet на сервер необходимо, чтобы в правилах сервиса в секции [skynet.skycore.namespaces.skynet](https://genisys.yandex-team.ru/sections/skynet.skycore.namespaces.skynet)  (**skynet** → **skycore** → **namespaces** → **skynet** → **&lt;название сервиса>**) был указан хост сервера. Чтобы установить или удалить сервис с сервера, напишите на рассылку [skynet@yandex-team.ru](mailto:skynet@yandex-team.ru).
    
    {% note info %}
    
    Для обновления версии {{ serviceName }}, установленной на сервер, также используется дистрибутив `skynet.bin`. Обновление выполняется только в том случае, если предварительно удалось выполнить остановку {{ serviceName }}.
    
    При обновлении Python перезапускаются все сервисы {{ serviceName }}. Если версия Python остается неизменной, перезапускаются только те сервисы, которые содержат обновления.
    
    {% endnote %}
    
### Узнайте больше

* [Процедура обновления версии Skynet (Вики)](https://wiki.yandex-team.ru/Skynet/HowToUpdate/)
