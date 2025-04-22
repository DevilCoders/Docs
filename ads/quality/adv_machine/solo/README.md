### Структура проекта ###

* PY3_PROGRAM creator, использующий build_basic_cli_v2 для создания CLI
* PY3_LIBRARY nanny_services для получения списка сервисов в няне, для которых генерируется конфигурация объектов SOLO
* PY3_LIBRARY registry для хранения конфигурации объектов
* PY3TEST tests для тестирования конфигурации
* a.yaml с описанием релизного процесса

### Запуск ###

* Собрать бинарь creator и выполнить с опцией --delete-untracked и по желанию --verbose. Так можно посмотреть дифф, создаваемый локальными изменениями.
* Нельзя использовать --apply-changes без понимания к чему это приведёт. Стейт SOLO хранится [на Locke в //home/adv_machine/solo/solo.state](https://yt.yandex-team.ru/locke/navigation?path=//home/adv_machine/solo/solo.state), соответственно при наличии прав и отстутствии понимания можно сломать мониторинги.

### Процесс выкатки ###

В [CI нашего проекта](https://a.yandex-team.ru/projects/advmachine/ci/releases/timeline) можно запустить релиз SOLO creator.
* Стадия Build SOLO creator говорит за себя названием.
* Create testing release релизит сандбокс ресурс ADV_MACHINE_SOLO_CREATOR с атрибутом testing
* Dry run SOLO creator запускает последний ресурс ADV_MACHINE_SOLO_CREATOR с атрибутом testing. В этой стадии стоит смотреть на дифф текущего релиза, и если он ожидаемый и ничего не ломает, запускать следующую стадию.
* Create stable release релизит сандбокс ресурс ADV_MACHINE_SOLO_CREATOR с атрибутом stable. Далее [шедулер](https://sandbox.yandex-team.ru/scheduler/713054/view) регулярно запускает последний ADV_MACHINE_SOLO_CREATOR с атрибутом stable, защищая состояние сгенерированных мониторингов от ручных изменений.
