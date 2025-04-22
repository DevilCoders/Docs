# Начало работы

Здесь мы настроим окружение для дальнейшей разработки бекенда. В разделе [Troubleshoting](#troubleshooting) приведены типичные ситуации возникающие в процессе разработки.

## Настройка SSH ключа

Генерируем ключ:

```(bash)
ssh-keygen -t rsa -b 2048 -f ~/.ssh/id_rsa -C your-login@yandex-team.ru
```

После запуска команды предложат ввести два раза пароль. Пароль следует выбирать довольно надежный.

Ключик можно добавить в SSH-Agent, чтобы не вводить каждый раз пароль (опционально):

```(bash)
ssh-add ~/.ssh/id_rsa
```

Далее нам необходимо получить содержимое публичного ключа следующим образом:

```(bash)
cat ~/.ssh/id_rsa.pub
```

Пример публичного ключа:

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCmgSOAF49p1rSQkPT9PcyVEttZ2T2GGCy0q5ixwG8WaOUxBL2btOkDZuoKoGjFL3JU/0zX/9+eCqnzMnNZAuqBLrTcl+uxsshIfSyUTlxOPdDxutoyLBmNJpEjsAiauhEy8POYUIVjJkuWXqWdTny8fwad7eTcH96Hj9k9+b3Pvj9fmMzQaZTod668f3O9ZGWfd8ihj0Hvo7QPclvxFgz2og9doSoaqnMMnEtCtiUjoWVyoiCsRnbSWs+DtZAmjz+5rWZRZHM6ayndHBtA13pKU/sAoklzq/hwerHhbFPIKW1XcKa1zeyajmpqhSrU11MOWl2TeTiPlxrJgfi9l83H iudovin@iudovin-nix
```

Переходим на [Стафф](https://staff.yandex-team.ru). В разделе SSH-ключи добавляем новый:
* Жмем на карандашик.
* Добавить ключ.
* В поле &laquo;Ключ&raquo; вводим ранее полученный публичный ключ.
* В поле &laquo;Описание&raquo; вводим любое описание.

### Зачем это нужно?

SSH-ключ позволит в дальнейшем получать доступ к dev-машинкам и обменивать его на OAuth-токены.

## Создание dev-машинки

Для создания dev-машинки воспользуемся сервисом QYP: [ссылка](https://qyp.yandex-team.ru/create-vm).

Важные настройки для своей dev-машинки:

Сетевой макрос (Network Macro): `_GENCFG_RTLINE_FRONTEND_SIMPLE_`.

ABC-сервис: `1796: Яндекс.Драйв`.

Указываем не менее 32 GB оперативки и 200 Гб HDD.

Указываем другие параметры, создаем VM.

## Подключение к VM

Для подключения в VM нужно использовать FQDN (адрес хоста в виде доменного имени), пример:

```(bash)
ssh dev-drive1.sas.yp-c.yandex.net
```

Дальнейшие действия выполняем на **dev-машинке**.

## Настройка Arc

Arc используется как замена git-репозитриям.

Проще всего воспользоваться следующей документацией: [ссылка](https://docs.yandex-team.ru/devtools/intro/quick-start-guide).

**Желательно, чтобы корень репозитория оказался в папке `~/arcadia/`, так как дальнейшие инструкции будут предполагать такое расположение.**

## Сборка и запуск бекенда

Чтобы убедиться что все настроено верно, необходимо осуществить сборку и запуск бекенда.

Запуск бекенда описан на этой [странице](https://docs.yandex-team.ru/drive/backend/start_backend).

## Настройка IDE

Для разработки удобно использовать Visual Studio Code, так как он поддерживает удаленную разработку. Скачиваем с [официального сайта](https://code.visualstudio.com/).

Далее необходимо настроить расширения для удаленной разработки. Можно воспользоваться официальной документацией: [ссылка](https://code.visualstudio.com/docs/remote/ssh-tutorial).

Для генерации воркспейса будет использована утилита `ide vscode-clangd` с ней можно ознакомиться на [странице](https://docs.yandex-team.ru/ya-make/usage/ya_ide/vscode).

### Актуальная версия
* Устанавливаем в SSH Remote расширение clangd
* Запускаем построение workspace
```(bash)
cd ~/arcadia
ya ide vscode-clangd drive/
echo "workspace-name.code-workspace" >> ~/.arcignore
```
* Открываем в VSCode `~/arcadia/workspace-name.code-workspace` через `File -> Open Workspace`. Соглашаемся с предложением поменять settings у расширения clangd
* Дожидаемся окончания индексации

### Старая версия
Также можно настроить себе дополнительные [удобства](https://wiki.yandex-team.ru/users/rudskoy/atushka/vscode/).

## Troubleshooting
При возникновении проблем можно обратиться на [страницу](https://docs.yandex-team.ru/drive/backend/newbies_troubleshooting).
