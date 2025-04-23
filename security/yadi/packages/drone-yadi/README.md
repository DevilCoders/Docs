drone-yadi
==========

Плагин для запуска Yadi в рамках пайплайна Drone.io.

Последняя стабильная версия: `0.5.7181473`

**Не забудьте добавить секрет  YADI_TOKEN с вашим/роботным OAuth-токеном для Yadi**

Пример простого использования (покомитная проверка зависимостей + мониторинг зависимостей из "продовой" master ветки):
```yaml
pipeline:
# Собираем наше приложение, устанавливаем зависимости, стартуем тесты, etc
  test_app:
    image: registry.yandex.net/spec/trusty-nodejs:6
    commands:
      - export PATH=/opt/nodejs/6/bin:$PATH
      - npm install -g yarn
      - yarn install
      - npm test
# Делаем покомитную проверку зависимостей
  yadi_test:
    when:
      event: push
    image: registry.yandex.net/product-security/yadi-drone:0.5.7181473
    action: test
# Синхронизируем "продовый" набор зависимостей при мердже в мастер
  yadi_sync:
    when:
      event: push
      branch: master
    image: registry.yandex.net/product-security/yadi-drone:0.5.7181473
    action: sync
```
