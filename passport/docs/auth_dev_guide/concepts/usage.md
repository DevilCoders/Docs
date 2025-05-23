# Использование системы авторизации на веб-сервисе

Для разработчиков веб-сервисов, использующих систему авторизации, разработаны следующие правила и рекомендации:

- Проверять авторизацию браузеров следует по [определенному алгоритму](before.md).
    
- Все сервисы, находящиеся вне доменов `yandex.ru`, `yandex.com` и `yandex.com.tr` должны использовать сквозную [мультидоменную авторизацию](MDA_About.md).
    
- Авторизацию на сервисе можно дополнительно защитить с помощью дополнительной [HTTPS-куки](https-sessionid.md).
- Для пользователей сервиса можно оформить [подписку](SID_About.md), чтобы отличать их от случайных посетителей.
- Веб-интерфейс авторизации реализован в [элементах Лего](interface.md).

