# CKEditor 5 test

[Перечень команд, доступных в API](COMMANDS.md)


## Разработка

```bash
npm install && npm start
```

Поднимится webpack dev сервер на `http://localhost:9000/`


## dist
```bash
npm run dist
```
Соберётся архив `editor.zip` с содержимым
```
/editor
   |- editor.html
   |- editor.js
```

```bash
npm run unminified-dist
```
Соберется точно такой же архив, но с неминифицировнным js-файлом
