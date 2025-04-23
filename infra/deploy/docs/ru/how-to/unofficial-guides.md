# Инструкции наших пользователей

Раздел содержит ссылки на ресурсы, посвящённые миграции в Y.Deploy и повседневным операциям с сервисами.

{% note alert %}

Команда Y.Deploy не отвечает за точность и полноту пользовательских публикаций, поскольку страницы могут изменяться владельцами без предупреждения.

{% endnote %}


## Миграция

- [Пошаговый гайд от ребят из образовательных сервисов](https://wiki.yandex-team.ru/e7n/dev/moving-schoolbook-to-deploy). Коллеги написали большой гайд, раскрывающий сложные и неочевидные моменты, связанные с переездом.
- [Пошаговый гайд от semenmakhaev@ про переезд из Qloud](https://wiki.yandex-team.ru/bliss/deploy-migration). Для тех, кто по каким-то причинам не хочет использовать миграторы из [Qloud](../how-to/migration/qloud/migrator.md) или из [Nanny](../how-to/migration/nanny.md).
- [Пошаговый гайд от borisovdenis@ про переезд Вебмастера](https://wiki.yandex-team.ru/users/borisovdenis/wmc-instrukcija-po-pereezdu-v-y.deploy/)
- [Из Самогона в Y.Deploy](https://wiki.yandex-team.ru/samogon/instrukcija-po-pereezdu-v-yandex-deploy).
- [Некоторые вопросы переезда от NOC](https://wiki.yandex-team.ru/noc/deploy). В качестве первых сервисов коллеги перевезли оверсер и графен и составили список особенностей, на которые следует обратить внимание при переезде.
- [Вики-кластер , посвящённый переезду Заправок](https://wiki.yandex-team.ru/benzin/dev/ya.deploy/).
- [Гайд](https://wiki.yandex-team.ru/users/sanyabas/deploy/) от группы разработки платформы TurboApps.
- [Тикеты на переезд от команды Браузера](https://st.yandex-team.ru/DECOMMISSIONING-231).

## Повседневные операции

### Как переключить трафик

1. Инструкция для смелых от укого:semenmakhaev: [вот тут](https://wiki.yandex-team.ru/bliss/deploy-migration/#shag8.perekljuchittrafik)

### Про автоматизацию в Y.Deploy

1. Инструкция от укого:mokosha по интеграции вашей CI и Y.Deploy [вот тут](https://wiki.yandex-team.ru/bliss/release-integration/)

### Нагрузочное тестирование

Нативное решение и соответствующие инструкции будут сделаны в рамках цели: [Нагрузочное тестирование в Y.Deploy](https://goals.yandex-team.ru/filter?user=12890&importance=1,2,0,3&goal=74077)
А пока можете использовать [вот эту инструкцию](https://wiki.yandex-team.ru/bliss/load-testing/), заменив компоненты Qloud соответствующими компонентами Y.Deploy.

#### Базовые возможности troubleshooting'а

1. Настоятельно рекомендуем ознакомиться с [официальным разделом](../concepts/pod/pod.md).
1. Еще немного про troubleshooting: [вот тут](https://wiki.yandex-team.ru/bliss/deploy-migration/#sekretytrablshutingadljadevops-manjakov)
