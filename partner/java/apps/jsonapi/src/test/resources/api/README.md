ApiTest основной интеграционный класс для тестов
-

Поднимает тестовое приложение и запускает тесты на основе json, хранящиеся в папке /api
Json-файлы должны содержать тег meta.git, где хранится ссылка на git перловых tjson тестов
и тег data, где хранится все содержимое из tjson-файла.

Варианты запуска:
-
1. С переменной окружения API_SOURCE_PATH=<директория или файл, где хранится json (Должны быть ниже /api)>.
Если есть переменная окружения API_SOURCE_PATH, то будут выполняться лишь json, находящиеся ниже по дереву.

Пример:
``API_SOURCE_PATH=/Users/leontevml/arc/arcadia/partner/java/apps/jsonapi/src/test/resources/api/test ya make -tt -F="*ApiTest*"``

Как запустить из Idea: находим класс ApiTest, в его Run configuration прописываем путь к нужному tjson через
переменную окружения API_SOURCE_PATH и можно дебажить.

2. GIT_DOWNLOAD=<ссылка(и) на перловый tjson>, перед запуском тестов загрузит файл(ы) из git.

Пример:
``GIT_DOWNLOAD=https://raw.github.yandex-team.ru/partner/partner2/master/t/lib/RestApi/Tests/v1/Users/mocked-yan-manager/current.tjson ya make -tt -F="*ApiTest*"``

3. GIT_UPDATE=1, перед запуском каждого json будет обновлять в нем содержимое в теге data
4. SELF_UPDATE=1, перед проверкой ответов каждого json-теста будет обновлять тег response

ВНИМАНИЕ!
-
2,3,4 не работают одновременно. Если заданы одновременно несколько из них, сработает только самая приоритетная.
Приоритет:
GIT_DOWNLOAD
GIT_UPDATE
SELF_UPDATE
