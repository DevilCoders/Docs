# Плагин JMF для IntelliJ IDEA

*Язык - Kotlin. Система сборки - Gradle*

## Настройка проекта
1. Предполагается, что уже установлены и настроены **arc** и утилита **ya**,
   а также смонтирована **arcadia**. В противном случае необходимо произвести
   базовую настройку инструментов согласно [инструкции](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)
2. В смонтированной Аркадии откройте каталог плагина
```bash
cd ~/arcadia/market/lilucrm/tools/idea/jmf_plugin # Предполагается, что исходные коды лежат в ~/arcadia
```
3. Сгенерируйте проект для IntelliJ IDEA при помощи **ya ide idea**, где *{local-path}* -
   произвольный путь до локального каталога под проект.
   Расшифровку флагов см. [здесь](https://docs.yandex-team.ru/ya-make/usage/ya_ide/idea)
```bash
ya ide idea -r {local-path} --with-content-root-modules
```
4. В IntelliJ IDEA откройте проект по пути указанном в *{local-path}* ранее
5. Импортируйте Gradle либо согласившись с подсказкой от IDE при открытии, либо
   явно вызвав `Import Gradle project` из контекстного меню файла `build.gradle`

## Разработка
В процессе разработки, для запуска IDEA со сразу же подключенным плагином, используйте
Gradle задачу `runIde` (для открытия окна Gradle можно воспользоваться пунктом основного
меню `View > Tool windows > Gradle`)

![](./docs/gradle_tasks.png)

Для отладки запустите задачу `runIde` в debug режиме, а если необходимо только собрать
плагин, используйте задачу `buildPlugin` (по умолчанию сборка происходит в каталог
`build/libs` проекта)

## Версии IntelliJ IDEA
Разрабатываемый плагин должен собираться под определенную версию IntelliJ Platform.
Целевую версию достаточно указать в `build.gradle` (см. рис. ниже). Номера версий и доп. информацию
можно найти [здесь](https://plugins.jetbrains.com/docs/intellij/build-number-ranges.html#intellij-platform-based-products-of-recent-ide-versions)

![](./docs/idea_version.png)

Этот же параметр влияет на версию IntelliJ IDEA запускаемой Gradle задачей `runIde`

## Справочная информация
- Оф. документация по [IntelliJ Platform SDK](https://plugins.jetbrains.com/docs/intellij/welcome.html)
- Оф. документация по [Kotlin](https://kotlinlang.org/docs/home.html)
