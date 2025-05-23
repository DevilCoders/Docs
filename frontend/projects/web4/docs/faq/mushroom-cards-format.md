# FAQ. Формат конструктора карточек

Здесь приводится описание формата конструктора карточек с примером. Описание дизайна можно найти тут: [Конструктор карточек](https://depot.yandex-team.ru/guidelines/bloki/cards-constructor/). С вопросами можно обратиться к [Серафиму Четверухину](https://staff.yandex-team.ru/chetverukhin) и в команду Красоты.

1. [Приступая к работе. Hello карточка](#Приступая-к-работе-Hello-карточка)
2. [Данные](#Данные)
3. [Шаблон карточки](#Шаблон-карточки)
4. [Свойства шаблона](#Свойства-шаблона)
5. [Свойства блоков](#Свойства-блоков)

## Приступая к работе. Hello, карточка

Перейдя по [этой ссылке](https://yandex.ru/search/?lr=213&exp_flags=beauty_mushrooms=1&exp_flags=beauty_mushrooms_enabled=1&foreverdata=4292028038) вы увидите страницу поисковой выдачи с двумя карточками. Она использует [foreverdata](https://forever.si.yandex-team.ru) для подстановки шаблона и данных карточек.

Вот что указано в адресе этой страницы

```
https://yandex.ru/search/?lr=213
    &exp_flags=beauty_mushrooms=1           ← Вкл. эксп карточек
    &exp_flags=beauty_mushrooms_enabled=1   ← Вкл. шаблоны карточек из данных
    &foreverdata=4292028038                 ← Подстановка из форевердаты
```

Чтобы заменить шаблон и данные этого примера на свои, [создайте новую форевердату](https://forever.si.yandex-team.ru/demo?project=SERP&hash=), вставьте в неё вот этот JSON и нажмине кнопку «Сохранить».

```
{"construct": [{
    "type": "mushroom",
    "subtype": "q",
    "title": "Нравится ли тюленям Северное сияние?",
    "path": [{ "url": "https://yandex.ru/q", "text": "Яндекс.Кью" }],
    "data": [
        { "message": "Так что думаю, когда тюлень лежит на спине и видит Северное сияние, он просто продолжает лежать и смотреть в небо. Может, закрадется мысль «Симпатично так»." },
        { "message": "Им нравится, когда они сыты, когда они со своей группой, когда они в безопасности и имеют достаточно времени на сон." }
    ],
    "config": {
        "сardWidth": 5,
        "firstCardWidth": 6,
        "order": [
            {
                "type": "text",
                "defaultProps": {
                    "text": "Ответ эксперта",
                    "bold": true
                }
            },
            {
                "type": "text",
                "bindings": {
                    "text": "message"
                }
            }
        ]
    }
}]}
```

Затем в урле страницы найдите параметр `hash`, скопируйте его значение и замените им параметр `foreverdata` страницы выдачи.

```
https://forever.si.yandex-team.ru/demo
    ?project=SERP
    &hash=4292028038        ← Вот этот параметр
```

Теперь, сохраняя изменения в вашей форевердате, вы увидите их на странице выдачи. Менять нам потребуется два поля – `construct[0].data` и `construct[0].config`.

## Данные

Данные карточек находятся в поле `construct[0].data`. Каждый элемент этого массива соответствует одной карточке. На примере ниже в массиве `data` лежат два элемента. Для каждого из них будет применен общий шаблон и на странице мы получим две карточки. Они будут выведены как две карточки. При этом в первую карточку будет подставлен текст «Тюленям нравится лежать на спине», а во вторую «Им нравится, когда они сыты».

```
"construct": [{
  "type": "mushroom",
  "data": [
    { "message": "Тюленям нравится лежать на спине" },    ← Первая карточка
    { "message": "Им нравится, когда они сыты" }          ← Вторая карточка
  ]
}]
```

## Шаблон карточки

Для отрисовки всех карточек используется один общий шаблон. Он лежит в поле `construct[0].config.order`. Каждый элемент этого массива соответствует одному элементу (блоку) карточки. Выводятся блоки в том же порядке, в каком записаны в массиве. На примере ниже, в массиве `order` находятся два элемента `type=text`. Это значит, что каждая отрисованная карточка будет содержать два текстовых блока. Текст в первом блоке на всех карточках будет одинаковым – «Ответ эксперта». Текст во втором блоке будет соответствовать данным из `construct[0].data`.

```
{"construct": [{
  "type": "mushroom",
  "config": {
    "order": [
      {
        "type": "text",             ← Какой блок выведется
        "defaultProps": {           ← Свойства, одинаковые для всех карточек
          "text": "Ответ эксперта", ← Этот текст будет на всех карточках
          "bold": true
        }
      },
      {
        "type": "text",
        "bindings": {           ← Свойства, значения которых будут взяты из данных отдельно для каждой карточки
          "text": "message"     ← Будет выведен текст из поля message из данных
        }
      }
    ]
  }
}]}
```

## Свойства шаблона

Есть пара свойств шаблона, которые влияют на вывод всех карточек.

```
"construct": [{
  "type": "mushroom",
  "config": {
    "сardWidth": 5,         ← Ширина карточки
    "firstCardWidth": 6,     ← Ширина первой карточки
    "singleCardFullwidth": true     ← Заполнение карточкой всю ширину, если она одна
  }
}]

```

| Название       | Значение  | Описание                                                                           |
| -------------- | --------- | ---------------------------------------------------------------------------------- |
| сardWidth      | 3, 4,… 12 | Ширина карточки (в колонках). По умолчанию 4.|
| firstCardWidth | 3, 4,… 12 | Ширина первой карточки (в колонках). По умолчанию используется значение сardWidth.|
| singleCardFullwidth | true/false | Заполнять ли всю ширину, если карточка одна |

## Свойства блоков

Свойства блока можно указыать в секциях `defaultProps` и `bindings`. Есть несколько свойств, общих для всех блоков. Специфические свойства см. в описании блока ниже.

| Название | Значение | Описание                                                     |
| -------- | -------- | ------------------------------------------------------------ |
| visible  | Boolean  | Позволяет спрятать блок на основе данных. По умолчанию true. |

### 📃 text

См. [mushroom-text](https://serpdocs.si.yandex-team.ru/constructives/mushroom-text)

### 🚸 text-with-icon

| Название     | Значение       | Описание                                                          |
| ------------ | -------------- | ----------------------------------------------------------------- |
| text         | String         | Видимый текст блока.                                              |
| size         | m, s, l        | Размер текста.                                                    |
| bold         | Boolean        | Жирный текст.                                                     |
| iconPosition | left, right    | Положение иконки слева или справа от текста.                      |
| iconUrl      | String         | Путь к произвольной картинке.                                     |
| iconHeight   | Number         | Кастомная высота иконки.                                          |
| iconWidth    | Number         | Кастомная ширина иконки.                                          |
| iconFit      | cover, contain | Способ ресайза иконки (при кастомной ширине). Допустимые значения |

См. [text-with-icon](https://serpdocs.si.yandex-team.ru/constructives/text-with-icon)

### 🔗 link

| Название | Значение | Описание                                    |
| -------- | -------- | ------------------------------------------- |
| text     | String   | Видимый текст блока.                        |
| url      | String   | Адрес ссылки.                               |
| counter  | String   | Название узла при отправке baobab-счётчика. |

### 💔 divider

См. [mushroom-divider](https://serpdocs.si.yandex-team.ru/constructives/mushroom-divider)

Плюс есть ещё несколько свойств

| Название | Значение | Описание                                         |
| -------- | -------- | ------------------------------------------------ |
| grow     | Boolean  | Разделитель занимает всё доступное пространство. |

### 🙋‍♂️user

См. [mushroom-user](https://serpdocs.si.yandex-team.ru/constructives/mushroom-user)

### 📅 date

См. [mushroom-date](https://serpdocs.si.yandex-team.ru/constructives/mushroom-date)

### 🖼 cover

См. [mushroom-cover](https://serpdocs.si.yandex-team.ru/constructives/mushroom-cover)

### 👍 social-reactions

См. [social-reactions](https://serpdocs.si.yandex-team.ru/constructives/social-reactions)

### 🛒 container, meta, footer

Позволяют разместить вложенные блоки особым образом:

-   container – блоки располагаются в строку (inline-block)
-   meta – в строку через интервал-разделитель (по-умолчанию имеет специальный стиль текста)
-   footer – в одну строку с возможностью прижать блок к правому краю (inline-flex)

Вложенные элементы указываются в поле `items` как на примере ниже.

```
{
    "type": "footer",
    "items": [
        {
            "type": "text",
            "defaultProps": { "text": "Ставь лайк" }
        },
        {
            "type": "text",
            "defaultProps": { "text": "И подписывайся на канал" }
        }
    ]
}
```
