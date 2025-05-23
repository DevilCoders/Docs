# Введение

В документе приведены общие сведения о Почте для доменов (ПДД) и описан интерфейс взаимодействия сервисов Яндекс.Почта и Яндекс.Паспорт (далее по тексту — <q>Почта</q> и <q>Паспорт</q> соответственно).

Документ адресован разработчикам сервисов Почта и Паспорт.

## Соглашение об обозначениях

В документе описывается синтаксис запросов HTTP-GET. Для удобства восприятия пары _аргумент=значение_ отделены друг от друга символом & с дополнительными пробелами, как показано ниже.

```http://passport-internal.yandex.ru/passport 
 ? mode=mdapi & target=account & op=add
 & login=<user@domain>
 & (passwd=<string> | cryptpasswd=<hash>)
 & [enabled=<0|1>]
 & [weakpass=<0|1>]
 & [changepass=<0|1>]
 & [domain=<URI>]
```

Аргументы в запросах условно подразделяются на постоянные, имеющие в точности такое значение, как показано в описании синтаксиса, и переменные. Если запрос имеет большое количество аргументов, переменные аргументы выводятся с новой строки один под другим.

Ниже описано применение спецсимволов в синтаксисе запросов:

- в квадратные скобки заключаются необязательные аргументы (переменные и постоянные);
- в угловые скобки берутся условные значения переменных аргументов;
- в круглые скобки помещается список альтернативных аргументов (разделителем является вертикальная черта).

