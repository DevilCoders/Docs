# X-Proxy

### Что это

X-Proxy - это HTTP-прокси сервер для имитации различных состояний бэкенда.
Сценарии использования:
 - Тестирование неожиданных сетевых условий в мобильных приложениях. Например, торможение/отключение ручек и т.п.
 - Подмена/задание ответов с бэкенда для тестирования различных фичей,
 - Тестирование поведения приложения на аномальных данных с бэкенда без его напряга. 
 Например, в случае почты, это может быть гигантский ящик, или огромное число прикреплений к письму. 
 
По-умолчанию, X-Proxy полностью проксирует запросы к указанному бэкенду. Конфигурируя X-Proxy, можно добиться любого
поведения указанного бэкенда вплоть до полного прехвата запросов.
X-Proxy так же предназначен для использования в автотестах.

### Пользуемся предустановленными конфигурациями

- Подключаем телефон к [PDAS](https://wiki.yandex-team.ru/YandexMobile/wifi/)
- Выбираем нужную конфигурацию из [списка](https://github.yandex-team.ru/mobmail/x-proxy/blob/master/configurations/common.ts). 
Например, конфигурация `metro` подойдет для эмуляции сети как в метро.
- Находим настройку хоста бэкенда, в который ходит приложение. Например, в случае мобильной iOS почты, она живет в `Base URL` из вкладки `Development`.
- Меняем его следующим образом. Пусть хост был https://XXX.yandex.ru/api. Меняем его на https://XXX_yandex_ru.xp.yandex-team.ru/c/metro/api 

![Drag Racing](https://jing.yandex-team.ru/files/amosov-f/xp-yandex-team-ru.png)

- Если `XXX = mail`, то можно ничего не добавлять слева от `xp.yandex-team.ru`. Например, хост `https://mail.yandex.ru/api/mobile` можно поменять просто на `http://xp.yandex-team.ru/c/metro/api/mobile`, 
если имя конфигурации `metro`
- В связи с требованиями безопасности, надо проковырять дырку от сети X-Proxy `XPROXYNETS` до вашего бэкенда, если ее еще нет.
Это можно сделать через [Puncher](https://puncher.yandex-team.ru/?source=_XPROXYNETS_&rules=exclude_rejected&values=all&sort=source) 
- Перезагружаем приложение, если это требуется для активации нового хоста.

Если в [списке](https://github.yandex-team.ru/mobmail/x-proxy/blob/master/configurations/common.ts) нет нужной конфигурации, то можете сделать ее сами.
Для этого надо будет запустить X-Proxy локально и в местном `sandbox` попробовать ее написать.

## Я хочу сделать новую конфигурацию
### Как запустить X-Proxy
- Выполняем все действия из корневого Readme в xmail
- Запускаем команду `Start X-Proxy on port 8080` справа сверху
- В логах появится запись "x-proxy listening on port 8080"
### Как подключиться к проксе
#### Эмулятор
- Меняем в приложении "Yandex host" на `http://10.0.2.2:8080`
#### Устройство
##### iOS
- Подключаем телефон и комьютер к общей сети https://stackoverflow.com/a/19387755
- Находим имя комьютера в настройках общего доступа
- Меняем в приложении "Yandex host" на `http://{имя компьютера}.local:8080/api/mobile`
##### iOS+Android
На Android описанная выше схема почему-то не работает. В бой идет тяжелая артиллерия:
- Запускаем `./ngrok http 8080`
- Берем https хост из строчки с `Forwarding` и прописываем его в "Yandex host" (см. настройки приложения) 
- После этого можно зайти на http://localhost:4040 и наблюдать все запросы и ответы прокси

После следующего запроса в логах X-Proxy появятся урлы, по которым приложение вызывает бэкенд. 
ngrok очень удобно использовать и на iOS.

### Как изменять поведение ручек
В основе X-Proxy лежит библиотечка [toxy](https://github.com/h2non/toxy).
Изменяя `sandbox.ts` в соответствии с [примерами](https://github.yandex-team.ru/mobmail/x-proxy/blob/master/configurations/sandbox.ts), можно добиться любого поведения ручек.
Из коробки доступен такой [набор](https://github.yandex-team.ru/mobmail/x-proxy/blob/master/poisons/poison.ts) изменений в поведении ручек ([документация](https://github.com/h2non/toxy#built-in-poisons)).

### Как локально включить конфигурацию
В некоторых тикетах есть ссылка на конфигурацию, которую надо включить, чтобы ручки начали вести себя нужным образом.
Например, [тут](https://st.yandex-team.ru/MOBILEMAIL-12652). 
Для включения конфигурации следует в файле `common.ts` изменить `ACTIVE_CONFIGURATION` на номер тикета. Пример: 

`static ACTIVE_CONFIGURATION = PublicConfigurations.MOBILEMAIL_12648;`

После рестарта прокси конфигурация начнет работать.

### Как настроить хосты проксирования через конфиг
Если вы хотите, чтобы все запросы проксировались на определенный хост, поменяйте `defaultForwardHost` в `config.ts`
Если надо поменять хост по определенному пути, то в `pathConfigurations` следует добавить
```
"/custom_path/*": {
    forwardHost: "https://custom.host",
    configurationName: "response500",
    parameters: [
        "50"
    ]
}
```
Можете править `/custom_path_prefix_example/*` который живет там для примера.
Рестартим X-Proxy (`kill -9` на процессе в Qloud).
Теперь запросы на `/custom_path/*` будут проксироваться на `https://custom.host` с использованием конфигурации `response500`.
forwardHost/configurationName/parameters являются опциональными

### Как зафиксировать ответ ручки
- Создаем в папке `resources/mail` json, который хотим отдавать в формате code: код ответа, body: тело ответа. Пример - `resources/mail/error/auth.json`
- Открываем `sandbox.ts` и в методе `configure` добавляем строку `toxy.all('ручка').poison(Poisons.responseJsonFrom('путь до файла, начиная с resources/'))`
Список ручек можно посмотреть в `handlers.ts`
- Можно не создавать файл, в таком случае можно воспользоваться `Poisons.responseJson(...)`
- Перезапускаем проксю

### Как включить нужный эксперимент
- Эксперименты эмулируются через ответ ручки uaz
- Копипастим конифг из AB и создаем в папке `resources/mail/experiment` соответствующий json. 
Например, https://ab.yandex-team.ru/testid/105146 превратился в `buckets.json`
- Добавляем в массив `MANDATORY_CONFIGURATIONS` из `registry.ts` элемент `new ExperimentConfiguration("имя файла с json")`
- Перезапускаем проксю
- Перезапускаем приложение, чтобы эксперименты обновились

### Как подменить даты писем
- Расскомментируем `// new TimeBucketConfiguration()` в `registry.ts`
- Стартуем проксю
- После подключения к проксе перезагружаем приложение и делаем clear cache
- Теперь даты писем должны соответствовать распределению из `buckets.json`
- Стратегия изменения дат писем описана в `buckets.ts`. 
Если нужна какая-то другая стратегия, то можно по-своему реализовать интерфейс `MessageTimeStrategy`. 

### Фиксим ошибку SSL handshake timed out
Если ваш тестовый бэкенд, в который вы ходите, работает только по https, но сертификат у него так себе, 
то X-Proxy поможет съесть ошибку, если другие способы не помогают
- Идем в config.ts и добавляем туда (если все запросы идут на /api)
```
"/api/*": {
    forwardHost: "https://secure.host.net"
},
```
- Поднимаем X-Proxy
- Если у вас Android приложение, то network_security_config.xml должен выглядеть так
```
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <domain-config cleartextTrafficPermitted="true">
        <domain includeSubdomains="true">10.0.2.2</domain>
    </domain-config>
</network-security-config>
```
- Меняем хост бэкенда с `https://secure.host.net/api` на `http://10.0.2.2:8080/api` в настройках приложения
- Запускаем приложение в эмуляторе
- Profit

Для Payment-SDK `config.ts` будет выглядеть так
```
export const PATH_PREFIX_CONFIGURATIONS = {
  defaultForwardHost: 'https://mobpayment-test.yandex-team.ru',
  pathConfigurations: {
    '/api/*': {
      forwardHost: 'https://pci-tf.fin.yandex.net',
    },
  },
}
```

### Как сделать пул-реквест в X-Proxy
- Через пул реквест в монорепу
