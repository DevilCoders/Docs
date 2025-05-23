### Задача
https://st.yandex-team.ru/RETAILSPECS-182

### Локальная задача
Добавить категорию "Скидки" в баннеры и в пипики (карусель категорий на главной магазина).

### Глобальная задача (которую и предлагаю тут решить)
Научиться любую категорию выводить в любое из трех мест:
- баннеры
- пипки
- карусели категорий

### Текущая логика, справочно
#### На фронте
Если для категории указано значение `banner_carousel`, то она отображается в
виде баннеров. Если для категории указано значение `categories_carousel`, то она
отображается в галереи категорий (пипки) Горзонтальные карусели – это все
категории, кроме категорий, у которых `show_in` только `banner_carousel` и кроме
указанных в экспе `eats_shops_home_carousels`

#### На беке
- динамические получают пустой `show_in` и, соответственно, показываются в каруселях
- дефолтные получают `show_in` = `categories_carousel` и идут в пипки
- кастомки получают `banner_carousel` и идут в карусели баннеров

### Решение
#### На беке
- [0.1д] добавить эксперимент `eats_products_horizontal_carousel_show_in`
- [0.5д] расширить список возможных значений поля `show_in` значением
  `horizontal_carousel` при помощи которого будет явно указываться нужно ли
  отображать категорию в виде горизонтальной карусели. Добавить алерт на то, что
  поле `show_in` не должно бысть пустым (самое простое - по логам, учитывая что
  это скорее всего никогда не случится). Самое простое было бы сделать
  minLength=1, но для старых клиентов это валидное значение, и не сработает.
- [0.5д] под экспериментом `eats_products_horizontal_carousel_show_in` для
  дефолтных категорий добавлять в `show_in` значение `horizontal_carousel`. То
  есть там будет приходить [`categories_carousel`, `horizontal_carousel`]
- [0.5д] под экспериментом `eats_products_horizontal_carousel_show_in` для
  динамических категорий добавлять в `show_in` значение `horizontal_carousel`.
  То есть там будет приходить [`horizontal_carousel`]
- (справочно) для кастомны категорий оставляем как есть. То есть там будет
  приходить [`banner_carousel`]
- [0.5д] добавить конфиг 3.0 `eats_products_categories_position_overrides`, который
  будет иметь следующую структуру:
```json
{
    "sort_order": -1000,  // Опционально. Будет перезаписывать sort_order, чтобы можно было управлять расположением
    "show_in": ["horizontal_carousel", "categories_carousel"]  // Обязательно
}
```
- в кваргах этого конфига должны быть, как минимум, `brand_id` и `category_id`
- [1.5д] по этому конфигу, переопределять значение поля `show_in`. Таким образом,
  получится любую категорию вынести в любое место.
- также по этому конфигу будет переопределяться `sort_order`. Это нужно, чтобы
  категорию можно было поставить в начало или в конец баннеров, например.
- (в дальнейшем можно подумать над выносом этого в админку)

#### На фронте
- при выборе, где показывать категорию, ориентироваться только на `show_in`.
  Другими словами:
    - если в `show_in` не пришло `horizontal_carousel` - НЕ показывать ее в
      каруселях (не смотреть на эксп `eats_shops_home_carousels`)
    - если `show_in` пустое - нигде не показывать категорию.
    - если пришло несколько значений - показывать во всех переданных местах
- картинку для категорий брать из `gallery` с соответствующим типом. Если нужной
  картинки нет - зажигать алерт но категорию показывать с картинкой -
  плейсхолдером
