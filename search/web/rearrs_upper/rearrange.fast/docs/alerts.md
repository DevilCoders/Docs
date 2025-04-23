# Описание алертов
## Алерт на возраст данных (fast data age) {#fast-data-age}
### Описание {#fast-data-age-desc}
Возраст быстрых данных (fast data) на инстансах ноапача превысил порог (больше 100 минут).
Возраст считается как разница между текущим временем на хосте и временем последнего коммита в  [rearrange.fast](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrs_upper/rearrange.fast).

* Алерт для **WEB**: [juggler](https://juggler.yandex-team.ru/check_details/?host=web_sandwich.NOAPACHE_fast_data_age_chart_for_all_dc&service=for_all_dc&last=1DAY)
* Алерт для **VIDEO**: [juggler](https://juggler.yandex-team.ru/project/search.noapache.fast_data/aggregate?host=noapache-video&service=fast-data-age)
* Алерт для **беток**: [juggler](https://juggler.yandex-team.ru/project/report-infra-alerts/aggregate?host=web_sandwich.NOAPACHE_fast_data_age_betas_chart_for_all_dc&service=for_all_dc)

1. Посмотреть на запуски релизов:
    * [fast-data WEB CI](https://arcanum.yandex-team.ru/projects/noapache-web/ci/releases/timeline?dir=search%2Fweb%2Frearrs_upper%2Frearrange.fast%2Fci%2FWEB&id=fast-data-release)
    * [fast-data VIDEO CI](https://arcanum.yandex-team.ru/projects/noapache-video/ci/releases/timeline?dir=search%2Fweb%2Frearrs_upper%2Frearrange.fast%2Fci%2FVIDEO&id=fast-data-release)
    * [fast-data betas CI](https://arcanum.yandex-team.ru/projects/noapache-web/ci/releases/timeline?dir=search%2Fweb%2Frearrs_upper%2Frearrange.fast%2Fci%2Fbetas&id=fast-data-release)
2. Найти **Failed** релиз:
    1. Зайти в любую Failed таску
    2. (Если есть) Child tasks
    3. (Если есть) Show all children
    4. (Если есть) Зайти в самую глубокую Failed/Timed out сабтаску
    5. Посмотреть на ошибку:
        Тип таски | Статус таски | Ошибка в таске | Причина | Как чинить
        :--- | :--- | :--- | :--- | :---
        DEPLOY_FAST_DATA | TIMEOUT |&nbsp;| Залипла выкладка данных на сервис. | [Как чинить?](how-to-fix.md#stucked-deploy)
        TEST_REARRANGE_DATA_FAST -> TEST_REARRANGE_DATA_FAST_ON_YAPPY_BETA -> DEPLOY_FAST_DATA | FAILURE/TIMEOUT |&nbsp;| Проблемы с выкладкой данных на бету. | [Как чинить?](how-to-fix.md#beta-deploy-fail)
        TEST_REARRANGE_DATA_FAST -> TEST_REARRANGE_DATA_FAST_ON_YAPPY_BETA | FAILURE | `Incorrect fast data version on ...` | Данные выложились на бету, но данные после этого поменялись. | [Как чинить?](how-to-fix.md#beta-deploy-fail)
3. Иначе:
    1. Зайти на [график возраста данных](https://nda.ya.ru/t/RBLxf5Kl3iN5wV)
    2. Топ по хостам (по убыванию)
    3. Если проблема только на одном хосте, пойти на него, почитать, сохранить логи (файлы `bstr.err`, `noapacheupper.err`).

### Когда получилось определить проблему (ну, или нет) {#ok-what-now}
1. Оповестить [@alex-ersh](https://staff.yandex-team.ru/alex-ersh).
2. Попробовать устранить проблему самостоятельно: [гайды](how-to-fix.md).
3. Если непонятно как, то передать [@mya-engineer](https://staff.yandex-team.ru/mya-engineer), [@alex-ersh](https://staff.yandex-team.ru/alex-ersh).
4. Сделать тикет в очереди [NOAPACHE](http://st.yandex-team.ru/NOAPACHE) с описанием проблемы, прикрепить логи, графики, ссылки на таски, исполнителем сделать [@mya-engineer](https://staff.yandex-team.ru/mya-engineer).
