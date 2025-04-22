## Инструкция по переезду в монорепо

#### Написано по мотивам

* [Бортовой журнал переезда в монорепу от mrdekk](https://wiki.yandex-team.ru/users/mrdekk/monorepo/)
* [Инструкция по переезду в монорепу от lenant](https://wiki.yandex-team.ru/users/lenant/movetomonorep/)
* [Инструкция по переезду в монорепу от thevery (MOBILECOM-13)](https://st.yandex-team.ru/MOBILECOM-13)
* ваша инструкция может быть тут =], шлите PR!

### Инструкция

В рамках [переезда всех мобильных приложений в единый репозиторий Tier1](https://clubs.at.yandex-team.ru/mobile-dev/524) нужно перенести ```%project% %platform%``` в подпапку as is (то есть зависимости и система сборки не меняются, меняется только место хранения кода). Процесс перехода состоит из двух частей:

1. Перенос кода в bb в подпапку в  testing-репозиторий, настройка новых конфигов teamcity и bitbucket, верификация. Команда разработки в этот момент продолжает работать как обычно, блокирующих процессов тут нет.
2. Перенос кода в  monorepo (продакшен-репозиторий), перенастройка teamcity с testing на monorepo. Перед переездом и до его окончания рекомендуется закрыть существующие PR-ы и ничего не коммитить, поэтому удобнее проводить его вечером-ночью-утром.

Для переноса кода можно воспользоваться помощью devtools или осуществить самостоятельно по инструкции ниже.

#### Инструкция по переносу кода в монорепу:

Перенос репы в монорепу (сначала  testing , затем  monorepo )

1. Запрашивам доступ в в оба репозитория через https://idm.yandex-team.ru -> Общий Bitbucket -> Mobile Monorepo -> * -> Project Write.
2. Скачиваем скрипт миграции путей с https://a.yandex-team.ru/arc/trunk/arcadia/vcs/migration/scripts/index_filter_subdir.sh и делаем ему 

    ```
    chmod:  chmod +x ~/index_filter_subdir.sh
    ```
    
    (на macOS надо заменить в скрипте \t на TAB, в Android Studio Tab ставится некорректно, лучше использовать vim)
3. Создаём папку для рабочей копии проекта и добавляем его как origin (обратите внимание на --bare и погуглите что это если не знаете), например:

    ```
    git init repo.git --bare
    cd repo.git
    git remote add origin git@github.yandex-team.ru:DataSync/datasync-android-sdk.git
    ```
    
4. Импортируем ветки/теги с префиксом (**поменяйте  common/android/datasync на свой префикс**):

    ```
    git config remote.origin.fetch 'refs/heads/*:refs/heads/common/android/datasync/*'
    git config --add remote.origin.fetch 'refs/tags/*:refs/tags/common/android/datasync/*'
    git fetch --no-tags origin
    ```

5. Запускаем миграцию путей скриптом (**поменяйте common/android/datasync на свой префикс**):

    ```
    git filter-branch --index-filter '~/полный/путь/до/index_filter_subdir.sh common/android/datasync' --tag-name-filter cat -- --all 
    ```

    **При вызове этого скрипта ВАЖНО! поменять  common/android/datasync на свой префикс.**

6. Добавляем testing, проверяем бранчи/теги:

    ```
    git remote add testing ssh://git@bb.yandex-team.ru/mobile/testing.git
    git push --tags testing --dry-run 
    git push --all testing --dry-run
    ```

7. Заливаем master-бранч, открываем PR для проверки:
 
    ```
    git push testing common/android/datasync/master
    ```

8. После проверки заливаем в прод:

    ```
    git remote add monorepo ssh://git@bb.yandex-team.ru/mobile/monorepo.git
    git push --all monorepo
    git push --tags monorepo
    ```