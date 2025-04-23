# Образ chrome на android
*Спасибо команде selenium (@vania-pooh) за [скрипты и материалы по сборке образа](https://bb.yandex-team.ru/projects/QAFW/repos/qa-docker-registry/browse/selenium/android/)*

### Сборка образа
1. Скачать apk нужной версии chrome с сайта [apkmirror](https://www.apkmirror.com/uploads/?appcategory=chrome) (из доступных загрузок нужно выбрать вариант apk под архитектуру x86) и положить его в директорию `chrome/`.
2. Выяснить версию ChromeDriver для данной версии chrome. Для этого нужно выполнить команду, заменив `<version>` на версию скачанного apk вида `100.0.4896.58` ([документация](https://sites.google.com/chromium.org/driver/downloads/version-selection) по выбору версии ChromeDriver).
```bash
VERSION=<version>; curl "https://chromedriver.storage.googleapis.com/LATEST_RELEASE_$(echo $VERSION | sed 's/.[0-9]*$//')"
```
3. Выполнить сборку образа с помощью интерактивного скрипта:
```bash
./build.sh
```

Для работы скрипта необходим docker. Рекомендуемый набор параметров:
- `Appium version` - 1.16.0.
- `Android version` - поддерживаются 4.4, 5.0, 5.1, 6.0, 7.0, 7.1, 8.0, 8.1, 9.0, 10.0, 11.0 (по мере необходимости можно добавлять новые версии в `build.sh`).
- `Would you like Android phone device` - y.
- `Specify device skin` - WXGA720.
- `Specify custom screen density if needed` - не указывать.
- `Specify SD card size, Mb` - 500.
- `Specify userdata.img size, Mb` - 500.
- `Do you need Chrome Mobile` - y.
- `Specify Chrome APK` - имя файла apk из директории `chrome/` шага 1, например, `chrome_77.apk`.
- `Specify custom Chromedriver version if needed` - версия ChromeDriver из шага 2.
- `Do you need custom WebView:` - n
- `Are you testing search app` - n.
- `Specify Selenium browser name` - имя браузера, влияет только на подсказку имени образа, например, `chrome`.
- `Specify Selenium version` - версия браузера, влияет только на подсказку имени образа, например, `phone-77.0`.
- `Specify timeout value` - 180000.
- `Do you need OpenCV` - n.
- `Specify image tag` - имя образа, например, `registry.yandex.net/selenium/chrome:phone-77.0`;

### Запуск образа
Вместо `<image_tag>` нужно подставить имя образа из предыдущего шага.
```bash
docker run -it --rm --privileged -p 4723:4723 -p 5900:5900 -e ENABLE_VNC='true' <image_tag>
```

### Проверка образа
Поднимаем сессию, подставив вместо `<browser_name>` и `<browser_name>` имя и версию браузера:
```bash
BROWSER_NAME='<browser_name>'; BROWSER_VERSION='<browser_version>'; curl -X POST 0.0.0.0:4723/wd/hub/session -d '{"desiredCapabilities":{"automationName":"UiAutomator1","browserName":"'"$BROWSER_NAME"'","deviceName":"android","platformName":"Android","skipDeviceInitialization":true,"version":"'"$BROWSER_VERSION"'"}}' --header "Content-Type: application/json"
```

Открыть VNC:
```
vnc://127.0.0.1:5900 # пароль 'selenoid'
```

Примечание: при работе на QYP нужно пробросить порт `5900` при подключении по ssh, заменив `<hostname>` на адрес своей qyp машинки:
```bash
ssh -L 5900:<hostname>:5900 <hostname>
```
И заходить по VNC соответственно:
```
vnc://<hostname>:5900
```

### Публикация образа
Вместо `<image_tag>` нужно подставить имя образа из шага по сборке.
```bash
docker push <image_tag>
```
