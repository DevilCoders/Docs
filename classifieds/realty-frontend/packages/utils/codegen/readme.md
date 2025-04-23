# Кодогенерация
Используем возможности библиотеки [hygen](https://www.hygen.io/).

### React
Находясь в директории, где необходимо сгенерировать компонент
```
npx codegen react component [name]
```
Для генерации компонента-контейнера
```
npx codegen react container [name]
```

### Project

Нужно находиться в корневой директории.

Для генерации нового проекта
(будет жить на нашем основном десктоп домене, но под своим pathname).
```
npx codegen project new
```

## Запуск из папки в IDE

### Webstorm
![webstorm exammple](./images/webstorm_example.png)

#### Настройка
![webstorm settings](./images/webstrom_settings.jpg)
Заходим в Settings -> Tools -> External tools, там Program: `npx`, Arguments: `codegen react component --name "$Prompt$" --path $FileDirRelativeToProjectRoot$`, в Working directory: `$ProjectFileDir$`.
Также можно назначить горячие клавиши на генераторы или находить через действия по `ctrl+shift+a`.

### VSCode

#### Настройка

В корне проекта в директории `.vscode` создаем `tasks.json`.

```json
// tasks.json
{
   "version": "2.0.0",
   "tasks": [
      {
         "label": "Codegen",
         "type": "shell",
         "command": "npx codegen react ${input:codegenType} --name ${input:componentName} --path ${relativeFileDirname}",
         "problemMatcher": []
      }
   ],
   "inputs": [
      {
         "id": "codegenType",
         "type": "pickString",
         "description": "Выберите тип генератора",
         "default": "component",
         "options": ["component", "container"]
      },
      {
         "id": "componentName",
         "type": "promptString",
         "description": "Название вашего компонента",
         "default": "Simple"
      }
   ]
}
```

#### Использование

Находясь в файле, в одной папке с которым нужно вызвать кодген вызываем меню команд (`⇧⌘P`) -> `Run Task` -> `Codegen`. Отвечаем на вопросы в открывшемся терминале.
