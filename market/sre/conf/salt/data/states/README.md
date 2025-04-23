Yandex.Market salt
==================

Документация: https://wiki.yandex-team.ru/market/administration/salt/howitworks/
Мастера: salt01e.market.yandex.net, salt01h.market.yandex.net

# Запуск

    ssh salt01e.market.yandex.net

    # Применить все изменения во всех средах
    sudo salt <target> state.apply

    # Только testing
    sudo salt <target> state.apply saltenv=testing

    # Показать что будет сделано, но ничего не делать
    sudo salt <target> state.apply test=True

    # Все хосты
    <target> = '*'

    # Один хост
    <target> = madeli01ht.market.yandex.net

    # Кондукторная группа
    <target> = -N market_delivery_apps-testing

# Организация кода

    # top.sls
    environment:
        minion_id:
            - state1
            - ...

## Environment
 Окружения указано в конфиге миньона в /etc/salt/minion.d/env.conf. Миньон применяет только стейты из top.sls только из своего окружения.
- production
- prestable
- testing
- development

## Minion ID

Все миньоны дожны матчиться по имени хоста или по кондукторной группе.

    production:
      conductor:groups:market_sovetnik-stable:
        - match: grain
        - formulaes.common.sysctl.tunnel-slb
        - formulaes.sovetnik

      conductor:match:corba_bulca-comments:
        - match: pillar
        - formulaes.docker
        - formulaes.bulca

## Стейты

Каждый стейт дожен соответствовать какому-то сервису и не должен быть привязан к хосту для возможности переиспользования.
