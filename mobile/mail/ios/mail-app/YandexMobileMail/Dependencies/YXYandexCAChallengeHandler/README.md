# YXYandexCAChallengeHandler

Фичи
- Позволяет использовать дополнительные корневые сертификаты в процессе проверки цепочки сертификатов при установлении ssl-соединения. По умолчанию включено доверие YandexInternalRootCA.
- Защита от отзыва сертификатов, в цепочке которых есть YandexCA.
- Защита от отзыва сертификатов, в цепочке которых есть Intermediate CA от GlobalSign + хост Яндекса.

## Подключение к проекту

В Podfile приложения прописать зависимость на YXYandexCAChallengeHandler
```ruby
s.dependency 'YXYandexCAChallengeHandler'
```

## Подключение к NSURLSession

- Реализовать делегат NSURLSessionDelegate
```objc
@interface YourSessionDelegate : NSObject <NSURLSessionDelegate>
@end
```
- Реализовать метод didReceiveChallenge делегата
```objc
@implementation YourSessionDelegate

- (void)URLSession:(NSURLSession*)session didReceiveChallenge:(NSURLAuthenticationChallenge*)challenge completionHandler:(void (^)(NSURLSessionAuthChallengeDisposition disposition, NSURLCredential* credential))completionHandler {
  [YXYandexCAChallengeHandler handleChallengeWithProtectionSpace:challenge.protectionSpace completionHandler:completionHandler];
}
@end
```

- Подключить делегат к NSURLSession
```objc
  self.urlSessionDelegate = [[YourSessionDelegate alloc] init];
  self.urlSession = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:self.urlSessionDelegate delegateQueue:nil];
```

## Подключение к WKWebView

- Реализовать делегат WKNavigationDelegate
```objc
@interface YourNavigationDelegate : NSObject <WKNavigationDelegate>
@end
```

- Реализовать метод didReceiveAuthenticationChallenge
```objc
@implementation YourNavigationDelegate

- (void)webView:(WKWebView*)webView didReceiveAuthenticationChallenge:(NSURLAuthenticationChallenge*)challenge completionHandler:(void (^)(NSURLSessionAuthChallengeDisposition disposition, NSURLCredential* __nullable credential)) completionHandler {
  [YXYandexCAChallengeHandler handleChallengeWithProtectionSpace:challenge.protectionSpace completionHandler:completionHandler];
}
@end
```

- Подключить делегат к WKWebView
```objc
YourNavigationDelegate* navigationDelegate = ...;
self.navigationDelegate = navigationDelegate;
WKWebView* webview = ...;
webview.navigationDelegate = navigationDelegate;
```

## Добавление исключений в ATS
https://developer.apple.com/documentation/bundleresources/information_property_list/nsapptransportsecurity?language=objc

Что бы доверие к кастомному корневому сертификату заработало, нужно отключить ATS либо глобально, либо для нужного списка доменов
- Глобальное отключение
```
Info.plist -> NSAppTransportSecurity -> NSAllowsArbitraryLoads = YES
```
- Отключение только для WKWebView
```
Info.plist -> NSAppTransportSecurity -> NSAllowsArbitraryLoadsInWebContent = YES
```
- Отключение для списка доменов
```
Info.plist -> NSAppTransportSecurity -> NSExceptionDomains -> {
    <domain-name-string>: {
        NSIncludesSubdomains : YES/NO
        NSExceptionAllowsInsecureHTTPLoads : YES
    }
}
```

## Встраивание дополнительных сертификатов
- Генерируем C-массив из сертификата (в формате PEM)
```sh
./tools/cert2inc.py --input <your-cert>.pem > YourCert-inc.h
```
По необходимости нужно сделать cert2inc.py исполняемым
```sh
chmod +x tools/cert2inc.py
```

- Подключаем С-массив
```objc
static unsigned char kYourCert[] = {
#include "YourCert-inc.h"
};
```

- Добавляем к списку extraRootCertificates
```objc
NSMutableArray* extraRootCertificates = ...;
[YXYandexCAChallengeHandler addCert:kYourCert length:sizeof(kYourCert) to:extraRootCertificates];
```
