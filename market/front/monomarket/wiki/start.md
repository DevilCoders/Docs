Начальная настройка
=================

1. Настройка **ssh**
    - Если вы никогда в яндексе не настраивали ssh, то скорее всего нужно выполнить [эту инструкцию](https://wiki.yandex-team.ru/q/devops/faq/generate-and-put-ssh-key/)
    - Иначе, всё скорее всего уже настроено


2. установить **nvm**
    - **ubuntu**:
        - устанавливаем [nvm](https://github.com/nvm-sh/nvm#install--update-script)
    - **macOS**:
        - сначала устанавливаем [XCode](https://itunes.apple.com/us/app/xcode/id497799835?mt=12) (или `xcode-select --install` в консоли) и **Homebrew** (в предустановленной программе Self Service -> Free Software).
        - затем в консоли:
           ```bash
           brew install nvm
           ```
          Возможно, для установки потребуется выдать права. Инструкция как это сделать будет в комментарии от `brew`.

3. Устанавливаем **yarn** и 16 версию **node**:
```bash
nvm install 16.9.1
nvm use 16.9.1
nvm alias default 16.9.1

npm i -g yarn@1.22.10 npm@6.14
```

4. Перенастраиваем registry npm на яндексовский
```bash
npm config set registry https://npm.yandex-team.ru
```

5. Устанавливаем **ya tool**
    - выполняем [Системные требования](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#system-requirements), [Установку Arc](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#arc-setup) и [Получение исходных кодов](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#mount) из инструкции: [Быстрый старт](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)
    - добавляем **arc/arcadia** в **PATH**. Для этого нужно прописать строчку вида `PATH="${PATH}:${HOME}/arc/arcadia"` к себе в `~/.bashrc` или аналогичный конфиг (зависит от окружения).
    - проверить, что **ya** установлен можно попыткой выполнить `ya` в консоли

6. Монтируем аркадию, переходим в `market/front/monomarket`

7. Вызываем `yarn run bootstrap`
   Если падает со словами `Command failed: tar -xzvf modules.tar.gz`, то надо посмотреть содержимое этого файла.
   Скорее всего там `{“reason”: “Unauthorized request from dynamic nets.“}`.
   В этом случае, нужно выполнить в консоли `ya whoami`. Если токен не установлен, но с svn всё ок и ssh настроен, то можно выполнить `ya whoami --save-token`. Должно помочь)


На этом минимальная настройка готова. Однако для удобной работы желательно сделать ещё пару вещей:

1. Устанавливаем глобальную копию **yammy**: `npm i -g @yandex-market/yammy` (достаточно сделать 1 раз, он автоматом берёт локальную версию из репозитория если находит её - так что обновления потребуются только при изменения мажорного релиза)

2. Подключаем авто-комплит для **yammy**:
   переходим в репозиторий и выполняем
   ```shell
   yammy _autocomplete > ~/.yammy_autocomplete.bash
   chmod +x ~/.yammy_autocomplete.bash
   echo "source '${HOME}/.yammy_autocomplete.bash'" >> .bashrc
   ```
