# Iconostasinator Office

## Выкладка нового конфига (перезагрузка конфига)

1. Зайти на [вкладку управления конфигами](https://icon.yandex-team.ru/configs)

2. В верхней части экрана выбрать нужный зомбик: правый или левый (если стоять лицом к иконостасу)

3. У нужного конфига нажать на кнопку **"Выложить"**, затем нажать **"Копировать CURL"**

4. Открыть терминал, вставить скопированный CURL, отправить на зомбик

{% note alert %}

Не использовать кнопку "Применить", она ломает агент иконостаса

{% endnote %}

{% cut "Чтобы точно знать какой левый, какой правый" %}

![icon_left_right](_screenshots/icon_office.png "how_to" =800x300)

{% endcut %}

{% cut "Инструкция в картинках" %}

1. Выбираем нужный зомбик [вот тут](https://icon.yandex-team.ru/configs):

    ![icon_left_right](_screenshots/icon_office_left_right.png "how_to" =800x100)

2. Нажимаем **Выложить** у нужного конфига

    ![icon_left_right](_screenshots/vilozhit.png "how_to" =800x100)

3. Копируем URL и вставляем скопированную команду в терминал

    ![copy_url](_screenshots/copy_url.png "copy_url" =800x600)

{% endcut %}

## Запуск иконостосинатора
1. [Запустить левый зомбик](http://zomb-prj-153-4.zombie.yandex.net:5188/list_versions/iconostasinator)
2. [Запустить правый зомбик](http://zomb-prj-153.zombie.yandex.net:5188/list_versions/iconostasinator)
