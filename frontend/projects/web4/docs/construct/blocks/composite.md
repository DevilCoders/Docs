# Composite

[Документация](https://serpdocs.si.yandex-team.ru/constructives/composite)

## Назначение
Composite предназначен для отрисовки стека блоков в рамках одного документа в результатах поиска.
Блок обрабатывает все сниппеты в рамках документа и отрисовывает их как один поисковый результат. Это проиллюстрировано на следующем примере.

[**Пример:**](https://forever.si.yandex-team.ru/?hash=1223678393)
```js
"construct": [
  {
    "type": "my-adapter-type",
    "template": "composite",
    "items": [
      {
        "block": "paragraph",
        "text": "Проверяем, что айтемы из двух адаптеров будут мержиться."
      },
      {
        "block": "paragraph",
        "text": "Этот параграф вместе с предыдущим приходят из первого адаптера."
      }
    ]
  },
  {
    "type": "my-second-adapter-type",
    "template": "composite",
    "items": [
      {
        "block": "paragraph",
        "text": "А этот – из второго."
      }
    ]
  }
]
```
Такая конструкция отрисует все параграфы друг под другом, сложив их в элементы одного блока Composite.
То же самое можно проделать с любыми блоками(см. [пример](https://forever.si.yandex-team.ru/?hash=2846186226)).

Пользуясь свойством `gap`, можно имитировать несколько ответов подряд (`gap: 'm'`),
складывать разные блоки в рамках одного ответа (`gap: 's'`), создавать "склеенные" карточки (`gap: 'none'`).

## Границы применимости
### Composite хорошо заточен под:
  * Имитацию нескольких результатов поиска друг под другом, то есть сборку больших блоков, типа  organic с `gap: 'm'` или с разделителями
<details>
  <summary>Скриншот</summary>
  <img src="https://jing.yandex-team.ru/files/sunny/muzei_moskvy__Yandeks_nashlos_97mlnrezultatov_2016-08-18_11-20-46.png"/>
</details>

  * Работу с цветными карточками, скленными через нулевой отступ  `gap: 'none'`
<details>
  <summary>Скриншот</summary>
  <img src="https://jing.yandex-team.ru/files/sunny/telefon_gostinitsy_kosmos__Yandeks_nashlos_5mlnrezultatov_2016-08-18_11-22-06.png"/>
</details>

  * Быструю и легкую сборку нескольких блоков, с усредненным и не всегда красивым отступом.


### Сomposite не предназначен для:
  * Сборки нескольких небольших блоков, с особенными и различными вертикальными отступами.
    Вот, например,  organic собирать через какую-то сетку, типа composite, категорически нельзя.
<details>
  <summary>Скриншот</summary>
  <img src="https://jing.yandex-team.ru/files/sunny/Yandeks_zadan_pustoi_poiskovyi_zapros_2016-08-18_12-34-42.png"/>
</details>

  * Размещения блоков горизонтально. Горизонтального композита не будет. Если вам нужно что то такое - то правильным решением будет - создать новый блок.
<details>
  <summary>Скриншот</summary>
  <img src="https://jing.yandex-team.ru/files/sunny/Yandeks_zadan_pustoi_poiskovyi_zapros_2016-08-18_11-24-31.png"/>
</details>

  * Прописывания стилей(ну мне чуть чуть), скриптов(ну пару строчек), или отступов в пикселях из адаптера. Если вам нужны кастомные стили и скрипты, которые уникальны и не ложатся органично в API композита - вам нужно создать новый блок.
    Поля в API типа **script**, **style**, или **gap в пикселях** - плохая идея - они разрушают консистентность внешнего вида серпа :)

__Важно:__ при сборке фичи старайтесь использовать готовые конструкции (`organic`, `fact`, `object-badge` и т.д.).

## Вложенность
С помощью Composite можно собирать сложносочиненные сниппеты и колдунщики, вкладывая блоки друг в друга.

[**Пример:**](https://forever.si.yandex-team.ru/?hash=1766388973)
```js
"construct": {
  "template": "composite",
  "fold": { "height": 200 },
  "gap": "m",
  "items": [
    {
      "template": "object-badge",
      "object-badge": { ... },
      "items": [ ... ]
    },
    { "block": "button", "text": "test" },
    {
      "template": "composite",
      "gap": "none",
      "items": [
        {
          "template": "fact",
          "fact": { ... }
        },
        {
          "block": "button",
          "text": "Больше информации",
          "url": "..."
        }
      ]
    }
  ]
}
```
Этот пример выведет Composite, часть которого скрыта с помощью [fold](https://serpdocs.si.yandex-team.ru/constructives/fold), содержащий внутри набор блоков и еще один Composite с [фактовой карточкой](https://serpdocs.si.yandex-team.ru/constructives/fact).
