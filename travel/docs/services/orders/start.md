---
title: Как начать работать с оркестратором
rank: 10
---

### Как начать работать с оркестратором

1. Ставим Idea Ultimate - [скачать](https://www.jetbrains.com/idea/download/#section=mac)
2. Поставить плагины: `lombok` (через стандартный поиск, см. ссылку в п.3), `arcadia plugin` (через поиск, но из нашего репозитория; [инструкция](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/intellij/#как-установить-плагин-1))
3. Включить `annotations processing` (см. https://wiki.yandex-team.ru/disk/java/faq/#nastraivaemideadljarabotyslombok)
4. Генерируем Idea проект по исходникам:
	```
	# mbobrov at mbobrov-osx in ~ [13:47:49]
	→ cd ~/arc/arcadia/travel

	# mbobrov at mbobrov-osx in ~/arc/arcadia/travel [13:47:54]
	→ ya ide idea -k -r ~/IdeaProjects/travel_orders -l orders -l api
	|71.7%| [SB] {RESULT} $(B)/contrib/java/org/jboss/spec/javax/transaction/jboss-transaction-api_1.2_spec/1.1.1.Final/jboss-transaction-api_1.2_spec-1.1.1.Final-sources.jar +1 more / Ok
	Info: Successfully generated idea project: /Users/mbobrov/IdeaProjects/travel_orders
	Info: Devtools IntelliJ plugin (Latest stable IDEA is required): https://a.yandex-team.ru/arc/trunk/arcadia/devtools/intellij/README.md
	Info: Codestyle config: /Users/mbobrov/.ya/tools/v4/441758406/intellij-codestyle.jar. You can import this file with "File -> Manage IDE Settings -> Import settings..." command. After this choose "yandex-arcadia" in code style settings (Preferences -> Editor -> Code Style).

	# mbobrov at mbobrov-osx in ~/arc/arcadia/travel [13:48:21]
	```
	(импортируем вместе с модулем API, т.к. он тоже позже потребуется, позже по аналогии можно будет через -l добавлять зависимые модули не как библиотеки, а как исходники)
5. Выполнить настройку code style-а по описанию из блока **Info: Codestyle config** в выводе предыдущего пункта
6. Прогон определённых тестов: `TrainOrderFlowTests` (находим класс через `Ctrl+Shift+N`) + кнопки запуска (все тесты целиком обычно проще и эффективнее прогонять через ya make -tt ./orders/app)
7. Запуск через Run. Если конфига нет, то необходимо создать:
    1. Add new configuration > Spring boot
    2. Main class: ru.yandex.travel.orders.OrdersApplication
    3. Spring boot > Active profiles: dev,local
    4. Если кнопка Run все равно серая, надо рестартнуть идею


#### На случай проблем:
- проверить опции запуска: `-Djava.library.path=/Users/mbobrov/IdeaProjects/ya-travel/dlls` (должны генерироваться автоматом)
- для запуска всего сервиса нужно отдельно настраивать профили окружения: `-Dspring.profiles.active=dev,local`
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
В таком случае необходимо перейти прямиком в папка `$A/travel/hotels/lib/java/partner_parsers` и в ней запускать `ya make` пока не соберется jar-файл с библиотекой

- ранее не настроенная IDEA может не понять, что проект на java11. Поправить можно через `⌘ ;` `Project Structure -> Project`, выбрать аркадийный jdk и выставить Project language level = 11. JDK можно найти командой ```ya tool java11 --print-path```

- Travel API Скорее всего не запустится, если не подключить руками собранные dll-ки в `⌘ ;` `Project Structure -> Libraries -> + -> Java`. В корне проекта есть папка dlls (~/IdeaProjects/travel_orders/dlls если собиралось по этой инструкции) - подключить её. ![projlib](https://jing.yandex-team.ru/files/mikhailche/2020-11-26_15-41-18.png)

- Конфигурации spring boot скорее всего не будут подключены к проекту автоматически. Заставить IDE понимать, что ты работаешь с Spring проектом можно либо через подсказки самой IDEA (она периодически говорит, что нашла непривязанные конфигурации), либо руками через `⌘ ;` `Project Structure -> Modules` ПКМ по модулю `Add -> Spring`. Дальше должно произойти автоопределение конфигураций (профилей).

- Lombok не всегда может подменять исходники на ходу. Если после изменения какого-нибудь класса с аннотациями от `lombok` получаем `java: cannot find symbol` при использовании - нужно просто перестроить весь проект через Build -> Rebuild project

#### Добавление исходников в проект
Если нужно, чтобы какой-то модуль был подключен не как библиотека, а как исходники, то можно перегенерить IDEA-проект поверх имеющегося. Например, добавляем `workflow`
```
ya ide idea -k -r ~/IdeaProjects/travel_orders -l orders -l api -l library/java/workflow
```
При этом остальные настройки проекта не сбрасываются (конфигурации запуска и т.п.). 
Известна одна проблема: при перегенерации слетают привязки dlls в Libraries, которые нужно привязать руками 
