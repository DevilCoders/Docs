## Как развернуть

Склонируй репозиторий

```bash
$ git clone https://github.yandex-team.ru/ekbstudent/OCRM.git
```

и открой его в [IntelliJIDEA](https://www.jetbrains.com/idea)

## Подготовка к запуску:
1. Создай файл `config.properties` в папке `resources`
2. Заполни его по шаблону из `resources/.config.properties`
3. Если хочешь запускать тесты локально, то нужно положить WebDriver для Yandex.Bro. Скачать с официального [github](https://github.com/yandex/YandexDriver), разархивировать и положить в папку `resources` и сделать его исполняемым (для linux и macOS):
```bash
cd resources
chmod +x yandexdriver
```

## Как запустить
### Из консоли
- Запустить все тесты - выполнить команду `mvn clean install test`
- Запустить тесты с определенным приоритетом - выполнить команду `mvn clean install test -Dgroups={приоритет}` (пример - `mvn clean install test -Dgroups=Critical`)
- Запустить тесты из определенного класса - выполнить команду `mvn clean install test {имя класса}`
- Запустить тесты из определенного класса с конкретным приоритетом `mvn clean install test {имя класса} -Dgroups={приоритет}`

### Запуск из IDE
#### Запуск всех тестов проекта
Для запуска тестов необходимо нажать правой кнопкой мыши на пакете проекта (пакет `OCRM`) и выбрать `Run 'All Tests'`

#### Запуск тестов из определенного класса 
Необходимо нажать правой кнопкой мыши по классу в котором хотим запустить тесты и выбрать `Run '{имя класса}''`

#### Запуск тестов через конфигурирование запускаемого файла
В данном разделе написано как можно гибко запускать тесты:
- помеченные определенной категорией
- только из определенных тестовых классов 

Запуск тестов через конфигурационный файл:
1. переименовать файл `RunTests.txt` (по пути `src/test/java/RunTest.txt`) в `RunText.java`
   - в аннотации `Categories.IncludeCategory` перечислить категории тестов которые хотим запустить 
   - в аннотации `Suite.SuiteClasses` перечислить тестовые классы из которых запускать тесты
2. нажать правой кнопкой мыши по классу `RunTests.java` и выбрать `Run 'RunTests'`
3. в итоге будут запущены тесты помеченные категориями из аннотации `Categories.IncludeCategory` из тестовых классов перечисленных в аннотации `Suite.SuiteClasses` 

## Как вливать изменения в проект:
### Отправить изменения на удалённый сервер
Через командную строку:
```bash
# Создаёшь веточку, где OCRM-NNNN – номер тикета из трекера
git checkout -b feature/OCRM-NNNN-feature-name
# Коммитишь изменения
git commit -m 'OCRM-NNNN: Коммент на русском'
# Вливаешь их на удалённый сервер
git push origin feature/OCRM-NNNN-feature-name
```
То же самое можно сделать в GitHub Desktop:
1. Создаёшь веточку https://jing.yandex-team.ru/files/borkk/2020-10-28_18-03-57.png с названием `feature/OCRM-NNNN-feature-name` https://jing.yandex-team.ru/files/borkk/photo_2020-10-28_18-09-48.jpg
2. Выбираешь файлы для коммита, пишешь коммент 'OCRM-NNNN: Коммент на русском' и нажимаешь кнопочку 'Commit to feature/OCRM-NNNN-feature-name' https://jing.yandex-team.ru/files/borkk/2020-10-28_18-10-52.png
3. Нажимаешь кнопку "Publish branch" https://jing.yandex-team.ru/files/borkk/2020-10-28_18-14-55.png

### Создать PR (Pull request)
1. Идёшь на github: https://github.yandex-team.ru/ekbstudent/OCRM
2. Видишь кнопку "Compare & pull request" рядом со своей веткой, нажимаешь на неё https://jing.yandex-team.ru/files/borkk/2020-10-28_18-15-55.png
3. Заполняешь поля title и comment. Скроллишь вниз, смотришь, что подтянулись все изменения и нажимаешь "Create pull Request" https://jing.yandex-team.ru/files/borkk/2020-10-28_18-33-07.png
4. Ждёшь, когда твой PR поревьюят (можно сходить к людям и попросить посмотреть) и как только PR закроется, твой код попадёт в мастер)
5. PROFIT!

## Подробнее о настройках в файле `config.properties`
Настройки SeleniumGrid:
- "selenium_grid_use_selenium_grid" - флаг указывающий на стенд где будут крутиться тесты. "true" - будет использоватеься selenium grid. "false" - на локальной машине;
- "selenium_grid_url" - урл до машины selenium grid. Найти его можно <a href="https://wiki.yandex-team.ru/selenium/">тут</a> (по дефолту использовать "http://selenium:selenium@sg.yandex-team.ru:4444/wd/hub");
- "selenium_grid_browser_name" - имя браузера который будет использоваться. Список браузеров доступен <a href="https://selenium.yandex-team.ru/#quota/selenium">тут</a> (по дефолту использовать "yandex-browser");
- "selenium_grid_browser_version" - версия браузера. Актуальную версию браузера можно посмотреть <a href="https://selenium.yandex-team.ru/#quota/selenium">тут</a>;

## Где смотреть скрины браузера в момент падения теста
В момент падения теста система делает скриншот браузера. Это может помочь в разборе падения теста. Скриншоты лежат по пути "target/surefire-reports"
