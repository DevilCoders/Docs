### Для чего

Утилита предназначена для быстрой проверки фида и всех офферов в фиде.
Выдает список ошибок с позициями в исходном файле.

### Как собрать

Утилита собирается как обычно с помощью `ya make`:

```commandline
> ya make -r 
```

### Как использовать

```commandline
> ./feed_checker <путь_к_фиду> <url_источника> <тип_фида>
```

`<путь_к_фиду>` - имя файла фида или url

`<url_источника>` - адрес сайта, офферы с которого представлены в фиде

`<тип_фида>` - тип фида: `doctors` или `education`

### Пример запуска

```commandline
> ./feed_checker doctors_s1.xml klinikabudzdorov.ru doctors 

> ./feed_checker https://alcomed.ru/goods_yml_new.xml alcomed.ru doctors
```

