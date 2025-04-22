## Генерация проекта:

https://wiki.yandex-team.ru/taxi/conversation/

Внутри папки `arcadia/taxi/crm/conversation` выполнить:
```bash
generate_project.sh -i /Users/$USER/projects/
```
После этого в папке projects создастся папка conversation c проектом IDEA
и "Run Service (generated)" конфигурацией.

По результатам вывода `generate_project.sh` настроить `codestyle`:
```
Info: Codestyle config: /Users/vdorogin/.ya/tools/v4/874273162/intellij-codestyle.jar. You can import this file with "File -> Manage IDE Settings -> Import settings..." command. After this choose "yandex-arcadia" in code style settings (Preferences -> Editor -> Code Style).
```

## Секреты

### Mac

Локально добавить в переменные окружения ( в файл .bash_profile)

```bash
export YAV_AUTH_TOKEN=`ya vault get version sec-01fn3ngpa2tbf0p6yze9qr3xfy -o YAV_AUTH_TOKEN`
export YT_TOKEN=`ya vault get version sec-01fq4606znpw1e5c73zp3czm0t -o YT_TOKEN`
```

### Linux
Идея не видит переменные в .bash_profile и .bashsc, поэтому нужно добавлять в .profile.
.profile выполняется только при старте Linux, поэтому, после редактирования файла, необходимо перезагрузить систему.

При этом, если в .profile написать команду вида,
```bash
export YT_TOKEN=`ya vault ....'
```
то при запуске системы выйдет ошибка
```bash
command 'ya' not found
```

Поэтому, рекомендуется, в .profile вставить ключи
```bash
export YAV_AUTH_TOKEN=`YAV_AUTH_TOKEN из секретницы`
export YT_TOKEN=`YT_TOKEN из секретницы`
```

## Запуск локально:
- в IDEA через Run Service (generated) конфигурацию
