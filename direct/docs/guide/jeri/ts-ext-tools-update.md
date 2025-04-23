# Обновление apisteps,balance-proxy,fake-proxy-responser,direct-handles

## Сборка
- Коммитим в репозиторий:
  - [apisteps](https://a.yandex-team.ru/arc/trunk/arcadia/direct/qa/direct-steps-proxy)
  - [balance-proxy](https://github.yandex-team.ru/qa-irt/xmlrpc-notifications-proxy) 
  - [fake-proxy-responser](https://a.yandex-team.ru/arc/trunk/arcadia/direct/qa/fake-bs-proxy-service)
  - [direct-handles-rest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/qa/direct-handles-web)
  - [direct-handles-static](https://a.yandex-team.ru/arc/trunk/arcadia/direct/qa/direct-handles-frontend)
- Переходим в дженкинс в джобу сборки:
  - [apisteps](https://jenkins-direct.qart.yandex-team.ru/job/direct-applications/job/directsteps-proxy/)
  - [balance-proxy](https://jenkins-direct.qart.yandex-team.ru/job/direct-applications/job/balance-proxy-notifications/) 
  - [fake-proxy-responser](https://jenkins-direct.qart.yandex-team.ru/job/direct-applications/job/fake-bs-proxy/)
  - [direct-handles-rest](https://jenkins-direct.qart.yandex-team.ru/job/direct-applications/job/direct-handles-rest/) для сборки апи
  - [direct-handles-static](https://jenkins-direct.qart.yandex-team.ru/job/direct-applications/job/direct-handles-static/) для сборки статики
- В меню слева нажимаем **Build with Parameters** (если такого пункта нет &mdash; жмите **log in** в правом верхнем углу)
- В параметре **TAG** вместо _latest_ вписываем минимально уникальный идентификатор, например, дату.
- Нажимаем **BUILD**
- Дожидаемся окончания таски: внизу слева отображен список, в нем полоса загрузки дойдет до конца и кружок таски позеленеет(если нет, надо смотреть логи таски, щелкнув по кружку).

## Обновление 
- Переходим в [Deploy](https://deploy.yandex-team.ru) и находим стейдж в проекте direct-infra:
  - [apisteps](https://deploy.yandex-team.ru/stage/direct-apisteps-proxy)
  - [balance-proxy](https://deploy.yandex-team.ru/stage/direct-balance-test-proxy)
  - [fake-proxy-responser](https://deploy.yandex-team.ru/stage/direct-bs-test-proxy)
  - [direct-handles](https://deploy.yandex-team.ru/stage/direct-handles-prod)
  - [direct-handles-test](https://deploy.yandex-team.ru/stage/direct-handles-test)
- Переходим на вкладку **Config** и нажимаем кнопку Edit
- Переходим в нужную часть (DeployUnit-Box) сервиса, если их больше одной, например rest или static
- Внутри Box в поле **Base Layer** меняем часть после двоеточия на ту, которую указывали при сборке (параметр TAG)
- Нажимаем **Update**, смотрим предложенный дифф
- Если все выглядит ожидаемо — жмем **Deploy**
