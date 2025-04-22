###### Структура пода
Один бокс ("инфраструктура", возможно, уедет в отдельный)

###### Статические ресурсы
/httpsearch
/models.archive
/vars.conf
/generation.conf

###### Динамические ресурсы
Создаётся вольюм /dynamic_resources,
в него пока ничего не качается, work in progress.

###### Слои с ресурсами
generator.configs.tar.gz разархивируется в /all

###### Runtime-слой
/usr/local/webruntime/
    instancectl_helper
    deployer-agent/*.sh
    multibeta-agent/*.sh
    prod/*.sh
    hamster/*.sh
    logrotate/*.sh
/var/log/webruntime/ (пустой каталог)

###### Переменные окружения
Legacy. Разрешено использовать только в instancectl helper.
- name: GENCFG_TIER
  value:
    literal_env:
      value: PlatinumTier0
