# Что делать если у вас сломался delpoy

Такое иногда бывает, что у вас заваливаются тесты при деплое документации.

Обычно это происходит из-за синтаксических ошибок в `.md` файле. Рассмотрим варианты дебага таких проблем.

## Вариант 1

Лучшим вариантом будет deploy проекта через с вашей локальной машины через IDE или CLI. Для этого достаточно:
- запустить команду `ya make`

Если `ya make` показывает:

```
Build time: 3915.590ms

tar: Failed to set default locale
Ok
```

То все `Ok`.

Если же `ya make` показывает:
```
ERR  Asset not found:  in /design/dc/hld/peerings.md

Build time: 4443.625ms
Failed
```

То проект не собрался и можете увидеть ошибку `ERR  Asset not found:  in /design/dc/hld/peerings.md`

Соответственно устраняете ошибку и все

## Вариант 2. Все поломалось при deploy через WEB

Более сложный вариант для дебага - у вас не проши тесты при deploy через WEB-интерфейс.

**Как дебажить**

###  Шаг 1

Находим тесты в красном цвете. Нажимаем на циферку (см. пример)

![](_images/img_01.jpg)

###  Шаг 2

- Нажимаем на Links
- Переходим по ссылке `Task with patch`
-
![](_images/img_02.jpg)

## Шаг 3

Переходим в файл с `err`. Находим ошибку.

![](_images/img_03.jpg)

## Шаг 4

Переходим в файл

![](_images/img_04.jpg)

![](_images/img_05.jpg)

Фиксим

![](_images/img_06.jpg)

## Распространенные ошибки

**Пустая ссылка**

`[mylink]()` - такая запись вернет ошибку `ERR  Empty link`
