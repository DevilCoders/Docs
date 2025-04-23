## Плагины

Список собственных плагинов для Hermione.

### CreateFallenTestsReport

Плагин готовит отчет о всех упавших тестах. JSON представляет собой массив с объектами, содержащими поля: `browserId` и `fullTitle`.
По желанию можно задать путь до файла отчета, используя поле `reportFile`. Дефолтное значение: `reports/fallenTestsReport.json`.

### FilterFallenTests

Плагин запускает только тесты, содержавшиеся в отчете. Если файла отчета нет или массив значений пустой - запустятся все тесты.
По желанию можно задать путь до файла отчета, используя поле `reportFile`. Дефолтное значение: `reports/fallenTestsReport.json`.

### SkipTestsByReport

Плагин игнорирует тесты, содержавшиеся в отчете. JSON представляет собой массив с объектами, содержащими поля: `browserId`, `fullTitle`, `reason`, `skipDate` и `fixTask`.
Если нужно игнорировать тест во всех браузерах, то просто не указываем поле `browserId`.
По желанию можно задать путь до файла отчета, используя поле `reportFile`. Дефолтное значение: `skipTestsReport.json`.
Если в файле отчета будут содержаться тесты, которых нет в проекте - будет брошено исключение: `Unknown skipped test`.
Пример файла отчета:

```
[
    {
        "browserId": "chrome_ios_tablet 77.0",
        "fullTitle": "Авиабилеты: Бронирование BOY Проверка совпадения данных на странице",
        "reason": "Все сломалось",
        "skipDate": "05.05.2020",
        "fixTask": "https://st.yandex-team.ru/TRAVELFRONT-2474"
    }
]
```

## Хранения отчетов между запусками

Можно воспользоваться механизмом [teamcity-artifact](https://www.jetbrains.com/help/teamcity/build-artifact.html).
После создания отчета - загружать его в артефакты. Потом указать его в [artifact-dependencies](https://www.jetbrains.com/help/teamcity/dependent-build.html#DependentBuild-ArtifactDependency) и выкачивать перед запуском.
