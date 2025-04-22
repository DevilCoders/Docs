## Графики метрики скорости конвейера в пулл-реквестах

### Добавить новый статус в графики метрики скорости конвейера в пулл-реквестах

#### 1. Создание отчета

- Заходим на [https://stat.yandex-team.ru/Yandex.Productivity](https://stat.yandex-team.ru/Yandex.Productivity)
- Жмем "Добавить отчет" и выбираем путь для нового отчета и его период
- Добавляем необходимые поля в отчет:
  * Измерения

    | Название | Тип | Заголовок |
    | -------- | --- | --------- |
    | fielddate| date| Время     |

  * Показатели

    | Название | Тип    | Заголовок          |
    | -------- | ------ | ------------------ |
    | duration | number | Длительность, сек. |
- Задаем человекопонятное название отчета
- Сохраняем

#### 2. Загрузка данных в отчет

- Добавляем в [конфиг](https://github.yandex-team.ru/search-interfaces/webhook-handler/blob/master/conf/statuses.json) данные нового статуса
  * `context` - Название статуса, берем из гитхаба
  * `statProject` - Путь созданного вами отчета
- Обновляем [версию проекта](https://github.yandex-team.ru/search-interfaces/webhook-handler/blob/master/package.json#L3)
- Отправляем пулл-реквес в [webhook-handler](https://github.yandex-team.ru/search-interfaces/webhook-handler)
  * После вливания пулл-реквеста ставим тег и обновляем проект, см. [доку](https://github.yandex-team.ru/search-interfaces/webhook-handler#%D0%94%D0%B5%D0%BF%D0%BB%D0%BE%D0%B9)

#### 3. График

**⚠️ Важно!** Добавленный вами новый статус автоматически учитывается в графике [Агрегированное время](https://stat.yandex-team.ru/Mart/test_regress?_tab=AgregirovannoeVremya)
Чтобы добавить отдельный график для статуса:

- Склонируем уже существующий график в `ChartEditor`е, [например](https://stat.yandex-team.ru/ChartEditor?name=SERP.infraspeed/build)
  ![Clone graph](./images/clone-graph.jpg)

- Сохраняем
  ![Save graph as](./images/save-as.jpg)

- Указываем источник данных
  ![Save graph as](./images/data-source.jpg)


### Метрика скорости конвейера в пулл-реквестах (перцентили)

#### 1. Добавление таба с виджетом на витрину

- Заходим на [витрину](https://stat.yandex-team.ru/Mart/User/timofey-em/pipeline-percentile?_tab=AgregirovannoeVremya)
- После нажимаем на меню `1.`, после чего нажимаем настройки `2.`
  ![Board settings](./images/board-settings.png)

- В появившемся окне можно добавить tab
  ![Board tabs](./images/board-tabs.png)

- В уже существующем табе или созданном добавляем виджет (тип график)
  ![Board tabs](./images/add-graph.png)

- В появившемся окне меняем `{source_name}` на имя отчёта(как создать смотри выше), где `{source_name}` название отчета после паттерна. На данный момент у нас есть определенный паттерн `/Yandex.Productivity/pipeline-speed/web4/**`
    - Например: `https://stat.yandex-team.ru/ChartPreview/ChartEditor?name=SERP.infraspeed%2Fpercentile-pipeline&source_name=gemini/desktop`
    - для создания виджет "по неделям" нужно добавить параметр `&date_format=ww` к урлу. Пример: `https://stat.yandex-team.ru/ChartPreview/ChartEditor?name=SERP.infraspeed%2Fpercentile-pipeline&source_name=gemini/desktop&date_format=ww`
    - чтобы ограничить график по оси `Y`, нужно добавить параметр `&Ylimit={value}`, где `{value}` любое целое число. Пример: `https://stat.yandex-team.ru/ChartPreview/ChartEditor?name=SERP.infraspeed%2Fpercentile-pipeline&source_name=gemini/desctop&Ylimit=50`
  ![Board tabs](./images/add-percentile-graph.png)

#### 2. Редактирование конфига в ChartEditor
- У нас есть унифицированный [конфиг](https://stat.yandex-team.ru/ChartEditor?name=SERP.infraspeed%2Fpercentile-pipeline&source_name=aggregated) для графиков с перцентилями, при редактировании которого будут затронуты все виджеты с перцентилями.
- [Документация](https://wiki.yandex-team.ru/Statbox/ChartEditor/) по ChartEditor.

##### Возможность комментирования графиков

В ChartEditor открываем вкладку **Config** и добавляем в объект `statface_graph` ключ `comments` со значением

```
comments: {
    path: 'путь до отчета?scale=s'
}
```

**⚠️ Важно!** Нужно обязательно указать  путь к отчету со скейлом на конце.
