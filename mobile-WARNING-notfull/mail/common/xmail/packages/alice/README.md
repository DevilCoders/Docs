##Бэкенд для Алисы

### Хочу только разрабатывать сценарий

- Скачиваем монорепу
- Открываем XMail в WebStorm (`mail/common/xmail`)
- Устанавливаем зависимости проекта  (конфигурация `Setup project` справа сверху)
- Разрабатываем сценарии в `packages/alice/code/scenario/`, отлаживаясь через запуск тестов в `__test__` (конфигурация `Alice: run all tests` справа сверху)
- Тесты сценариев работают на моках
- Для тестов сетевых запросов можно использовать свой oauth токен
- Получить его можно таким запросом 
```
curl -v -F grant_type=password -F username=LOGIN -F password=PASSWORD -F client_id=e7618c5efed842be839cc9a580be94aa -F client_secret=81a97a4e05094a4c96e9f5fa0b21f794 "https://oauth.yandex.ru/token"
``` 


### Хочу попробовать прогнать сценарий в приложении

#####1. Содаем вируалку
- Заводим виртуалку в qyp https://qyp.yandex-team.ru/. Выбираем:
	* дефолтный макрос: _SEARCHSAND_
	* Internet Access: NAT64
	* объём жесткого диска: больше 60гб (мегамайнд выжрет много)
- Заходим на нее `ssh ИМЯ.sas.yp-c.yandex.net` https://wiki.yandex-team.ru/arcadia/starterguide/#svn
- Генерирует `ssh–ключ` на удалённой машине, выкладываем его на стафф

#####2. Скачиваем Алису
- Устанавливаем утилиту `ya` https://wiki.yandex-team.ru/arcadia/starterguide/#ya-clone
- Скачиваем Алису 
```
cd arcadia
./ya make -j0 --checkout alice
``` 

#####3. Создаем новый сценарий
- Создаем конфиг для нашего сценария. Его структуру можно взять из файла `miles.pb.txt`, который лежит тут рядом:
```
nano alice/megamind/configs/dev/scenarios/miles.pb.txt
```
- Прописываем в конфиге мегамайнда, где надо искать конфиг для нашего сценария 
```
nano alice/megamind/configs/dev/megamind.pb.txt
```
- Делаем грамматику для обработки наших запросов
```
nano alice/megamind/configs/dev/scenarios/miles.grnt
```
Взять ее можно из файла `miles.grnt`, который лежит тут рядом. Сейчас достаточно добавить свой конфиг в папку ```alice/megamind/dev/scenarios```, и он подтянется сам.

#####4. Получаем экспериментальный флаг для ПП
- Компилируем грамматику в base64, чтобы потом явно указывать, какой сценарий использовать. Для этого сначала собираем тулу granet
```
ya make alice/nlu/granet/tools/granet
```
Затем запускаем ее на нашей грамматике
```
alice/nlu/granet/tools/granet/granet grammar pack -g "alice/megamind/configs/dev/scenarios/miles.grnt" --lang ru
```
Получится base64, его нужно сохранить, потом его нужно будет прописать в клиенте.

#####5. Поднимаем miles локально
- Возвращаемся сюда
- Прописываем секрет для TVM в файле `tvmtool/local.properties` в формате `mobapi_secret=your_secret`. Его можно взять тут https://abc.yandex-team.ru/services/mobileonline/resources/?show-resource=8580526
из поля client_secret.
- Устанавливаем TVM-демона локально и запускаем на порту 2222 - запускаем docker-конфигурацию `Alice: run TVM tool`
- Запускаем Miles на порту 80 - конфигурация `Start Alice backend on port 80`
- Запускаем ngrok `./ngrok http 80` - получаем публичный хост, который будет отправлять запросы в наш localhost:80 (Пример хоста: http://6459998b.ngrok.io).

#####6. Поднимаем megamind
- Полученный хост надо прописать в конфиге мегамайнда
- Заходим на виртуалку и редактируем host для ngrok в Handlers -> BaseUrl
```
nano /alice/megamind/configs/dev/scenarios/miles.pb.txt
```
- Добавляем ключ ssh
```
eval $(ssh-agent -s)
ssh-add
```
- Компилируем и запускаем Megamind
```
ya make --build=debug --sanitize=address -j8 --force-build-depends --checkout alice/megamind/scripts/run && alice/megamind/scripts/run/run -p 7007 -c alice/megamind/configs/dev/megamind.pb.txt
```

#####7. Настраиваем бету ПП
- См. https://wiki.yandex-team.ru/alice/megamind/protocolscenarios/otladka-v-prilozhenii/
- И в VINS Url надо прописать адрес своей виртуалки
- В качестве флага экспериментов прописываем тот base64 скомпилированной грамматики
```
bg_granet_source_text=H4slAAAAAAAA...
```

### Хочу задеплоить Алису
- Запрашиваем роль https://idm.yandex-team.ru/system/docker#role=13052617,f-role-id=13052617
- Открываем `build_and_publish.sh`, проходим по ссылке, получаем токен для репозитория Docker-образов
- Вставляем в скрипт свои `USERNAME` и `TOKEN`
- Инкрементим версию Алисы в скрипте
- Запускаем конфигурацию `Alice: build and publish docker image` справа сверху
- Идем в https://deploy.yandex-team.ru/project/mail-alice-backend и деплоим новую версию TODO

### For QA
Для тестирования на локально поднятом Мегамайндом необходимо проделать следующие действия:
1. Зайти на удалённую машину по ssh `ssh mobile-mail-alice-backend-v3.sas.yp-c.yandex.net`. Там уже настроены ключи, выкачан проект Мегамайнда, настроены урлы.
2. Запускаем ssh-агента и добавляем ssh-ключи `eval $(ssh-agent -s) ssh-add`, команда ssh-add запросит ключ, его можно узнать у `a-kononova`.
3. Перейти в директорию Аркадии `cd arcadia`
4. Запустить Мегамайнд `ya make --build=debug --sanitize=address -j8 --force-build-depends --checkout alice/megamind/scripts/run && alice/megamind/scripts/run/run -p 7007 -c alice/megamind/configs/dev/megamind.pb.txt`.
Note: если Мегамайнд уже запущен, то нужно убить процесс Мегамайнда
5. Скачать бету ПП (тут есть ссылки на бету https://wiki.yandex-team.ru/alice/megamind/protocolscenarios/otladka-v-prilozhenii/)
6. В приложении нужно прописать URL Мегамайнда `http://mobile-mail-alice-backend-v3.sas.yp-c.yandex.net:7007/speechkit/app/pa/`
*Android*: Панель отладки→Dialog→VINS URL
*iOS*: панель отладки -> Assistant/Settings -> Vins Url
7. Прописать ключ эксперимента
```
bg_granet_source_text=H4sIAAAAAAAAA9VY3W4TORR-lSrK3jGD9jY3vQAh7QVcwAVaIYSGxE0CmRnkmVAihNS0QnS1hX2VkDakSZvpK9hvtOfY82PP2JMpICKqSE2-843H_s6Pj_2-1adeQOIXByH1vfjFW0KjYRi0Oq0_W3daIy_ow1c6hu--N0TYH45I5PZpEAMWk3dx1Oq8R-PobpcSLyZOQA4d_O3gkJLZedbCH509SXGB4iIFhoAPDcO4A__34O9Z-54X7O-1n5Cgt9d-CJznkoR4RuIn7Jot2IKf8rMUAiBh3zSIf2QJ_8RPMsYNMJB1zi7TIfEl2Zh_jIjvexl3w2bAv-SngqtBUzbjx8V7E37MbvgRGOdGEJ5Q2MvquEv7uAnwrgqmhKYAaczKPBN4a8IWGsD_Zat01SiqedViGvwMVco0nMLDCfvK_wG9N-yyGHXBrvlnAK7kqAfD0YjQbNh2EAYRgY80tp7fkRHSIyMCEWKLDmm2RsZ9YZZRsZ-FhQSN64EwuQBxCwULINVvF3LkWgyjrkd7TncASUYiuyiS56Y8izrt-5KWqSJ_mdeFcXQtF2CAykEo4VmRVHMMP-TlOkGkL9ga4x0NuVYYruymsSD90IkHNBz3B0KLyCRGP3RTjtAhMoXJUy-IsYJ4EwiVyb5eRdBoDpZStdDriagW3sT8JOb5kn0F8lGxeglirBzp6Qr5zj-hfEBYGUAtteFhzGYY2Qjq3pKGC4jCtZB-bhosNUMq5C8_lxVDmb0KKUNA-K9h1t8UHwtgqb8IobWaHFh59QdzaGmYI5Y4fgI1TTUJGafaDET2mn2C7uP_qT--qI7Nn67JfYyG4zzulWIwKxavFQPxvmah7nv0teNFztB_E9IYQtKa_ch0vcjNmbb8fwjENNbh318ZPV8ofW1dKKa4vqGkkLEYGCGtouYvN79xLhy4gR3pugSpu9a8jO6yVmf-gu6lt9VVSPodvZQmX1abNrqLKsaSs2z2XbotgPbU6i402tz0CGypl9IlIGKu_tiPLdgFFKwvYs75fEWrwc-gju1ch9DxguiQULsYoSsZFkVgBgux4Td7YW2e1OXHY7DpwiNi1uzWG2mVrcHN9qHSZvbT3AozwB5qWrRVt_czJW9GkxrdwWoXHoxl5QGyd5DzapGZV8tR84NUqT0RG3atuvYMyedi0raZlJH3ljg96h3YCwhSXEGxifoEGLqmiFgXwz-KrnGjtlcK2OTMArGMbaE8A4KSv6a-AGBPdzRaBcpP-blA1iO59UxdPoHvstKOA1H6uuG4pqeTJFeQ7KGDJ5dH5FDKk4ePJSEb9usi95YyODKo0q2rDTJMwHZBIi8VlFuGhbGBuM3eV9tZZ8VXb8u_20UHNPS3eQg5Ngc9AJs8ZMLEYfH7mqPQal6tOJopoYsOwDupZJuLb4RztQuhtIqKxZdLawGWEgcku7LeVKHxVvuafj5Cd2zzYSXdVj_sy3hAfPutUupMQbJ58-lg2B3gpcH45SvSLfV-wmjxpkieWRGgEkjyy7Z0QHOxRrkVCfEmEBP5Kr3BW5sN6x07aFWEVg6UE3Il59rYkRMSbWtRgVLfo7b_Jul9EH4z63KhXmQlolyd6hvBubheRaE2jWZfXIfDTOUpPeNuuRRXSOZ7UZVQf1moMGtu0RTW1gsIA9fU1Cs002FLNdvOIApnyxuM7a1it_dsKsnQqyjmug28SjNtIlWWsTwpNHvwY4x9-PA_sTXX06QZAAA
```
*Andoid*: панель отладки -> experiments flags -> vins experiments
*iOS*: панель отладки -> Assistant/Settings -> Experiment list
8. Перезапустить ПП

### Как запустить Алису где угодно
Если на вашей тачке есть `docker-compose`, вы можете запустить Алису прямо здесь и сейчас. 
Для этого:
- Установите `docker-compose` на вашу машину `https://docs.docker.com/compose/install/`
- Скачайте монорепу `git clone ssh://git@bb.yandex-team.ru/mobile/monorepo.git`
- Перейдите в интересующую ветку `cd monorepo && git checkout BRANCH_NAME`
- Перейдите в папку с Алисой `cd mail/common/xmail/packages/alice`
- Добавьте в local.properties строку с `client_secret` отсюда https://abc.yandex-team.ru/services/mobileonline/resources/?show-resource=8580526
`echo mobapi_secret=SECRET > tvmtool/local.properties`
- Запустите Алису `sudo docker-compose up` - она поднимется на 80 порту
- Проверьте, что все работает - должна ответить ручка `http://localhost:80/ping`
- Для запуска в фоне используйте `docker-compose up -d`
- Теперь, посмотреть логи запущенной Алисы можно так: `docker-compose logs -f -t`

### Как пострелять в Алису
- Получите oauth токен пользователя, чей почтовый ящик мы будем менять во время нагрузочного тестирования
```
curl -v -F grant_type=password -F username=LOGIN -F password=PASSWORD -F client_id=e7618c5efed842be839cc9a580be94aa -F client_secret=81a97a4e05094a4c96e9f5fa0b21f794 "https://oauth.yandex.ru/token"
```
- Найдите конфигурацию `start:ammo:record` в `package.json` и вбейте туда свой токен 
- Запустите связку Мегамайнд+Алиса. Алису надо запустить через `start:ammo:record`
- Пройдите любой сценерий в Аманде/через ПП
- Запросы из сценария окажутся в файле `ammo.txt`
- Выберите последнюю стрельбу и склонируйте ее https://lunapark.yandex-team.ru/MOBILEMAIL-16468 (иконака справа)
- В качестве мишени выберите хост, где развернута интересующая версия Алисы на порту 80
- Залейте ваши патроны из `ammo.txt`
- Выберите схему нагрузки
- Огонь!
