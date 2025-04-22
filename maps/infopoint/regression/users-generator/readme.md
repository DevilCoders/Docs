## Генерация пользователей (create_users)
Генерация пользователей производится с помощью [TUS (Test User Service)](https://wiki.yandex-team.ru/tus/)

Для генерации потребуется [tus token](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=9052de6e4cf142039a7ee44ac03e4614)

Утилита выводит в stdout uid, username, password сгенерированных пользователей.

Пример использования:
```sh
# Если tus-token не предоставлен, будет прочитана перемернная окружения TUS_TOKEN
./create_users.py -c 1 [-t <tus_token>] > users_file
```

## Генерация OAuth токенов (generate_tokens)
Для получения OAuth токена нужно воспользоваться утилитой generate_tokens

Для работы потребуются [секреты приложения](https://yav.yandex-team.ru/secret/sec-01fmw0h4qpyvn2jmykqssjvsv1), а именно client_id и client_secret

```sh
# Если client_id не предоставлен, будет прочитана перемернная окружения INFOPOINT_USERS_GENERATOR_CLIENT_ID
# Если client-secret не предоставлен, будет прочитана перемернная окружения INFOPOINT_USERS_GENERATOR_CLIENT_SECRET
./generate_tokens.py -u <users_file> [-i <client_id> -s <client-secret>] > users
```

[Пользователи](https://yav.yandex-team.ru/secret/sec-01f8fr0m1s1g4bzqxvrv4z3kde/explore/versions), созданные на данный момент
