#Список подъездов для первого адреса

## 1. Где добавляются подъезды

1)  ручка /4.0/suggest для типа "а" добавит список подъездов
    первому адресу (если это дом с подъездами).

2)  ручка /4.0/zerosuggest для типа "а" добавит в голову списка
    адресов новый адрес с подъездами (если это дом с подъездами).
    В zerosuggest новый адрес формируется из элемента с типом "а"
    массива request.state.fields.
    
3)  ручка /4.0/finalsuggest для типа "а" и методов finalize и pin_drop добавит подъезды в первый адрес из `results`,
    если это дом с подъездами и адрес не был получен из pp, userplace или arrival_point
    

## 2. Регулирование

Регулируется экспериментом `entrances_list_in_suggest`
```yaml
    SuggestEntrancesExp:
        type: object
        description: |
            Эксперимент на добавление списка подъездов в первый объект результата
            ручек suggest и zerosuggest
        additionalProperties: false
        properties:
            suggest_enabled:
                type: boolean
                default: false
            zerosuggest_enabled:
                type: boolean
                default: false
            finalsuggest_enabled:
                type: boolean
                default: false
            min_entrances_to_show_no_entrance:
                description: минимально необходимое количество подъездов в доме, чтобы
                    показывать надпись "Подъезд не указан", если подъезд не указан
                type: integer
                default: 1
                minimum: 1
            entrance_key:
                type: string
                default: "suggest.append.entrance"
            button_key:
                type: string
                default: "suggest.append.entrance"
            filter_distance:
                type: number
                default: 100.0
```

## 3. Использование на клиенте

1) Клиент проверяет первый адрес на наличие информации о подъездах, которая
   выглядит следующим образом:
```json
{
   "entrances_info": {
    "show_no_entrances_label": true,
     "suggested_entrances": [
       {
         "entrance_number": "F2",
         "title": "подъезд F2",
         "point": [ 33.0, 56.0],
         "distance_value": "275398.602990",
         "distance": "276 км"
       },
       {
         "entrance_number": "F3",
         "title": "подъезд F3",
         "point": [ 33.0001, 56.0001],
         "distance_value": "275397.038037",
         "distance": "276 км"
       }
     ],
     "text": "Levoberezhnaya street, 12, подъезд",
     "button_text": "подъезд"
   }
}
```
2) Если информация присутствует, отрисовывается кнопка для
     отображения списка подъездов. Иначе кнопка отсутствует.

3) При выборе определенного подъезда из списка, отправляется
     запрос на /4.0/finalsuggest с action=geomagnet с выбранным подъездом, точкой
     подъезда и prev_log=log, где log - поле "log" у рассматриваемого первого адреса.

4) При самостоятельном вводе подъезда после вывода списка подъездов
     клиент фильтрует список относительно введенных пользователем
     данных. При нажатии пользователя на "поиск" отправляется запрос
     на /4.0/finalsuggest с action=geomagnet с введенным пользователем подъездом,
     точкой адреса и prev_log=log, где log - поле "log" у рассматриваемого первого адреса.

     Если ввод пользователя перестает содержать в себе entrances_info.text, то
     возвращаемся на /4.0/suggest c action=user_input.

5) При движении пина по карте (`/finalsuggest` `pin_drop`) или после выбора из списка в саджесте
    (`/finalsuggest` `finalize`) при выполнении усповий в п. 1.3 в ответе будут подъезды, из этого ответа
    на саммари нужно использовать поле `show_no_entrances_label`, если оно `true`, то добавлять к адресу сабтайтл
    "Подъезд не указан" (согласно дизайну https://www.figma.com/file/AlmKcg4t3uA51BRThwKnGX/PickUp-%26-DropOff?node-id=433%3A7197).
    Сам текст берется из ручки `/launch`

6) При переходе в окно выбора точки А, нужно использовать последнюю информацию, которая пришла из `/finalsuggest`,
    для отрисовки кнопки отображения списка подъездов.
