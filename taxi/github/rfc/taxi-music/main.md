## Описание интеграция Я.Музыки в такси

### Задача
Необходимо предоставить возможность пассажирам управлять музыкой в такси.
Подразумевается интеграция с Яндекс.Музыкой. Предоставлять возможность планируется
пассажирам, у которых активна подписка Я.Плюс.

Таким образом:
1. На клиенте во время поездки появляется музыкальный плеер с контентом Я.Музыки.
2. У водителя таксометр проводом подключен к автомобильным колонкам и умеет играть Я.Музыку.


### Главные проблемы
1. SDK Я.Музыки на таксометре должно уметь играть музыку юзеру, в т.ч. и приватные плейлисты. 
Для этого надо уметь матчить конкретный таксометр с конкретным пассажиром на стороне Я.Музыки.
2. Необходимо понять как отправлять команды управления музыкой на таксометр.


### Возможное решение

#### Вопрос с авторизацией
Запросы из таксометра должны идти от лица пользователя. Есть несколько возможных решений
1. ~~Передать токен клиента на таксометр~~ (не секьюрно)
2. ~~В начале поездки сходить в бек музыки и проассоциировать таксометр с пользователем~~ (проблемы с лицензиями у музыки)
3. Сгенерировать временный токен, с которым водитель может получать доступ к музыке.  

#### Сервис управления музыкой taxi-music
С++ сервис с pgsql базой данных. Сервис будет в 4.0

##### Ручка получения состояния плеера
Клиентское приложение будет периодически поллить ручку (раз в секунду) для того, чтобы обновить плеер - доступность 
кнопок, текущая песня и т.д.
Ручка будет отвечать 406, если плеер не доступен.

##### Ручка обновления состояния плеера
Таксометр после получения песни из SDK Я.Музыки будет обновлять плеер (событийно или раз в некоторое время).

##### Ручка для команд управления плеером
Клиентское приложение может отправить команды управления:
- плей/пауза
- следующий/предыдущий трек
- играть по индентификатору
- громкость

Далее команды передаются на таксометр

##### Отправление команд на таксометр
Необходимо отправлять команды на таксометр, пока кажется что реалистчиный вариант - делать это через пуш.
Надо подумать как гарантировать доставку, чтобы плеер не завис в неконститентном состоянии.

#### Клиентское приложение
На экранах поездки клиентского приложение отображается плеер, если:
- включен эксперимент
- есть подписка плюс
- авторизация портальным аккаунтом.

##### TOTW
Чтобы не заливать в ручку сразу тысячи rps, предлагается действовать через эксперимент 3.0 в totw.
После первого totw, приложение поймет попало оно под эксперимент или нет. И на статусе транспортинг начнет поллить 
ручку плеера. 

##### Обновление состояния плеера
Начиная со статуса транспортинг периодически поллит ручку состояни плеера.
В случае 406 поллинг останавливается.

#### Таксометр
На таксометре стоит SDK Я.Музыки, которое при наличии токена может играть песни.

##### Получение команд
Если пассажир захочет включить свою музыку на таксометр отправляется команда.
Таксометр передает команду SDK и обновляет плеер.

##### Обновление состояния плеера
Таскометр ходит в ручку сервиса taxi-music и обновляет плеер.

#### Процессинг заказа stq py2
Небходимо обрабатывать как минимум два события:
- назначение водителя

При назначении надо понимать доступна ли музыка, возможно устанавливать связь с бекендом музыки для авторизации и 
ходить в сервис taxi-music для создания плеер.  

- завершение поездки

При завершении поездки надо закрывать плеер.

