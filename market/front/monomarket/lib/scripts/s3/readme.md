S3
==

Библиотека для работы с s3-стораджем.

Для авторизации требуется выставить переменные окружения

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`

###Посмотреть список бакетов
`yammy bin s3-buckets`

###Очистка устаревших файлов

`yammy bin s3-find-old <bucket> [days=360] [prefix] > old-files.out && yammy bin s3-delete <bucket> < old-files.out`, где `<bucket>` - это бакет, `[days=360]` - кол-во дней, ранее которых удалять, `[prefix]` - префикс.
