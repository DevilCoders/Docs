# e2e/screenshot тестирование

Отдельный сервис для запуска тестов на Hermione

## Локальный запуск

Для локального запуска потребуется [завести виртуалку](https://wiki.yandex-team.ru/JandexMetrika/frontend/devcomputerforeveryone/)

### Подготовительный этап

Убедиться, что в окружении есть переменная NODE_EXTRA_CA_CERTS для загрузки секретов:

```
echo $NODE_EXTRA_CA_CERTS
```

Если возвращается пустота, то её надо добавить в `.bashrc` и перезагрузить оболочку:
```
echo 'export NODE_EXTRA_CA_CERTS=/usr/local/share/ca-certificates/Yandex/YandexInternalRootCA.crt' >> ~/.bashrc && source ~/.bashrc
```

Ставим зависимости и подтягиваем секреты:
```
# зависимости
npm run bootstrap:hermione-testing

# секреты
npx lerna run secrets:initial --scope=hermione-testing
```

### Запуск тестов

Когда тестируем свой код на виртуалке — сервис запускаем в одной вкладке, а Hermione в другой.

В качестве хоста передаем адрес нашей тачки:
```
export HERMIONE_HOST='https://gbiz.dev.metrika.yandex.ru'
```

Когда же тестируем авто-бету или любую другу среду, то просто запускаем Hermione с нужным хостом.
```
# выставляем хост, куда будет смотреть Hermione
export HERMIONE_HOST='https://metrika.yandex.ru'

# переходим в директорию с сервисом
cd ~/www/frontend/services/hermione-testing

# запускаем тесты через cli
npm run hermione:cli:metrika

# либо через gui
npm run hermione:gui:metrika
```

Чтобы запустить тесты через gui, надо знать FQDN из [настроек тачки](https://qyp.yandex-team.ru/)

Он выглядит примерно так: `gbiz.vla.yp-c.yandex.net`

Когда FQDN известен — переходим на него, указав порт 9090:
```
http://gbiz.vla.yp-c.yandex.net:9090
```

## Запуск на авто-бете

- Перейти в интерфейс html-reporter: `https://auto-beta-host/hermione/`
- Убедиться, что в конце пути указали слеш
- Запустить нужные тесты

## Как обновить секреты

### Токены

Скопировать последнюю версию секрета для [robot-metrika-test](https://yav.yandex-team.ru/secret/sec-01cq6h5rtj649gg8h94zwqshc8/explore/versions)
и обновить значение в `services/hermione-testing/vault/secrets.ts`

### Пароль для авторизации

Скопировать последнюю версию секрета для [metrika-frontend-testing](https://yav.yandex-team.ru/secret/sec-01dc2e47bg95qvz40g9jx9p5gs/explore/versions)
затем обновить [metrika.deploy.frontend.hermione-testing](https://bishop.mtrs.yandex-team.ru/environment/metrika.deploy.frontend.hermione-testing#)

## Решение проблем

### Почему-то не открывается
Возможно дело в `/`. Когда указываем хост на который смотрит Hermione, то он идет без слеша.
Но когда переходим в интерфейс html-reporter на авто-бете, то там обязательно должен идти слеш в конце.

### Порт 9090 уже используется
Освобождаем командой:
```
sudo kill -9 $(sudo lsof -t -i:9090)
```

### Тесты выполняются очень долго на авто-бете
На авто-бете задействовано только одно ядро под запуск тестов, поэтому для ускорения используем локальный запуск на виртуалке, где можно задействовать до 32х ядер.
