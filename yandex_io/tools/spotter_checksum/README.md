## Утилита для подсчета чексуммы кастомного споттера

Для установки кастомного споттера через космодром нужно одним из полей указать
контрольную сумму файлов споттера. Подробности [здесь](https://wiki.yandex-team.ru/quasar/howto/#zagruzkakastomnogospottera).

### Использование

```
./spotter_checksum --dir /path/to/spotter/dir
```

В указанной папке должны лежать файлы споттера.

### Пример

```
$ mkdir spotter
$ tar -xzf alice-valid.tar.gz -C spotter
$ ls spotter
acoustic_model.nnet flags.txt           lda.mat             words.txt
$ ./spotter_checksum --dir ./spotter
2408432594
```