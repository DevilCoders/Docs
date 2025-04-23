# Contributing guide
Основа описания взята с [вики](https://wiki.yandex-team.ru/SergejjPopov/geometalaunch/).

## Как поднять свою версию геопоиска?
Нужно счекаутить toolkit для настройки копии геопоиска.
```
$ svn co svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/search/geo/tools/metasearch_G.E.C.K beta_directory && cd beta_directory
```

### Вариант 1. Новое место для разработки "с нуля"
```
$ ./install.sh -c -u порт_для_верхнего -m порт_для_среднего
$ ./make.sh
$ ./update_all.sh
$ ./start.sh
```

В этом случае:
  * код будет лежать `beta_directory/arcadia`
  * данные будут лежать `beta_directory/rearrange-data`

Можно использовать `./pull.sh` + `./make.sh` для обновления/сборки.

### Вариант 2. У вас есть данные и метапоиск собранные локально из транка
```
./install.sh -u порт_для_верхнего -m порт_для_среднего -a путь_к_корню_аркадии
./start.sh
```

### Вариант 3. Вы хотите получить все стабильно и ничего менять в метапоиске не хотите
В этом случае метапоиск и данные будут взяты из последнего релиза.

```
./install.sh -u порт_для_верхнего -m порт_для_среднего
./start.sh
```

## Описание команд setup tookit геопоиска
| Команда               | Описание |
| --------------------- | -------- |
| `./make.sh`           | собирает геометапоиск и данные (для вариантов 1 и 2) |
| `./pull.sh`           | обновляет локальные копии кода и данных, а также набор скриптов (для вариантов 1 и 2) |
| `./update_configs.sh` | обновляет конфиги метапоиска на актуальные (для всех вариантов) |
| `./update_its.sh`     | обновляет локальный конфиг из its (требуется, если вы хотите сравнивать себя с /search/stable) (для всех вариантов) |

## Тестирование свой версии геопоиска
### БЯК
Чтобы визуализировать результаты работы геопоиска, можно направить на него верстку карт:
```
l7test.yandex.ru/maps?host_config[inthosts][search]=http://хост:порт/
```
**Внимание.** `/` - в конце обязателен!

### Колдунщик
```
https://yandex.ru/search/?text=кафе&srcrwr=GEOV:хост:порт:10000000
```
**Внимание.** В этом случае к номеру порта нужно прибавить 4.

### МЯК
1. [Скачайте](https://beta.m.soft.yandex.ru/description?app=maps&platform_shortcut=android&branch=dev) dev-сборку.
2. [Скачайте](https://play.google.com/store/apps/details?id=krow.dev.scheme) специальное приложение.

Инструкция от [a-dd@](https://staff.yandex-team.ru/a-dd):
> В ссылке для открытия карт.
> Её можно открыть через adb или какое-нибудь стороннее приложение типа https://play.google.com/store/apps/details?id=krow.dev.scheme
> adb shell am start -a android.intent.action.VIEW -d "yandexmaps://add_exp/MAPS_GEOSEARCH?maxadv=10"]>
> в общем случае для параметров потребуется префикс experimental_, например expeirmental_source=middle:хост:порт

Более подробно про тестирование мобильных читай на [вики][https://wiki.yandex-team.ru/maps/analytics/mobile/experiments/newexp/testing/].

## Настройка базовых поисков
  * [Инструкция про разработку ППО и НК от sobols@](https://wiki.yandex-team.ru/JandeksPoisk/GeoPoisk/geobasesearch/quickstartguide/)

## FAQ
### Не удалось поднять свою версию геопоиска
На исправление проблем есть тикет: https://st.yandex-team.ru/GEOSEARCH-5225

**Перед запуском** ` ./start.sh ` обновите скачанные данные `./update_all.sh`.

#### `make.sh` выдаёт ошибки по ходу работы, не скачивает нормально `arcadia/extsearch/geo`, но продолжает работать
Здесь помогает руками закачать нужный каталог:
```
$ cd arcadia
$ svn up extsearch // или svn revert -R extsearch перед этим
$ rm -rf extsearch
$ cd ..
$ ./pull.sh
```

#### `make.sh` на последнем этапе качает rearrange-data из skynet выдаёт ошибку, но завершается якобы успешно
`skynet` не работает по умолчанию, если присутствует backbone интерфейс - обычно дело на машинках в отделе Карт.
Нужно руками запустить команду `sky`, добавив опцию `—-network=Backbone` или перейти на другую машину, где нет backbone интерфейса.

#### Запускаем сервис командой `start.sh`, а он пишет `OFFLINE`
Смотрим логи в каталоге logs. У меня `./install.sh` и `./start.sh` не принёс конфиги `upper.cfg` и `middle.cfg`.
Скачиваем их командой `update_configs.sh` или `update_all.sh`.
