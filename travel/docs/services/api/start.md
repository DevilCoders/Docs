---
title: Как начать работать с Travel-API
rank: 20
---

## Как начать работать с Travel-API

### Используемые в доке переменные окружения
`$ARCADIA` - путь до корня Аркадии. Например ~/prog/arcadia (или ~/workspace/arcadia)

`$IDEA_PROJECTS` - путь до директории, где хранятся idea проекты. Например ~/prog/idea

`$IDEA_PROJECTS_ABSOLUTE` - то же что и выше, но путь абсолютный. Например /Users/zeliboba/prog/idea


### Подготовка окружения

1. Собираем JDK нак написано в [Документации по сборке Java в Аркадии](https://docs.yandex-team.ru/ya-make/manual/java/)
Не забыть указать правильную версию JDK=11, пример:
```
cd $ARCADIA/jdk
ya make -DJDK_VERSION=11
mkdir ~/jdk && tar xf jdk11.tar -C ~/jdk
```

2. Получаем yt токен [как получить читаем тут](https://yt.yandex-team.ru/docs/quickstart#how-to-get-oauth-token) и кладем в `~.yt/token` - пригодится для сборки с использованием yt кэша
   - `mkdir -p ~/.yt ; chmod 700 ~/.yt ; echo 'ваш_полученный_токен' > ~/.yt/token ; chmod 400 ~/.yt/token`
3. Получаем [yp токен](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=f8446f826a6f4fd581bf0636849fdcd7) и кладем в `~.yp/token` - нужен для работы Yp service discovery

### Проект для Idea

1. Ставим Idea Ultimate
  - [скачать](https://www.jetbrains.com/idea/download)
  - либо через Self Service на MacOsx
2. Ставим плагины:
   - `lombok` (через стандартный поиск, см. ссылку в п.3; забандлен в Yandex сборку Idea которая ставится через Self Service)
   - `arcadia plugin` (через поиск, но из нашего репозитория; [инструкция](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/intellij/#как-установить-плагин-1))
3. Включаем `annotations processing` (см. https://wiki.yandex-team.ru/disk/java/faq/#nastraivaemideadljarabotyslombok)
4. Генерируем Idea проект по исходникам:
	```
	cd $ARCADIA/travel

	ya ide idea -k -r $IDEA_PROJECTS/travel_api -l api

	...
	Ok
    Info: Successfully generated idea project: /home/alexcrush/prog/idea/travel_api
    Info: Devtools IntelliJ plugin (Latest stable IDEA is required): https://a.yandex-team.ru/arc/trunk/arcadia/devtools/intellij/README.md
    Info: Codestyle config: /home/alexcrush/.ya/tools/v4/441758406/intellij-codestyle.jar. You can import this file with "File -> Manage IDE Settings -> Import settings..." command. After this choose "yandex-arcadia" in code style settings (Preferences -> Editor -> Code Style).
	```
    **Внимание!** этот пункт возможно придется выполнить больше одного раза. Ибо может падать с ошибкой.

5. Выполнить настройку code style-а по описанию из блока **Info: Codestyle config** в выводе предыдущего пункта
6. Настраиваем JDK указывая путь до JDK собранной в "Подготовка окружения".

### Запуск

* Запускать надо `travel/api/src/main/java/ru/yandex/travel/api/Application.java`.
* В параметрах запуска (в VM Options) надо указать список окружений: `-Dspring.profiles.active=dev,local`
* В папке проекта (`$IDEA_PROJECTS/` в примере выше) создать файл `application-local.yml`, и все локальные настройки делать в нём.

Теперь можно проверить что все работает: `http://localhost:8080/swagger-ui.html`!

P.S.: В логах могут быть ошибки про то что YpNameResolver что то там не зарезолвил. Это не страшно. Так и задумано.

#### На случай проблем:
- проверить опции запуска: `-Djava.library.path=$IDEA_PROJECTS_ABSOLUTE/travel_api/dlls` (должны генерирвоаться автоматом)
- Если при сборке возникает проблема `You aren't using a compiler supported by lombok, so lombok will not work and has been disabled`, есть workaround: в `File | Settings | Build, Execution, Deployment | Compiler | Build process VM options`  добавить `-Djps.track.ap.dependencies=false`
- Иногда при сборке проекта возникает проблема сборки библиотека `partner_parsers` (отельная библиотека клиентов и парсеров). При этом выводится длинный стектрейс от `lombok` похожий на
```
------- [JV] {debug, FAILED} $(B)/travel/hotels/lib/java/partner_parsers/java-partner_parsers.jar
command /Users/mbobrov/.ya/tools/v4/1752940792/python /Users/mbobrov/arc/arcadia/build/scripts/with_pathsep_resolve.py /Users/mbobrov/.ya/tools/v4/1752940792/python /Users/mbobrov/arc/arcadia/build/scripts/run_javac.py --sources-list /Users/mbobrov/.ya/build/build_root/e3b7/001082/travel/hotels/lib/java/partner_parsers/misc/bf.txt /Users/mbobrov/.ya/tools/v4/1323882764/bin/javac @/Users/mbobrov/.ya/build/build_root/e3b7/001082/travel/hotels/lib/java/partner_parsers/misc/bf.txt -classpath /Users/mbobrov/.ya/build/build_root/e3b7/001082/bfg.jar -Xpkginfo:always -processor lombok.launch.AnnotationProcessorHider$AnnotationProcessor -d /Users/mbobrov/.ya/build/build_root/e3b7/001082/travel/hotels/lib/java/partner_parsers/cls -g -encoding UTF-8 failed with exit code 3 in /Users/mbobrov/.ya/build/build_root/e3b7/001082


The system is out of resources.
Consult the following stack trace for details.
java.lang.StackOverflowError
	at jdk.compiler/com.sun.tools.javac.code.Symbol$ClassSymbol.complete(Symbol.java:1326)
	at jdk.compiler/com.sun.tools.javac.code.Symbol$ClassSymbol.members(Symbol.java:1264)
	at jdk.compiler/com.sun.tools.javac.comp.Resolve.findField(Resolve.java:1424)
	at jdk.compiler/com.sun.tools.javac.comp.Resolve.findField(Resolve.java:1432)
	at jdk.compiler/com.sun.tools.javac.comp.Resolve.findVar(Resolve.java:1482)
	at jdk.compiler/com.sun.tools.javac.comp.Resolve.findIdentInternal(Resolve.java:2349)
	at jdk.compiler/com.sun.tools.javac.comp.Resolve.findIdent(Resolve.java:2341)
	at jdk.compiler/com.sun.tools.javac.comp.Resolve.resolveIdent(Resolve.java:2602)
	at jdk.compiler/com.sun.tools.javac.comp.Attr.visitIdent(Attr.java:3488)
	at jdk.compiler/com.sun.tools.javac.tree.JCTree$JCIdent.accept(JCTree.java:2248)
	at jdk.compiler/com.sun.tools.javac.comp.Attr.attribTree(Attr.java:655)
	at jdk.compiler/com.sun.tools.javac.comp.Attr.visitSelect(Attr.java:3573)
	at jdk.compiler/com.sun.tools.javac.tree.JCTree$JCFieldAccess.accept(JCTree.java:2114)
	at jdk.compiler/com.sun.tools.javac.comp.ArgumentAttr.visitTree(ArgumentAttr.java:207)
	at jdk.compiler/com.sun.tools.javac.tree.JCTree$Visitor.visitSelect(JCTree.java:3101)
	at jdk.compiler/com.sun.tools.javac.tree.JCTree$JCFieldAccess.accept(JCTree.java:2114)
	at jdk.compiler/com.sun.tools.javac.comp.ArgumentAttr.attribArg(ArgumentAttr.java:197)
	at jdk.compiler/com.sun.tools.javac.comp.Attr.attribTree(Attr.java:653)
	at jdk.compiler/com.sun.tools.javac.comp.Attr.attribArgs(Attr.java:751)
	at jdk.compiler/com.sun.tools.javac.comp.Attr.visitApply(Attr.java:1997)
	at jdk.compiler/com.sun.tools.javac.tree.JCTree$JCMethodInvocation.accept(JCTree.java:1634)
	...
```
В таком случае необходимо перейти прямиком в папка `$ARCADIA/travel/hotels/lib/java/partner_parsers` и в ней запускать `ya make` пока не соберется jar-файл с библиотекой

- ранее не настроенная IDEA может не понять, что проект на java11. Поправить можно через `⌘ ;` `Project Structure -> Project`, выбрать аркадийный jdk и выставить Project language level = 11. JDK можно найти командой ```ya tool java11 --print-path```

- Travel API Скорее всего не запустится, если не подключить руками собранные dll-ки в `⌘ ;` `Project Structure -> Libraries -> + -> Java`. В корне проекта есть папка dlls (~/IdeaProjects/travel_orders/dlls если собиралось по этой инструкции) - подключить её. ![projlib](https://jing.yandex-team.ru/files/mikhailche/2020-11-26_15-41-18.png)

- Конфигурации spring boot скорее всего не будут подключены к проекту автоматически. Заставить IDE понимать, что ты работаешь с Spring проектом можно либо через подсказки самой IDEA (она периодически говорит, что нашла непривязанные конфигурации), либо руками через `⌘ ;` `Project Structure -> Modules` ПКМ по модулю `Add -> Spring`. Дальше должно произойти автоопределение конфигураций (профилей).

- Lombok не всегда может подменять исходники на ходу. Если после изменения какого-нибудь класса с аннотациями от `lombok` получаем `java: cannot find symbol` при использовании - нужно просто перестроить весь проект через Build -> Rebuild project.

- Если возникает ошибка при запуске приложения:
    ```
    PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target
    ```
    В таком случае необходимо установить и использовать [аркадийную jdk](https://wiki.yandex-team.ru/yatool/java/#prerequisitesustanovkaarkadijjnojjjdk) (рекомендуемый способ) или выполнить [инструкцию](https://wiki.yandex-team.ru/security/ssl/sslclientfix/#vjava).
