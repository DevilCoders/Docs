# Тест FillFeatures() и генерация входных данных
Цель - контроль добавления новых факторов, чтобы модели раньше времени не приходили на вход те, на которых она не обучалась.

### Запуск теста
`ya make -A`

### Добавление/обновление факторов в модели
Канонизация нового выхлопа - `ya make -AZ`
Версия i2t задана в константе CURRENT\_I2T\_VERSION и должна быть заменена при замене версии в продакшене.

### Обновление входных данных из метадока
1. Сдампить их из метадока
`./fill\_factors\_test DumpMetadocEntries --output-file metadoc\_json.txt  --server <server\_name> --index-prefix //home/images --index-state <index\_state>`
2. Залить в Sandbox
`ya upload --ttl=inf --backup <path>`
3. Обновить id ресурса в DATA в ya.make
`sbr://2095581299=input\_data`
4. Канонизировать тесты
