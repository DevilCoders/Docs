# Как начать работу с MapKit для iOS
Библиотека MapKit для платформы iOS 12 и выше доступна в [репозитории CocoaPods](https://cocoapods.org/pods/YandexMapsMobile). Чтобы создать приложение с картой Яндекса:

## Шаг 1. Получите ключ для работы с MapKit {#key}

1. Перейдите в [Кабинет Разработчика](https://developer.tech.yandex.ru/).
2. Авторизуйтесь с учетной записью Яндекса или зарегистрируйте новый аккаунт.
3. Нажмите **Получить ключ** и выберите пакет **MapKit SDK**.
4. Заполните информацию о проекте, укажите нужный тариф и нажмите **Отправить**.

Дальнейшие инструкции придут на почту.

Полученный ключ можно использовать для работы с MapKit в нескольких приложениях.

## Шаг 2. Добавьте библиотеку в проект {#install}

Добавьте библиотеку в проект с помощью CocoaPods.

1. Перейдите в каталог с [Xcode](https://developer.apple.com/xcode/)-проектом.
2. Создайте [Podfile](http://guides.cocoapods.org/using/the-podfile.html) для перечисления зависимостей от других библиотек:
    ```
    $ pod init
    ```
3. Откройте Podfile в текстовом редакторе и добавьте зависимость для своей цели:
    ```
      use_frameworks!
      # Облегченная библиотека, содержит только карту, слой пробок, 
      # LocationManager, UserLocationLayer и возможность скачивать офлайн-карты (только в платной версии).
      pod 'YandexMapsMobile', '4.1.0-lite'
      
      # Полная библиотека в дополнение к lite версии предоставляет автомобильную маршрутизацию, 
      # веломаршрутизацию, пешеходную маршрутизацию и маршрутизацию на общественном транспорте, 
      # поиск, suggest, геокодирование и отображение панорам.
      # pod 'YandexMapsMobile', '4.1.0-full'
    ```
4. Выполните в каталоге проекта команду:
    ```
    $ pod install
    ```

    Чтобы открыть файл проекта, выполните команду:
    ```
    $ open *.xcworkspace
    ```

## Шаг 3. Настройте библиотеку {#setup}

Чтобы использовать библиотеку в приложении, инициализируйте ее с заданными параметрами. Откройте `xcworkspace` и внесите следующие изменения:

1. Добавьте элемент **View** на storyboard.
2. Укажите класс `YMKMapView` для добавленного View.
3. Запросите необходимые разрешения в файле `info.plist`:
    ```
    NSLocationWhenInUseUsageDescription
    ```
4. Подключите библиотеку MapKit:
    **Swift**
    ```swift
    import YandexMapsMobile
    ```
    **Objective-C**
    ```objectivec
    #import <YandexMapsMobile/YMKMapKitFactory.h>
    ```
5. Задайте ваш API-ключ в методе `application:didFinishLaunchingWithOptions` делегата приложения и инстанцируйте объект `YMKMapKit`:
    **Swift**
    ```swift
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
        YMKMapKit.setApiKey("Ваш API-ключ")
        YMKMapKit.sharedInstance()
    }
    ```
    **Objective-C**
    ```objectivec
    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        [YMKMapKit setApiKey: @"Ваш API-ключ"];
        [YMKMapKit mapKit];
    }
    ```
    :warning: Если вы используете многомодульное приложение и хотите инициализировать MapKit не в `application:didFinishLaunchingWithOptions`, то после создания объекта MapKit вызовите метод `onStart()`:
    **Swift**
    ```swift
    YMKMapKit.setApiKey("MAPKIT_API_KEY")
    YMKMapKit.sharedInstance().onStart()
    ```
6. Инициализируйте карту в контроллере нужного View:
    **Swift**
    ```swift
    override func viewDidLoad() {
        super.viewDidLoad()
    
        mapView.mapWindow.map!.move(
            with: YMKCameraPosition.init(target: YMKPoint(latitude: 55.751574, longitude: 37.573856), zoom: 15, azimuth: 0, tilt: 0),
            animationType: YMKAnimation(type: YMKAnimationType.smooth, duration: 5),
            cameraCallback: nil)
    }
    ```
    **Objective-C**
    ```objectivec
    - (void)viewDidLoad {
        [super viewDidLoad];
        YMKPoint *target = [YMKPoint pointWithLatitude:55.751574 longitude:37.573856];
        [self.mapview.mapWindow.map moveWithCameraPosition:[YMKCameraPosition cameraPositionWithTarget:target
                    zoom:11
                 azimuth:0
                    tilt:0]];
    }
    ```

## Шаг 4. Соберите и запустите приложение {#run}

Соберите приложение. Для запуска можно выбрать:

* **iOS-устройство**.
  Выберите в меню **Product → Destination**, затем выберите устройство в разделе **Device**.

* **Эмулятор**.
  Выберите в меню **Product → Destination**, затем выберите симулятор в разделе **iOS Simulators**.
  
Запустите приложение. Для этого выберите в меню **Product → Run**.

## Шаг 5. Обратите внимание при дальнейшей работе {#work}

:warning: MapKit хранит слабые ссылки на передаваемые ему Listener-объекты. Необходимо самим хранить ссылку на них в памяти:
**Примечание.** Все Listener-объекты должны наследоваться от класса `NSObject`.
**Swift**
```swift
internal class CameraListner: NSObject, YMKMapCameraListener {
    func onCameraPositionChanged(with map: YMKMap?, cameraPosition: YMKCameraPosition, cameraUpdateReason: YMKCameraUpdateReason, finished: Bool) {
        // Do something
    }
}
let cameraListener = CameraListner()

override func viewDidLoad() {
    super.viewDidLoad()
    mapView.mapWindow.map!.addCameraListener(with: cameraListener)
}
```
**Objective-C**
```objectivec
@interface CameraListener: NSObject<YMKMapCameraListener>
@end

@implementation CameraListener
- (void)onCameraPositionChangedWithMap:(nullable YMKMap *)map cameraPosition:(nonnull YMKCameraPosition *)cameraPosition cameraUpdateReason:(YMKCameraUpdateReason)cameraUpdateReason finished:(BOOL)finished {
    // Do something
}

@end

@property(nonatomic) CameraListener *cameraListener;

- (void)viewDidLoad {
    [super viewDidLoad];
    self.cameraListener = [[CameraListener alloc] init];
    [self.mapView.mapWindow.map addCameraListenerWithCameraListener:self.cameraListener];
}
```

:warning: По умолчанию методы всех Listener-объектов и платформенных интерфейсов вызываются на главном потоке, если в документации метода не сказано обратное.

:warning: Для эмулятора под M1 минимальная поддерживая версия: iOS 13.

:warning: На эмуляторе под M1 не поддерживается OpenGL, поэтому в конструкторы ```YMKMapView``` и ```YMKPanoView``` необходимо передавать ```vulkanPreferred: true```. Эта настройка требуется только для сборки под эмулятор.

:warning: Рекомендуемый флаг линковки: ```-ObjС```.

## Пример приложения {#samples}
```swift
import UIKit
import Foundation
import YandexMapsMobile

/**
 * В этом примере показывается карта и камера выставляется на указанную точку.
 * Нужно указать ваш API-ключ в файле AppDelegate.swift с помощью метода YMKMapKit.setApiKey(MAPKIT_API_KEY).
 * Не забудьте запросить необходимые разрешения.
 */
class MapViewController: UIViewController {
  @IBOutlet weak var mapView: YMKMapView!

  let TARGET_LOCATION = YMKPoint(latitude: 59.945933, longitude: 30.320045)

  override func viewDidLoad() {
       super.viewDidLoad()

       mapView.mapWindow.map!.move(
           with: YMKCameraPosition(target: TARGET_LOCATION, zoom: 15, azimuth: 0, tilt: 0),
           animationType: YMKAnimation(type: YMKAnimationType.smooth, duration: 5),
           cameraCallback: nil)
  }
}
```

Полный код примера доступен в репозитории [GitHub](https://github.com/yandex/mapkit-ios-demo).
