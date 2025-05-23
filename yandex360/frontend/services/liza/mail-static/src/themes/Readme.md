# Themes for the new mail

## Подготовка изображений для темы
Темы у нас бывают "нарезанными" из мелких изображений, который масштабируются/повторяются на всю область (космос, природа, и другие) и сделанные из цельных изображений (сезоны, трава, региональные и другие).
Для тем с цельными изображениями картинки  бывают очень тяжелыми (~1.9 Мб для одного фона). Их нужно оптимизировать, и сделать jpg прогрессивным для быстроты загрузки.
Сделать это можно, воспользовавшись скриптом tools/optimizeJpg из модуля liza. Также нужно следить за актуальностью картинок и удалять неиспользуемые, чтобы минимизировать нагрузку на облачное хранилище.

## Добавление абсолютно новой темы с нуля

Допустим, новая тема назвается `whatever`.

### С помощью `make newtheme` [устарело]

Проще всего подготовить всё для новой темы, используя команду make, выполненную в корне либо репозитория `mail-static`, либо репозитория `mail-themes`:

``` bash
make newtheme name=whatever
```

Создаст минимально необходимые файлы и папки (аналогично тому, как это делается вручную)

### Вручную

Если почему-то не хочется использовать `make`, либо хочется понять что же эта команда делает, то можно создать всё для темы вручную.

#### В репозитории [`mail-static`](https://github.yandex-team.ru/Daria/mail-static):

1. В папку `src/styl/` добавить файл `theme-whatever.styl`.

2. Содержимое этого файла должно быть следующим:

```
@require '../lib/**'
init_theme('whatever')
```

(Как и прочие файлы в этой папке, когда-нибудь это будет автогенериться, так что не стоит писать какие-либо дополнительные стили в этом файле).

#### В этом репозитории ([`mail-themes`](https://github.yandex-team.ru/Daria/mail-themes)):

1. В корне создать папку `whatever`.
2. В этой папке создать файл `theme.json`.
3. В этой же папке создать подпапку `skins`.

#### `skins/`

В папке `skins` должны находиться все изображения, использующиеся для тем.

Изображения, применяемые для всех скинов должны лежать в корне этой папки, например:

```
skins/
  background.jpg
```

##### Нумерованные скины

Изображения, сгруппированные по нумерованным скинам кладутся в соответствующие нумерованные папки (скины нумеруются начиная с единицы):

```
skins/
  1/
    background.jpg
  2/
    background.jpg
```

##### Адаптивные изображения

Для автоматической подгонки нужного изображения под текущий размер вьюпорта браузера файлы фонов именуются так, чтобы в их названии были указаны их размеры:

```
skins/
  1/
    1024x768.jpg
    1280x960.jpg
    1440x1080.jpg
    1680x1260.jpg
    1920x1440.jpg
  2/
    1024x768.jpg
    1280x960.jpg
    1440x1080.jpg
    1680x1260.jpg
    1920x1440.jpg
```

Если у нас один скин, то можно сразу изображения закидывать в папку skins/ и в поле `count` в theme.json указать значение `1`:

```
skins/
  1024x768.jpg
  1280x960.jpg
  1440x1080.jpg
  1680x1260.jpg
  1920x1440.jpg
```

``` json
{
  "skins": {
    "count": 1
  }
}
```
#### `theme.json`

Это джейсон со всеми настройками конкретной темы. Нужно стремиться к тому, чтобы всё-всё-всё настраивалось с его помощью.

Данные из джейсонов тем в дальнейшем будут реиспользованы и в динамике, поэтому для того, чтобы не грузить в динамике ненужные там поля, они именуются начиная с подчёркивания. При этом, вложенные в поле с подчёркиванием поля не нужно называть с подчёркиванием.

##### Поле `name`

В теме обязательно нужно задать поле `name`, являющееся идентификатором этой темы:

``` json
{
  "name": "whatever"
}
```

##### Поле `_bg_page`

Это поле задаёт фон всей странице.

Также этот фон будет использоваться в качестве фолбека когда картинки ещё не загрузились.

``` json
{
  "_bg_page": "#DFD4C4"
}
```

##### Поле `_bg_aside`

Это поле задаёт фон левой колонки.

``` json
{
  "_bg_aside": "rgba(#FFF, 0.65)"
}
```

##### Поле `_bg_content`

Это поле задаёт фон содержимому правой колонки (или обеих правых колонок, в случае трипейна).

Некоторые страницы и блоки в Почте не тематизируются, так, например, композ всегда будет на белом фоне.

``` json
{
  "_bg_content": "rgba(#FFF, 0.8)"
}
```

##### Поле `_accent_color`

Это поле задаёт цвет фона для выделенной папки в списке папок.
Для новой темы - это еще и цвет выделенного письма фокусом, прыща непрочитанности,
кнопки "Написать".

``` json
{
  "_accent_color": "#000"
}
```

##### Поле `_themed_text_color`

Это поле задаёт цвет текста отправителя и темы в списке писем.

``` json
{
  "_themed_text_color": "#999"
}
```

##### Поле `_bottom_padding`

Это поле задаёт нижний отступ под всей страницей.Используется для того, чтобы в темах с иллюстрациями в фоне на их нижнюю часть можно было бы посмотреть просто домотав страницу до конца.

На самом деле задаёт не отступ, а минимальную высоту блоку `.mail-Layout-Themes`, использующийся для добавление в футер всяких специальных блоков для темы.

Работает только для двапейна.

``` json
{
  "_bottom_padding": 200
}
```

##### Поле `_min-height`

Это поле задаёт минимальную высоту фона для темы. Если наслаивающиеся изображения сверху и снизу начинают некрасиво наслаиваться, то необходимо задать этот параметр так, чтобы картинкам хватало места.

``` json
{
  "_min-height": 910
}
```

##### Поля `page_is_dark`, `aside_is_dark` и `content_is_dark`

В некоторых темах фон под всей страницей, под контентом и/или левой колонкой могут быть тёмными. В этом случае необходимо это явно указать, используя соответствующие параметры:

``` json
{
  "page_is_dark": true,
  "aside_is_dark": true,
  "content_is_dark": true,
}
```

Эти параметры можно использовать как на верхнем уровне, так и внутри переопределений для группы и/или отдельного скина.

CSS классы для модификаторов: `with-dark-page`, `with-dark-aside`, `with-dark-content`

##### Поле `_layers`

Одно из двух самых важных полей, задающее то, на какие «слои» бьётся фон темы, с заданием дефолтных параметров для каждого слоя.

Всего существует пять слоёв, на которых рекомендуется применять картинки: `page`, `page-extras`, `cover`, `cover-extras`, `page-extras2` и `page-extras3`. Слои перечислены в порядке их применения с нижнего по верхний.

###### Статичные фоны

Для слоёв `page`, `page-extras`, `page-extras2` и `page-extras3` фон статичен, то есть в двапейне будет скроллиться вместе с контентом.
Модификаторы `page`, `page-extras`, `page-extras2` и `page-extras3` в новых темах будут недоступны, переходим на `cover`, `cover-extras`, `cover-extras2`.

###### Фиксированные фоны

Для слоёв `cover` и `cover-extras` фон фиксированный, то есть и в двапейне и в трипейне он всегда будет размером с вьюпорт и не будет скроллиться вместе с контентом страницы.

###### Адаптивные фоны

Для адаптивных фонов необходимо использовать слои `cover` и `cover-extras`. На одном слое не могут быть обычные изображения и адаптивные, так что стоит их разделять по разным слоям.

Адаптивный фон задаётся параметром слоя `stops`, в котором перечисляются какие бывают размеры адаптивных изображений:

``` json
{
  "_layers": {
    "cover": {
      "stops": [
        [1024, 768],
        [1280, 960],
        [1440, 1080],
        [1680, 1260],
        [1920, 1440]
      ]
    }
}
```

Адаптивные изображения будут автоматически собраны из соответствующих указанным значениям файлов, лежащих в папке `skins/`.

###### Обычные фоны и картинки по углам

Обычные, не адаптивные фоны и картинки по углам и сторонам могут спокойно сосуществовать на одном слое.

Все соответствующие изображения нужно перечислять в параметре слоя `images`, где ключ — имя картинки, а значение — объект с параметрами конкретной картинки или значение `true`:

``` json
{
  "_layers": {
    "page": {
      "images": {
        "background.jpg": { "position": "0 0", "repeat": "repeat" }
      }
    },
    "page-extras": {
      "images": {
        "bl.png": { "position": "0 100%" },
        "br.png": { "position": "100% 100%" },
        "tl.png": { "position": "0 0" },
        "tr.png": { "position": "100% 0" }
      }
    }
  }
}
```

В этом примере отдельно задаётся повторяющийся фон в слое `page`, после чего задаются картинки по углам на слое `page-extras`.

В данном случае картинки разделяются на два слоя, так как фон на `page` одинаков для всех скинов, тогда как изображения по углам меняются для каждого скина.

###### Параметры изображений

В качестве значения изображения (либо на одном уровне с адаптивным изображением) передаётся объект с различными параметрами. Для фонов, в которых изображения меняются, эти параметры будут выступать в качестве умолчательных.

- `bg` — задаёт фон-фолбек для изображения.

- `position` — задаёт значение `background-position` для изображения. По умолчанию изображения центрируются по горизонтали и вертикали. Не стоит забывать, что у нас во всех поддерживаемых браузерах работают новые значения для `background-position` вида `bottom 10px right 20px` для того, чтобы задавать позицию изображения не только с верхнего левого угла.

- `repeat` — задаёт значение `background-repeat` для изображения. По умолчанию `no-repeat`.

- `disabled` — отключает конкретную картинку. Используется тогда, когда определённая картинка из набора должна полностью отключаться в каком-то из скинов, либо когда она может в зависимости от скина находиться в разных слоях (см. тему `kitekat`).

##### Поле `skins`

Внутри поля `skins` задаётся структура скинов со скоупами для темы.

###### Поле `count`

Для тем, в которых может быть больше одного скина, необходимо задавать поле `count`:

``` json
{
  "skins": {
    "count": 17
  }
}
```

В таком случае при применении изображений по слоям будет произведен поиск соответствующих изображений по папкам, соответствующим номерам скинов (номера скинов начинаются с единицы).

###### Поля переопределений для определённых нумерованных скинов

Для скинов, которым нужно задать параметры, отличающиеся от тех, что были указаны в поле `_layers`, можно использовать поля переопределений:

``` json
{
  "skins": {
    "count": 6,
    "skin-1": {
      "_layers" : {
        "page-extras": {
          "images": {
            "tr.png": { "position": "top 220px right 30px" }
          }
        }
      }
    },
    "skin-2": {
      "_layers" : {
        "page-extras": {
          "images": {
            "bl.png": { "position": "0 100%" }
          }
        }
      }
    }
  }
}
```

В качестве ключа выступает `skin-` + номер скина, в качестве значения — объект `_layers`, в котором можно переопределить какие-то из значений слоёв для данного конкретного скина. В примере выше переопределяются позиции для двух скинов в слое `page-extras`.

###### Поле `disabled` для  отключённых скинов

Если какой-то скин нужно отключить (совсем его не рендерить), то можно использовать поле `disabled`:

```
{
  "skin-1": { "disabled": true }
}
```

###### Поле `scope` для групп скинов

В случае, если скины в теме делятся на группы, используются «скоупы». Скажем, если в теме все скины делятся на группы `foo` и `bar`, это можно выразить следующим образом:

``` json
{
  "skins": {
    "scopes": {
      "foo": {
        "count": 6
      },
      "bar": {
        "count": 7
      }
    }
  }
}
```

Все группы задаются внутри объекта с ключом `scopes`, внутри ключами выступают названия групп, а значениями — объекты аналогичные полю `skins`.
Это значит, что группы, в случае необходимости, могут быть вложенными друг в друга.
Группы являются взаимоисключающими, то есть одновременно может быть либо группа `lightside` или `darkside`.

##### Автоматическое определение наличия картинки в скине

После определения всех картинок для слоя в `_layers`, при генерации стилей для скинов стайлус будет автоматически подключать только те изображения, что фактически есть в папке скина/группы.

Это полезно тем, что, по сути, разные скины и группы могут иметь разные наборы второстепенных изображений, но во время объявления того, какие изображения в каких слотах бывают можно просто указать все слоты, а стайлус сам разберётся к какому скину какие слоты относятся на основе лежащий в файловой системе для конкретного скина файлов.

## Представление темы и скина на странице

Все стили темы применяются строго через модификатор на HTML, имеющий вида `.theme-whatever`.

Конкретный скин применяется через модификатор вида `.m-skin-…`, например, `.m-skin-1` или `.m-skin-summer.m-skin-summer-4` и т.д., где опциональному номеру скина предшествует название группы через дефис. Кроме того, в случае групп всегд обязательно добавлять класс для группы, а не только для скина, при этом также нужны будут модификаторы и для каждой подгруппы: для гипотетического `.m-skin-summer-june-night-4` на HTML нужно будет вешать также `.m-skin-summer`, `.m-skin-june` и `.m-skin-night`.
