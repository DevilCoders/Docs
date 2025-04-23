# Отображение релизов в infra.yandex-team.ru

В отдельном сервисе можно включить автоматическое создание событий про выкладку в [infra.yandex-team.ru](https://wiki.yandex-team.ru/infra/).

## Важные моменты {#notes}

1. Каждая новая выкладка сервиса будет приводить к созданию нового события в infra;
1. Пользователь, включающий экспорт событий в infra, должен быть админом соответствующего infra-окружения;
1. `nanny-robot` должен быть админом окружения в infra;

    {% note warning %}

    Экспортируются только события про активацию сервиса, не про prepare-стадию.

    {% endnote %}

1. Если экспорт в infra не работал из-за временных проблем (лежащих компонент nanny, или лежащих компонент infra.yandex-team.ru, или проблем с сетью), то события будут досланы в инфру после того как проблемы решатся;
1. Если в нянесервисе указан лейбл `dc`, то события будут создаваться в соответствующем `dc` в инфре. В противном случае события в инфре будут создаваться во всех ДЦ infra-environment.

## Как включить? {#how-to}

1. Решить, будет ли использоваться существующий [service в infra.yandex-team.ru](https://infra.yandex-team.ru/account/services), или создать новый. Если для сервиса выполняется одно из условий:
    * входит в одну из поисковых вертикалей;
    * от него зависит стабильность работы сервисов Поискового Портала;
    * хочет, чтобы его релизы попали на [общий production-дашборд](https://beta.infra.yandex-team.ru/timeline?preset=arTt9MFTRED), то его надо сразу включить в правильное место в иерархии, чтобы узнать его, нужно обратиться к коллегам из дежурной смены. В противном случае [создать service в infra.yandex-team.ru](https://infra.yandex-team.ru/account/services)

1. Чтобы включить экспорт из Nanny в infra.yandex-team.ru, в интересующем Nanny-сервисе в блоке `Information` заходим на страницу `General`, ищем раздел `Infra service and environment` и нажимаем на кнопку редактирования
    ![img](https://jing.yandex-team.ru/files/sshipkov/GeneralInfo.1a525e0.png)

1. Если нужный сервис в infra уже есть, то выбираем в открывшемся окне infra-service и infra-environment. Если все сделано правильно, во вкладке General появится информация:
    ![img](https://jing.yandex-team.ru/files/sshipkov/general_edited.bd3c30c.png)

1. Если подходящего сервиса в инфре нет, то его можно создать из Nanny. Инструкция:
    1. Жмём `Create new infra service`.
    1. Выбираем `namespace` из предложенных.
    1. Придумываем и вводим `service name` и `environment name`.
    1. Нажимаем **Create**.

        ![create.png](https://jing.yandex-team.ru/files/sshipkov/create.e29774a.png)

    После этого нужно выдать права на него всем пользователям, ответственным за сервис. В противном случае эти пользователи не смогут делать копии нянесервисов, в которых включён экспорт в инфру. Это будет поправлено с поддержкой ABC в infra.yandex-team.ru: [https://st.yandex-team.ru/INFRA-166](https://st.yandex-team.ru/INFRA-166)
    По умолчанию в `environment` проставляются все ДЦ: `iva, myt, man, sas, vla` и автоматически выдаются права пользователю `nanny-robot`.

1. Если сервис представлен с одним ДЦ, то заполнить лейбл `dc` его именем: `iva, myt, man, vla, sas`.

    ![img](https://jing.yandex-team.ru/files/sshipkov/dc.4f94b69.png)

