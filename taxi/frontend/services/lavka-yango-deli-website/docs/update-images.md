# Обновить изображения

1. Идем в фигму где собрана раскадровка
   https://www.figma.com/file/f1l3H6C5iLTdDqiI1EV5jO/Yango-Deli-Images

1. Меняем в компоненте изображение

1. Выбираем все размерные фреймы (6 фреймов)

1. Экспортируем их (12 файлов в сумме, для каждого фрейма экспортируется @2x и обычная версии)

1. Закидываем скаченные изображения в https://tinypng.com

1. Скачиваем оптимизированные изображения

1. Все @2x изображения закидываем в [tinypng](https://tinypng.com) еще раз

1. Скачиваем их с заменой уже существующих

1. Копируем оптимизированые изображения в `client/components/SectionImage/${name}/assets/${region}/`

1. Оригинальные изображения экспортированые из фигмы переносим в `client/components/SectionImage/${name}/assets/${region}/original`. Директорию в git не добавляем.

1. Переходим в `original/` директорию
   ```bash
   cd client/components/SectionImage/${name}/assets/${region}/original
   ```

1. Создаем webp версии изображений
    ```bash
    for file in *.jpg ; do cwebp -q 75 "$file" -o "${file%.jpg}.webp"; done
   ```

1. Полученные webp изображения переносим в `client/components/SectionImage/${name}/assets/${region}/`

1. `original/` директорию удаляем
