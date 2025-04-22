# Аркадизированный salt
Про аркадизацию можно почитать тут [yandex_salt_components][1]

# Стейты
Salt стейты nocdev лежат в [`~/arcadia/admins/salt-media/noc/`][2]

# Выкатка салтом на процент, aka salt-autodeploy

Юнит тут [units/percent][3]
Этот юнит содержит такие стейты
- макрос `smooth_update` который получает детерменированный (по fqdn) хеш хоста через вызов `salt['random.seed']`
- кучу `jinja` кода для формирования правильных `packages` и `packages_map` через использование макроса `smooth_update`
  версии пакетов будут рассчитаны на основе попадания хоста в процент деплоя новой версии.
- стейт записывающий рассчитанные версии пакетов в файл `/var/tmp/salt-autodeploy.json`, этот файл используется в мониторинге из юнита `units.auto`

## Подключение формулы для авторелизов

Перед подключением необходимо обеспечить консистентное состояние кластера, то есть на всём кластере должны быть одинаковые версии пакетов, которые планируется катить через юнит.

Дальше необходимо выполнить ряд шагов
1. добавить на кластер в pillar `salt-autodeploy-sls` юнит `units.percent`, пример подключения есть [тут][5]
2. добавить в этот же `pillar` другие `sls` файлы или юиныт, в которых происходит импорт и использование переменных `packages` или `packages_map` для установки пакетов. Пример из `yanet-agent`
    ```(yaml)
    {% from "units/percent.sls" import packages_map %}   # <<< импортируем (с сайдэффектом рассчёта) пакеты с правильными версиями

    yanet-agent:
      pkg.installed:
        - version: {{packages_map["yanet-agent"].version}}  # ставим нужый пакет с правильной версией
        - allow_updates: True
      module.run:
        - name: service.systemctl_reload
        - onchanges:
          - file: yanet-agent.service
      service.running:
        - enable: True
        - restart: True
        - wait3: True
        - init_delay: 3
        - watch:
          - pkg: yanet-agent
    ```
   за счёт импорта переменных с версиями появляется невероятная гибковть, можно изобретать стейт любой сложности.
   Ещё одни пример из `nocdev-valve/autodeploy`
   ```(yaml)
   {% from "units/percent.sls" import packages %}
    valve-packages:
      pkg.installed:
        - pkgs:
          - python3-psycopg2
          - python3-requests
          - python3-dateutil
          {% for pkg in packages %}
          - {{pkg.name}}: {{pkg.version}}
          {% endfor %}

   ```
3. помечаем добавленные `sls` как `monitor: True`, это включает мониторинг для применения этих стейтов. Будет добавлен juggler-client манифест и появится проверка `salt-autodeploy`
   
4. добавить `pillar`-ы описывающие какие пакеты нужно катить. [пример][4], именно из этих версий в sls файлах будут рассчитываться "правильные" версии.
    - подключение делается через каталог в `/pillar/<cluster name>/`
    - в каталог нужно положить `init.sls` с `pillar`-ами которые раньше были в `/pillar/<cluster name>.sls` 
    - и файл `autodeploy.yaml` в `/pillar/<cluster name>/autodeploy.yaml` который описывает набор пакетов и версий
        ```yaml
        sentinel: 9143758                   # строка с ревизией
          packages:
            - name: yanet-agent             # имя пакета
              version:
                old: 1.0.0-9143758          # установленная на кластере версия
                new: 1.0.0-9143758          # версия которую планируем катить
              percent: 100                  # процент раскатки (можно указать 0)
              dc: man
        ...
            - name: yanet-agent
              version:
                new: 1.0.0-9143758
                old: 1.0.0-9102424
              percent: 0
              dc: vla
        ```
3. После применения новых стейтов юнитом `units.auto` на хосте появтися проверка `salt-autodeploy`, эта проверка сделит за
    - успешность накатки крона
    - актуальности версии пакетов на машинке  (чурез копию `pillar` последней успешной катки и `dpkg -l`)
    - экспортирует в juggler последний `uuid` из `pillar`-ов в `description` проверки.

4. сварить кулебяку, которая аггрегирует событие `salt-autodeploy` в одноимённый агрегат, готовый шаблон [тут][6] пример использования [тут][7]
5. добавить CI flow в котором описать шаги с необходимым процентом по ДЦ кубиком `projects/noc/salt_percent_deploy`. [Пример][8]

После этого можно пробовать запускать выкатку через CI.

  [1]: <https://a.yandex-team.ru/arcadia/admins/yandex_salt_components/README.md>
  [2]: <https://a.yandex-team.ru/arcadia/admins/salt-media/noc/>
  [3]: <https://a.yandex-team.ru/arcadia/admins/salt-media/noc/roots/units/percent.sls>
  [4]: <https://a.yandex-team.ru/arcadia/admins/salt-media/noc/pillar/noc-fw/autodeploy.yaml?rev=r9203610#L2>
  [5]: <https://a.yandex-team.ru/arcadia/admins/salt-media/noc/roots/units/auto>
  [6]: <https://a.yandex-team.ru/arcadia/noc/mondata/kulebyaks/juggler_templates/salt-autodeploy.yml?rev=r9538575#L1>
  [7]: <https://a.yandex-team.ru/arcadia/noc/mondata/kulebyaks/yanet_firewall.yaml?rev=r9538575#L58>
  [8]: <https://a.yandex-team.ru/arcadia/noc/yanet/yanetagent/a.yaml?rev=r9143758#L158>
