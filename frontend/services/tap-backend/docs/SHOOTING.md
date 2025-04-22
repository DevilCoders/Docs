# Нагрузочное тестирование

- [Как стрелять](#Как-стрелять)
- [Конфиг Стрельбы](#Конфиг-стрельбы)
- [Как сделать патроны](#Как-сделать-патроны)


## Как стрелять

1. Открыть пул-реквест с кодом, который нужно протестировать.

    - В названии ветки должно быть `*stress-deploy*`, чтобы собрался и выкатился [нагрузочный стенд](https://deploy.yandex-team.ru/stage/tap_backend_stress)
    - Можно стрелять по релизной версии, тогда нужно вручную раскатить нужную версию Docker образа на [нагрузочный стенд](https://deploy.yandex-team.ru/stage/tap_backend_stress)

2. Проверить, что стенд открывается
	
	- Открыть стенд можно по адресу: https://api-stress.tap-tst.yandex.ru/
	- **Важно**: балансер используется только для проверки стенда, в него нельзя стрелять

3. Создать тикет на нагрузочное тестирвоание

	- Открыть задачу в ST
	- Нажать «Действия»
	- [Выбрать «Отправить на нагрузочное тестирование»](https://jing.yandex-team.ru/files/yuu-mao/3.png)

4. Подготовить конфиг для стрельбы. 

	- Взять [шаблон конфига](#Конфиг-стрельбы)
	- [Выяснить FQDN мишени и танка](https://jing.yandex-team.ru/files/nodge/2020-10-15T11:40:06Z.26f43dd.png) в конфиге [нагрузочноно стенда](https://deploy.yandex-team.ru/stage/tap_backend_stress)
	- Заменить `{API_FQDN}` на адрес мишени
	- Заменить `{TANK_FQDN}` на адрес танка
	- Заменить `TAP-0000` на настоящий номер задачи
	- Заполнить описание стрельбы в полях `job_name`, `job_dsc` и `ver`
	- Указать нужные патроны и схему нагрузки
	- По необходимости поменять http заголовки
		
5. Запустить стрельбу в [Лунапарке](https://lunapark.yandex-team.ru/)

	- Нажать «Пострелять»
	- Скопировать подготовленный конфиг в [текстовый редактор конфига](https://jing.yandex-team.ru/files/nodge/Zapustit_strelbu_2019-07-08_19-46-54.png)
	- [Указать урл для стрельб](https://jing.yandex-team.ru/files/nodge/Zapustit_strelbu_2019-07-08_19-48-07.png), либо [загрузить файл с патронами](https://yandextank.readthedocs.io/en/latest/tutorial.html#preparing-requests)

6. Провести стрельбы с нужными схемами нагрузки, [проанализировать отчеты и мониторинг](https://jing.yandex-team.ru/files/nodge/2212064_-_LPC-3863_UC_Sdelat_strelby_po_prokse_turbo-stranits_2019-07-08_19-49-23.png).


## Конфиг стрельбы

```yaml
phantom:
  package: yandextank.plugins.Phantom
  enabled: true
  address: '{API_FQDN}'
  header_http: '1.1'
  headers:
    - 'Host: api-stress.tap-tst.yandex.ru'
    - 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8'
    - 'Accept-Encoding: gzip, deflate'
    - 'Accept-Language: ru,en;q=0.9'
    - 'Cache-Control: no-cache'
    - 'Connection: keep-alive'
    - 'Cookie: yandexuid=566263081514371336;'
    - 'Pragma: no-cache'
    - 'User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/56.0.2924.87 Safari/537.36'
  load_profile:
    load_type: rps
    # Подробнее про схемы нагрузки: https://yandextank.readthedocs.io/en/latest/tutorial.html
    schedule: 'const(10, 60s)'
  # Подробнее по формату патронов: https://yandextank.readthedocs.io/en/latest/tutorial.html#preparing-requests
  uris:
    - "/url-1"
    - "/url-2"

uploader:
  package: yandextank.plugins.DataUploader
  enabled: true
  operator: lunapark
  api_address: https://lunapark.yandex-team.ru/
  task: 'TAP-0000' # Нужно обязательно указать правильный номер задачи, иначе стрельба не запустится
  job_name: 'TAP-0000: Пострелять' # Заголовок задачи
  job_dsc: 'const(10, 60s)' # Человеко-понятное описание стрельбы
  ver: 'v0.0.0' # версия приложени, по которой стреляем
  lock_targets:
    # Блокируем одновременную стрельбу в сервис с адресами Маркета
    - 'pers-address-prestable.vs.market.yandex.net'
  meta:
    use_tank: '{TANK_FQDN}'
    use_tank_port: '8083'

# Сигналы для автоматической остановки стрельбы
autostop:
  autostop:
    - 'time(10s,5s)'     # Скорость ответа превышает 10 секунд в течение 5 секунд
    - 'http(3xx,5%,5s)'  # 5% редиректов в течение 5 секунд
    - 'http(400,1%,2s)'  # 1% Bad Request в течение 2 секунд
    - 'http(404,5%,5s)'  # 5% Not Found в течение 5 секунд
    - 'http(5xx,10%,5s)' # 10% пятисоток в течение 5 секунд
    - 'net(xx,1,10s)'    # 1 RPS сетевых ошибок в течение 10 секунд

yasm:
  package: yandextank.plugins.YASM
  enabled: true
  panels:
    tank:
      host: ASEARCH
      tags: 'itype=deploy; stage=tap_backend_stress; deploy_unit=Tank'
    api:
      host: ASEARCH
      tags: 'itype=deploy; stage=tap_backend_stress; deploy_unit=App'
```

## Как сделать патроны

Стрессовый черный ящик смотрит в слепок продовой базы, поэтому для авторизации нужно использовать продовые OAuth токены или куки.

Для получения OAuth токена можно воспользоваться ссылкой:
> https://oauth.yandex.ru/authorize?response_type=token&client_id=bf7d5a95ea154ebf96384e82f898941d

Полученный токен подставляем в заголовок для авторизации патрона.

```bash
[Authorization: OAuth <TOKEN_HERE>]
/v1/market-pers-address/ read
```
Сохраняем этот файл и заливаем через [формочку](https://lunapark.yandex-team.ru/firestarter/).

В конфигурации стрельбы указываем вместо `uris`:
```
ammo_type: uri
ammofile: 'https://link_to_file'
```
[Пример](https://storage-int.mds.yandex.net/get-load-ammo/15228/0dcfbaacf895471fbdf527a92f05d0e1) файла с 5 разными патронами.
