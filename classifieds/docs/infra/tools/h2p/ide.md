# Работы через IDE

Настройки для работы в IDE (для тех программ, которые поддерживают импорт настроек) отправляются на почту сотруднику при получении роли.

## Импорт настроек для IDE из письма {#import}

{% cut "Sequel Pro" %}

Шестеренка внизу слева -> `Import...` -> Выбираем файл `sequel-pro.plist` из письма

![Пример настроек в Sequel Pro](_assets/ide/sequel-pro.png)

{% endcut %}

{% cut "TablePlus" %}

Правая кнопка мыши -> `New` -> `Connection from URL...`

![Пример настроек в Sequel Pro](_assets/ide/tableplus.png)

{% endcut %}

{% cut "MySQL Workbench" %}

Пункт меню `Tools` -> `Configuration` -> `Restore Connections` -> Выбираем файл `mysql-workbench.zip` из письма.

После импорта необходимо указать путь до ssh ключа в `openssh` формате.

![Пример настроек в Sequel Pro](_assets/ide/mysql-workbench.png)

{% endcut %}

{% cut "DataGrip" %}

Необходимо скопировать в буфер обмена всё содержимое из файла `datagrip.txt` из письма (открыть в редакторе, выделить все, скопировать в буфер).

Потом `New` -> `Import from Clipboard`

![Пример настроек в Sequel Pro](_assets/ide/datagrip.png)

{% endcut %}

## Ручная настройка
Если ваша IDE не поддерживает импорт настроек, вы можете настроить соединение самостоятельно.
Для этого потребуется установить соединение через SSH-туннель.

{% list tabs %}

- MySQL

  Настройки для подключения:

  Параметр | Значение
    :--- | :---
  `Host` | `<database>.mdb-(ro/rw)-<cluster id>.query.consul`
  `User` | `analyst` **без пароля**
  `SSH host` | `h2p.vertis.yandex.net`
  `SSH user` | **ваш логин на Стаффе**
  `SSH port` | 2222

  #### Примеры для разных IDE
  {% cut "Sequel Pro" %}

  В `Sequel Pro` нужно выбрать SSH ключ.
  Для этого надо нажать на "ключик" в поле "Пароль" снизу и выбрать ваш приватный SSH ключ.

  ![Пример настроек в Sequel Pro](_assets/mysql/sequel-pro-settings.png)

  {% endcut %}

  {% cut "TablePlus" %}

  ![Пример настроек в TablePlus](_assets/mysql/tableplus-settings.png)

  {% endcut %}

  {% cut "MySQL Workbench" %}

  Тут потребуются дополнительные шаги (надо сделать один раз):

    * Поставить `PuTTY`

      **windows**: [Инструкция](https://wiki.yandex-team.ru/security/ssh/windows/#generate-key-pair)

      **linux**: `sudo apt install putty`

      **macos**: `brew install putty`

    * Сконвертировать ваш приватный SSH ключ в `openssh` формат.

      **windows**: [Инструкция](https://wiki.yandex-team.ru/security/ssh/windows/#generate-key-pair)

      **linux/macos**: `puttygen ~/.ssh/id_rsa -O private-openssh -o ~/.ssh/id_rsa `

  ![Пример настроек в MySQL Workbench](_assets/mysql/mysql-workbench-settings.png)

  {% endcut %}

  {% cut "DataGrip" %}

  В `DataGrip` по умолчанию происходит подключение по паролю (пустой пароль - тоже пароль).
  Чтобы этого избежать, надо нажать правой кнопкой на поле с паролем и выбрать `Set empty`.

  ![Пример настроек в DataGrip](_assets/mysql/datagrip-settings.png)
  ![Пример настроек в DataGrip](_assets/mysql/datagrip-settings-2.png)
  ![Пример настроек в DataGrip](_assets/mysql/datagrip-settings-3.png)

  {% endcut %}

  {% cut "Консольный клиент" %}

  ![Пример настроек в DataGrip](_assets/mysql/console-settings.png)
  ![Пример настроек в DataGrip](_assets/mysql/console-settings-2.png)

  {% endcut %}

- PostgreSQL

  Настройки для подключения:

  Параметр | Значение
    :--- | :---
  `Host` | `<database>.pg-(ro/rw)-<cluster id>.query.consul`
  `Port` | **6432**
  `User` | **любой**
  `Password` | **любой**
  `SSH host` | `h2p.vertis.yandex.net`
  `SSH user` | **ваш логин на Стаффе**
  `SSH port` | 2222

  #### Примеры для разных IDE

  {% cut "DataGrip" %}

  ![Пример настроек в DataGrip](_assets/pg/datagrip-settings.png)
  ![Пример настроек в DataGrip](_assets/pg/datagrip-settings-2.png)
  ![Пример настроек в DataGrip](_assets/pg/datagrip-settings-3.png)

  {% endcut %}

  {% cut "Консольный клиент" %}

  ![Пример настроек в DataGrip](_assets/pg/console-settings.png)
  ![Пример настроек в DataGrip](_assets/pg/console-settings-2.png)

  {% endcut %}

{% endlist %}

