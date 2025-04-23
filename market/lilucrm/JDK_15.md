## Про что эта инструкция

Сейчас идет процесс перехода на Java 15. Эта инструкция для тех, кто уже работал на 11 версии и использовал скрипты
генерации `./bin/idea-local.sh` (если вы генерируете проект не так, самое время начать так делать)

## 12.04.2021

### Вы сгенерировали проект на новой версии скрипта, где указан флаг `-DJDK_VERSION=15` (12.04.2021)

Вы молодец! Теперь нужно синхронизировать состояние в IDEA:
1. Нужно добавить новую Java SDK в IDEA. Для этого нужно выполнить [инструкцию](./README.md) п.8.2
2. В настройках проекта (Linux: `Ctrl+Alt+Shift+S`) выбираете в качестве _Project SDK_ SDK добавленный в предыдущем пункте
3. _Project language level_ устанавливаете на 11 (т.к. пока что мы живем на Java 11)
4. Убираете галочку `Use '--release' option for cross-compilation` в _File | Settings | Build, Execution, Deployment | Compiler | Java Compiler_

На данном этапе приложения запускаются на Java 11, прод и тестинги живут на Java 11. Каждый отдельный проект может
начать собираться и тестироваться в CI на Java 15, добавив себя
[сюда](https://a.yandex-team.ru/arc/trunk/arcadia/autocheck/linux/jdk15_targets.inc). В частности, __operator-window__
уже собирается и тестируется под Java 15. Дальнейшие планы — начать использовать Java 15 в проде, не используя фичи
Java 15 в коде

## 20.04.2021

### Теперь хотите запускать приложение в тестингах/проде на Java 15

1. Замените include `market/lilucrm/package-include.json` в своем _package.json_ на 
   `market/lilucrm/package-include-without-jdk.json` и `market/lilucrm/package-include-jdk-15.json`
2. Если ваш package.json имеет ссылки на `build -> package`, то в _package.json_ в секцию `build -> package` рядом
   с `targets` добавьте секцию `flags` с содержимым `[{"name": "JDK_VERSION", "value": "15"}]`:
    ```json
    {
        "build": {
            "package": {
                "targets": [
                    "{package_root}"
                ],
                "flags": [
                    {
                        "name": "JDK_VERSION",
                        "value": "15"
                    }
                ]
            }
        }
    }
    ```

## 11.05.2021

### Начать использовать фичи Java 15 в коде

Нужно исключить ya модули из автосборки под платформу по умолчанию. Для этого делаете в месте, где происходит `RECURSE` в ваши модули условие
```
IF(JDK_VERSION > 14)
    RECURSE(
        newServiceExp
        ocrm
        b2bcrm
        operator-window
    )
ENDIF()
```

Модули, которые и дальше должны жить на дефолтной версии, остаются в `RECURSE` вне этого условия

Для облегчения проверки, что все действительно перестало собираться по дефолтную платформу, в модулях, которые вы хотите
перевести на Java 15, в `ya.make` добавьте `INCLUDE(${ARCADIA_ROOT}/market/lilucrm/ya.make.jdk15.inc)`

## 21.06.2021

### Начать использовать preview фичи Java 15 в коде

В своих `ya.make`, в которых генерируется startup script, нужно добавить jvm опцию `--enable-preview`. На уровне компиляции ya make уже все включено
