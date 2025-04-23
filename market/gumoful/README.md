# GUMOFUL

## Как открыть в CLION

Открываем проект
```bash
cd arcadia/market/gumoful
ya make . --add-protobuf-result # --add-protobuf-result, чтобы протоклассы подтягивались в проект
ya ide clion --make-args '--add-protobuf-result'
clion .
```

Как дебажить в clion: https://wiki.yandex-team.ru/arcadia/ide/clion/#debuginclion

## Как релизить гумофул тулзу.

Гумофул тулзу нужно релизить 3 разными способами.

#### 1. Tar пакетом для RTC

Склонировать таску https://sandbox.yandex-team.ru/task/454271086/view
поменять description
запустить
После успешного создания, зарелизить сначала в на testing окружение, потом на prod.

#### 2. Debian пакетом

1. Обновить ченджлог и собрать командой debuild
    ```bash
    cd arcadia/market/gumoful/tools
    dch --no-auto-nmu -i "MBO-XXX ....." # может потребоваться руками поменять debian/changelog
    # на этом шаге нужно закоммитить и запушить изменения
    debuild
    cd ../
    dupload --to market-trusty yandex-market-gumoful_1.1.0_amd64.changes
    ```
   Внимание! Собирать дебиан пакет нужно командой debuild. Командой ya package pkg.json --debian НЕЛЬЗЯ
   <details>
     Странно, что старый деб сохраняет бинари в 
     ```
     /usr/lib/yandex/gumoful/tools/yt_renderer
     /usr/lib/yandex/gumoful/tools/stream_renderer
     /usr/lib/yandex/gumoful/tools/standalone_renderer
     /usr/lib/yandex/gumoful/tools/rendering_viewer
     ```
     
     А новый в
     ```
     /usr/bin/yt_renderer
     /usr/bin/stream_renderer
     /usr/bin/standalone_renderer
     /usr/bin/rendering_viewer
     ```
   </details>

2. Раскатить на дев/тестинг/прод машинки
   * дев машинки: aida, callisto, braavos.market.yandex.net, derkoat (добавьте еще дев машинки)  
    ```bash
    ssh aida
    sudo apt-get update # обновляем индексы
    # sudo apt-get purge yandex-market-gumoful # удалить пакет (ВЫПОЛНЯТЬ НЕ ОБЯЗАТЕЛЬНО)
    sudo apt-get install yandex-market-gumoful=1.1.0 # устанавливаем пакет нужной версии. Если пакет не найден, то надо подождать еще чуть чуть и повторить
    ```
   * На тестинг и прод раскатывать с помощью: https://c.yandex-team.ru/packages/yandex-market-gumoful
   * Потом обновить в дебиан зависимостях в приложениях (см. выкладку в мультитестинг)
   
#### 3. В Мультитестинг
Перед тем, как релизить в мультитестинг нужно зарелизить debian пакетом и RTC пакетом. 
Связано это с тем, что если сначала обновить версию для мультитестинга, то потом нельзя будет выложить релиз в тестинг и прод (актуально только для выкладки через кондуктор).

Чтобы в МТ обновилась версия, нужно поменять версию во всех файлах debian/control.






