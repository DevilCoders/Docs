- [Общие принципы](#Общие-принципы)
- [Настройки бота](#Настройки-бота)
    - [/setname](#setname)
    - [/setuserpic](#setuserpic)
    - [/setabouttext](#setabouttext)
    - [/setdescription](#setdescription)
    - [/setcommands](#setcommands)
    - [/setjoingroups](#setjoingroups)
- [Основные сценарии](#Основные-сценарии)
    - [/start](#start)
    - [Просмотр пробок](#Просмотр-пробок)
      - [Пользователь не указал свое местоположение](#Пользователь-не-указал-свое-местоположение)
      - [Пользователь указал свое местоположение](#Пользователь-указал-свое-местоположение)
      - [Посмотреть пробки около меня](#Посмотреть-пробки-около-меня)
      - [Просмотр маршрута дом-работа](#Просмотр-маршрута-дом-работа)
    - [Поиск](#Поиск)
      - [Пользователь не указал свое местоположение](#Пользователь-не-указал-свое-местоположение-1)
      - [Пользователь указал свое местоположение](#Пользователь-указал-свое-местоположение-1)
    - [Изменение настроек](#Изменение-настроек)
      - [Пользователь не указал свое местоположение](#Пользователь-не-указал-свое-местоположение-2)
    - [Просмотр помощи](#Просмотр-помощи)
    - [Пользователь не смог отправить свое местоположение](#Пользователь-не-смог-отправить-свое-местоположение)
- [Реакция на слова](#Реакция-на-слова)
- [Список всех команд](#Список-всех-команд)

# Функциональная спецификация

## Общие принципы
1. При первом заходе просим задать язык интерфейса. Пропустить этот шаг нельзя, т.к. без этого знания непонятно как общаться с пользователем.
2. Задавать команды можно тремя способами:
  * непосредственно командой `/traffic`
  * с помощью кнопки `Пробки`
  * определение команды из запроса, т.е. можно написать боту `пробки`
3. Взаимодействие через кнопки — приоритетный способ.
4. Для работы пробок и поиска необходима геолокация. При первом запросе спрашиваем геолокацию. Без этого воспользоваться функционалом бота нельзя.

## Настройки бота
### /setname
Yandex Maps
### /setuserpic
![userpic](userpic.png)
### /setabouttext
Real-time traffic information, company or address location on Yandex.Maps.
### /setdescription
Ask me about current traffic conditions in your city, an address or company location, and see it all on a map right in your chat window!
### /setcommands
traffic - See real-time traffic information
search - Search for addresses or companies near you
settings - View the bot's settings
forget - Remove all your data from the bot’s memory
help - Get help with the bot
### /setjoingroups
false

## Основные сценарии
### /start
При первом взаимодействии с ботом пользователь всегда вводит команду `/start` (с помощью кнопки в интерфейсе).

1. Пользователь устанавливает язык.
  * inline-кнопки: `Русский`, `English`...
  * клавиатура: нет
2. Бот отображает стартовое привествие с описанием своей работы.
  * inline-кнопки: нет
  * клавиатура: `Пробки`, `Поиск`, `Настройки`, `Помощь`
3. Пользователь выбирает один из основных сценариев.

### Просмотр пробок
#### Пользователь не указал свое местоположение
1. Пользователь нажимает кнопку `Пробки`.
2. Бот спрашивает геолокацию пользователя, чтобы определить его регион.
  * inline-кнопки: нет
  * клавиатура: `Посмотреть пробки около меня`, `Вернуться в главное меню`
2. Бот показывает пробки в регионе и рядом с пользователем (картинка, балл, прогноз).
  * inline-кнопки: `Открыть в Яндекс.Картах`
  * клавиатура: `Посмотреть пробки около меня`, `Вернуться в главное меню`.

#### Пользователь указал свое местоположение
1. Пользователь нажимает кнопку `Пробки`.
2. Бот показывает пробки в регионе (картинка, балл, прогноз).
  * inline-кнопки: `Открыть в Яндекс.Картах`
  * клавиатура: `Посмотреть пробки около меня`, `Вернуться в главное меню`.

#### Посмотреть пробки около меня
1. Пользователь нажимает кнопку `Посмотреть пробки около меня`.
2. При клике по кнопке `Посмотреть пробки около меня` бот спрашивает геолокацию пользователя.
3. Бот показывает пробки возле пользователя (картинка и балл).
  * inline-кнопки: `Открыть в Яндекс.Картах`
  * клавиатура: `Пробки`, `Поиск`, `Настройки`, `Помощь`

### Просмотр маршрута дом-работа
При запросе пробок (в регионе или около пользователя) показывается специальный промобанер, который рассказывает об установке дома и работы.

Промобанер перестает показываться в двух случаях.

1. Пользователь нажал кнопку `В другой раз`.
2. Пользователь установал дом и работу.

Предусловие. Пользователь установил дом и работу.

1. Пользователь нажимает кнопку `Пробки`.
2. Бот показывает маршрут от работы до дома.
  * inline-кнопки: `Домой N минут`, `Напомнить, когда будет лучше`, `Маршрут обратно`, `Пробки в городе`
  * клавиатура: `Пробки`, `Поискать на карте`, `Настройки`, `Помощь`
3. Пользователь нажимает на кнопку `Домой N минут` и ссылка открывается на touch картах или в МЯК/Навигатор.

#### Включение напоминаний
1. Пользователь нажимает на кноку `Напомнить, когда будет лучше`.
2. Бот сообщает, что напоминания включены.
3. Бот проверяет пробочную ситуацию на маршруте пользователя каждые 5 минут.
  * если время маршрута с пробками превышает маршрут без пробок не более, чем на 10–20%, то посылаем пуш пользователю о том, что пора ехать. После этого уведомления отключаются автоматически.
  * если время маршрута с пробками превышает маршрут без пробок более, чем на 10–20%, то каждые 30 мин шлем промежуточный пуш с информацией о пробках.
  * если в течение 8 часов ситуация на дороге не изменилась, то отключаем нотификации и сообщаем об этом пользователю.

#### Выключение напоминаний
1. Бот присылает промежуточный пуш о текущей пробочной ситуации.
  * inline-кнопки: `Посмотреть пробки`, `Выключить напоминания`
2. Пользователь нажимает на кнопку `Выключить напоминания`.
3. Бот сообщает, что уведомления отключены.

### Поиск
#### Пользователь не указал свое местоположение
1. Пользователь нажимает кнопку `Поиск`.
2. Бот спрашивает геолокацию пользователя, чтобы определить его регион.
  * inline-кнопки: нет
  * клавиатура: `Отправить мое местоположение`, `Вернуться в главное меню`
3. Пользователь нажимает кнопку `Отправить мое местоположение`.
4. Бот выводит список популярных категорий.
  * inline-кнопки: `Где поесть`, `Кафе` и т.д.
  * клавиатура: `Вернуться в главное меню`
5. Пользователь нажимает кнопку одной из категорий.
6. Бот показывает результаты рядом с пользователем.
  * inline-кнопки: нет
  * клавиатура: `Поискать рядом со мной`, `Вернуться в главное меню`

#### Пользователь указал свое местоположение
1. Пользователь нажимает кнопку `Поиск`.
2. Бот выводит список популярных категорий.
  * inline-кнопки: `Где поесть`, `Кафе` и т.д.
  * клавиатура: `Вернуться в главное меню`
3. Пользователь нажимает кнопку одной из категорий.
4. Бот показывает результаты рядом с пользователем.
  * inline-кнопки: нет
  * клавиатура: `Поискать рядом со мной`, `Вернуться в главное меню`

### Изменение настроек
#### Пользователь не указал свое местоположение
1. Пользователь нажимает кнопку `Настройки`.
2. Бот показывает доступные настройки.
  * inline-кнопки: `Поменять язык`
  * клавиатура: `Пробки`, `Поискать на карте`, `Настройки`, `Помощь`

#### Пользователь указал свое местоположение
1. Пользователь нажимает кнопку `Настройки`.
2. Бот показывает доступные настройки.
  * inline-кнопки: `Поменять язык`, `Изменить регион`
  * клавиатура: `Пробки`, `Поискать на карте`, `Настройки`, `Помощь`

### Просмотр помощи
1. Пользователь нажимает кнопку `Помощь`.
2. Бот показывает информацию о помощи.

### Пользователь не смог отправить свое местоположение
Если в течение 1 минуты после задания языка пользователь не отправил свое местоположение, то считается, что у пользователя возникли проблемы и бот отправляет ему специальный пуш с помощью по включения расшаривания местоположения, а также кнопку для задания региона вручную.

Если пользователь задал регион вручную, то пробки показываются только по региону и поиск, соответственно, тоже.

## Реакция на слова
По умолчанию любой запрос в бота считается поисковым, т.е. он превращается в команду:
```
/search <query>
```

Если бот находит в запросе одно из ключевых слов (например, пробки или привет), то он выполняет соответствующую команду.
Список всех ключевых слов находится в [танкере](https://tanker.yandex-team.ru/~search/?query=detect-&project=yandex-maps-telegram-bot). Ключи именуются по принципу `detect-<command>-command`.

## Список всех команд
Большинство команд никак не фигурирует в интерфейсе бота и вызывается неявно через кнопки или в качестве реакции на ключевые слова в запросе.

  * `/forget` — стереть данные пользователя
  * `/hello` — поздороваться с пользователем
  * `/help` — вывести справку
  * `/home` — указать дом
  * `/lang` — сменить языка
  * `/location` — показать местоположение пользователя
  * `/me` — рассказать о местоположении бота
  * `/menu` — показать главное меню
  * `/region` — сменить регион пользователя
  * `/search` — поискать на карте
  * `/settings` — показать настройки
  * `/start` — вывести стартовое приветствие
  * `/thanks` — отреагировать на "спасибо" от пользователя
  * `/traffic` — показать информацию о пробках
  * `/version` — показать версию бота
  * `/work` — указать работу
