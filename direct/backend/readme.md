# Эксперементальный Бэкенд Директа

Тут происходит сборка прототипа бекенда Директа на Котлине.

## FAQ

### Q: При сборке в Idea вылетает ошибка `Kotlin: [Internal Error] java.lang.AssertionError: org.jetbrains.kotlinx.serialization.compiler.extensions.SerializationResolveExtension caused LinkageError`

В проекте используется плагин компилятора kotlinx-serialization версии 1.6.21 (как и версия котлина в Аркадии), но в новых версиях Idea плагин поддержки Kotlin был обратно несовместимо обновлен до 1.7.0. Временное решение - откатить Idea до 2021.3.3 и установить плагин [kotlin-plugin-213-1.6.21-release-334-IJ6777.52](https://plugins.jetbrains.com/files/6954/169248/kotlin-plugin-213-1.6.21-release-334-IJ6777.52.zip?updateId=169248&pluginId=6954&family=INTELLIJ).
