# market-partner - запуск АТ в Sandbox

## Установка
```
npm i -g @yandex-market/market-partner-cli
```
Чтобы обновиться до последней версии также работает `npm i -g @yandex-market/market-partner-cli`.

## Залогиниться в sandbox
Нужно вызвать один раз.
```
market-partner login
```

## Запустить АТ

### Из мастера на **тестинге**
```
market-partner at run MARKETPARTNER-21702 marketmbi-9999 marketmbi-9998
```
Первый параметр - название тикета, куда придет отбивка о прогоне.
Второй параметр - список из marketmbi- или MARKETPARTNER- идентификаторов.

### Из ветки на **демо-стенде**
Укажи параметры `branch` и `baseUrl`:
```
market-partner at run MARKETPARTNER-21702 marketmbi-1337 marketmbi-1338 --branch=MARKETPARTNER-23507-dsbs-api-settings-stocks --baseUrl=https://partner-front--marketpartner-23507-cocon.demofslb.market.yandex.ru
```

### Запустить вместе **с заскипанными**
Укажи параметр `--all`
```
market-partner at run MARKETPARTNER-21702 marketmbi-9999 marketmbi-9998 --all
```

## Узнать статус последней запущенной таски
```
market-partner at status
```

## Настройка
Чтобы посмотреть существующие настройки, выполни:
```
market-partner config
```
~~Утилита попробует найти путь к yandex-browser, если не получится, нужно указать путь к браузеру. Чтобы указать путь к Я.Бро, Хром или Хромиум выполни команду:~~
<s>
```
market-partner config browser.path <путь к исполняемому файлу>
```
</s>

----

<i>
Мета-тикет про утилиту: https://st.yandex-team.ru/MARKETPARTNER-21570  

Про sandbox api:  
wiki https://wiki.yandex-team.ru/sandbox/api/  
redoc https://sandbox.yandex-team.ru/api/redoc#operation/task_list_post  
swagger https://sandbox.yandex-team.ru/media/swagger-ui/index.html#/  
</i>
