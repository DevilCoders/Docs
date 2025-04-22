# yandex-direct-send-logs-to-logbroker

### Пакет содержит в себе
- конфигурационный файл для push-client
- кронтаб по подготовке хардлинков для некоторых логов
- конфигурацию для monrun по проверке валидности конфигурации push-client
- настройки logrotate для лога push-client
- настройки logrotate для директории `/opt/ppc-data/export/statbox/`, в которую пишут:
  - ручка `/logs-commander`
- создание директории `/var/log/ppc.yandex.ru` (root:adm, g+s), *не везде присутствует, но логи из нее описаны в конфиге push-client'а - а без директории конфиг невалиден. Код создания скопирован из правил сборки yandex-direct.*
- создание директории `/opt/ppc-data/export/statbox`, *по той же причине.*

Конфигурационный файл `/etc/yandex/statbox-push-client/push-client.yaml` является симлинком, зависящим от типа окружения (предоставленного пакетом yandex-environment и yandex-direct-conf-sandbox):
- `/etc/yandex/statbox-push-client/push-client.production.yaml` - для продакшена, используется прод логброкера
- `/etc/yandex/statbox-push-client/push-client.testing.yaml` - для тестовых и разработческих окружений, используется престейбл логброкера
- `/etc/yandex/statbox-push-client/push-client.empty.yaml` - для песочницы и **всех остальных** окружений, используется престейбл логброкера с **пустым списком логов**

### После первой установки
Если на машине до этого не был установлен push-client - первый раз его нужно запустить вручную: `sudo /etc/init.d/statbox-push-client start`

### После изменения конфигурации push-client
Перезапуск push-client делается из postinst пакета, но полезно проверить по логам, что перезапуск был успешен и конфигурация перечиталась
