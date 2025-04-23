# Частые проблемы

### Failed to obtain k8s OAuth token: cannot get token from ssh keys {#k8s-token-fail}

Чтобы выполнять действия с объектами от имени текущего пользователя, консольная утилита должна представиться им. Для этого infractl пытается найти в локальном окружении ssh-ключ текущего пользователя и обменять его на OAuth-токен, с которым она будет делать запросы к серверу. Рассматриваемая ошибка возникает если обменять ssh-ключ на OAuth-токен не удалось.

#### Возможные причины проблемы {#ssh-keys-troubleshooting}
1. Не удалось найти доступные ssh-ключи. Проверить их можно с помощью команды `ssh-add -l`, в ответе должен быть хотя бы один ключ.
2. Если вы до этого никогда не заводили ssh-ключи и не настраивали [yubikey/skotty](https://docs.yandex-team.ru/skotty/), создайте свой первый ssh-ключ с помощью [инструкции](https://wiki.yandex-team.ru/security/ssh/#instrukciiponastrojjkessh-klientov) или настройте [yubikey/skotty](https://docs.yandex-team.ru/skotty/quick-start-guide).
3. Если у вас уже есть приватный ключ, и вы уверены, что он лежит в директории `~/.ssh`, то убедитесь, что он добавлен в ssh-agent: `ssh-add -K ~/.ssh/id_rsa`.
4. Если вы используете [yubikey/skotty](https://docs.yandex-team.ru/skotty/), то для работы infractl нужа корректно выставленная переменная окружения `SSH_AUTH_SOCK`. Попробуйте повторить проблемную команду с ней: `SSH_AUTH_SOCK=~/.skotty/sock/default.sock <command>`. Если infractl заработал, то для системного решения проблемы рекомендуем [выставить эту переменную окружения глобально](https://docs.yandex-team.ru/skotty/ssh-client#zamena-shtatnogo-ssh-agenta).
5. Если вы используете [ECDSA-ключи](https://en.wikipedia.org/wiki/ECDSA), то OAuth-токен придётся пробросить в infractl [вручную](https://docs.yandex-team.ru/infractl/troubleshooting#set-oauth-manually). Также рекомендуем перейти с хранения приватных ключей на рабочей станции на более безопасный механизм [yubikey/skotty](https://docs.yandex-team.ru/skotty/).
6. Если ключ находится, но команда не работает, убедитесь, что публичная часть ключа загружена на [staff](https://staff.yandex-team.ru).

#### Как передать OAuth-токен вручную? {#set-oauth-manually}
Если вариант с получением токена по ssh-ключам не подходит, передать его в infractl можно и вручную. Для этого получите токен по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=141d6d975f6049789ba7c78bf82ada5d) и запишите в переменную окружения `INFRACTL_TOKEN`, выполнив `export INFRACTL_TOKEN=AQAD-...`, после чего повторите проблемную команду.
