# Геохелпер

[![OKO health](https://badger.yandex-team.ru/oko/repo/morda/geohelper/health.svg)](https://oko.yandex-team.ru/repo/morda/geohelper)

### Requirements
deb:
- yandex-passport-vault-client
- yandex-passport-tvmtool
- libgeobase6-nodejs
- nodejs-12
- p2p-distribution-geobase6-config

### Стартовая помощь тем, кто разрабатывает дивные блоки для ПП
Перед тем как зайти на дев машину разработки геохелпера по ssh
```
ssh v158.wdevx.yandex.net
```

убедитесь, что у нас вас актуальные rsa ключи на гитхабе и активны ключи на вашей локальной машине
```
ssh-add -L  # вернет список ключей, если они активны
ssh-add # команда, чтобы добавить ключи
```
затем на девовской машине геохелпера можно будет выполнить следующее

### How to checkout new dev
```
sudo mkdir /opt/www/geohelper-d{номер инстанса}
sudo chown $USER /opt/www/geohelper-d{номер инстанса}
git clone git@github.yandex-team.ru:morda/geohelper.git /opt/www/geohelper-d{номер инстанса}
cd /opt/www/geohelper-d{номер инстанса}
make dev
```

### Другие полезные команды:
```
make start // запуск приложения
make log // просмотр логов
npm run div-test // запуск тестов, делает снепшот блока
npm run hermione  // запуск снепшотных тестов
npm run hermione:gui // создание скриншота для нового блока
npm run eslint // проверить на ошибки eslint-a
```

### Тестирование дивных блоков
#### ПП
Для удобства тестирования дивных блоков в дев приложении ПП на симуляторе стоит отключить дзен.
```
Квадратик -> Шестеренка -> Настройки ленты -> Лента дзена (выключить)
```
После того как вы написали код для дивной карточки, id вашего блока указано в админке и запрашивается на деве,
 можно открыть стенд на симуляторе и искать свое приложение в табе "Сервисы".

В симуляторе в настройках приложения указываем путь до вашего стенда, в переменной HOST_HOME
```
http://v157d0.wdevx.yandex.ru/portal/api/search?geohelper_host=https://geohelper-v158d{номер инстанса}.wdevx.yandex.ru //  для андроида
https://www-v157d0.wdevx.yandex.ru?geohelper_host=https://geohelper-v158d{номер инстанса}.wdevx.yandex.ru // для айфона
```
d{номер инстанса} - имя папки куда вы склонили свою ветку геохелпера (geohelper-d{номер инстанса})

Полезная ручка: https://l7test.yandex.ru/geohelper/api/v3/divcheck?dev=v157d0&geohelper_dev=v158d{номер вашего инстанса}
Возвращает requestedBlocks и renderedBlocks для конкретного инстанса.

### Полная документация по разработке:
https://wiki.yandex-team.ru/morda/div-platform/geohelper/

