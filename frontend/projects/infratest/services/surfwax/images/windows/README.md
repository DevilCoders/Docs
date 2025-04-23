# Инструкция

Спасибо [Ване Крутову](https://staff.yandex-team.ru/vania-pooh) за уже проделанное [исследование](https://github.com/aerokube/windows-images), на базе которого была создана текущая документация, представляющая собой пошаговую инструкцию по сборке Linux-образа с виртуалкой Windows (7 и 10) и браузера IE (8-11) или EdgeHtml (17.1). Все действия необходимо выполнять в директории с текущим README.

## Пререквизиты

- Ubuntu 18.04 (виртуалка в QYP)
- Поддержка виртуализации на машине:
  ```bash
  $ ls -l /dev/kvm # файл должен существовать
  ```
- [Qemu](https://www.qemu.org/download/#linux) версии 2.11.1, поставляемый из дистрибутива Ubuntu 18.04

## Установка Windows

- создать диск, на который будет установлен Windows:
  ```bash
  $ qemu-img create -f qcow2 hdd.img 16G
  ```
- скачать паравиртуальные драйвера [virtio-win-0.1.141.iso](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/archive-virtio/virtio-win-0.1.141-1/virtio-win-0.1.141.iso) (запасная [ссылка](https://disk.yandex.ru/d/3EnFbE3PIuXs6A)) и образ [Windows 7](https://disk.yandex.ru/d/CtL1rOKt4AVtLw) (IE8-IE11) или [Windows 10](https://disk.yandex.ru/d/62cavxtLll-r-g) (далее положим, что образ называется `windows.iso`)
- запустить виртуальную машину:
  ```bash
  $ sudo qemu-system-x86_64 -enable-kvm \
    -cpu qemu64,vmx=off,svm=off -machine q35,accel=kvm -smp 2,sockets=1,cores=2,threads=1 -m 8G \
    -usb -device usb-kbd -device usb-tablet -rtc base=localtime \
    -device e1000,netdev=nw0 -netdev user,id=nw0,ipv6-net=2001:db8:0:2::/64,hostfwd=tcp::4444-:4444 \
    -drive file=hdd.img,media=disk,if=virtio \
    -drive file=windows.iso,media=cdrom \
    -drive file=virtio-win-0.1.141.iso,media=cdrom \
    -vnc $(hostname):0
  ```
- открыть адрес `vnc://<hostname>:5900`, где `<hostname>` – это FQDN виртуалки, например, `vnc://gavryushin-bionic.man.yp-c.yandex.net:5900`, в любом VNC-клиенте (например, [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/))

### Windows 7

- [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2019.27.35.png) `Далее` в открывшемся окне установщика Windows
- [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2019.29.45.png) `Установить`
- принять условия лицензии и [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2019.31.33.png) `Далее`
- [выбрать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2019.33.40.png) полную установку Windows
- [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2019.35.09.png) `Загрузка`, а затем в открывшемся окне [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2019.35.58.png) `Обзор`
- найти папку `CD Drive (E:) virtio-win-0.1.1` → `viostor` → `w7` → `x86`, выбрать папку и [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2019.37.54.png) `OK`
- [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2019.40.04.png) `Далее`, затем еще раз [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2019.41.01.png) `Далее` (начнется [установка](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2019.41.39.png), нужно будет подождать)
- [указать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2019.56.28.png) пользователя `Пользователь`, [не устанавливать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2019.57.08.png) пароль
- отключить автоматическую активацию Windows при подключении к интернету и [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2019.59.58.png) пропустить
- [отложить решение](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2020.01.21.png) в окне настройки Windows по установке обновлений
- [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2020.03.46.png) `Далее` в окне настройки Windows по установке даты и времени
- [выбрать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2020.05.05.png) `Рабочую сеть` в окне настройки Windows по выбору текущего местоположения компьютера
- подождать завершения установки и [загрузки](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2020.07.47.png) системы

### Windows 10

- [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2012.38.36.png) `Next` в открывшемся окне установщика Windows
- [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2012.41.57.png) `Install now`
- выбрать операционную систему `Windows 10 Education N` и [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-24%20at%2013.05.56.png) `Next`
- принять условия лицензии и [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2012.45.06.png) `Next`
- [выбрать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2012.48.55.png) полную установку Windows (`Custom: Install Windows only (advanced)`)
- [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2013.29.38.png) `Load driver`, затем в открывшемся окне [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2013.31.37.png) `Browse`
- найти папку `CD Drive (E:) virtio-win-0.1.1` → `viostor` → `w10` → `x86`, выбрать папку и [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2012.55.32.png) `OK`
- [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2012.56.41.png) `Next`, затем еще раз [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2012.58.12.png) `Next` (начнется [установка](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2013.00.41.png), нужно будет подождать)
- оставить регион `United States` и [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2013.05.22.png) `Yes`
- оставить раскладку `US` и [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2013.07.22.png) `Yes`
- [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2013.40.08.png) `Add layout`, выбрать `Russian (Russia)` и [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2013.43.02.png) `Next`, далее выбрать `Russian` и [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2013.44.20.png) `Add layout`
- [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2013.09.09.png) `Skip for now` в окне настройки сети
- [указать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2013.10.12.png) пользователя `user`, [указать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2013.46.46.png) пароль `user` (пароль нужно будет подтвердить второй раз), ответами на три контрольных вопроса тоже [указать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2013.11.56.png) `user`
- [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2013.13.00.png) `No` в окне `Make Cortana your personal assistant?`
- отключить все тумблеры в окне `Choose privacy settings for your device` и [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2013.16.19.png) `Accept`
- подождать завершения установки и [загрузки](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2013.51.57.png) системы

## Настройка Windows

### Windows 7

- отключить брандмауэр
  - в строке для поиска приложений ввести `Брандмауэр` и [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2020.41.36.png) `Брандмауэр Windows` в панели управления
  - [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2020.51.49.png) `Включение и отключение брандмауэра Windows`
  - отключить брандмауэр Windows в параметрах размещения в домашней или рабочей сети и [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2020.53.36.png) `OK`
  - закрыть окно `Брандмауэр Windows`
- установить английский язык языком по умолчанию
  - в строке для поиска приложений ввести `Язык и региональные стандарты` и [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-14%20at%2012.43.35.png) найденное приложение
  - в появившемся окне выбрать `Языки и клавиатуры`, затем [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-14%20at%2012.44.12.png) `Изменить клавиатуру...`
  - в появившемся окне `Языки и службы текстового ввода`на вкладке `Общие` выбрать английский язык языком по умолчанию и [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-14%20at%2012.45.04.png) `Применить`
  - закрыть настройки
- настройка w32tm
  - в строке для поиска приложений ввести `regedit` и [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2021.54.46.png) найденное приложение
  - заменить значение разделов `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\W32Time\Config\MaxNegPhaseCorrection` и `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\W32Time\Config\MaxNegPhaseCorrection` на `ffffffff`
  - закрыть `Редактор реестра`
- настроить сетевое подключение
  - в строке для поиска приложения ввести `Центр управления сетями и общим доступом` и [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2020.10.29.png) найденное приложение
  - [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2020.12.41.png) `Изменение параметров адаптера`
  - в появившемся окне `Сетевые подключения` нажать правой кнопкой мыши (ПКМ) по `Подключение по локальной сети` и [выбрать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2020.15.35.png) `Свойства`
  - в появившемся окне `Подключение по локальной сети - свойства` в списке `Отмеченные компоненты используются этим подключением` выбрать `Протокол Интернета версии 6 (TCP/IPv6)`, затем [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2020.20.22.png) `Свойства`
  - в появившемся окне `Свойства: Протокол Интернета версии 6 (TCP/IPv6)` [выбрать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2020.22.39.png) `Использовать следующие адреса DNS-серверов`
  - в поле `Предпочитаемый DNS-сервер` указать `2a02:6b8:0:3400::1023`, затем [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2020.25.36.png) `OK`
  - [закрыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2020.27.39.png) окно свойств
  - в окне `Сетевые подключения` нажать ПКМ по `Подключение по локальной сети` и [выбрать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2020.29.44.png) `Отключить`, затем снова нажать ПКМ по `Подключение по локальной сети` и [выбрать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2020.31.51.png) `Включить`
  - закрыть окно `Сетевые подключения`
  - [проверить](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2020.34.02.png) подключение к интернету (заработает в течение 10-15 секунд)
- установить Firefox (этот браузер нужен, чтобы скачивать с Яндекс.Диска и официального сайта Microsoft, так как с помощью дефолтного IE8 этого сделать не получится)
  - скачать установщик Firefox с официального сайта (запасная [ссылка](https://disk.yandex.ru/d/2k786kEU1JLCeQ))
  - запустить установщик Firefox и следовать инструкциям
- установить (IE8 установлен по умолчанию)
  - [IE9](https://disk.yandex.ru/d/G6vAEC_0bDUIvA) или
  - [IE10](https://disk.yandex.ru/d/G6vAEC_0bDUIvA) или
  - IE11
    - скачать IE11 с официального сайта Microsoft (запасная [ссылка](https://disk.yandex.ru/d/TKd9TFZyY3SSiQ))
    - [скачать](https://docs.microsoft.com/ru-ru/troubleshoot/browsers/prerequisite-updates-for-ie-11) и [установить](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2021.30.20.png) (в ходе установки соглашаться со всем, не перезагружать систему) необходимые обновления Windows для установки IE11 (запасная [ссылка](https://disk.yandex.ru/d/WeXrOi42Y32etw))
    - перезагрузить Windows
    - запустить установщик IE11 и следовать инструкциям (согласиться с перезагрузкой системы)
    - [скачать](https://www.microsoft.com/en-us/download/confirmation.aspx?id=45134) и установить обновление безопасности для IE11 (запасная [ссылка](https://disk.yandex.ru/d/hY-iCpBDlL6UnA))
    - в строке для поиска приложений ввести `regedit` и [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-01%20at%2021.54.46.png) найденное приложение
    - [создать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2010.24.26.png) раздел `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Internet Explorer\MAIN\FeatureControl\FEATURE_BFCACHE`, в этом разделе [создать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2010.27.20.png) `Параметр DWORD (32 бита)` с [ключом](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2010.34.10.png) `iexplore.exe` и значеним `0`
    - закрыть `Редактор реестра`
- настроить IE (ниже приводится настройка IE11, настройка IE8-IE10 выполняется по аналогии)
  - подождать, пока откроется настройщик Internet Explorer 11, выбрать `Не использовать рекомендуемые параметры` и отключить отправление запросов `Do Not Track`, затем [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2010.09.12.png) OK (в IE8 при первом открытии нужно завершить [настройку](https://jing.yandex-team.ru/files/gavryushin/a873d7f456173c8af667608b45f71bb2_i-67.jpeg) браузера; использовать кастомную настройку с отключением всех фич)
  - перейти в настройки IE11 в правом верхнем углу, затем [выбрать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2010.12.01.png) `Свойства браузера`
  - на вкладке `Безопасность` отключить защищенный режим для [зоны](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2010.16.07.png) `Интернет` и [зоны](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2010.17.22.png) `Опасные сайты`, затем нажать `Применить` (согласиться со всеми предупреждениями и нажать `OK`)
  - на вкладке `Общие` [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2011.54.23.png) `Удалить` в графе `Журнал браузера`, в открывшемся окне выбрать все элементы, [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2011.56.25.png) `Удалить` и [выбрать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-21%20at%2011.07.13.png) `Удалять журнал браузера при выходе`
  - [перейти](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-21%20at%2011.08.40.png) в раздел `О программе` в настройках браузера и [отключить](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-21%20at%2011.10.10.png) обновление IE11
  - перезапустить браузер и [выбрать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2011.10.19.png) `Больше не показывать это сообщение`, что защищенный режим отключен (в IE8 нужно явно [кликнуть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-14%20at%2013.35.12.png) в предупреждение, чтобы появилось меню с нужным пунктом)
  - убедиться, что значение `Zoom` (Масштаб) у браузера [выставлено](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-14%20at%2012.51.56.png) в `100 %`.
- (если необходимо) настроить режим мобильной эмуляции Windows Phone в IE11 по [документации](https://st.yandex-team.ru/FEI-7460#59a3fbdd89ab6e5c03627dd9) (с использованием следующего [UA](https://st.yandex-team.ru/QAFW-1886#59a4297960777ae413c602f4))
- настройка Webdriver-а
  - скачать IEdriver [3.145.1](https://disk.yandex.ru/d/SBzOzoTL03UuHA), [selenoid_windows_386.exe](https://disk.yandex.ru/d/ydU27FZpA1JfWg), [resync_datetime_n_start_ie_driver.bat](https://disk.yandex.ru/d/zW7ntUTnnH7O-g) и соответствующий конфиг для [IE11](https://disk.yandex.ru/d/rpSnCobJV5yH5g) (или [IE11](https://disk.yandex.ru/d/CQCimSr-NV_vPA) в режиме мобильной эмуляции Windows Phone) или [IE10](https://disk.yandex.ru/d/17-2OuRtWVkwyA), или [IE9](https://disk.yandex.ru/d/cpjDFaMJoszaEA), или [IE8](https://disk.yandex.ru/d/kHo0BDomSIyofg) (с дальнейшим переименованием файла в `browsers.json`)
  - создать директорию `C:\Windows\System32\selenium\logs`
  - переместить загруженные файлы в директорию `C:\Windows\System32\selenium`
- настроить сертификат (следующие шаги были взяты из документации на [Вики](https://wiki.yandex-team.ru/security/ssl/sslclientfix/#vwindows))
  - скачать [YandexInternalRootCA.crt](https://disk.yandex.ru/d/eFEohqj2bBlwyw)
  - в строке для поиска приложений ввести `certmgr.msc` и [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2011.19.28.png) найденное приложение
  - в графе `Сертификаты - текущий пользователь` [выбрать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2011.23.45.png) `Доверенные корневые центры сертификации`, затем нажать ПКМ по `Сертификаты` в графе `Тип объекта` и [выбрать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2011.21.14.png) `Все задачи > Импорт...`
  - в появившемся окне [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2011.24.39.png) `Далее`, затем [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2011.25.38.png) `Обзор...` и [выбрать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2011.26.34.png) загруженный файл `YandexInternalRootCA.crt`, затем нажать [Далее](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2011.27.44.png) → [Далее](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2011.28.27.png) → [Готово](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2011.29.28.png) → [Да](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2011.30.18.png) → [OK](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2011.30.56.png)
  - закрыть приложение `certmgr.msc`
- очистить окружение
  - очистить директорию с загрузками (с очищением корзины)
  - удалить браузер Firefox
    - в строке поиска приложений ввести `Установка и удаление программ` и [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2011.50.34.png) найденное приложение
    - [удалить](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2011.51.30.png) браузер Firefox
- настроить разрешение экрана
  - [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2011.33.57.png) ПКМ по пустой области рабочего стола и выбрать `Разрешение экрана`
  - в появившемся окне в поле `Разрешение` выбрать `1600x1200`, [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2011.38.27.png) `Применить`, затем нажать `Сохранить изменения`
  - закрыть настройки разрешения экрана
- перезагрузить Windows, затем завершить работу Windows

### Windows 10

- отключить обновления
  - в строке для поиска приложений (`Type here to search`) ввести `services.msc` и [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2013.56.34.png) найденное приложение `Services`
  - в появившемся окне найти и [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2013.59.09.png) в списке сервисов `Windows Update` (правая кнопка мыши (ПКМ) → `Properties`)
  - в открывшихся настройках заменить значение поля `Startup type` с `Manual` на `Disabled`, [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.00.53.png) `Apply`, затем `OK`
  - закрыть приложение `Services`
- отключить Firewall
  - в строке для поиска приложений ввести `Windows Defender Security Center` и [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.03.54.png) найденное приложение
  - [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.06.05.png) `Firewall & network protection`
  - [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.07.38.png) `Domain network`, [перевести](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.09.13.png) тумблер из `On` в `Off`, [вернуться](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.10.32.png) на предыдущую страницу
  - [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.12.11.png) `Private network`, [перевести](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.13.25.png) тумблер из `On` в `Off`
  - закрыть приложение `Windows Defender Security Center`
- настройка w32tm
  - в строке для поиска приложений ввести `regedit` и открыть найденное приложение
  - заменить значение разделов `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\W32Time\Config\MaxNegPhaseCorrection` и `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\W32Time\Config\MaxNegPhaseCorrection` на `ffffffff`
  - закрыть `Редактор реестра`
- настроить местный часовой пояс
  - в строке для поиска приложений ввести `date` и открыть найденное приложение `Date & time settings`
  - в поле `Time zone` указать московский часовой пояс
- настроить Ethernet
  - в строке для поиска приложений ввести `Ethernet` и [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.14.37.png) найденное приложение `Change Ethernet settings`
  - [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.16.00.png) `Network (No Internet)`, [заменить](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.18.40.png) `Network profile` с `Public` на `Private`, вернуться на предыдущую страницу
  - [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.20.27.png) `Change adapter options`
  - в появившемся окне `Network Connections` [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.21.57.png) ПКМ по `Ethernet` и выбрать `Properties`
  - в появившемся окне `Ethernet Properties` в списке `This connection uses the following items` выбрать `Internet Protocol Version 6 (TCP/IPv6)`, затем [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.28.04.png) `Properties`
  - в появившемся окне `Internet Protocol Version 6 (TCP/IPv6) Properties` [выбрать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.32.22.png) `Use the following DNS server adresses`
  - в поле `Preferred DNS server` указать `2a02:6b8:0:3400::1023`, затем [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.34.53.png) `OK`
  - [закрыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.36.39.png) окно `Ethernet Properties`
  - в окне `Network Connections` [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.38.04.png) ПКМ по `Ethernet` и выбрать `Disable`, затем снова [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.39.15.png) ПКМ по `Ethernet` и выбрать `Enable`
  - [закрыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.41.23.png) окно `Network Connections`
  - в окне общих настроек Ethernet должно быть [видно](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.43.06.png) `You're connected to Internet`
  - закрыть окно общих настроек Ethernet
- настроить Edge
  - [перейти](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.45.53.png) в меню браузера в правом верхнем углу
  - [перейти](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.47.02.png) в `Settings`
  - [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.53.08.png) `View advanced settings`, [выключить](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.54.29.png) `Use page prediction to speed up browsing...` и `Help protect me from malicious sites and downloads...`
- настройка Webdriver-а
  - скачать [MicrosoftWebdriver.exe](https://disk.yandex.ru/d/uugcryVBtqdVfw), [selenoid_windows_386.exe](https://disk.yandex.ru/d/ydU27FZpA1JfWg), [resync_datetime_n_start_microsoft_webdriver.bat](https://disk.yandex.ru/d/4htPUxcyoYY1fw) и соответствующий конфиг для [MicrosoftEdge 17.1](https://disk.yandex.ru/d/moyz9MT3S2Uocw) (с дальнейшим переименованием файла в `browsers.json`)
  - создать директорию `C:\Windows\System32\selenium\logs`
  - переместить загруженные файлы в директорию `C:\Windows\System32\selenium`
- настроить сертификат (следующие шаги были взяты из документации на [Вики](https://wiki.yandex-team.ru/security/ssl/sslclientfix/#vwindows))
  - скачать сертификат [YandexInternalRootCA.crt](https://disk.yandex.ru/d/eFEohqj2bBlwyw)
  - в строке для поиска приложений ввести `certmgr.msc` и [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2015.34.40.png) найденное приложение
  - в графе `Certificates - Current User` [выбрать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2015.35.54.png) `Trusted Root Certification Authorities`, затем нажать ПКМ по `Certificates` в графе `Object Type` и [выбрать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2015.37.55.png) `All tasks > Import`
  - в появившемся окне [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2015.42.20.png) `Next`, затем [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2015.44.13.png) `Browse...` и [выбрать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2015.47.06.png) загруженный файл `YandexInternalRootCA.crt`, затем нажать [Next](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2015.48.12.png) → [Next](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2015.49.31.png) → [Finish](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2015.50.30.png) → [Yes](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2015.52.08.png) → [OK](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2015.53.29.png)
  - закрыть приложение `certmgr.msc`
- очистить окружение
  - очистить директорию с загрузками (с очищением корзины)
  - открыть настройки браузера Edge и [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.48.40.png) `Choose what to clear`, выбрать все элементы, [нажать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2014.50.09.png) `Clear`, закрыть браузер Edge
- настроить разрешение экрана
  - в строке для поиска приложений ввести `display` и [выбрать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2015.55.00.png) найденное приложение `Change display settings`
  - в [появившемся](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2015.57.06.png) окне в поле `Resolution` [выбрать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2015.58.16.png) `1600x1200`, затем нажать `Keep changes`
  - закрыть окно настроек дисплея
- перезагрузить Windows, затем завершить работу Windows

## Создание снапшота Windows

- создать образ, который будет содержать снапшот состояния системы:
  ```bash
  $ qemu-img create -b hdd.img -f qcow2 snapshot.img
  ```
- запустить виртуальную машину с использованием снапшота:
  ```bash
  $ sudo qemu-system-x86_64 -enable-kvm \
    -cpu qemu64,vmx=off,svm=off -machine q35,accel=kvm -smp 2,sockets=1,cores=2,threads=1 -m 8G \
    -usb -device usb-kbd -device usb-tablet -rtc base=localtime \
    -device e1000,netdev=nw0 -netdev user,id=nw0,ipv6-net=2001:db8:0:2::/64,hostfwd=tcp::4444-:4444 \
    -drive file=snapshot.img,media=disk,if=virtio \
    -monitor stdio \
    -vnc $(hostname):0
  ```
- запустить Webdriver
  - Windows 7
    - в строке для поиска приложений ввести `cmd` и [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2012.26.26.png) найденное приложение от имени администратора (ПКМ по найденному приложению → `Запуск от имени администратора`)
    - в появившемся окне терминала перейти в директорию `C:\Windows\System32\selenium`
    - запустить управление службой времени:
      ```bash
      net start w32time
      ```
    - [запустить](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2012.33.45.png) команду:
      ```bash
      selenoid_windows_386.exe -listen :4444 -conf C:\Windows\System32\selenium\browsers.json -log-output-dir C:\Windows\System32\selenium\logs -save-all-logs -disable-docker -enable-file-upload -limit 1
      ```
    - [свернуть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-02%20at%2012.35.25.png) окно терминала Windows
    - [заблокировать](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-12-17%20at%2013.37.30.png) текущего пользователя (необходимо, чтобы окно, в котором запускается IE, было не в фокусе, иначе IE теряет фокус на элементах)
  - Windows 10
    - в строке для поиска приложений ввести `cmd` и [открыть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2016.20.57.png) найденное приложение `Command Prompt` от имени администратора (ПКМ по найденному приложению → `Run as administrator`)
    - в появившемся окне терминала перейти в директорию `C:\Windows\System32\selenium`
    - запустить управление службой времени:
      ```bash
      net start w32time
      ```
    - запустить команду:
      ```bash
      selenoid_windows_386.exe -listen :4444 -conf C:\Windows\System32\selenium\browsers.json -log-output-dir C:\Windows\System32\selenium\logs -save-all-logs -disable-docker -enable-file-upload -limit 1
      ```
    - [свернуть](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2016.26.37.png) окно терминала Windows
- перейти в окно терминала, где запущен qemu, и ввести:
  ```bash
  savevm windows
  ```
- затем в этом же окне ввести
  ```bash
  quit
  ```
- убедиться, что виртуальная машина запускается из снапшота:
  ```bash
  $ sudo qemu-system-x86_64 -enable-kvm \
    -cpu qemu64,vmx=off,svm=off -machine q35,accel=kvm -smp 2,sockets=1,cores=2,threads=1 -m 8G \
    -usb -device usb-kbd -device usb-tablet -rtc base=localtime \
    -device e1000,netdev=nw0 -netdev user,id=nw0,ipv6-net=2001:db8:0:2::/64,hostfwd=tcp::4444-:4444 \
    -drive file=snapshot.img,media=disk,if=virtio \
    -loadvm windows \
    -vnc $(hostname):0
  ```
- создать, а затем удалить сессиию, чтобы убедиться, что все работает корректно
- закрыть qemu через `CTRL^C`

## Сборка образа

- собрать контейнер:
  ```bash
  $ docker build -t registry.yandex.net/selenium/<name:version> .
  ```
  где `<name:version>` - идентификатор браузера и его версии, например, `edge:17.1`
- проверить работоспособность контейнера
  - запустить контейнер
    ```bash
    $ docker run -it --rm --privileged -p 4444:4444 -p 5900:5900 -e ENABLE_VNC='true' registry.yandex.net/selenium/<name:version>
  - по адресу `vnc://<hostname>:5900` должен открыться снапшот ранее созданной системы (пароль `selenoid`)
  - по адресу `http://127.0.0.1:4444/status` должен отображаться [статус](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-11-22%20at%2017.13.32.png)
  - создать, а затем удалить сессию, чтобы убедиться, что все работает корректно:
    ```bash
    # пример для IE11
    BROWSER_VERSION=11; curl --header "Content-Type: application/json" -v http://127.0.0.1:4444/wd/hub/session -d '{"capabilities":{"alwaysMatch":{"browserName":"internet explorer","browserVersion":"'"$BROWSER_VERSION"'"}},"desiredCapabilities":{"browserName":"internet explorer","browserVersion":"'"$BROWSER_VERSION"'"}}'

    # пример для MicrosoftEdge 17.1
    BROWSER_VERSION=17.1; curl --header "Content-Type: application/json" -v http://127.0.0.1:4444/wd/hub/session -d '{"capabilities":{"alwaysMatch":{"browserName":"MicrosoftEdge","browserVersion":"'"$BROWSER_VERSION"'"}},"desiredCapabilities":{"browserName":"MicrosoftEdge","browserVersion":"'"$BROWSER_VERSION"'"}}'

    # в логах запуска предыдущей команды будет id-сессии
    curl -X DELETE -v http://127.0.0.1:4444/wd/hub/session/<SESSION_ID>
    ```
  - остановить контейнер через `CTRL^C`
- запушить контейнер
  ```bash
  $ docker push registry.yandex.net/selenium/<name:version>
  ```
