# Пользовательский CRM Маркета: Операционный CRM

* [Страница](https://wiki.yandex-team.ru/Market/Development/operator-window/) разработки на Wiki

## Настройка проекта

1. Выполнить общую [настройку](../README.md).

   Базовым сценарием рассматривается проект находящийся в `${HOME}/projects/lilucrm`.  
   Все ниже описанные относительные пути относительны каталога `${HOME}/projects/lilucrm/market/lilucrm`.

   <details>
      <summary>Альтернативные варианты</summary>
      Все они генерируют проект с флагом <a href="https://clubs.at.yandex-team.ru/arcadia/22285">--local</a>,
   что позволяет генерировать только указанные проекты, а все их зависимости компилировать и класть только jar файлы в 
   classpath

    * Для генерации более компактного проекта (в папку `${HOME}/projects/ow`), можно
      использовать `operator-window/bin/idea.sh` (обёртку вокруг `lilucrm/idea-local.sh`)
    * То же самое, что предыдущий пункт, только генерирует проект с именем `lilucrm`. Может быть нужно, например, если
      вы изначально генерировали проект через `lilucrm/bin/idea.sh`, но потом захотели генерировать более компактный
      проект, а настраивать конфигурации запуска заново не хочется
   </details>
1. Скопировать из [секретницы](https://yav.yandex-team.ru/secret/sec-01cwnp4gahdp79r4npweszhjvc)
   пароли в соответствующие конфигурационные файлы проекта (файлы создать при отсутствии). Значения забирать из наиболее
   свежей записи секретницы.
    * local.properties `operator-window/src/main/properties.d/local/local.properties`
    * tvm-local.json `operator-window/src/main/conf/local/tvm-local.json`

1. Настройка логирования. Скопировать с заменой `operator-window/src/main/conf/local/logback.template.xml`
   в `operator-window/src/main/conf/local/logback.xml`

1. Настроить локальную базу
    * Произвести установку postgresql согласно
      [инструкции](https://wiki.yandex-team.ru/market/development/operator-window/pgaas/#lokalnajabd)
    * В `operator-window/src/main/properties.d/local/local.properties` добавить/указать свойства подключения
      ```
      sql.username=lilucrm
      sql.password=your_secret_password
      sql.jdbc.url=jdbc:postgresql://localhost:5432/your_db_name?currentSchema=${sql.schema}&${sql.connect.opts}
      sql.jdbc.master.url=jdbc:postgresql://localhost:5432/your_db_name
      sql.jdbc.readonly.url=jdbc:postgresql://localhost:5432/your_db_name
      sql.schema=your_schema_name
      ```

1. Установить и настроить nginx согласно
   [инструкции](https://wiki.yandex-team.ru/Market/Development/operator-window/development-environment/#lokalnyjjnginx)

1. Настраиваем запуск приложения из idea

    * Скопировать `operator-window/idea_run_configuration.xml` в подпапку
      `${HOME}/projects/lilucrm/.idea/runConfigurations` (каталог `runConfigurations` создать при отсутствии).

      <details>
          <summary>Альтернативный вариант</summary>
          В случае генерации проекта через `operator-window/bin/idea.sh` (в папку `${HOME}/projects/ow`),
          для этого заготовлен скрипт `operator-window/bin/copy-idea-run-configuration.sh`.
      </details>

    * Прописать `LILUCRM_STAFF_OAUTH_TOKEN`
        * В меню _Run->Edit Configurations..._ в разделе _Application_ выбираем operator-window
        * В поле _Enviroment variables_ заменяем `${YT_TOKEN}` на свой yt token (который обычно лежит
          здесь `~/.yt/token`)

   **Важно:** Далее базовым сценарием запуска приложения является старт проекта через idea - меню _Run->Run->
   operator-window_ и его shortcut'ы

   <details>
      <summary>Альтернативный вариант (полностью ручная настройка)</summary>

    * В меню _Run->Edit Configurations..._ нажимаем '+' в левом верхнем углу
    * В выпавшем списке выбираем _Application_
    * В поле _Name_ указываем *operator-window*
    * В поле _Main class_ указываем `ru.yandex.market.crm.operatorwindow.Server`
    * В поле _VM Options_ добавляем (к уже имеющимся там `-Djava.library.path` и `-Djna.library.path` - обе с одинаковым
      значением, по умолчанию: `${HOME}/projects/lilucrm/dlls`, где `${HOME}` надо заменить на свою домашнюю директорию,
      а вместо `lilucrm` может быть `ow`)
        * `-Djava.net.preferIPv6Addresses=true`
        * `-Duser.timezone=Europe/Moscow`
        * `-Dlog.dir=log`
        * `-Dlogback.statusListenerClass=ch.qos.logback.core.status.OnConsoleStatusListener`
    * В поле _Working directory_ указываем `$MODULE_WORKING_DIR$`
    * В поле _Enviroment variables_ указываем
        * `PROPERTIES_DIR=${HOME}/arcadia/market/lilucrm/operator-window/src/main/properties.d/`, где `${HOME}` надо
          заменить на свою домашнюю директорию
        * `LILUCRM_STAFF_OAUTH_TOKEN=${YT_TOKEN}`, где `${YT_TOKEN}` надо заменить на свой yt token (который обычно
          лежит здесь `~/.yt/token`)
    * В поле _Use classpath of module_ указываем *operator-window*
   </details>

При ошибке компиляции _(возможна на IDEA старше 2020.3)_ и сообщении:
`You aren't using a compiler supported by lombok, so lombok will not work and has been disabled.` можно ознакомиться с [ответом на github](https://github.com/mplushnikov/lombok-intellij-plugin/issues/952#issuecomment-741821327).

1. Настройка работы локального web-интерфейса и компиляции JS.

   Базовый вариант (рекомендован фронтами) - webpack dev server (serve) - произвести настройку по
   инструкции [readme.md](webapp/readme.md)

   **Важно:** Далее базовым сценарием запуска web-интерфейса является запуск
   скриптом `operator-window/bin/serve-local.sh`

   <details>
      <summary>Альтернативный вариант (только если понимаешь последствия) - webpack watch</summary>

    * Настроить nginx - в конфиге `/etc/nginx/sites-available/operator-window` заменить секцию `location /` на:
       ```
       add_header Strict-Transport-Security "max-age=0;";
       proxy_set_header Host $host; # чтобы не ломалось определение паспорта по хосту
       proxy_pass http://localhost:34840/;
       ```
    * запуск через скрипт `operator-window/bin/watch.sh` (`watch-ow.sh` если проект генерировался с помощью
      `operator-window/bin/idea.sh`).  
      **Важно:** чтобы приложение подхватило эту сборку надо чтобы пропертя `http.webapp.dir` была
      пустой: `http.webapp.dir=`

1. Добавить себя в админы,
   руководствуясь [статьей](https://wiki.yandex-team.ru/Market/Development/operator-window/development-environment/#dobavleniesebjavadministratorynachistojjbd)

1. Все готово. Для локального старта стенда используются
   * старт бека проекта через idea - меню _Run->Run->operator-window_ и его shortcut'ы
   * старт web-интерфейса `operator-window/bin/serve-local.sh`

## Локальный запуск из консоли

### Linux
Если вы пользуетесь линуксом и у вас все хорошо, то можно запустить приложение без idea с помощью `bin/run.sh`

### Mac
Если вам повезло меньше и у вас мак, то необходимо установить `coreutils` & `gnu-tar` с помощью `brew`

```sh
brew install coreutils gnu-tar
```

Затем добавить симлинки на установленные команды `greadlink` как  `readlink` и `gtar` как `tar` в `$PATH`

```sh
cd ~/bin
ln -s $(which greadlink) readlink
ln -s $(which gtar) tar
```

Потом понять где у вас находится 8ая java и положить симлинк на ее домашнюю директорию в `/usr/local` как `java8`

```sh
cd /usr/local
sudo ln -s /Library/Java/JavaVirtualMachines/jdk1.8.0_162.jdk/Contents/Home java8
```

## Логгирование времени работы служебных команд
Чтобы это заработало надо заменить `~/bin/ya` из пункта 5 [выше](../README.md) на симлинку на `~/arcadia/market/lilucrm/operator-window/bin/ya-logged`:
```sh
cd ~/arcadia/market/lilucrm/operator-window
rm ~/bin/ya
ln -sr bin/ya-logged ~/bin/ya
```
После этого в папке `~/.ya/logs/timings` начнут писаться логи вида `ya.${DATE}.tsk?v` `ya.2018-12-17.tsv` (и `.tskv`). Набор и порядок колонок:

* `timestamp` - число секунд с epoch (00:00 1 января 1970 по UTC)
* `date_time` - время запуска команды по UTC (ISO 8601)
* `duration_s` - время выполнения команды в секундах
* `args` - массив аргементов, переданных в `ya`. Все параметры в кавычках с экранированными спец символами, через
  запятую. Пример: `['tool', 'hg', 'st', '--', 'test\tqwe']`
* `pwd` - переменная окружения `PWD`

**NOTE:** Если Аркадия лежит не в `~/arcadia`, то достаточно дописать в `~/.profile` экспортирование переменной окружения `ARCADIA_HOME`:
```sh
export ARCADIA_HOME="$HOME/path/to/arcadia"
```
