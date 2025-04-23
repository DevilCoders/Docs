
1. [Авторизуем пользователя](https://oauth.yandex.ru/authorize?response_type=token&client_id=2c2ca38a291e4ecc905f0f3787b5bac7), получаем OAuth токен.
Пользователь должен хотя бы раз зайти на вики (wiki.yandex.ru) чтобы Вики была создана!

2. Создаем структуру папок
```
./wiki2conf --mkdirs /home/neofelis/imports/org
```

2. правим config.yaml и распаковываем архив в /home/neofelis/imports/org/raw (должен быть файл /home/neofelis/imports/org/raw/entities.xml)
```yaml
org_id: ВПИСАТЬ DIR_ID
oauth: ВПИСАТЬ OAUTH
```

3. Парсим entities.xml
```
./devtools/confluence.sh --init "/home/neofelis/imports/org"
```

4. Заливаем данные
```
./devtools/confluence.sh --offset 0 --limit 1000 "/home/neofelis/imports/org"
```

5. Заливаем файлы
```
./devtools/confluence.sh --offset 0 --limit 1000 --attaches "/home/neofelis/imports/org"
```

6. Создаем spaces
```
./devtools/confluence.sh --offset 0 --limit 1000 --spaces "/home/neofelis/imports/org"
```

7. Вы прекрасны


# Особые опции

Выгрузть аттачи для спейса `do`, начиная с 109го и возобновляя с файла который называется Снимок23.PNG

```
 ./devtools/confluence.sh --offset 109  --limit 5000 --resume Снимок23.PNG --only do --attaches  "/home/neofelis/imports/docdoc"
```

Выгрузть страницы для спейса `do`, начиная с 109го; Если страница уже есть, не перезаливать (--skip)

```
 ./devtools/confluence.sh --offset 109 --skip --limit 5000 --only do "/home/neofelis/imports/docdoc"
```

## ОШИБКИ

```
AssertionError: {'debug_message': 'Organization(id=7111081,cloud_idNone) does not exist', 'error_code': 'FORCED_SYNC_REQUIRED', 'level': 'ERROR', 'message': ["You don't have permission to access the requested resource."]}
```
Пользователь должен хотя бы раз зайти на вики (wiki.yandex.ru) чтобы Вики была создана!




