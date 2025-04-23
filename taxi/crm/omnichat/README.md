## Секреты

### Mac

Локально добавить в переменные окружения ( в файл .bash_profile)

```bash
export OMNICHAT_BACKEND_TVM_SECRET_KEY=`ya vault get version sec-01g3y78rpevq9xqvwsen7tw7sm -o client_secret`
export OMNICHAT_BACKEND_YDB_TOKEN=`ya vault get version sec-01g5hc8jx6wfvgcvkzxgy51kxz -o YDB_TOKEN`
```

### Linux
Идея не видит переменные в .bash_profile и .bashsc, поэтому нужно добавлять в .profile.
.profile выполняется только при старте Linux, поэтому, после редактирования файла, необходимо перезагрузить систему.

При этом, если в .profile написать команду вида,
```bash
export OMNICHAT_BACKEND_YDB_TOKEN=`ya vault ....'
```
то при запуске системы выйдет ошибка
```bash
command 'ya' not found
```

Поэтому, рекомендуется, в .profile вставить ключи
```bash
export OMNICHAT_BACKEND_TVM_SECRET_KEY=`TVM_SECRET_KEY из секретницы`
export OMNICHAT_BACKEND_YDB_TOKEN=`YDB_TOKEN из секретницы`
```

## Конфиги

Положить файлик config.yaml на машине разработчика (переделать из configs/config.local.yaml) по пути
```bash
/etc/yandex/taxi/crm/omnichat
```


## Генерация проекта

Сгенерировать проект для idea можно командой
```bash
ya ide idea --iml-in-project-root -l -r $HOME/projects/taxi/crm/omnichat $HOME/arcadia/taxi/crm/omnichat
```
