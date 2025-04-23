# Moisha
Возвращает по запросу цены услуг на auto.ru.

Живет в Аркадии.
## Релиз матрицы цен для дилеров

1. Дождаться апрува от tsuper@ в тикете,
согласно [регламенту](https://wiki.yandex-team.ru/vertis/autoru-money-dev/process/tariff-changes/)
изменения дилерских тарифов (аудит требует, чтобы апрув был до тестирования цен).
2. (если не было сделано раньше) Установить и настроить Amazon S3-клиент
по [гайду](https://wiki.yandex-team.ru/vertis/autoru-money-dev/docs/zagruzka-novojj-matricy-cen/).
3. Установить `xmllint` (скрипт `upload_matrix.sh` проверяет, что файл является валидным XML).
4. Выложить матрицу в тестинг:
`./upload_matrix.sh testing dealers <path_to_file>`
5. Протестировать изменения матрицы.
**Написать комментарий** о тестировании в тикет в стартреке (требуется для аудита).
Пример такого комментария: https://st.yandex-team.ru/VSMONEY-1698#5ed0bc8e802a026dec238865
6. Выложить матрицу в продакшн:
`./upload_matrix.sh production dealers <path_to_file>`


# Релиз пакетов

Общая информация:
1. В названии ветки и PR нужно указывать ID тикета на st.
Если хочется в название ветки добавить ещё небольшое словесное описание, отделить его от ID тикета знаком подчёркивания.
Например: `VSMONEY-12_release_improvements`.
Если планируется запуск на отдельном бранче в Shiva, в названии ветки можно использовать только определенный набор символов.
   Подробности в [документации](https://docs.yandex-team.ru/classifieds-infra/deploy/specification/branch#validaciya-imeni-vetvi).
2. Джобы в TeamCity выкатывают в тестинг все пакеты автоматически.
3. Пакеты в TeamCity:
   - [autoru-moisha-api-release](https://t.vertis.yandex-team.ru/buildConfiguration/Autoru_moisha_AutoruMoishaApiReleaseArcadia?mode=builds)
   - [autoru-moisha-eds-release](https://t.vertis.yandex-team.ru/buildConfiguration/Autoru_moisha_AutoruMoishaEdsReleaseArcadia?mode=builds)

## Релиз в тестинг
Смержить PR в мастер и запустить нужную сборку в tc.
После сборки, пакет будет автоматически выкачен в тестинг.

## Релиз в тестинг в отдельную ветку
Сделать PR, затем запустить нужную сборку в tc вручную (custom build), указав название бранча в github в разделе Changes.

Пакет будет автоматически выкачен в тестинг в бранч Shiva с названием бранча в github.
Если выкладка в Shiva не прошла (напимер из за названия бранча), деплой можно сделать вручную.
Подробностии в [документации по Shiva](https://docs.yandex-team.ru/classifieds-infra/deploy/quick-start#deploj)


## Релиз в продакшн
1. Смержить свою ветку в master.
Для этого удобно нажимать Merge pull request (с выбором Create merge commit) в интерфейсе PR на GitHub.
2. Запустить нужную сборку в tc.
3. После сборки, пакет выкатится в тестинг
4. Какие могут быть проблемы при порядке релиза, о чём стоит подумать:
  Если добавляли новое поле в матрицу, то
    - Релизим eds
    - Подождать когда переиндексится матрица. В логе должно быть "was successfully produced with version"
    - Релизим api
    - Выкатываем новую матрицу

    Почему так: если выкатить api и не переиндексить матрицу, мойша будет сыпать ошибками 400. Несмотря на то что новых полей фактически в матрице ещё нет, в бинарном формате/его парсинге api уже считает что оно должно быть. А в матрице его нет.

5. Выкатить новые стабильные пакеты в prod в Shiva
    - [api](https://admin.vertis.yandex-team.ru/services/auto2-moisha-api)
    - [eds](https://admin.vertis.yandex-team.ru/services/auto2-moisha-eds)

    Есть несколько способо выкатывания. Они описаны в [документации по Shiva](https://docs.yandex-team.ru/classifieds-infra/deploy/quick-start#deploj)

    **Важный момент**: для каждого тикета в релизе должна быть ссылка на выкладку в prod shiva (это требование аудита). Проще всего это сделать, добавив ключи тикетов в список задач при запуска деплоя в Shiva.
6. После выкатки, смотрим на
- графики мойши https://grafana.vertis.yandex-team.ru/d/GWx6SSc7k/moisha-shiva?orgId=1&refresh=10s&var-datasource=Prometheus
- появились ли ошибки от мойши на графике public-api https://grafana.vertis.yandex-team.ru/d/I1-gRG8Zk/drills-overview?viewPanel=24&orgId=1&refresh=5m&from=now-3h&to=now
- в [логе](https://grafana.vertis.yandex-team.ru/explore?orgId=1&left=%5B%22now-1h%22,%22now%22,%22vertis-logs%22,%7B%22expr%22:%22service%3Dauto2-moisha-api%20layer%3Dprod%20%20%22,%22fields%22:%5B%22thread%22,%22context%22,%22message%22,%22rest%22%5D,%22limit%22:100%7D%5D) мойши, смотрим появились ли 500ки, появились ли 400(это частый кейс, если ошибаемся в порядке релиза, на предмет 400 всегда стоит посмотреть)

## Integration with IntelliJ IDEA:
  * copy run configurations from ./idea_build_configurations to
    ".idea/runConfigurations"
  * maven run configuration will be available in
    Maven Projects (Panel) -> salesman -> Run Configurations

## Локальный запуск
Для запуска понадобятся конфиги с dev тачки, инструкция [тут](https://wiki.yandex-team.ru/vertis-admin/dev-containers/).
Недостающие параметры можно подсмотреть в [конфиге сервиса](https://github.com/YandexClassifieds/services/tree/master/conf/moisha)

