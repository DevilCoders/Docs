# Плашка о сборе кук - v.2

![Image description](./screen.png)

## Разработка

```bash
cd ./packages/gdpr-popup
npm ci
npm start
# Смотреть: http://localhost:3000/index.html
# Сразу открывать вкладку с настройками: http://localhost:3000/index.html?settings=1
```

#### Обновление переводов
```
npm run i18n:pull
```

## Сборка

```bash
npm run build:ru
# Собирает скрипт для вставки плашки в папке build - ru.js

npm run build
# Собирает все языки
```

### Локальная проверка

Для тестов скрипты загружаются в bucket internal-metrika-betas c помощью:
```npm run create-test-stand```

Важно: загрузить с виртуалки в s3 не получится, доступ есть только с ноутбука сотрудника, настройка aws:

https://wiki.yandex-team.ru/mds/s3-api/s3-clients/#nastrojjkaawscli

После запуска файлы плашки для разных языков будут лежать тут:

https://s3.mds.yandex.net/internal-metrika-betas/gdpr-popup/v2/ru.js

https://s3.mds.yandex.net/internal-metrika-betas/gdpr-popup/v2/en.js

Чтобы проверить интеграцию со счетчиком, надо собрать код счетчика и запустить прокси с подмененным адресом попапа, доку по запуску можно найти тут:

https://a.yandex-team.ru/arc/trunk/arcadia/metrika/frontend/watch#testirovanie-gdpr-plashki

Попап можно увидеть в режиме инкогнито по ссылке:

https://yandex.ru/?yagdprcheck=1

Важно: если попапа нет, проверить, что не выставлена кука gdpr.

### Тестирование в ветке

Для тестирования в ветке, плашку надо собрать из ветки:
```npm run create-test-stand```

После чего дать qa в комментариях к тикету инструкцию по запуску прокси в коде счетчика:

https://a.yandex-team.ru/arc/trunk/arcadia/metrika/frontend/watch#testirovanie-gdpr-plashki

### Тестирование в релизе

Аналогично тестированию в ветке, но собрать надо из релизной ветки, а не ветки с задачей.

### Выкладка новой версии с помощью Sandbox
Задача `METRIKA_FRONTEND_STATIC_UPLOAD` с параметрами:
```
1) git репозиторий - git@github.yandex-team.ru:metrika/frontend.git;
2) ветка - та, из которой нужно собрать (скорее всего релизная);
3) bucket - gdpr;
4) версия - любая;
5) versioned_folders - не нужны;
6) unversioned_folders = packages/gdpr-popup/build: popup/v2
```

![task](./task.png)

[`Пример задачи`](https://sandbox.yandex-team.ru/task/735290012/view)

Скрипты загружаются в bucket gdpr:

```
https://s3.mds.yandex.net/gdpr/popup/v2/<lang>.js
https://yastatic.net/s3/gdpr/popup/v2/<lang>.js
```

### События GDPR

Первый экран:
* Принять = **GDPR-ok, GDPR-ok-view-default**.
* Настроить = **GDPR-settings**.

Второй экран:
* Принять все = **GDPR-ok, GDPR-ok-view-detailed**.
* Принять выбранные = **GDPR-ok-view-detailed-[0-3]** - в зависимости от выбора настроек, в соответствие со
значениями флага gdpr. В случае, если отмечена еще какая-то группа, кроме технической, добавляется **GDPR-ok**.
