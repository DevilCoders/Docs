# Перенос сервиса на стэк Apphost + Report Renderer

## Тестинг

Чтобы разрабатываться под стэком apphost + report-renderer в тестинге, достаточно использовать пакет [apphost-service](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/apphost-service). На основе этого же пакета работает [стаб](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/services/stub)
Этот пакет позволяет сделать следующие вещи для тестинга:
- Деплой графа apphost
- Создание нового шаблона (новый тип ресурса) report-renderer
- Запись в балансере hamster для вашего урла

## Перенос: шаг 0

**Вы должны знать как работает ваш сервис.**

Это означает, что вы знаете как и какими сервисами обрабатывается ваш текущий запрос. Через какие балансеры/бэкенды он проходит, кто отдает конечный html. 

Чтобы коллеги, которые поддерживают стэк apphost + report-renderer, смогли вам помочь в переносе сервиса, им и вам нужна вся информация по текущему устройству вашего сервиса, поэтому обязательно разберите по пунктам как работает ваш сервис в данный момент.

## Безопасность

Перед выкаткой в продакшен на внешних пользователей, обязательно закажите аудит у безопасников. Воспользуйтесь [инструкцией](https://wiki.yandex-team.ru/product-security/audit/) для прохождения аудита.

## Шаги для релиза сервиса в продакшен

- Запись в балансере
- Создание продакшен графа в apphost
- Запись в http_adapter
- Релиз шаблона report-renderer

### Запись в балансере

Если нужен свой поддомен, [изучаем доку](https://wiki.yandex-team.ru/L7/).

Далее говорим про так называемый [L7 Fast балансер](https://wiki.yandex-team.ru/l7/docs/#arxitektura). Он позволяется создать запись только на путь по главному домену `yandex.{tld}/new-service`.

Новая запись в балансере делается запросом [через форму](https://wiki.yandex-team.ru/L7/create_task/). Там же показано как завести тикет для аудита безопасности для вашего будущего урла, **это нужно сделать перед заполнением формы**. 
[Пример тикета на запись в балансере созданного через форму.](https://st.yandex-team.ru/MINOTAUR-2210)

**Итог:** имеем запись в L7 Fast балансере, что по урлу `yandex.{tld}/new-service` идем в apphost.

### Создание продакшен графа в apphost

Графы для apphost можно увидеть в специальной админке [Horizon](https://horizon.z.yandex-team.ru/graphs?arcpath=trunk&vertical=&textFilter=), подробнее почитать про [Horizon тут](https://wiki.yandex-team.ru/horizon/). 
Коротко: Horizon выгружает ваши графы из аркадии, и затем расскатывает их в продакшен по всем локациям, делается это периодично, где-то раз в сутки. Поэтому после коммита в аркадию, надо будет какое-то время подождать, пока граф доедет до прода.

**Важно!** Добавляя новый граф в аркадию, у вас упадут тесты. Вам необходимо будет их поправить, а именно переснять каноничные снапшоты. Почитать про тесты в аркадии [можно тут](https://wiki.yandex-team.ru/yatool/test), конкретно про канонизацию [здесь](https://wiki.yandex-team.ru/yatool/test/#canonization).

Еще раз по шагам:
- Добавляем новый граф в нужную папку(вертикаль), например сюда для [SHARED](https://a.yandex-team.ru/arc/trunk/arcadia/web/app_host/conf/graph_generator/vertical/SHARED)
- Далее локально запускаем тесты для графов в папке [graph_generator](https://a.yandex-team.ru/arc/trunk/arcadia/web/app_host/conf/graph_generator), командой `arcadia/ya make -t`. Пример [коммита нового графа](https://a.yandex-team.ru/review/1093410/files/3), все файлы измененные в папке `graph_generator/tests/` - это канонизация снапшотов. В вашем прогоне должны упасть похожие тесты(понятное дело, тесты меняются/удаляются/добавляются).
- Далее канонизируем все упавшие тесты, по одному, командой `arcadia/ya make -tF <test name> --canonize-tests`.
- Делаем PR в аркадию, если для вас это впервые - [читайте документацию по работе с arc](https://wiki.yandex-team.ru/arcadia/starterguide/)

Ссылки которые помогут вам:
- [Дока по apphost](https://doc.yandex-team.ru/apphost)
- [Horizon](https://horizon.z.yandex-team.ru/graphs?arcpath=trunk&vertical=&textFilter=)
- [Докуметация Horizon](https://wiki.yandex-team.ru/horizon/)
- [Тесты в аркадии](https://wiki.yandex-team.ru/yatool/test)
- [Первый коммит в arc](https://wiki.yandex-team.ru/arcadia/starterguide/), и [еще дока](https://wiki.yandex-team.ru/search-interfaces/arc/)
- [Описание структуры графа](https://doc.yandex-team.ru/apphost/dg/concepts/graphs-configuration.html#opisanie-grafa)
- [Пример коммита с новым графом](https://a.yandex-team.ru/review/1093410/files/3)

**Итог:** имеем свой граф в продакшене и видим это в Horizon.

### Запись в http_adapter

Тут все просто, делать коммит в аркадию умеем, после шага выше, поэтому просто идем в конфиг `http_adapter` своей вертикали, делаем коммит и все. Пример коммита в вертикаль [SHARED](https://a.yandex-team.ru/review/1104850/files/1).

**Итог:** имеем запись в `http_adapter` про выбор нашего графа по урлу `/new-service`.

### Релиз шаблона report-renderer в продакшен

Смотреть [тут](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/docs/release_rr.md)

**Итог:** имеем свой шаблон в продакшене

Если вы все сделали верно, и все конфиги/графы успели везде доехать и расскатиться, вы сможете увидеть свою ручку в проде. По любым вопросам обращайтесь в [поддержку монорепозитория фронтенда](https://github.yandex-team.ru/search-interfaces/frontend#поддержка).
