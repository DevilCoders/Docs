# Стрельба в Inestor

## Стрельба из танка
1. Заказываем дырки от танка к мишине https://wiki.yandex-team.ru/Load/howto/idm-puncher/
2. Устанавливаем танк
    ```bash
       echo "deb http://load-xenial.dist.yandex.ru/load-xenial stable/all/" | sudo tee -a /etc/apt/sources.list.d/yandex-tank-xenial.list
       echo "deb http://load-xenial.dist.yandex.ru/load-xenial stable/amd64/" | sudo tee -a /etc/apt/sources.list.d/yandex-tank-xenial.list
       sudo apt-get update
       sudo apt-get install yandex-tank-internal
    ```
3. Собираем пушку
4. Проверяем что танк работает
    ```bash
    yandex-tank -c config/sample-tank-load.yaml
    ```

## Стрельба из pandora
Для отладки пушки, танк не нужен.
```bash
ya make gun && ./gun/short-term-storage-gun config/sample-load.yaml
```

## Подгатавливаем патроны
1. Включаем в конфигации Ingestor трассировку запросов(по умолчанию уже включена для 1% запросов)
2. Скачиваем к себе результаты трассировки
    ```bash
    ./downloadTrace.sh solomon_test_sts
    ```
3. Будут скачены последние отратировавшийся лог с каждой машинки в папку `trace`
4. Из trace логов генерируем патроны
    ```bash
   ya make ammo-gen
   ./prepareAmmo.sh
    ```
5. Патроны будут в директории ammo, для каждого хоста в отдельности и для кластера,
в зависимости от мишени выбираем нужные патроны

## Стрельба по одному хосту
1. Скачиваем и подготавливаем патроны
2. Берем патрон подготовленный для хоста и указываем до него путь в файле `sample-load.yaml` или `sample-tank-load.yaml`
3. Стреляем пандорой или танком по выбору
