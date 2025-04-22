# Выкладка в тестинг и продакшн
```bash
arc co trunk
arc pull
# User ветка, с которой будет собираться релиз, должна оканчиваться на release-garden
arc co -b {version}-release-garden
# Поднимаем минорную версию и создаем тег
npm run release:minor
# Создаем pr на влитие новой версии в транк.
# Одной из задач в нем будет выкладка в тестинг (release-testing). После того как она выполнилась надо смержить pr
arc pr create --push --publish

# Ecли что-то пошло не так во время сборки, то можно поднять патч-версию и попробовать снова в том же pr
npm run release:patch
arc push

# Выложить текущий тестинг в продакшен
npm run deploy:production
```
