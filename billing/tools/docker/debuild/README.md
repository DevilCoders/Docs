# Образ контейнера для сборки пакетов
Собран на базе registry.yandex.net/balance/toolsbase
Готовый образ: registry.yandex.net/balance/debuild

# Использование контейнера
Контейнер создавался для использования в teamcity.
Добавить шаг сборки с типом "Docker / Vagrant", в поле Image Name запихать ссылку на образ.
Чтобы при сборке были доступны ssh-ключи и gpg-подписи, написать в Additional Docker Parameters:
```
-v /home/robot-billing-ci/:/home/robot-billing-ci/:rw
```
Это примонтирует в образ хомяк пользователя robot-billing-ci.
Рабочая директория агента по-умолчанию монтируется в контейнер по пути /checkout
Чтобы собранные пакеты после сборки не потерялись в автоматически удаляемом контейнере, надо чтобы репозиторий для сборки клонировался в субдиректорию.
VCS Checkout Rules:
```
+:. => subdir
```
Build Step Command:
```bash
cd subdir
some_command_to_run_build
```
