# CI

## Токены
Все действия в CI выполняются от имени робота [robot-pay-ment](https://abc.yandex-team.ru/services/ecosystem_interfaces/?scope=virtual)
Для автоматизации работы с токенами реализована схема централизованного хранения токенов доступа в секретнице:
 * все необходимые токены хранятся в одной записи в секретнице: https://yav.yandex-team.ru/secret/sec-01f6728tcjgem3q4dphyfxnt84
 * для получения нужного токена из записи в секретнице в процессах CI используется токен робота для yav (*хранится там же :)*)
 * получение токена выполняется archon компонентой [vault-data-getter](../.config/archon/components/vault-data-getter.js)
   * Например, [получение ssh-ключа для туннелера](../.config/archon/commands/get-ssh-key.js#L26)
 * Для редактирования записи/добавления новых токенов в запись нужно получить роль [Управляющего секретами](https://abc.yandex-team.ru/services/ecosystem_interfaces/?scope=secrets_management)

## Проверки
### Hermione
Запускается параллельно в двух режимах application и storybook.
Публикует два отчета для каждого из режимов.
Для запуска использует tunneler и ssh ключ робота.
