# Ticount HTML Report

HTML Report для инструмента [Ticount](https://wiki.yandex-team.ru/velocity/serp/ticount/)

## Запуск

```
ticount-report --url https://yandex.ru --title "Главная страница Яндекса" --output report.html --data pathToBaseData pathToActualData
```

## Конфиг

Конфиг пока используется для сортировки отображения и заголовков метрик

`config.json` по умолчанию
```
{
    "metric": {
        "first_contentful_paint": "FCP",
        "largest_contentful_paint": "LCP",
        "dom_content_loaded": "domContentLoaded",
        "load": "load",
        "bem_inited": "bem_inited",
        "before_static": "before_static",
        "react_hydrate_first_wave_end": "react_hydrate_first_wave_end",
        "react_inited": "react_inited"
    }
}
```
