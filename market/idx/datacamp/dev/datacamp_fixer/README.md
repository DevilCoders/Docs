# datacamp-fixer

Приложение для ручного изменения офферов хранилища

Перед запуском необходимо создать таблицу с идентификаторами офферов в формате <business_id,shop_sku>. Например:
https://yql.yandex-team.ru/Operations/YU1_Z65OD-peGbraSjjTGEUD4TTjNrwWoogAV7WLWiw=

Если нужны несколько конкретных офферов, табличку можно создать с помощью INSERT INTO. Например:
https://yql.yandex-team.ru/Operations/YYGLTxJKfXPkrw0HMUtKhNII43mOBfzwwEXMZrTW42M=

Пример запуска:
```bash
./datacamp_fixer -c ../conf/production --ticket 42203 --yt-token-path yt-token --yt-source-offers-ids-path '//tmp/yql/evlyubimov/70cfbdcf-ada4364-4af58a8a-9268b5db'
Enter 'tvm_token': tvm_token из секретницы
```

Посмотреть на отправляемые данные можно в режиме DryRun (см. файл common.log):
```bash
./datacamp_fixer -c ../conf/production --ticket 42203 --yt-token-path yt-token --yt-source-offers-ids-path '//tmp/yql/evlyubimov/70cfbdcf-ada4364-4af58a8a-9268b5db' --dry-run
Enter 'tvm_token': tvm_token из секретницы
```

### Как запустить fixer в SandBox
```cd <arcadia_directory_path>/market/idx/datacamp/dev/datacamp_fixer```
#### 1.  Собрать архив
```ya package package.json```  

В текущей директории сгенерируется файл архива *.tar.gz .  
Посмотреть содержимое архива можно с помощью
```tar -ztvf <archive_name.tar.gz>```.
#### 3. Загрузить ресурс на sandbox
```ya upload <archive_name.tar.gz>```  

#### 4. Создать и запустить sandbox task
1. Используя [шаблон](https://sandbox.yandex-team.ru/template/datacamp_fixer/view), создать новый таск:
 Create new task
2. Указать в аргументрах командной строки {{cwd}}/conf/testing или {{cwd}}/conf/production
3. Указать в аргументах командной строки тикет
4. Указать в аргументах командной строки путь до таблицы
5. В Bundle resource подставить resource id, полученное на предыдущем шаге 

Готово

