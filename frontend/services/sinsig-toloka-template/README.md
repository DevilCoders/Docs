# SinSig
Шаблон в Яндекс.Толока для SinSig (Единый сигнал).
* До этого разработка велась в другом репозиории: [Ссылка на репозиторий](https://bb.yandex-team.ru/projects/ASSESSMENT/repos/relevance-context/browse)
* О проекте: [Статья на вики](https://wiki.yandex-team.ru/JandeksPoisk/KachestvoPoiska/AnalyticsAndProductization/offline-metrics/Edinyjj-signal/)
* О шаблоне: [Статья на вики](https://wiki.yandex-team.ru/JandeksPoisk/KachestvoPoiska/AnalyticsAndProductization/offline-metrics/Edinyjj-signal/SinSigQueryCard/)

Проект содержит 5 шаблонов:

* Основной шаблон (/src/sinsig) – главный шаблон для оценки документов
* Обоснования (/src/rationale) - шаблон дополнительного обоснования оценки пользователем
* Проверки обоснования (/src/rationale-check) – шаблон проверки обоснования другим пользователем ответа из шаблона обоснования
* Проверка карточки (/src/complaint-check) - шаблон проверки жалобы на карточку
* Doc-by-Doc (/src/dbd)

Общая директория (/src/shared) - содержит общие тулзы, компоненты и т п, которые используются в нескольких или всех шаблонах

## Запуск
```
❯ npm install
❯ npm run <template-key>:start
# <template-key>: sinsig | rationale | rationale-check | dbd | complaint-check
```

## Деплой шаблона
* Получить [Oauth-токен](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982).
Это нужно для того, что бы скрипт деплоя сходил от твоего имени в api секретницы за авторизационными данными заказчиков

* После этого необходимо выполнить следующую команду:
```
❯ OAUTH_TOKEN="твой Oauth-токен" npm run deploy -- --key <batch-key>
# <batch-key> - один из ключей в файле `sinsig.deploy.batch.json` или all:<env>.
# Например:
# sinsig:sandbox
# rationale:production
# all:sandbox
```

* Для того, что бы каждый раз не передавать свой токен можно в директориии проекта создать файл `.env` и добавить в него:
```
OAUTH_TOKEN="твой Oauth-токен"
```

Если деплой падает с ошибкой `Response code 401 (UNAUTHORIZED)`, скорее всего, у тебя нет доступа к какому то из секретов.
Вот список используемых секретов (там написанно у кого можно попросить доступ):
* Токен для [robot-sinsig](https://yav.yandex-team.ru/edit/secret/sec-01d2w5sp6m2kmcj90spk7q2ksn/explore/versions)
* Токен для [robot-yang-req](https://yav.yandex-team.ru/edit/secret/sec-01d2w5x3frsfvtxq6z2yd5acb5/explore/versions)
* Токен для [robot-yang-tutor](https://yav.yandex-team.ru/secret/sec-01daxfpv3djnyvxxb2p4n2y5r2/explore/versions)
* Токен для [dbd-toloka](https://yav.yandex-team.ru/secret/sec-01daxffsfbfsca6dgc1xcpzae7/explore/versions)

## Мониторинги

* [Error Booster](https://error.yandex-team.ru/projects/sinsig-toloka-tpl)


## Разработчики
* **Vlad Potapov** - *Разработка и поддержка проекта в настоящее время* - [@vladpotapov](https://staff.yandex-team.ru/vladpotapov)
* **Daniil Gorbachev** - *Разработка и поддержка проекта в настоящее время* - [@allonsydaniel](https://staff.yandex-team.ru/allonsydaniel)
* **German Volkov** - *TTK developer, initial work* - [@volkov97](https://staff.yandex-team.ru/volkov97)
* **Alexander Verkhoglyad** - *Yandex.Toloka developer, PR reviews* - [@hexode](https://staff.yandex-team.ru/hexode)

## При поддержке
* [toloka-templates-kit](https://bb.yandex-team.ru/projects/ASSESSMENT/repos/toloka-templates-kit/browse) - tool for developing templates for Yandex.Toloka
