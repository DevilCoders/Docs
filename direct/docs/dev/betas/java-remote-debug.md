# Дебаг удаленной java (на бете Директа)

## Задача

Хотим через локальную Idea дебажить java-процесс, запущенный на какой-то другой машине, а именно — на ppcdev, на бете Директа.

## Теория 

Для удаленного дебага:

- java-процесс должен быть запущен со специальными параметрами 
- в Idea надо сделать и запустить Run-конфигурацию специального типа — Remote 

На бетах Директа удаленная отладка нужна редко.
Обычно хорошо подходит запустить приложение локально и сделать, чтобы запросы к бете пробрасывались на локальное приложение (TODO: ссылка на раздел инструкции)


## Инструкция

### 1. Чекаутим локально тот же код, который собран на бете

TODO: коротко о спецэффектах от расхождения кода

### 2. Применяем на бете патч, чтобы java запускалась с нужными параметрами

Правка в файле `direct/perl/etc/quasi-make/Beta.pm`, внутри функции `_start_java_service` (проверь, что правишь нужную функцию!):

```diff
--- direct/perl/etc/quasi-make/Beta.pm  (index)
+++ direct/perl/etc/quasi-make/Beta.pm  (working tree)
@@ -1237,6 +1237,7 @@ sub _start_java_service {
         ($beta_settings->{java_agent_path} ? "-agentpath:$beta_settings->{java_agent_path}" : ()),
         ($classpath ? ('-cp' => "$classpath/*:") : ()), 
         (map { "-D$_" . '=' . $O{$_} } keys %O), 
+        ($name eq "intapi" ? "-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=127.0.0.100:"._beta_port() : ()),
         "-Xmx2g",
         "-Xms512m",
         "-XX:ParallelGCThreads=2",
```

В конструкции `$name eq "intapi"` вместо `intapi` можно подставить другое приложение: `web`, `api5`. Это сравнение делается на случай нескольких java-приложений на бете, чтобы они не пытались занять один и тот же порт для отладки.

### 3. Перезапускаем java-приложение на бете

Проверяем через `ps`, что в параметрах запуска есть `-agentlib` и так далее.

### 4. Создаем в Idea Run-конфигурацию Remote (если ее еще не было)

Меню `Run` → `Edit Configurations...` → `Add new configuration` (плюсик вверху слева),
выбираем тип `Remote`,
даем красивое имя (_удобно назвать "Remote Debug — Direct Beta"_),
больше ничего не меняем, сохраняем.

{% cut "Скриншоты процесса" %}

![alt text](_assets/java-remote-debug-01.png "Edit configurations")
![alt text](_assets/java-remote-debug-02.png "Add Remote configuration")
![alt text](_assets/java-remote-debug-03.png "Confirm")

{% endcut %}

<br/>

### 5. Запускаем ssh с пробросом портов

Локально:
```
ssh -N -L localhost:5005:127.0.0.100:<beta_num> ppcdev<N>.yandex.ru
```

### 6. Запускаем дебаг 

В Idea выбираем run-конфигурацию `Remote Debug — Direct Beta` и жмем Debug (зеленый жук справа).

### Готово

В Idea можно расставлять брекпойнты, открывать бету в браузере и смотреть отладчик. 

### После окончания отладки

Прибиваем ssh из п. 5.

## Проблемы и решения

### Ничего не работает

Проверь на бете ожидается ли коннект, одной из команд:

```
ss -nlp | grep 13605
telnet 127.0.0.100 13605
```

Если нет - проверь, правильно ли применён патч.

## Ссылки

- [Туториал от JetBrains](https://www.jetbrains.com/help/idea/tutorial-remote-debug.html)
- [Обсуждение на StackOverflow](https://stackoverflow.com/questions/21114066/attach-intellij-idea-debugger-to-a-running-java-process)
- [Создание и управление бетами](betas.md)

