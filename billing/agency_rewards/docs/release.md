Выкладка релиза
===============

- вмержить все пул реквесты:

  - https://github.yandex-team.ru/Billing/yb-ar/milestones

- проверить diff с тестовой веткой:

```bash
    $ git diff origin/testing-2019XX
```

- прогнать тесты:

```bash
    # юнит тесты
    $ make test

    # регрессия для платформы
    $ regress-platform-tests

    # регресия для python расчетов (+ celery/sqs)
    $ make regress-worker &
    $ make regress-tests
```

- поднять версию:

```bash
    $ make release VER=1.20.0
    $ git push origin master
```

- собрать релиз в `teamcity` из ветки `master:`

  - https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Billing_AgencyRewards_BuildTestPy3

- выложить в прод

  - https://c.yandex-team.ru/packages/yb-ar/tickets

- обновить конфиги в бункере, посмотрев, что изменилось:

```bash
    $ git diff --stat 1.18.12 master deployment/bunker/
```

- запустить расчет в проде, чтобы убедиться, что ничего не сломано

- удалить результаты запуска, если есть разница с последним запуском
