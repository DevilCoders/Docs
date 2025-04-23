![Y.Deploy](_assets/deploy-introduction/favicon32x32.png)  **Y.Deploy**

Единая система деплоя контейнеров в [RTC](https://rtc.yandex-team.ru/docs/).

## Ссылки на ресурсы по Y.Deploy {#links}

* Рассылка **[yd-announces@yandex-team.ru](https://ml.yandex-team.ru/lists/yd-announces/)**
* GUI Y.Deploy доступен по адресу: [https://deploy.yandex-team.ru/](https://deploy.yandex-team.ru/)
* Очередь в трекере для предложений по улучшению, вопросов по миграции и сообщений об ошибках: [https://st.yandex-team.ru/rtcsupport](https://st.yandex-team.ru/rtcsupport)
* Чат поддержки: [Telegram](https://t.me/joinchat/Be0kOD50fVxMoi_8hPvG6Q)
* [Клуб](https://clubs.at.yandex-team.ru/infra-cloud/) в Этушке, чтобы быть в курсе последних новостей

## Мигрировать {#migration}

Мы разработали инструменты для миграции из других систем деплоя и подготовили документацию, которая облегчит ваш переезд.
* [Nanny](how-to/migration/nanny.md)
* [Qloud](how-to/migration/qloud/qloud.md)

Если вас всё устраивает в Nanny, то рекомендуем в ней и остаться. Y.Deploy и Nanny поддерживаются и развиваются. До тех пор, [пока не станут одной системой](https://clubs.at.yandex-team.ru/infra-cloud/1450).

{% note warning %}

C Qloud [рекомендуется](https://clubs.at.yandex-team.ru/qe/1227/) съезжать как можно быстрее.

{% endnote %}

## Текущие возможности системы {#abilities}

* Система позволяет запустить stateless-сервис, состоящий из одинаковых реплик.
* Вы можете воспользоваться одной из 2-х политик деплоя:
  1. c покластерным окном деплоя PerClusterService;
  2. с общим окном деплоя на несколько кластеров MultiClusterService.
* Использование в качестве артефактов деплоя как Docker-образов, так и SandBox-ресурсов.
* Реализована централизованная [поставка логов](logs/index.md) (stderr/stdout) в YDB и YT. В UI Y.Deploy доступен [просмотр логов](logs/gui.md) прямо из YDB, а также основные операции с логами: фильтрация и выполнение запросов.
* Поддержана <q>из коробки</q> [интеграция с TVM-tool](concepts/pod/sidecars/tvmtool.md).
* Реализована [интеграция с секретницей](how-to/secrets.md): проброс секретов в переменные окружения.
* Доступен просмотр истории релизов и возможность быстрого "отката" к предыдущей версии релиза (с просмотром дифа изменений).
* Возможность доступа по SSH в контейнеры, [YubiKey поддержаны](https://docs.yandex-team.ru/skotty/).
* Метрики потребления вычислительных ресурсов и не только (CPU, RAM, IO, Page Faults и другие).
* Self healing на основе HTTP/TCP/bash-script проверок, а также перенос инстансов вашего сервиса с поломанных машин с учетом указанного пользователем disruption budget.
* Возможность настройки балансировки с использованием AWACS и [Service Discovery](https://docs.yandex-team.ru/service-controller/) YP.
* Поддержка требований SOX и PCI DSS (merchant).
