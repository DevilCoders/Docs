# Agency-office


## Первый запуск

### 1. Получаем токены и прописываем их в переменные окружения
* SANDBOX_AUTH_TOKEN по [ссылке](https://sandbox.yandex-team.ru/oauth)
* STATFACE_TOKEN по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=801af94c94e040848ebe206086a7a4e2)

### 2. Прописываем в hosts резолв на локальную машину
`127.0.0.1 localhost.yandex.ru`

### 3. Устанавливаем проект и зависимости
`$ npm install`

### 4. Запускаем проект
`$ npm start`

### 5. Добавляем сертификат в браузер
После запуска проекта, в консоли появится надпись, о том куда был сохранен сертификат. Данный сертификат нужно [добавить](https://wiki.yandex-team.ru/security/ssl/sslclientfix/#vbrauzeraxsecerrorunknownissuer) в браузер. В гайде устанавливается не тот сертификат, нам нужен именно, скачанный при запуске проекта, сертификат (в линуксе путь до сертификата `~/.config/templar/ssl/rootCA.crt`).

### 6. Открываем веб интерфейс
Переходим на https://localhost.yandex.ru:3443/agency-cabinet

### Что можно сделать если не работает
- Перезагрузить компьютер.
- Стопнуть проект, прожать `$ npm run clean-archon` (в консоли появятся дополнительные инструкции), выполнить заново с 4го пункта.


## Бункер
Бункер добавили [тут](https://st.yandex-team.ru/BUNKERCREATE-187), [документация по бункеру](https://wiki.yandex-team.ru/verstka/tools/bunker/doc-tmp/)
В бункере у нас есть конфиг, по которому мы понимаем, для каких агентсв какие открыты разделы (в рамках бета-тестирования)
[основная морда](https://bunker.yandex-team.ru/agency-cabinet/), [схемы](https://bunker.yandex-team.ru/agency-cabinet/.schemas)


## Настройка уведомлений
Незабываем настроить уведомления в аркануме, инструкция [тут](https://docs.yandex-team.ru/arcanum/notifications/pr)


## Разработка автотестов

### Документация по гермионе
Долго и нудно изучаем доки по гермионе [тут](https://wiki.yandex-team.ru/search-interfaces/testing/hermione/#faq) [тут](https://github.com/gemini-testing/hermione)

### Первый запуск

#### Устанавливаем nvm
```shell
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.38.0/install.sh | bash
source ~/.nvm/nvm.sh
```
Убеждаемся, что в .bash_profile в конец добавилось
```shell
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

#### Настраиваем arc
[Документация](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)

#### Устанавливаем
`$ npm ci`

#### Собираем
`$ npm run build`

#### Добавляем переменные окружения для тестов
1. Создаем файл `.env` в корне проекта (рядом с файлом `package.json`).
2. Добавляем в файл переменную VAULT_TOKEN, значение нужно взять [тут](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982).
3. Добавляем в файл переменную TEST_INST_URL, значение может быть или `https://hamster.yandex.ru/agency-cabinet` или `https://localhost.yandex.ru:3443/agency-cabinet`, если хотите отлаживаться с локальной версией.
4. В итоге в файл `.env` должны быть добавлены две переменные:
```
VAULT_TOKEN=***
TEST_INST_URL=***
```

> Не забывайте, что для работы с локальной версией ее необходимо настроить и поднять (описано выше)

#### Запускаем gui со всеми тестами
```shell
npm run hermione:gui
```
