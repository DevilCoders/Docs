# aptly

## Общая информация

Представляет собой оберткy над **aptly**, предназначенную для кэширования и автоматического обновления пакетов. Сервис живет в докере, написан на GO.

* [Сайт Aptly](https://www.aptly.info/)
* [Код сервиса](https://a.yandex-team.ru/arc_vcs/classifieds/infra/aptly)
* [Секреты](https://yav.yandex-team.ru/secret/sec-01g63hzvghswkh9qckg7c61zqe/explore/versions)
* Графики: [update job](https://grafana.vertis.yandex-team.ru/d/4HD32Vq7z/aptly-update?orgId=1), [promote job](https://grafana.vertis.yandex-team.ru/d/eGI3h43nz/aptly-promote?orgId=1)
* Админка: [update job](https://admin.vertis.yandex-team.ru/services/aptly-update), [promote job](https://admin.vertis.yandex-team.ru/services/aptly-promote)

## Логика работы

Сервис создает зеркала во [внутреннем S3](https://yc.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/storage/buckets/adm?key=aptly%2F) для следующих репозиториев:
* `http://mirror.yandex.ru/ubuntu xenial-updates`
* `http://mirror.yandex.ru/ubuntu focal-updates`
* `http://common.dist.yandex.ru/common stable/all/`
* `http://common.dist.yandex.ru/common stable/amd64/`

{% note info %}

Стоит заметить, что репозитории не полностью зеркалируются, а только для тех пакетов, которые указаны в роли [common-packages](https://a.yandex-team.ru/arcadia/classifieds/infra/vertis-ansible/roles/common-packages).

{% endnote %}

## Архитектура и принцип работы

Состоит из двух батч-джоб - `aptly-update` и `aptly-promote`.

Схематичная архитектура и функции компонентов
![image](images/aptly.jpg)

### update

Данная джоба запускается **каждый понедельник в 12:30**.

Алгоритм работы:
* Через локальный `aptly` создает два зеркала - зеркало текущего состояния репозитория в S3 и актуальное зеркало удаленного репозитория.
* Сливает их в один снапшот, **сохраняя удаленные версии пакетов**.
* Загружает полученный снапшот в S3. Таким образом, в S3 мы добавляем все новые версии пакетов, сохраняя старые.
* Проверяет новые версии пакетов из ансибла в новом снапшоте. Если есть обновления - создает Пулл-реквест на обновление в **тестинге**, и пушит в S3 метаинформацию (список новых версий пакетов) для **корректного обновления прода**

### promote

Данная джоба запускается **каждую среду в 12:30**.

Алгоритм работы:
* Проверяем, что Пулл-реквест для тестинга смерджен. Если нет - пропускаем текущую итерацию
* Создаем Пулл-реквест для **прода**, обновляя в нем пакеты до версий, до которых обновили в тестинге. Именно для этого необходимо сохранять метаинформацию в S3

## Для дежурного

**В понедельник:**

Дежурному нужно проверить, что новые пакеты ничего не ломают, затем смержить PR и закрыть тикет. Если есть сомнения - лучше обсудить обновление пакета в чате vertis-admin.

**В среду:**

Дежурному надо проверить, что обновление в тестинге прошло успешно и ничего не сломалось за два прошедших дня. Если все хорошо - смерджить PR и закрыть тикет.

