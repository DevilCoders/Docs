How to start
---

1. Получаем токен из Секретницы

   https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982

2. Добавляем его в env

FAQ
---

Ошибка Caused by: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target

https://wiki.yandex-team.ru/security/ssl/sslclientfix/#vjava

---

Если модуль не отрисовался в ide, нужно выполнить
cd qa
ya make --rebuild --clear
Build -> Regenerate and Reload: ya ide
File -> Invalidate caches..


ya tool allure generate allure-results -o allure-manual-report

Запуск

ya make -tA --test-tag ya:manual --allure=allure-report
ya upload allure-report  --type ALLURE_REPORT --attr project=bss--do-not-remove  --ttl 7  --description 'Результат автотестов'
