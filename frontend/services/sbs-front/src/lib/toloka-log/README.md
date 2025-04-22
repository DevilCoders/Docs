### Библиотека логирования пользовательских действий в Толоке

Работает в трех режимах: **single**, **client**, **hub**
 * **single** - режим работы без айфреймов
 * **client** - отправляет сообщения родительскому окну через *postMessage*
 * **hub** - принимает сообщения от айфрема. Ожидается, что будет инстанс в режиме client, который будет отправлять сообщения.

#### Подключение
В head шаблона или прототипа нужно добавить скрипт

```html
<script>
    (function(s,a,m,_a,d,h,i){s["__"+d]=[],s[d]=s[d]||function(){s["__"+d].push(arguments)},h=a.createElement(m),h.src=_a+"?rnd="+1*new Date,
    h.onload=function(){s.__tlklggr=new TolokaLog()},i=a.getElementsByTagName(m)[0],i.parentNode.insertBefore(h,i);
    })(window, document, "script", "https://toloka-log.s3.yandex.net/toloka-lib-prod.js", "tolokaLog");
</script>
```

#### Использование
После подключения скрипта конструктор **TolokaLog** будет доступен в глобальной области видимости 
* **single**

```js
  // Инициализация
  const logger = new TolokaLog({
    mode: 'single',
    useConsoleLog: Boolean // вывод сообщений в консоль браузера
  })

  // Использование
  logger.log('message')

  // Получить массив всех залогированных событий
  logger.getLogs()
```

* **client**
После добавления скрипта на страницу в глобальной области видимости будет доступен метод **tolokaLog**, ожидает на вход сообщение, передаст его в родительский айфрейм. Инициализацию делать не нужно.

```js
  tolokaLog('Шаблон загружен')

  button.addEventListener('click', function() {
    tolokaLog('Нажата кнопка')
  })
```

* **hub**
Для работы в режиме **hub** при инициалации нужно передать список **validId**. Это список аттрибутов **name** айфреймов, сообщения которых будут обрабатываться. Если сообщение придет от айфрема с **name**, которого нет в этом списке - оно будет проигнорированно.
В режиме **hub** ожидается, что в дочерних айфремах будет работать инстанс логгера в режиме **client**, который будет присылать сообщения.

```js
  // Инициализация
  const logger = new TolokaLog({
    mode: 'hub',
    useConsoleLog: Boolean // вывод сообщений в консоль браузера
    validId: String[] | Number[]
  })

  // Логирование так же доступно в родительском айфреме
  logger.log('message')

  // Получить массив всех залогированных событий
  logger.getLogs()
```

#### Деплой
Для того что бы сделать деплой библиотеки нужно получить доступ к s3 запросив роль в [IDM](https://idm.yandex-team.ru/user/vladpotapov/roles#rf=1,rf-role=tgxRW0SM#s3-mds/sbs3-1474-62552/service-account-role/admin;;;,f-status=all,sort-by=-updated,rf-expanded=tgxRW0SM).

После получения роли нужно получить **access key**, с которым будет выполнятся запись в s3. Как это сделать описанно на [Wiki](https://wiki.yandex-team.ru/mds/s3-api/authorization/#sozdanieaccesskey)

Деплой выполняется командой:
```bash
ENV=<prod|test> ACCESS_KEY_ID=<публичная часть access key> SECRET_ACCESS_KEY=<приватная часть access key> npm run deploy-toloka-log
```
