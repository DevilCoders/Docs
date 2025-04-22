[Что такое радар](../../glossary/glossary.md#radar)

# Обновление радара

- Коммитим в [репозиторий](https://github.yandex-team.ru/qa-irt/radar)
- Переходим в [дженкинс](https://jenkins-direct.qart.yandex-team.ru/job/direct-applications/)
- Выбираем нужную джобу(проект):
  - [radar-rest](https://jenkins-direct.qart.yandex-team.ru/job/direct-applications/job/radar-rest/) для сборки апи
  - [radar-static](https://jenkins-direct.qart.yandex-team.ru/job/direct-applications/job/radar-static/) для сборки статики
- В меню слева нажимаем **Build with Parameters** (если такого пункта нет &mdash; жмите **log in** в правом верхнем углу)
- В параметре **TAG** вместо _latest_ вписываем минимально уникальный идентификатор, например, дату —
должно получиться что-то вроде `radar-rest-202008272005`.
- Нажимаем **BUILD**
- Дожидаемся окончания таски: внизу слева отображен список, в нем полоса загрузки дойдет до конца и кружок таски позеленеет(если нет, надо смотреть логи таски, щелкнув по кружку).
- Переходим в [Deploy](https://deploy.yandex-team.ru) и находим [стейдж с радаром](https://deploy.yandex-team.ru/stage/radar-prod)
- Переходим на вкладку **Config** и нажимаем кнопку Edit
- Переходим в нужную часть (DeployUnit-Box) сервиса: rest или static
- Внутри Box в поле **Base Layer** меняем часть после двоеточия на ту, которую указывали при сборке (параметр TAG)
- Нажимаем **Update**, смотрим предложенный дифф
- Если все выглядит ожидаемо — жмем **Deploy**
