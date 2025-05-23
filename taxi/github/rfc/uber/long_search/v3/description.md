# Долгий поиск

 

 ### Задача
 [UBR-14: Долгий поиск](https://st.yandex-team.ru/UBR-14 )

 
  ### Figma
 [Макеты долгого поиска в Uber](https://www.figma.com/file/XOZTS4jHddktQcEdkzJa9D/Долгий-поиск?node-id=841%3A14565)

  ### Зависимоти

    Эксперимент регулируется на бекенде из данных эфффективности, через плагин uroutestats, как рефренс можно смотреть на плагин combo

  ## Описание

  Делаем поиск UberX 2-3 минуты, вместо 10-30 секунд.
  За счет этого мы найдем более выгодного водителя и поездка будет дешевле.

 
  ### Summary

  <img src="./static/long_search_summary_mockup.png" width="450">

 Добавляем на саммари ToolTip (бабл):
 - в случае наличия попапа в ответе добавляем шеврон к тайтлу, по нажатию на который открываем Popup c информацией и кнопкой закрытия.
 - кнопка закрыть ("Понятно") возвращает нас на саммари


  Добавим новый branding с типом `long_search`
 **JSON:**
```json
{
    "service_levels": [
        ...
        {
            "brandings": [
                {
                    "title": "Поиск около 2 минут",
                    "popup": { // опционально
                        "title": "Поиск машины займет около 2 минут",
                        "text": "В тарифе UberX мы ищем машину, которая подъедет к вам быстрее всех. Поиск чуть дольше, зато цена поездки самая низкая",
                        "button_title": "Понятно",
                    },
                    "type": "long_search"
                },
                ...
            ],
            ...
        },
    ]
}
```

### Searching

  <img src="./static/long_search_searching_mockup.png" width="450">


 На поиске:
 - в случае наличия попапа в ответе добавляем шеврон к тексту, который шлет бекенд, по нажатию на который открываем Popup c информацией и кнопкой закрытия.
 - кнопка закрыть ("Понятно") возвращает нас обратно на поиск