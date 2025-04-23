Старт с нуля для новичков
----

Инструкция структурирована в виде чеклиста и является компиляцией ссылок на другие полезные инструкции и ресурсы. Последовательное движение по чеклисту приведет вас к успешному запуску проекта.


### Общее

1. Убедитесь, что у вас
    - сгенерирован ssh ключ
       ```sh
       ls -l ~/.ssh/id_rsa
       ```

    - добавлен в ssh-agent
      ```sh
      # The `-K` is Apple's specific option, which stores the passphrase in your keychain for you when you add an ssh key to the ssh-agent.
      ssh-add -K ~/.ssh/id_rsa
      ```

    - прописан в ssh конфиге
       ```sh
       cat ~/.ssh/config
       Host *
         UseKeychain yes
         AddKeysToAgent yes
         IdentityFile ~/.ssh/id_rsa
       ```

    - добавлен на [стафф](https://staff.yandex-team.ru)

2. Сразу стоит поставить `brew` – пакетный менеджер для macos.
    - https://brew.sh


### Система хранения версий

В Яндексе вместо git'а используют собственную систему контроля версий – [arc](https://docs.yandex-team.ru/arc/). Необходимо её установить.
- https://docs.yandex-team.ru/arc/
- https://wiki.yandex-team.ru/lavka/dev/front/arcadia/

1. Монтировать лучше не всю аркадию, а только нужные директории. Пример алиаса для монтирования аркадии:
   ```sh
   # Подразумевается, что
   #  - ~/Projects      – директория для хранения рабочих проектов
   #  - ~/Projects/arc  – директория под аркадию
   # Алиас для монтирования аркадии, использование: arc_mount
   arc_mount () {
      arc_mount_args=(
        # Каталог, в котором будет смонтировано рабочее дерево
        -m ~/Projects/arc/arcadia
        # Каталог, в котором будет храниться локальное состояние репозитория и скачиваемые данные
        -S ~/Projects/arc/store
        # --path-filter позволяет селективно чекаутить рабочее дерево, аналог sparse-checkout
        # 1. taxi – дериктория для всех проектов фудтеха и райдтеха
        --path-filter taxi
        # 2. frontend/packages – общеяндексовые npm пакеты
        --path-filter frontend/packages
        # 3. junk/$USER – личная папка
        --path-filter junk/$USER
        # 4. ya – cli утилита, представляет собой единую точку входа для любых действий,
        #    связанных с процессом разработки в репозитории Arcadia
        #    https://wiki.yandex-team.ru/yatool/
        --path-filter ya
        # 5. Прочие системные директории и файлы. Требуются для корректной работы ya утилиты.
        --path-filter devtools
        --path-filter build
        --path-filter .arcadia.root
        --path-filter .arcignore
      )
      arc mount "${arc_mount_args[@]}"
   }
   ```

   > **Note:** если у вас уже есть смонтированная аркадия, то чтобы корректно перейти на вариант с `--path-filter`
   > необходимо убедиться что:
   > 1. Сохраните всё, что вы не хотите потерять
   >    - запушьте все ваши изменения
   >    - сохраните файлы из stash'а
   > 2. Убедитесь, что вы указываете правильный путь к вашему стору. Если вы укажите новый путь, то «потеряете» всё
   >    сохраненное вами ранее: локальные ветки, стеш и т.д. Для этого убедитесь, что вы укажите тот же путь к стору,
   >    что вы уже используете.
   >    `cat ~/.arc/mounted_points`
   > 2. Перемонтируйте арк
   >    ```sh
   >    arc unmount
   >    arc_mount # используем алиас
   >    ```
   > 3. Теперь сделайте reset, вам об этом сообщит команда `arc mount` на предыдущем шаге.
   >    ```sh
   >    arc reset --hard HEAD
   >    ```

   Добавляем его в `~/.bashrc` или `~/.zshrc`.

2. `--path-filter` на данный момент экспериментальная функция и имеет ряд ограничений.
    - https://clubs.at.yandex-team.ru/arcadia/26719/26750#reply-arcadia-26750

3. Создаем алиас для `ya` утилиты
   ```sh
   ln -s ~/Projects/arc/arcadia/ya /usr/local/bin/ya
   ya --version
   ```

4. Проверяем, что мы авторизированы
   ```sh
   ya whoami
   ```
   Если нет, то получаем токен
   ```sh
   # Получаем токен https://oauth.yandex-team.ru/authorize?response_type=token&client_id=f4d36b7671004ed9850148fa645acac6
   # и сохраняем его в .ya_token файле
   nano ~/.ya_token
   chmod 600 ~/.ya_token
   ya whoami
   ```

5. Если используете WebStorm, то требуется его пропатчить, чтобы избежать тормозов при работе с репозиторием.
   ```sh
   ya ide fix-jb-fsnotifier
   ```
    - Подробнее [здесь](https://clubs.at.yandex-team.ru/arcadia/26326)

6. Также следует поставить плагин, если вы пользуетесь VSCode или WebStorm
    - https://clubs.at.yandex-team.ru/arcadia/26326


### Запуск приложения

1. Устанавливаем [nvm](https://github.com/nvm-sh/nvm), чтобы через него поставить нужную версию nodejs и npm.

2. Переходим в директорию монорепы Лавки
   ```sh
   cd ~/Projects/arc/arcadia/
   cd taxi/lavka/frontend
   ```

3. Устанавливаем необходимую версию nodejs
   ```sh
   nvm install
   nvm use
   ```

4. Устанавливаем зависимости
   ```sh
   npm ci
   ```

5. Настраиваем нужный вам проект
   ```sh
   npm bootstrap:webview
   # или
   npm bootstrap:website
   ```

6. Переходим к инструкции необходимого вам проекта
    - [Webview](https://a.yandex-team.ru/arcadia/taxi/lavka/frontend/projects/webview/README.md)
    - [Website](https://a.yandex-team.ru/arcadia/taxi/lavka/frontend/projects/website/docs/CONTRIBUTING.md)


### Troubleshooting

1. Конспект встречи по Аркадии. Основные мысли и полезные ссылки.
https://wiki.yandex-team.ru/lavka/web/meeting-summaries/21-03-2022-arcadia-qa/
