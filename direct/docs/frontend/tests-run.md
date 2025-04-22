
## Как запускать тесты { #run-tests }

```bash
# простой запуск
npm run hermione

# запуск веб-сервера гермионы
npm run hermione gui

# запуск в режиме записи
npm run hermione -- --save

# запуск веб-сервера в режиме записи
npm run hermione gui -- --save
# запуск в режиме чтения
npm run hermione -- --play

# запуск frozen набора тестов гермионы
npm run hermione -- --set frozen
# или
npm run hermione:frozen

# запуск functional набора тестов гермионы
npm run hermione -- --set functional

# выборочный запуск тестов, отфильтрованных регуляркой
npm run hermione -- --grep 'Название теста'

# запуск гермионы на локальном selenium-сервере
# На забудьте запустить селениум перед запуском тестов: npm run selenium
npm run hermione:standalone

# запуск гермионы на локальном selenium-сервере
# в случае падения тест запускается 3 раза
npm run hermione:standalone -- --grep 'Название теста' --retry 3

# запуск гермионы на локальном selenium-сервере
# уровень логирования debug
LOG_LEVEL=debug npm run hermione:standalone -- --grep 'Название теста'

# запуск гермионы в сендбоксе
npm run hermione:sandbox
# или для перезапуска упавших тестов
npm run hermione:sandbox-failed <taskId>
```
