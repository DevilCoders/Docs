# Деплой
https://a.yandex-team.ru/projects/ticket/ci/releases/timeline?dir=travel%2Favia%2Frevise&id=regular-release

# Запуск на дев-хосте

```
$ cp ./tools/samples/environments.sh ./tools
$ vi ./tools/environments.sh
$ ./tools/run-dev-local-extractor.sh PARTNER_CODE DEEP_LINK
```

Пример запуска:

```
$ ./tools/run-dev-local-extractor.sh ozon "https://www.ozon.travel/partnertools/deeplink_v1_0/flight/?Date1=2020-08-26&ServiceClass=ECONOMY&Flight=MOWSVX&Dlts=1&utm_source=avia.yandex.ru&utm_medium=metasearch&Infants=0&partner=yandex&Children=0&FlightsClassCode=R&prices=3035&searchId=26c9943d-9c22-4e3c-b863-21e061397ca2&FlightsNo=N4173&fareBasis=%231&yaclid=IjIwMjAtMDgtMDlUMDc6Mjk6MDEi.tfKPLuBCc8NtGOkPE5C-HClQI9o&_openstat=ticket.yandex.ru%3Bozon%3BКупить+Авиабилет%3Bavia.yandex.ru&partnerref=0a72c69b-a5e969-e91a-4697-9072-4247030b83e41"
Ok
=== Step 1 === info ('url', 'https://www.ozon.travel/partnertools/deeplink_v1_0/flight/?Date1=2020-08-26&ServiceClass=ECONOMY&Flight=MOWSVX&Dlts=1&utm_source=avia.yandex.ru&utm_medium=metasearch&Infants=0&partner=yandex&Children=0&FlightsClassCode=R&prices=3035&searchId=26c9943d-9c22-4e3c-b863-21e061397ca2&FlightsNo=N4173&fareBasis=%231&yaclid=IjIwMjAtMDgtMDlUMDc6Mjk6MDEi.tfKPLuBCc8NtGOkPE5C-HClQI9o&_openstat=ticket.yandex.ru%3Bozon%3B\xd0\x9a\xd1\x83\xd0\xbf\xd0\xb8\xd1\x82\xd1\x8c+\xd0\x90\xd0\xb2\xd0\xb8\xd0\xb0\xd0\xb1\xd0\xb8\xd0\xbb\xd0\xb5\xd1\x82%3Bavia.yandex.ru&partnerref=0a72c69b-a5e969-e91a-4697-9072-4247030b83e41')
=== Step 2 === info ('price', <selenium.webdriver.remote.webelement.WebElement (session="9c3349400602e8f701785adecf2ef48ee01b129c391a304ba68487184b10129e", element="ad1de424-2128-4aed-ae33-ab8f8d5944bb")>)
=== Step 3 === info ('price_text', u'3035\u20bd ')
=== Step 4 === info ScreenShot 'price parsed'
=== Step 5 === info {'currency': 'RUB', 'price': 3035.0}
REPORT:
{
    "price_revise": 3035.0,
    "description": "Prices differ",
    "price_diff_rel": 2935.0,
    "shown_price_diff_abs": 2935.0,
    "price_diff_abs": 2935.0,
    "shown_result": "problem",
    "result": "problem",
    "shown_price_diff_rel": 2935.0,
    "revise_data": "[[\"url\", \"https://www.ozon.travel/partnertools/deeplink_v1_0/flight/?Date1=2020-08-26&ServiceClass=ECONOMY&Flight=MOWSVX&Dlts=1&utm_source=avia.yandex.ru&utm_medium=metasearch&Infants=0&partner=yandex&Children=0&FlightsClassCode=R&prices=3035&searchId=26c9943d-9c22-4e3c-b863-21e061397ca2&FlightsNo=N4173&fareBasis=%231&yaclid=IjIwMjAtMDgtMDlUMDc6Mjk6MDEi.tfKPLuBCc8NtGOkPE5C-HClQI9o&_openstat=ticket.yandex.ru%3Bozon%3B\\u041a\\u0443\\u043f\\u0438\\u0442\\u044c+\\u0410\\u0432\\u0438\\u0430\\u0431\\u0438\\u043b\\u0435\\u0442%3Bavia.yandex.ru&partnerref=0a72c69b-a5e969-e91a-4697-9072-4247030b83e41\"], \"('price', <selenium.webdriver.remote.webelement.WebElement (session=\\\"9c3349400602e8f701785adecf2ef48ee01b129c391a304ba68487184b10129e\\\", element=\\\"ad1de424-2128-4aed-ae33-ab8f8d5944bb\\\")>)\", [\"price_text\", \"3035\\u20bd \"], {\"kind\": \"screenshot\", \"name\": \"price parsed\", \"key\": 4}, {\"currency\": \"RUB\", \"price\": 3035.0}]"
}
QUANTITY OF SCREENSHOTS:  1
screenshot 0: screenshots/0.png
```

## Локальная сборка докер-образа

```
$ ya package --docker --docker-registry registry.yandex.net --docker-repository avia travel/avia/revise/pkg.json
```

# Запуск проверок отдельных партеров на макбусе
## Установка
* brew install python
* brew link --overwrite python
* pip install selenium
* brew install selenium-server-standalone
* brew install geckodriver
* brew install chromedriver

## Запускаем
Запускаем selemium сервер:

```
$ selenium-server -port 4444
```

Прописываем в settings хост локального selenium: `http://localhost:4444/wd/hub`

Прописываем browser_capabilities_default:

```
browser_capabilities_default = {
    'acceptInsecureCerts': True,
    'browserName': 'chrome', # or 'firefox'
}
```

## Дополнительные плюшки при локальной разработке:
* Сайтик открывается у вас на макбуке, так что при желении можно дебажиться
* Можно в extractor писать driver.get_screenshot_as_file('/tmp/some.png'). Чтобы картинка сохранилась прям на ваш макбук

## Где взять data?
```
$ executer ssh %avia_revise
$ vim /var/log/yandex-avia-revise/report.log
$ grep PARTNER_NAME
```
