## Check-flow-files

Прекомитный хук, который вызывается с помощью: 
`yarn run check-flow-files`

### Добавление в прекомитный хук.
Для добавления в прикомитный хук, нужно прописать в *precommit* 
- title - название хука
- command - команда вызова
- include - расширения файлов для отслеживания
- exclude - расширения файлов для игнорирования
- types - действия с файлами

*Пример*: 
```
"precommit": [
    ...
     {
        "title": "Check flow files",
        "command": "yarn run check-flow-files",
        "include": "\\.js\\.flow$|\\.ts$|\\.[jt]sx?$",
        "exclude": "\\.spec\\.ts$|\\.d\\.ts$",
        "types": [
          "changed",
          "created",
          "renamedto"
        ]
      }
    ],
```
