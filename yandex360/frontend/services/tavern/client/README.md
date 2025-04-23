
# Клиентские приложения таверны


## Разработка

### Первоночальная настройка
Выполнить [действия](../README.md#первоночальная-настройка) описанные в корне проекта.

### Как запустить iframe сборку
```bash
npm start
```
Это запустит dev-сборку для iframe приложения. Артефакты сборки кладутся в `./client-build` и `../server/client-build`. После сборки клиента можно запускать `npm start` в `../server` и тогда само приложение доступно по адресу https://XXX.tavern-dev.mail.yandex.ru/ где `XXX` имя вашей qyp машины. Альтернативно можно выполнить одну команду `npm start` в корне проекта.

### Как запустить шторку
Для локальный разработки шторки необходимо собрать придолжение и "подсунуть" его в сборку мобильного приложения.

#### Подготовка ios DevApp
Смотреть сборку проще в специальном [DevApp](https://a.yandex-team.ru/arc_vcs/mobile/mail/ios/mail-app/YandexMobileMail/DevApp). Далее пример именно на основе этого:
1. Поставить Xcode
2. Выполнить инструкцию по настройке сборки https://a.yandex-team.ru/arc_vcs/mobile/mail/ios/mail-app
3. В `arcadia/mobile/mail/ios/mail-app/YandexMobileMail/DevApp`:
  1. Раскомменьтить `yo_module 'Taverna'` в `Podfile`
  2. Выполнить `pod install`
4. Открыть в Xcode и запустить сборку `DevApp.xcworkspace` нажатием на треугольник

#### Запуск шторки в приложении 
Собрать шторку можно командой `npm run build:mobile`. 
1. Перейти в директорию `cd ~/arcadia/arcadia/mobile/mail/ios/mail-app/YandexMobileMail/Modules/Screens/Taverna/Resources/Taverna`
2. Очистить её `rm -rf ./*`
3. Стянуть сборку: ``scp -r qyp:/home/`(whoami)`/www/services/tavern/client/build-mobile ./  && cp -r ./build-mobile/* ./`` (`qyp` тут сокращение вашей персональный qyp машинки)
4. Запустить сборку  DevApp в Xcode

Иногда залипает старая сборка шторки. Тогда: 1) убедиться что симулятор остановлен, 2) сделать `pod install` в `DevApp`. К райнем случае можно удалить приложение внутри симулятора.

## Доставка приложения в prod
В случае шторки и в случае iframe это разные процессы.

### Доставка шторки в prod 
1. Код шторки публикуется как npm пакет, разработчики мобильных приложений скачивают npm пакет и встраивают в свою шторку.
2. Если разработчики влюкчили опцию, то мобильное приложение может само сходить в https://tavern.mail.yandex.ru/mobile-manifest и выкачать новую версию шторки если она есть. При этом выкачиваение проихойдет не из npm, а согласно путям описанным в манифесте.

Сравнение версий в 2) происходит по полю "version", поэтому необходимо циферку менять.

#### Деплой шторки
Сейчас процесс кривоватый:
```bash
npm run package X.X.X
```

1. опубликовать в npm
2. пушнуть в ветку
    1. дождаться сборки sbr [https://sandbox.yandex-team.ru/resource/2769570863/view](https://sandbox.yandex-team.ru/resource/2769570863/view) 
    2. поменять sbr в services/tavern/tools/deploy-specs/front-app.j2
    3. вмержить ветку
3. залить новую deploy спеку `make prestable && make put-prestable`


### Доставка iframe приложения в прод
soon...
