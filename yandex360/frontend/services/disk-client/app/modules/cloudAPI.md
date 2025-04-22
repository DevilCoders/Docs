### Cloud API adapter
[Описание со стороны бэкенда](https://beta.wiki.yandex-team.ru/disk/photoslice-smartcache/#spisokruchek)

Сейчас есть 3 ручи:

* getSnapshot
* getClusters
* getDiff

Все ручки принимают параметр `user` как его передаёт `models.jsx`.
На самом деле из него используется только поле `uid`.
Не забываем, что если `params` не указан явно, то он наследуется. Поэтому вызовы ручек можно
вообще писать просто: `'cloudAPI:getSnapshot()'`

#### cloudAPI:getSnapshot()

Создает и возвращает снапшот фотосреза

Params:

* user
* typeClustering
* locale — язык интерфейса

```js
'cloudAPI:getSnapshot()'

de.call('cloudAPI:getSnapshot()', {
    params: {
        user: '.user',
        typeClustering: '"geo"',
        locale: '.locale'
    }
})
```

#### cloudAPI:getClusters()

Возвращает массив кластеров с структурой

Params:

* user
* idSlice — id снэпшота
* revision — номер ревизии
* ids — id кластеров через запятую

```js
de.call('cloudAPI:getClusters()', {
    params: {
        user: { uid: '.uid' },
        idSlice: '.idSlice',
        revision: '.revision',
        ids: '.ids'
    }
})
```

#### cloudAPI:getDiff()

Возвращает диффы начиная с revision по текущую версию

Params:

* user
* idSlice — id снэпшота
* revision — номер ревизии от которой нужны диффы
* locale — язык интерфейса

```js
'cloudAPI:getDiff()'
```
