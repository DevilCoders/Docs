# Админка
[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=carsharing/ya-drive-admin&vcs=github&repoFilter=admin_next)](https://oko.yandex-team.ru/github/carsharing/ya-drive-admin?repoFilter=admin_next)

## Перед началом
1. Устанавливаем arc https://docs.yandex-team.ru/devtools/intro/quick-start-guide
2. Монтируем репозиторий:
```
mkdir -p arc && cd arc
mkdir -p arcadia store
arc mount -m arcadia/ -S store/
cd arcadia/drive/frontend/services/ya-drive-admin/
```

При перезагрузке компьютера необходимо выполнить монтирование снова, использовав только 2 последние команды:
```
arc mount -m arcadia/ -S store/
cd arcadia/drive/frontend/services/ya-drive-admin/
```

3. При необходимости прописываем в hosts
```
127.0.0.1 localhost.yandex-team.ru
```

4. Запрашиваем необходимые роли в idm. После выдачи ролей понадобится некоторое время, чтобы доступы появились

5. В начале работы настраиваем прекоммит хуки (или если по каким-то причинам они не запускаются) следующей командой:
```
printf "\n[pre-commit-hook \"drive/frontend/services/ya-drive-admin/admin_next\"]\n    pre-commit-check = drive/frontend/services/ya-drive-admin/admin_next/pre-commit" >> ~/.arcconfig
```

## Разработка
* Устанавливаем "свежий npm" для возможности использовать установку
пакетов из lock-файла
```
npm ci
```
* Для работы в админке нам понадобится установить зависимости не только в admin_next, но и в packages. Не забываем, что пакета два:
```
packages/jssip
packages/release-frontend
```

* выполнение команд
```
make install
```

* запуск storyBook
```
npm run storybook
```

## Выкатка проекта
### Настройка окружения для MacOS
1. Устанавливаем docker из self service
2. Настройка docker
    1. При необходимости запрашиваем доступ к docker registry в [IDM](https://nda.ya.ru/t/R_LHyR7x3qUgkC)
    2. Заходим в docker registry
        ```
        docker login registry.yandex.net
       ```
    - Login - логин, как на стаффе
    - Password - токен по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1)
3. Скачиваем и устанавливаем git-restore-mtime
    ```
   cd ~/some/dir
   git clone https://github.com/MestreLion/git-tools.git
   ```
4. Устанавливаем [ya tool](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)
5. Прописываем алиасы для git-restore-mtime и ya в rc файл вашего терминала (~/.zshrc или ~/.bashrc, проверить можно командой ```echo $0```)
    ```
    echo 'export PATH=$PATH:~/some/dir/git-tools(путь до папки с git-restore-mtime):~/some/dir(путь до папки с ya или до папки с аркадией)' >> ~/.bashrc
    ```

### Сборка релиза

Логи сборки складываются в build_release.log, build_docker.log, eslint-report.log и stylelint-report.log

Сборка:
- мастера (на carsharing.yandex-team.ru катаются только релизы от мастера)
    ```
    make publish [опции]
    ```
  Дополнительные опции:
  1) REVISION=<patch | minor | major | остальные параметры, доступные для npm semver>
  2) PREVIOUS_RELEASE=<версия релиза, которая есть в папке releases> -- на случай, если последняя версия релиза в папке releases некорректно собралась или работает, но еще не выкатывалась

- ветки
    ```
    make publish_branch TICKET=<номер задачи> [доп. опции]
    ```

  Отличия сборки ветки от мастера:
  - версионирование с ключом тикета и по принципу prerelease;
  - сборка не сохраняется в папку releases для фолбеков.

### Деплой релиза

Админка релизится в Nanny.

1. Открываем нужный сервис из [дашборда](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/carsharing_admin/).
 - ya-drive-admin-yp соответствует [carsharing.yandex-team.ru](carsharing.yandex-team.ru) , ya-drive-prestable и -testing - [prestable.carsharing.yandex-team.ru](prestable.carsharing.yandex-team.ru) и [testing.carsharing.yandex-team.ru](testing.carsharing.yandex-team.ru) соответсвенно
 ![Скриншот_дашборда_в_Nanny](https://nda.ya.ru/t/SSzguasG3rQvPJ)
2. На странице сервиса переходим в раздел Instance Spec.
![Скриншот страницы сервиса в Nanny](https://nda.ya.ru/t/HfI6FHEL3rQvwQ)
3. В поле Image name меняем docker тег на тег релиза. (Тег вашего релиза можно увидеть в терминале в конце сборки). Нажимаем на Save.
![Скриншот терминала с тегом релиза](https://nda.ya.ru/t/-0iNX7bL3rQyCk)
![Скриншот раздела Instance Spec](https://nda.ya.ru/t/waoOVTCB3rQx3r)
4. В появившейся модалке заполняем комментарий к релизе (можно просто продублировать тег релиза) и сохраняем.
![Скриншот модалки сохранения](https://nda.ya.ru/t/5q42JXB13rQz9i)
5. Переводим серый snapshot в cостояние Active.
![Кнопка изменения состояния](https://nda.ya.ru/t/V1wAtKPE3rR3xy)
![Модалка изменения состояния](https://nda.ya.ru/t/gU_XgcYD3rR4BP)

#### Дополнительно
- Troubleshooting деплоя в няне: [гайд 1](https://wiki.yandex-team.ru/market/frontend/infra/faq/nanny-deploy-troubleshooting/), [гайд 2](https://rtc.yandex-team.ru/docs/support/troubleshooting/nanny#deploy-fail).
- [Про blue-green деплой](https://martinfowler.com/bliki/BlueGreenDeployment.html). Активный snapshot в няне всегда синий, готовые к использованию - зеленые.

### Сборка и деплой стенда для тестирования

#### Настройка окружения
0. Подготавливаем окружение, выполнив все пункты из раздела "Настройка окружения для MacOS"
1. Если у ya tool не настроен токен (нет файла ~/.ya_token), то запускаем ```ya whoami --save-token```.
2. Получаем токен для qtools. [Авторизация qtools](https://github.yandex-team.ru/maps/infra/tree/master/packages/qtools#authorization)

#### Создание стенда
Создание стенда осуществляется пакетом @yandex-drive/release-frontend. Пока пакет не опубликован, перед началом работы нужно в папке с ним запустить npm ci.

Запуск создания стенда (должен быть включен Docker и доступен по алиасу ya):
```bash
npm run stand -- --ticket=<ключ тикета>
```
В конце вывода команды будут ссылки на стейдж и домен стенда.

#### Перевыкатка стенда
Перевыкатка стенда работает по той же команде, что и выкатка стенда

#### Удаление стенда
Удаление стенда пока необходимо делать вручную. (После https://st.yandex-team.ru/COMMONPY-279 перейдем на автоматику)

Для этого необходимо строго соблюдать порядок удаления объектов. Удаления объекта происходит не сразу, нужно дожидаться окончания этапа прежде чем переходить к следующему.
1. Переходим на [страницу балансера](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/testing.carsharing.yandex-team.ru/show/), нажимаем на домен <ваш тикет>.stand.carsharing.yandex-team.ru и удаляем домен.
   ![Кнопка удаления домена](https://nda.ya.ru/t/tOBNTw0I3uHhSN)
2. Переходим на страницу upstream'ов балансера, выбираем upstream с ключом тикета и удаляем.
   ![Кнопка удаления апстрима](https://nda.ya.ru/t/1LI2mI9v3uHjfu)
3. Переходим на страницу бекендов балансера, находим бекенд с ключом тикета и удаляем.
   ![Кнопка удаления бекенда](https://nda.ya.ru/t/7FTcMUwn3uHjwB)
4. Переходим в Deploy на страницу стейджа со стендом (ссылка вида https://deploy.yandex-team.ru/stages/<ключ_тикета>). Нажимаем Delete и подтверждаем удаление.
   ![Кнопка удаления стейджа](https://nda.ya.ru/t/g0rgoEWl3uHkEu)

#### Дополнительно
Для удобства оповещения заказчика в трекере в очереди DRIVEFRONT есть макрос, который автоматически формирует ссылку на стенд и переводит задачу в тестирование
![Макрос в трекере](https://nda.ya.ru/t/_kGydChS3uHhDM)

#### Ссылки:
- [Все стейджи стендов в Deploy](https://deploy.yandex-team.ru/projects/drive-admin-stands)
- [Страница балансера стендов](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/testing.carsharing.yandex-team.ru)
