## Переезд в Аркадию

### Полезные ссылки

1. [Базовая инструкция](https://docs.yandex-team.ru/devtools/intro/quick-start-guide) по работе с Аркадией.
2. Работа с PR и Review в [Арканум](https://docs.yandex-team.ru/arcanum).
3. Аркадия [FAQ](https://wiki.yandex-team.ru/arcadia/arc/faq).
4. Полный список [Arc CI](https://docs.yandex-team.ru/arc/ref/commands).
5. [Родительская задача](https://st.yandex-team.ru/TRAVELFRONT-7656) по переезду в Аркадию.
6. [Канал в Slack](https://yndx-travel.slack.com/messages/C039R39S022) по координации и статусам.
7. [Настройки командного интерпретатора](https://docs.yandex-team.ru/devtools/src/arc/config#shell).

### FAQ на время пеерезда

#### 1. Где теперь находятся проекты из Travel UI.

В папочке frontend: https://a.yandex-team.ru/arc_vcs/travel/frontend

#### 2. Что с ветками, PR из которых не были замержены в dev.

Все ветки при миграции получили такой префикс: `external/github/travel-ui/ya-travel/...`. Один из возможных путей:

```
arc pull trunk
arc fetch external/github/travel-ui/ya-travel/<branch-name>
arc checkout -b 'users/<your-login>/<branch-name>' external/github/travel-ui/ya-travel/<branch-name>
arc rebase trunk
arc push -u users/<your-login>/<branch-name>
arc pr create -m '<pr-name>'
```

#### 3. Клиентские precommit/prepush хуки.

Необходимо скопировать файл `.arcconfig` из корня portal и положить по пути `~/.arcconfig`:
Пропустить проверку можно через: `--skip-hook=HOOK-NAME`
Обязательно проверяем глазами в PR работу prettier!

#### 4. Перестал работать TVM demon.

В процессе миграции пришлось отозвать тестовый TVM Token на тестовых окружениях. Необходимо [скопировать последнюю версию](https://yav.yandex-team.ru/secret/sec-01dq7m4t97es448ye96w6fd9ac/explore/version/ver-01g07c6g3tncmf1d3yb3nsjm8r), поменять в конфиге и перезапустить TVM demon.

#### 5. Тестовые стенды.

Появляются https://travel.farm.yandex-team.ru/project/ya-travel на вкладке Portal.

#### 6. Что-то не работает, остались вопросы и предожения.

В задачку https://st.yandex-team.ru/TRAVELFRONT-7656 в комменты или в канал https://yndx-travel.slack.com/messages/C039R39S022 или
в лс maxim-urukov.
