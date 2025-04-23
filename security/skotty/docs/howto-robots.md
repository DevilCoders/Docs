# Роботные SSH-сертификаты

Т.к. наша целевая картина мира - отказ от обычных SSH-ключей и полный переход на SSH-сертификаты, роботам тоже нужно их получать. Но, к сожалению, учитывая среду использования роботов ни о каких хардварных токенах речи быть не может :( Поэтому предлагается получать для оных короткоживущие сертификаты в обмен на OAuth-токен.

## RoboSSH

Для упрощения процесса получения сертификатов и минимизации факапов с их протуханием - существует [RoboSSH](https://a.yandex-team.ru/arc_vcs/security/skotty/robossh). Это такой SSH-Agent схожий с OpenSSH Agent, но который:
  - умеет обменить OAuth-токен на SSH-сертификаты
  - следить за их сроком жизни и переполучать их при необходимости
  - имеет расширенное логирование

В остальном (включая запуск дочернего приложения, Lock/Unlock, TTL ключей и т.д.) он не отличим для пользователя.

## Установка

RoboSSH собирается в пакетик `yandex-robossh` и выкладывается в репозитарий Яндекса. Поэтому для его установки достаточно:
  1. Подключить common-репозитарий (если еще нет):
      ```
      $ sudo tee /etc/apt/sources.list.d/yandex.list <<EOF
      deb http://dist.yandex.ru/common/ stable/all/
      deb http://dist.yandex.ru/common/ stable/amd64/
      EOF

      $ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 7FCD11186050CD1A
      $ sudo apt update && sudo apt -y install yandex-archive-keyring
     ```

  2. Устанавливаем пакет `yandex-robossh`:
      ```
      sudo apt install yandex-robossh
      ```

## Использование

Использование RoboSSH довольно не замысловато:
  1. Запрашиваем в IDM роль [Skotty/RoboSSH/Insecure CA](https://idm.yandex-team.ru/#rf=1,rf-role=I7k9P54L#skotty/robossh/insecure(fields:()),f-status=all,sort-by=-updated,rf-expanded=I7k9P54L)
  2. Получить OAuth-токен для вашего робота: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=80a656c7a6de46d5af611bceb536bb0f
  3. Запустить RoboSSH, передав OAuth-токен в переменной окружения `ROBOSSH_TOKEN`:
     ```
     $ export ROBOSSH_TOKEN='AQAD-....'

     # Запускаем robossh-agent с получением сертификата и запуском bash по окончании
     $ robossh-agent --with-certs -- bash

     # Проверим, что ssh видит наш сертификат
     $ ssh-add -l
     256 SHA256:LH7Hc/2p7pSmUqhWFOrhv36qUMSSsFPEUrg7zLV3dpg insecure@robossh (ECDSA-CERT)

     # Посмотрим на него
     $ ssh-add -L  | ssh-keygen -L -f -
     (stdin):1:
         Type: ecdsa-sha2-nistp256-cert-v01@openssh.com user certificate
         Public key: ECDSA-CERT SHA256:LH7Hc/2p7pSmUqhWFOrhv36qUMSSsFPEUrg7zLV3dpg
         Signing CA: ECDSA SHA256:9PsYUcGRMBPVEHlt5gZYXduP7fCceJ7BVnoV3NsXZsA (using ecdsa-sha2-nistp256)
         Key ID: "skotty:insecure:robot-skotty:r52630-1419:MmEwMjo2Yjg6YzFiOjI5MWQ6MTBkOmFkMDg6NWU1Zjow"
         Serial: 1644073079798424727
         Valid: from 2022-02-05T17:57:59 to 2022-02-06T17:57:59
         Principals:
                 robot-skotty
         Critical Options: (none)
         Extensions:
                 permit-X11-forwarding
                 permit-agent-forwarding
                 permit-port-forwarding
                 permit-pty
                 permit-user-rc
     ```

## Логирование

`robossh-agent` реализует два наиболее популярных паттерна:
  - логировать в нужный файл, для него ему можно передать переменную окружения `ROBOSSH_LOG_PATH`, например:
  ```
  $ export ROBOSSH_LOG_PATH=/tmp/robossh.log
  $ robossh-agent -- sh
  $ cat /tmp/robossh.log
  2022-02-05T18:06:40.383+0300	INFO	robossh-agent/do_start.go:114	agent started	{"pid": 55204, "version": "0.9.9110646"}
  ```

  - логировать в stderr, при запуске в foreground режиме, например:
  ```
  $ robossh-agent --with-certs -D
  2022-02-05T18:05:15.665+0300	INFO	watcher/watcher.go:83	starts update certificates	{"pid": 54501}
  2022-02-05T18:05:15.665+0300	INFO	watcher/watcher.go:85	issue certificates	{"pid": 54501}
  2022-02-05T18:05:15.716+0300	INFO	watcher/watcher.go:101	add new certificates	{"pid": 54501}
  2022-02-05T18:05:15.716+0300	INFO	watcher/watcher.go:105	added certificate	{"pid": 54501, "name": "insecure@robossh", "fingerprint": "SHA256:wamYdGP04+wh643aJ3eix/+2cImKFPwqF87XjwhCM3s"}
  2022-02-05T18:05:15.716+0300	INFO	watcher/watcher.go:109	hide old certificates	{"pid": 54501}
  2022-02-05T18:05:15.716+0300	INFO	watcher/watcher.go:121	certificates updated	{"pid": 54501}
  2022-02-05T18:05:15.717+0300	INFO	robossh-agent/do_start.go:152	certs watcher started	{"pid": 54501}
  2022-02-05T18:05:15.717+0300	INFO	robossh-agent/do_start.go:114	agent started	{"pid": 54501, "version": "0.9.9110646"}
  SSH_AUTH_SOCK=/var/tmp/robossh-2548124769/agent.49031; export SSH_AUTH_SOCK;
  SSH_AGENT_PID=54501; export SSH_AGENT_PID;
  echo Agent pid 54501;
  ```
