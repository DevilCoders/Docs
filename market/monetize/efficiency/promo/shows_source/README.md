### Отчетность по показам и кликам
Тут хранятся черновики проекта по забору информации о кликах и показах из симтем Metrika и AppMetrica по инструментам продвижения.

Это черновиек проекта, однако в нем будет поддерживаться архитектура конфиг среза с источников, классификация срезов, построение конечного запроса к источнику, сохранение результатов и истории изменений результирующих таблиц.

Для удобства использования конфига(который не мал и трудно читаем), сделаны функции преобразования конфига json в xlsx и обратно(но данный формат предназанчен только для первичной и черновой работы, в дальнейшем предполагается что все изменения вносятся сразу в конфиг и по нему прогонятся тесты)

Ну а пока есть 2 скрипта которые позволяют редактировать конфиг "через excel"

Для преобразования конфига в excel есть команда из корня shows_source ``bash create_excel_for_edit.sh /Path/To/save/your_excel.xlsx`` где ``/Path/To/save/your_excel.xlsx`` абсолютный путь к сохранению excel

Описание и поля конфига в дальнейшем будут меняться, а пока пусть остаются теми же, по примеру как это работает можно обращаться к @kirillkuzikov

Для преобразования excel в конфиг есть команда из корня shows_source ``bash import_excel_from_edit.sh /Path/To/save/your_excel.xlsx`` где ``/Path/To/save/your_excel.xlsx`` абсолютный путь к отредактированной ранее excel

Запускается все через [reactor](https://reactor.yandex-team.ru/browse?selected=10199037) для наглядности есть [схема зависимостей процессов](https://reactor.yandex-team.ru/slice?id=11703363&mode=GRAPH) постороенная в slice nirvana

Весь процесс запуска строится на yql по этапам 

1. выжимке из источников (этап 0_exract, хранятся от 14 до 90 дней от созданий), 
2. сотавлений более легких таблиц (этап 1_staging(хранятся от 90 до 720 дней от создания)) и 
3. построении агрегатов для отрисовки на графиках (этап 2_calc, не удаляются), 

дополнительно используется один общий конфиг логинов и токенов для запуска хранимый в [артефакте](https://reactor.yandex-team.ru/browse?selected=11678968) 

На и текущий момент yql операции выполняются из под робота robot-mrkt-promocod [график потребления yt за последние 4 недели](https://monitoring.yandex-team.ru/projects/yt/dashboards/monnc3bj5ugmpii904fu?p.cluster=hahn&p.tree=physical&p.pool=robot-mrkt-promocod&from=now-4w&to=now&utm_source=yt-interface-scheduling-monitor&refresh=300000), однако графы nirvana создаются из под kirillkuzikov, т.к. у robot-mrkt-promocod нет доступа к [проекту marketmoney в reactor](https://reactor.yandex-team.ru/browse?selected=6870828&selectedTab=quota)

В дальнейшем предполагаю что данные будут унифицироваться, добавится baobab как источник данных в этап 0_exract
