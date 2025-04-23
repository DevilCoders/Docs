# Как мы работаем с arc

## Flow

```
  arc checkout -b feature/WIKI-XXXX_description
  arc add .
  arc commit -am "Message"
  ya pr create --push
```

## Работа с внутренними инструментами

Чтобы не писать все 6 тысяч ручками сорцов, есть препроцессор
```
  yamake_prep ya.make.template
```
он раскрывает макросы и порождает файл в той же папке `ya.make.template -> ya.make` или `megainclude.inc.template -> megainclude.inc`
Поэтому после добавления нового питоновского файла или ресурса.

```
make ya
```

чтобы перегенерить все файлы. Если ругнется на то что yamake_prep не собран -

```
cd devtools/yamake_prep
ya make
```

## Работа с ветками

```
arc checkout -b
```

Аркадия не поддерживает merge by design. Поэтому надо научиться ребейзить. Щпаргалка

### Сквош ветки до одного коммита.

Зачем нужно - более эффективно делать ребейз и разрешать конфликты у ветки из одного коммита.

0. Получить хэш коммита от которого отведена текущая ветка:

```
arc fetch --all; arc pull trunk; arc reset --soft $(arc merge-base trunk HEAD);
arc commit
arc push -f  # Attention! затираем историю коммитов
```

### Ребейз на транк

```
arc fetch --all
arc rebase --onto arcadia/trunk
```


### Собрать миграции

```
  make make-migrations a=favourites_v2
```

Выведет миграцию в stdout
