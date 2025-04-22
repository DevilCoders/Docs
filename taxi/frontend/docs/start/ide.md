# Настройки IDE

У нас наиболее широко используется 2 среды: WebStorm и VS Code. (скачать их можно так же из Self Service). Выбирай привычную.

{% note info %}

Часть сервисов разрабатываются на удалённых машинах.

{% endnote %}  

Существует два основных подхода в работе на удаленном сервере:
1. Работать прямо на сервере (с использованием плагина VSCode Remote)
2. Держать и изменять файлы локально и заливать их по SFTP при изменениях. Либо вариант, держать файлы локально и на удалённой машине, а синхронизировать лишь изменённые файлы.

1 вариант проще, т.к. вам не нужно следить за синхронизацией проекта, но есть риск потерять незапушенные файлы на удалённой машине, т.к. нет гарантий, что машинку не "вайпнут".

Так же переодически удалённые машинки недоступны из-за учений в ДЦ.

{% list tabs %}

- Visual Studio Code

    1. Окрыть VSCode
    2. Установить расширение [remote-ssh](vscode:extension/ms-vscode-remote.remote-ssh)
    3. В левом нижнем углу нажать на кнопку `Open Remote Window`
    4. Выбрать `Connect to Host` → `+ Add New SSH Host`
    5. Выбрать
    6. Enter `<your name>@{VM name}.yp-c.yandex.net` (например twin@twin.sas.yp-c.yandex.net)
    7. Подключение создано
    8. Снова клик по кнопке в левом нижнем углу → `Connect to Host` → Выбрать созданное подключение
    9. Соединение установлено

- WebStorm

    Для использования SFTP с WebStorm нужно научить JVM работать с IPv6.
    Для этого в конфиге `Help` → `Edit Custom VM Options (или Edit Custom Properties)` нужно добавить
    
    ```bash
    -Djava.net.preferIPv4Stack=false
    ```

  1. `Preferences` > `Tools` > `SSH Connections`
  2. Нажать `+` (Add)
  3. Выключаем галку (если включена) `Visible only for this project`
  4. `Host` - {your login}.{VM name}.yp-c.yandex.net
  5. `User Name` - ваш логин
  6. `Private key file` - `/Users/{your login}/.ssh/id_rsa`
  7. Проверяем подключение. Если ок, идём дальше
  8. `Preferences` > `Build, Execution, Deployment` > `Deployment`
  9. Нажать `+` (Add) > `SFTP`, Указываем любое имя
  10. Выключаем галку (если включена) `Visible only for this project`
  11. Выбираем `SSH Configuration` тот, что создали выше
  12. Указываем `Root Path` - `/home/{your login}`
  13. Переходим на вкладку и указываем `Deployment path` согласно директории где лежит проект. Учитывайте что Deployment path конкатенируется с Root Path. Например, `/www/myproject`

  {% cut "screens" %}

     ![](https://jing.yandex-team.ru/files/tumenbaev/connection.7a8d430.png)
     ![](https://jing.yandex-team.ru/files/tumenbaev/deploy1.c637065.png)
     ![](https://jing.yandex-team.ru/files/tumenbaev/deploy2.06e6105.png)

  {% endcut %}

{% endlist %}