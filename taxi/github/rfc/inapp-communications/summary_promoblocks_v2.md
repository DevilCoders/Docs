# Intro
[Задача [UFC Growth] Новый UI плашек рекомендаций](https://st.yandex-team.ru/TAXIPROJECTS-2117)  
### Дизайн
[Figma](https://www.figma.com/file/OmooncuMjX6xkcxCeMB1Vh/%D0%92%D0%BE%D1%80%D0%BE%D0%BD%D0%BA%D0%B0-%D1%82%D0%B0%D0%BA%D1%81%D0%B8?node-id=8546%3A102747)(область «Эксперименты»)

### Основные изменения
1. Стиль отображения промо-плашек(старая/новая тень) - [линк](#новая-тень)
2. Различные типы кнопок(кнопка +, кнопка содержащая только текст) - [линк](#кнопки)
3. Действия на кнопках - [линк](#действия-на-кнопках)

# Новая тень
### Отображение
В новом дизайне мы переставляем тень плашки таким образом, что она находится внутри свернутого саммари (не над кнопкой)  

### Implementation
В `SummaryOffers.promoblocks` из ответа `/4.0/inapp-communications/promos-on-summary`([link](https://github.yandex-team.ru/taxi/uservices/blob/a203c25c35d5c9ce8efd8d92d64b143d0911ae59/services/inapp-communications/docs/yaml/definitions.yaml#L1196)) добавляется optional `style`
```yaml
style: # default: v1 - old style
  type: object
  properties:
    version:
      type: string
      enum:
        - v1
        - v2_shadow_under_promoblock
  required:
    - version
```
Для предотвращения горячего перехода с одного стиля на другой в рамках одной сессии в момент изменения экспа в `PromoblockClientInfo` из запроса добавляется optional `style`. При наличии этого поля в запросе `/4.0/inapp-communications/promos-on-summary` вернет `style` неизменным. При отсутствии - ответ будет определяться экспериментом

Серверный эксп регулирующий общее для всех плашек отображение старая/новая тень
```yaml
promos_on_summary_style:
  type: object
  properties:
    version:
      type: string
      enum:
        - v1
        - v2_shadow_under_promoblock
    control_group_hide_other_promos:
      type: boolean
  required:
    - version
```
`control_group_hide_other_promos` - временное поле для сокрытия прочих промок(для которых не будет включена новая тень) на контрольной группе. Для уравнивания условий с тестовой группой  
***Для A/B клозы экспа должны быть ограничены версией клиентов поддерживающей новую тень***

### MVP
Новая тень только для плашек:
* чуть дороже / чуть дешевле
* редирект на Детский
* редирект на Комфорт  

Т.к. есть и другие плашки, а показывать одновременно старые и новые не хотим - на стороне `/4.0/inapp-communications/promos-on-summary` гарантируется: при включенном экспе перечисленные плашки получают `style.shadow_under_promoblock == true`, а ***прочие плашки, для которых новая тень не будет поддержана в рамках MVP выпиливаются из ответа***


# Кнопки
### Отображение
К кнопке ">" добавляются:
* кнопка "+"
* кнопка содержащая только текст

Кнопка ">" уже поддерживает текст, для кнопки "+" нужно аналогично

### Implementation
При наличии `button` в `supported_features[type == 'promoblock'].widgets` в `PromoblockItem.widgets` из ответа `/4.0/inapp-communications/promos-on-summary` добавляется виджет `button` [schema](summary_promoblocks_v2_button.yaml) и текущий [definitions](https://github.yandex-team.ru/taxi/uservices/blob/a203c25c35d5c9ce8efd8d92d64b143d0911ae59/services/inapp-communications/docs/yaml/definitions.yaml)  
`button` заменяет собой `deeplink_arrow_button` + `drive_arrow_button`  
Включение этого флоу регулируется серверным экспом
```yaml
inapp_communications_button_widget:
  type: object
  properties:
    enabled: boolean # default: false
```

### MVP
Плашка драйва не поддержана -> специфика драйва в `button` отсутствует  
actions не поддержаны, действие передается через deeplink
Админка не будет правиться, настройка кнопок будет через серверный эксп:
```yaml
promos_on_summary_extend_buttons:
schema:
  buttons:
    type: array
    items: '#/definitions/button'

definitions:
  button:
    type: object
    properties:
      id: string
      type:
        type: string
        enum:
          - arrow
          - plus
          - text # любая кнопка может иметь текст, а тут - только текст
```

Прочие детали промоблока настраиваются сейчас из админки

# Действия на кнопках
* открытие раскрытого саммари для определенного тарифа - *есть*
* открытие раскрытого саммари для определенного тарифа и долистываение до нужной опции - *MVP*
* открытие способов оплаты - *финальный этап*
* открытие сториз - *финальный этап*

### Implementation
Открытие раскрытого саммари для определенного тарифа сейчас реализовано через диплинк вида:
```
yandextaxi://route?tariffClass=business&vertical=taxi&expandingState=expanded
```

Для открытия раскрытого саммари для определенного тарифа и долистывания до нужной опции нужно расширить это диплинк требованием  
Кмк, есть 2 варианта это сделать:
1. Добавить параметр
`requirement`
`yandextaxi://route?tariffClass=business&vertical=taxi&expandingState=expanded&requirement=child_seat`
2. Использовать якорь  
`yandextaxi://route?tariffClass=business&vertical=taxi&expandingState=expanded&list=requirements#child_seat`  
или  
`yandextaxi://route?tariffClass=business&vertical=taxi&expandingState=expanded#requirements-child_seat`  
или  
`yandextaxi://route?tariffClass=business&vertical=taxi&expandingState=expanded#child_seat`

Кажется, что 1ый вариант возможно немного проще в реализации, а 2ой несколько естественнее для структуры URL(якори обычно и используются для "долистать до"). Принципиальной разницы не вижу, хотелось бы узнать мнения