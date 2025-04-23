# Зомбико-генератор для тестирования

**Форма для запуска:** https://zomber.in.yandex.net

**Расширение:** https://zomber.in.yandex.net/extension

### Команда для запуска:
```
stand=telemost.dsp conf=123 zombname=qwe mute=yes lifetime=2 npx wdio run wdio.conf.js
```

### Параметры

* `telemost.dsp` - стенд
* `123` –– номер конференции
* `qwe` –– имя зомбика
* `mute` –– `yes`/`no`: нажать ли кнопку мьюта после входа в конференцию
* `lifetime` –– от 1 до 30, время жизни зомбика в минутах

### Запустить несколько зомбиков одновременно
```
#!/bin/bash

for (( i=1; i < 10; i++ ))
do
    conf=123 zombname=qwe mute=yes lifetime=2 npx wdio run wdio.conf.js &
done
```

### Собрать релиз
```
zomber_version=1.1.0
docker build -t registry.yandex.net/maksimbark/telemost-zomber-internal:$zomber_version .
docker push registry.yandex.net/maksimbark/telemost-zomber-internal:$zomber_version
```

### Выкатить релиз
Обновить версию образа докера в [Деплое](https://deploy.yandex-team.ru/stages/maksimbark-stage)

### Требования:
Node.js 12.18.0
