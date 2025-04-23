## Как изменить и применить жагглерные проверки в juggler-ansible

Основная дока: https://wiki.yandex-team.ru/sm/juggler/ansible

Применять изменения можно с ноутбука, для этого нужно:
1. Установить ansible в venv https://wiki.yandex-team.ru/sm/juggler/ansible/#ansible1.9
2. Выбрать метод аутентификации, в примере ниже используется OAuth-токен: https://wiki.yandex-team.ru/sm/juggler/authentication/#kakosushhestvljaetsjadostupknamespace
3. Внести изменения в нужные файлы
4. Проверить правильность изменений ```$ ./venv/bin/ansible-playbook portal-morda-admin/juggler-ansible/main.yml --check -vv```
5. Применить: ```$ JUGGLER_OAUTH_TOKEN=AQAD-*** ./venv/bin/ansible-playbook portal-morda-admin/juggler-ansible/main.yml```
