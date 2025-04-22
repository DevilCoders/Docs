# Как начать работу с MapKit для Android
Библиотека **MapKit** для платформы Android 5.0 и выше доступна в [репозитории Maven Central](https://search.maven.org/search?q=maps.mobile). Чтобы создать приложение с картой Яндекса:

## Шаг 1. Получите ключ для работы с MapKit {#key}

1. Перейдите в [Кабинет Разработчика](https://developer.tech.yandex.ru/).
2. Авторизуйтесь с учетной записью Яндекса или зарегистрируйте новый аккаунт.
3. Нажмите **Получить ключ** и выберите пакет **MapKit SDK**.
4. Заполните информацию о проекте, укажите нужный тариф и нажмите **Отправить**.

Дальнейшие инструкции придут на почту.

Полученный ключ можно использовать для работы с MapKit в нескольких приложениях.

## Шаг 2. Установите библиотеку MapKit {#install}

1. [Создайте](http://developer.android.com/training/basics/firstapp/creating-project.html) новый проект или откройте существующий, например, в [Android Studio](http://developer.android.com/intl/ru/tools/studio/index.html).
2. Откройте файл `build.gradle` **проекта**. В секции `repositories` добавьте репозитории [Maven Central](http://central.sonatype.org/) и [Google Maven](http://maven.google.com/):
    ```
    repositories {
        ...
        mavenCentral()
        maven {
             url "http://maven.google.com/"
        }
    }
    ```
3. Откройте файл `build.gradle` **приложения (модуля)**. В секции `dependencies` добавьте [зависимость](https://docs.gradle.org/current/userguide/artifact_dependencies_tutorial.html):
    ```
    dependencies 
    {
        // Облегченная библиотека, содержит только карту, слой пробок, 
        // LocationManager, UserLocationLayer и возможность скачивать офлайн-карты (только в платной версии).
        implementation 'com.yandex.android:maps.mobile:4.1.0-lite'
    
        // Полная библиотека в дополнение к lite версии предоставляет автомобильную маршрутизацию, 
        // веломаршрутизацию, пешеходную маршрутизацию и маршрутизацию на общественном транспорте, 
        // поиск, suggest, геокодирование и отображение панорам.
        // implementation 'com.yandex.android:maps.mobile:4.1.0-full'
    }
    ```
4. Синхронизируйте проект, чтобы применить изменения. Например, в Android Studio можно нажать **Sync Now** или выбрать в меню **File → Synchronize**. Дождитесь окончания синхронизации. 

Если синхронизация завершилась успешно, при компиляции библиотека будет добавлена в проект автоматически.

## Шаг 3. Настройте библиотеку {#setup}

1. Добавьте карту на Activity:
    ```xml
    <com.yandex.mapkit.mapview.MapView
        android:id="@+id/mapview"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
    ```    
2. Инициализируйте карту в методе `onCreate()` нужного Activity:
    ```java
    private MapView mapview;

    @Override
    protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);
        MapKitFactory.setApiKey("Ваш API-ключ");
        MapKitFactory.initialize(this);

        // Укажите имя Activity вместо map.
        setContentView(R.layout.map);
        mapview = (MapView)findViewById(R.id.mapview);
        mapview.getMap().move(
            new CameraPosition(new Point(55.751574, 37.573856), 11.0f, 0.0f, 0.0f),
            new Animation(Animation.Type.SMOOTH, 0),
            null);
    }
    ```
    :warning: **Примечание.** Не рекомендуется вызывать `MapKitFactory.initialize()` в методе `Application.onCreate()`. Это может привести к лишним операциям и повышенному расходу батареи устройства.
3. Передайте события `onStart` и `onStop` в `MapKitFactory` и `MapView`. Иначе MapKit не сможет отобразить карту и остановить обработку карты, когда Activity с картой становится невидимым для пользователя:
    ```java
    @Override
    protected void onStop() {
        mapView.onStop();
        MapKitFactory.getInstance().onStop();
        super.onStop();
    }
    
    @Override
    protected void onStart() {
        super.onStart();
        MapKitFactory.getInstance().onStart();
        mapView.onStart();
    }
    ```

## Шаг 4. Соберите и запустите приложение {#run}
При работе в Android Studio приложение можно сразу запустить, сборка будет выполнена автоматически. Следуйте инструкциям ниже, чтобы запустить приложение на:

* [эмуляторе](http://developer.android.com/training/basics/firstapp/running-app.html#Emulator).

* [Android-устройстве](http://developer.android.com/training/basics/firstapp/running-app.html#RealDevice), подключенном через USB к компьютеру разработчика (в режиме отладки).

## Шаг 5. Обратите внимание при дальнейшей работе {#work}
:warning: MapKit хранит слабые ссылки на передаваемые ему Listener-объекты. Необходимо самим хранить ссылку на них в памяти:
```java
private final CameraListener cameraListener = new CameraListener() {
    // ...
}  
mapview.getMap().addCameraListener(cameraListener);
```

:warning: По умолчанию методы всех Listener-объектов и платформенных интерфейсов вызываются на главном потоке, если в документации метода не сказано обратное.

## Пример приложения {#samples}
```java
package com.yandex.mapkitdemo;

import android.os.Bundle;
import android.app.Activity;

import com.yandex.mapkit.Animation;
import com.yandex.mapkit.MapKitFactory;
import com.yandex.mapkit.geometry.Point;
import com.yandex.mapkit.map.CameraPosition;

import com.yandex.mapkit.mapview.MapView;

/**
 * В этом примере показывается карта и камера выставляется на указанную точку. 
 * Не забудьте запросить необходимые разрешения.
 */
public class MapActivity extends Activity {
    /**
     * Замените "your_api_key" валидным API-ключом.
     * Ключ можно получить на сайте https://developer.tech.yandex.ru/
     */
    private final String MAPKIT_API_KEY = "your_api_key";
    private final Point TARGET_LOCATION = new Point(59.945933, 30.320045);

    private MapView mapView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        /**
        * Задайте API-ключ перед инициализацией MapKitFactory.
        * Рекомендуется устанавливать ключ в методе Application.onCreate(),
        * но в данном примере он устанавливается в Activity.
        */
        MapKitFactory.setApiKey(MAPKIT_API_KEY);
        /**
        * Инициализация библиотеки для загрузки необходимых нативных библиотек.
        * Рекомендуется инициализировать библиотеку MapKit в методе Activity.onCreate()
        * Инициализация в методе Application.onCreate() может привести к лишним вызовам и увеличенному использованию батареи.
        */
        MapKitFactory.initialize(this);
        // Создание MapView.
        setContentView(R.layout.map);
        super.onCreate(savedInstanceState);
        mapView = (MapView)findViewById(R.id.mapview);

        // Перемещение камеры в центр Санкт-Петербурга.
        mapView.getMap().move(
                new CameraPosition(TARGET_LOCATION, 14.0f, 0.0f, 0.0f),
                new Animation(Animation.Type.SMOOTH, 5),
                null);
    }

    @Override
    protected void onStop() {
        // Вызов onStop нужно передавать инстансам MapView и MapKit.
        mapView.onStop();
        MapKitFactory.getInstance().onStop();
        super.onStop();
    }

    @Override
    protected void onStart() {
        // Вызов onStart нужно передавать инстансам MapView и MapKit.
        super.onStart();
        MapKitFactory.getInstance().onStart();
        mapView.onStart();
    }
}
```

Полный код примера доступен в репозитории [GitHub](https://github.com/yandex/mapkit-android-demo).
