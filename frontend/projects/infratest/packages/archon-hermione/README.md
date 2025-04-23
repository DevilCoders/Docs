# archon-hermione

Команда и компонент `hermione` для [archon-а](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/archon), 
реализующая запуск [hermione](https://www.npmjs.com/package/hermione) вместе с dev-сервером [kotik](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/archon-renderer-devserver-command). 
Если вам не нужен kotik при запуске hermione, не используйте эту команду.

Используется вместе с обязательными hermione-плагинами:
* [@yandex-int/url-decorator](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/url-decorator)
* [@yandex-int/hermione-base-url-changer](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/hermione-base-url-changer)

## Установка

```bash
$ npm install @yandex-int/archon-hermione --registry http://npm.yandex-team.ru
```

## Опции команды hermione

 * `--play` - запуск в режиме проигрывания дампов данных
 * `--create` - запуск в режиме создания дампов данных. Если дамп существует, то он не изменится
 * `--save` - запуск в режиме записи дампов данных. Если дамп существует, то он будет перезаписан
 * `все опции команды dev-сервера` - опции [kotik-а](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/archon-renderer-devserver-command)
  можно использовать только с префиксом реиспользуемых команд, например,
  `--kotik-` и `--renderer-`. Это необходимо, чтобы не перепутать, например, `--renderer-workers` и `--kotik-workers`. 
  Несколько аргументов предопределены специально для hermione, например: `--kotik-local=true`, `--kotik-public=true` и их нельзя менять.
 * `все опции утилиты hermione и её плагинов` - будут прокинуты в hermione без изменений.

Все доступные опции можно узнать с помощью команды:

`npx archon hermione --help`
