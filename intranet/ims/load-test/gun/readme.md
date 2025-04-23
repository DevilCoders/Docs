### Пушка для нагрузочного тестирования

Команда для сборки пушки:
``` ya make --target-platform=DEFAULT-LINUX-X86_64  ```

Пушка содержит следующие методы и соответствующие типы патронов:
- createIdentity (intranet_ims_create_identity)
- deleteIdentity (intranet_ims_delete_identity)
- getIdentity (intranet_ims_get_identity)
- listIdentities (intranet_ims_list_identities)
- listIdentityGroups (intranet_ims_list_identity_groups)
- moveIdentity (intranet_ims_move_identity)
- addToGroup (intranet_ims_add_to_group)
- removeFromGroup (intranet_ims_remove_from_group)
- existsInGroup (intranet_ims_exists_in_group)

#### Инструкция, как стрелять
Достаточно подробно можно почитать по [ссылке](https://wiki.yandex-team.ru/telephony/backend/load-testing/#njuansypogrpc)
