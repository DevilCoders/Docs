**Как добавить новый профиль Scraper'a?**

0. Прочитать [документацию](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/docs/profile_info_schema.json), в которой описаны поля профиля
1. Убедиться, что среди существующих профилей нет нужного
2. Добавить новый профиль. Id профиля будет имя файла без расширения. 
   Пример: файл профиля weak_consistency__web_robot__touch_c1-vm__tuer0_tier1.json => id профиля: weak_consistency__web_robot__touch_c1-vm__tuer0_tier1
3. Закоммитить изменения в Аркадию
4. В течение 10 минут новый профиль должен появиться в [списке профилей на сервисе](https://scraper.yandex-team.ru/profile)
5. Указать id профиля в поле profile-id батча, в нирвановском кубике указать id в поле profile.

**Как изменить/удалить профиль Scraper'a?**

0. Прочитать [документацию](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/docs/profile_info_schema.json).
1. Убедиться, что изменения не поломают остальные скачки, использующую этот профиль
2. Закоммитить изменения в Аркадию

**Как добавить/удалить/изменить конфиг адаптивной нагрузки?**

0. Прочитать [документацию](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/docs/cluster_load_config.json), в которой описаны поля конфига
1. Убедиться, что среди существующих конфигов нет нужного
2. Добавить новый конфиг в файл с именем кластера или изменить поля текущего конфига
3. Закоммитить изменения в Аркадию
4. В течение 10 минут новый конфиг должен загрузиться в базу данных Скрепера

**Как добавить новый парсер?**
1) Сделать таск в Стартреке, (можно в [очереди Scraper](https://st.yandex-team.ru/SCRAPER) с описанием  задачи) 
2) Установить локально свежую [JDK8](http://www.oracle.com/technetwork/java/javase/downloads/index.html), если ее нет
4) Установить рекомендованную [IDE](https://www.jetbrains.com/idea/download/)
5) Скачать код из [репозитория](https://bb.yandex-team.ru/projects/SEARCH_INFRA/repos/scraper-parser/browse). 
Код парсеров лежит в модуле parsers. Парсеры реализуют абстрактный класс AbstractSerpParser.
6) Нужно убедиться, что расширения существующего парсера не достаточно и действительно нужен новый. Стоит почитать код существующих парсеров, посоветоваться с командой Scraper. Прочитать описание возвращаемого [ParserResult’a](https://scraper.yandex-team.ru/api/ui-facade/schema/ParserResult)
7) Написать код парсера в отдельной ветке c именем "feature/<id тикета в Trackera>". 

 Если нужно добавить новый парсер: 
  - Важно, чтобы класс парсера был stateless - иначе состояние при парсинге предыдущего серпа может повлиять на результат парсинга текущего. 
  - Добавить значение типа парсера в enum ParserType и в SearchEngineType.
  - Добавить класс парсера и тип в ConcreteSerpParserFactory. Метод isYandex должен возвращать корректное значение для нового SearchEngineType.
  - Добавить worker для парсера в ScraperWorkerFactory
 
 Если достаточно изменений в текущем парсере: 
  - Если есть пример батча, результат парсинга которого хочется изменить/добавить, то узнаем его search-engine в атрибутах батча. 
  - Идем в ScraperWorkerFactory и по SearchEngineType узнаем его ParserType.
  - В ConcreteSerpParserFactory по ParserType узнаем имя класса парсера.
  Пример: есть батч, search-engine = "yandex-web-islands", ScraperWorkerFactory: SearchEngineType.YANDEX_WEB_ISLANDS -> ParserType.YANDEX_WEB_ISLANDS, ConcreteSerpParserFactory: ParserType.YANDEX_WEB_ISLANDS -> YandexIslandsHtmlWebSearchParser.class.
8) Написать тесты на парсер. Тесты лежат в тестовой директории модуля parsers. Имя тестового класса для парсера образуется прибавлением к имени парсера суффикса "Test". Пример: Парсер YandexIslandsHtmlWebSearchParser -> тесты для парсера в YandexIslandsHtmlWebSearchParserTest.
   Тестовый парсер должен быть отнаследован от AbstractConcreteParserTest. В методе getTestDataDirectory должен быть указан путь до исходных файлов с html и результирующих json'ов отностиельно директории папки resources в parsers/test. 
   Схема теста такая: взять html по имени из папки с ресурсами getTestDataDirectory, распарсить парсером, сравнить поля ParserResult'а с ожидаемыми. Можно сериализовать ожидаемый ParserResult в json и сохранить в папку с ресурсами, а дальше сравнить сериализованный результат парсинга с этим json'ом.
9) Запускать тесты можно из IDE. Если хотите запустить только тест вашего парсера, то устанавливать локально БД не требуется. В этом случае тест легче запускать из IDE, можно продебажить тест.
10) Сделать pull-request и пройти coder-review. Идем в [список веток](https://bb.yandex-team.ru/projects/SEARCH_INFRA/repos/serp-scraper/branches), выбираем подходящую ветку, переходим по ссылке и в форме в качестве ревьюеров указываем: @selivanov, @inikiforov, @sunlight, @starlight, @g-s-v, @amosov-f. Нажимаем конпку create pull request. 
11) После успешного прохождения pull-request'a, дежурный команды Scraper'a делает merge кода в продакшен и выкатку его делать команда scraper.