# Зелёный протокол

Зачем нам зелёный протокол? Удобство:
- информирования: текущий статус на видном месте чата, в истории тикета, возможность подписки на инциденты
- координации: не нужно беспокоиться о том, что активная переписка в факапном чате кому то помешает
- возможность завести SPI и разобрать аварию: история чата сама загрузится в инцидентный тикет

## Шпаргалка
Пробуешь первый раз? Пропусти врезку, читай внимательно с раздела [{#T}](#start-protocol).  
_врезка для тех, кто уже читал и хочет вспомнить команды_.

{% note tip "TL;DR" %}

1. `/proto@YaIncBot`, поделись ссылкой
1. `/proto desc описание проблемы`
1. `/proto component direct`
1. `/proto call <login>`
1. `/proto status какой сейчас статус проблемы`, при необходимости `/proto mute` 
1. `/proto finish` (если заводили SPI — ещё нажать в нём кнопку **Сервис восстановлен**)

{% endnote %}

## 1. Запусти протокол { #start-protocol }
В [личке с ботом](https://t.me/YaIncBot) или в чате, где добавлен `@YaIncBot` (например, Дежурство в директе)
1. Скомандуй `/proto`
1. Перейди в созданный чат **Зеленый протокол**
1. Опиши проблему ответом на _1. Укажи, пожалуйста, краткое описание проблемы ответом на это сообщение._
1. Напиши `direct` ответом на _2. Укажи, пожалуйста, компоненту инцидента ответом на это сообщение._, выбери кнопкой нужную подсистему (не vertical)
1. Робот спросит _Заведен ли тикет инцидента?_ — это **не обязательно** и торопиться не нужно:
    - можно нажать кнопку **Завести тикет** позже, убедившись что происходящее — действительно авария
    - или не нажимать вовсе, если масштаб или критичность не подтвердились
1. Поделись ссылкой на созданный закрытый чат или перешли запиненное сообщение из него всем кому нужно

## 2. Добавь нужных людей
Команда `/proto call <login>` добавит в чат нужного человека по логину со стаффа.

Можно получить ссылку на готовую zoom-конференцию командой `/proto zoom`.

## 3. Обновляй статус
Когда появляются заметные новости — давай _status update_, для этого пиши в факапный чат:
```
/proto status <дальше простым текстом апдейт>
```
Примеры:
- `/proto status продолжаем искать воспроизведение проблемы`
- `/proto status воспроизвели проблему на бете, готовим хотфикс`
- `/proto status выложили хотфикс`

Команда запишет сообщение в инцидентный тикет (под кат _Таймлайн действий_), обновит запиненное сообщение в чате и отправит отбвику в чат Дежурства в Директе.
В результате в шапке чата всегда будет видно текущее состояние:  
![пример текущего статуса в запиненном сообщении](_assets/yaincbot-status-update.png "скриншот запина" =460x89)

Время от времени робот может спрашивать в чате: _Укажи, пожалуйста, текущий статус проблемы ответом на это сообщение._ — можно отвечать на это сообщение.  
Если такие сообщение становятся неуместны — отключить "пинговалку" можно командой `/proto mute`.

## 4. Заверши протокол и инцидент
Починили?
- нажми в факапном чате кнопку **Завершить протокол** (под запином) или напиши `/proto finish`
- если заводили SPI-тикет, то нажми в нём кнопку:
   - **Сервис восстановлен** (**Service recovered**) или если такой нет
   - сначала **Диагностика** (**Analyze**) и сразу потом **Сервис восстановлен** (**Service recovered**)

{% note info %}

История чата выгрузится в тикет только после завершения протокола.  
Все сообщения, написанные в чате после этого — в тикет не попадут.

Если случился рецидив проблемы, то:
- проще [снова начать](#start-protocol) зеленый протокол
- либо добавить руками в чат `@robot_searchmon`,
   начать протокол с продолжением в этом чате
   и **ещё раз** [привязать](#link-spi) инцидент к чату (командой `/proto SPI-XXX`)

{% endnote %}

## Проверь себя

### Теория

Несколько вопросов для самопроверки:
[ссылка](https://forms.office.com/Pages/ResponsePage.aspx?id=91gB6oFweEaw7X55tD91WioDI29cj_FKvM5f4YSFsflUN1kyRjVZWTBGOVVXNzRUTlJTWFlEWVpZVi4u)

Если опросник не показывается, залогинься по [инструкции](../guide/basics/howto-office-com-login.md)

### Практика

Ниже описано как потренироваться действовать по зеленому протоколу,
вместе с боллее опытным коллегой (например [ppalex@](https://staff.yandex-team.ru/ppalex)) или в одиночку.

Создание тикета в тренеровку не входит, если будешь пробовать — **обязательно поменяй** в тикенаторе **Очередь в ST** (выпадушка в самом низу) на `TEST`.

1. Запусти зеленый протокол
1. Привяжи протокол к любому из перечисленных SPI: `SPI-17298`, `SPI-17682`, `SPI-17724`, `SPI-17727`, `SPI-17782`, `SPI-17783`
1. Попроси кого-нибудь зайти в чат и написать любое сообщение (текстом)
1. Дай несколько status-update'ов
1. Заверши инцидент (статус тикета)
1. Заверши протокол

