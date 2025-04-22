Сборка: `../gradlew build`

Запуск локально (по умолчанию используется профиль development) из папки infor-sce/packing2:
- из идеи:
  - Working directory: `$MODULE_WORKING_DIR$`
  - VM options: `-Denv.config=../properties/local/local.properties`
- в терминале:
  - `../gradlew bootRun -Denv.config=../properties/local/local.properties`
  - `java -jar -Denv.config=../properties/local/local.properties build/distributions/packing2.jar`

Открывается здесь: `http://localhost:8182/packing2`

### Новый флоу на реакте локально

Нужно запустить receiving с выключенной/включенной авторизацией,
иначе фронт не сможет залониться.

