# Дебаг в мобильных браузерах

_Рассмотрен самый распространенный кейс дебага Android и iOS на macOS. Остальныее кейсы можно найти в полезных ссылках._

## Удаленный дебаг в YaBro на Android устройстве

### Установка ADB

1. Установить homebrew

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

2. Установить adb

```bash
brew cask install android-platform-tools
```

3. Посмотреть список подключенных Android девайсов

```bash
adb devices
```

_Другие варианты установки adb на [StackOverflow](https://stackoverflow.com/a/32314718)_

### Включение режима разработчика на девайсе

1. Перейти в _Settings_;
2. Выбрать меню _System_;
3. Выбрать пункт _About phone_ (или найти строку с номером сборки в другом месте);
4. 7 раз тапнуть по пункту _Build number_;
5. Вернуться в предыдущее меню и выбрать пункт _Developer Options_;
6. Включить режим дебага через usb.

### Дебаг YaBro

1. В DevTools _Main menu_ > _More Tools_ > _Remote devices_;
2. Чекнуть галочку _Discover USB devices_;
3. Подключить девайс к компьютеру и убедиться через команду _adb devices_ что устройство определено;
4. Выбрать нужный девайс во вкладке _Remote devices_;
5. Открыть нужную страницу в мобильном браузере. Окно удаленного Devtools в десктопном YaBro откроется автоматически.

### Удаленный дебаг в Safari на iPhone

1. Подключить девайс к компьютеру;
2. В настройках Safari на девайсе включить пункт _Web Inspector_;
3. Открыть нужную страницу на девайсе;
4. В десктопном Safari перейти в меню Develop, выбрать нужный девайс, выбрать сессию. Окно инспектора откроется автоматически.

### Полезные ссылки

-   [Debugging on Mobile Devices](https://support.brightcove.com/debugging-mobile-devices)
-   [Get Started with Remote Debugging Android Devices](https://developers.google.com/web/tools/chrome-devtools/remote-debugging)
-   [How to Install ADB on Windows, macOS, and Linux](https://www.xda-developers.com/install-adb-windows-macos-linux/)
