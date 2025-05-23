# deprecation

Пакет для плавного отказа от функциональности и удаления кода.

## Идея

У вас есть код, который хочется удалить.
Но вы не знаете когда именно он работает, например, это зависит от входящего запроса.
И поэтому хочется добиться того, что в реальных условиях этот код не вызывается.

Решение - разметить такой код через этот пакет.

```ts
import { Deprecation } from "@yandex-int/deprecation";
const myDeprecation = new Deprecation("DEPR-1", "My code is deprecated", "silent");

function foo() {
  myDeprecation.log();
  console.log("I'm deprecated");
}

function bar() {
  myDeprecation.log((msg) => console.log(msg));
  console.log("I'm also deprecated");
}
```

Сначала надо создать новый объект `Deprecation`.
Достаточно создать один такой объект, даже если нужно удалить код сразу в нескольких местах.

Тут видно три аргумента. Первый - id этого `deprecation`. Он нужен для точечного контроля через переменные окружения.
Удобно использовать id тикета из Трекера.

Второй аргумент это сообщение о том, как и почему этот код считается плохим.

Третий - уровень этого `deprecation`. Есть три уровня: `silent`, `verbose` и `throw`. Про них - ниже.

Затем его надо использовать перед тем кодом, который хочется удалить.
`deprecation` это объект, чтобы залоггировать срабатывание надо вызвать метод `log()`.
У него один опциональный аргумент, это логгер `(message: string) => void`

По умолчанию логгер пишет в `stderr`.

По умолчанию сообщения будут логгироваться не чаще, чем раз в минуту. Это нужно, чтобы ограничить количество логов.
Подробнее в разделе [Переменные окружения](#Переменные-окружения)

## Уровни и порядок удаления кода

Удаление кода пройдёт в 4 шага.

1. Добавление `deprecation` на уровне `silent`.
Для нового `deprecation` нужно придумать новый id, например завести новую задачу.
В таком виде поведение по умолчанию никак не меняется.
Можно при помощи переменой окружения `Y_DEPRECATION_VERBOSE` включить логгирование при попадании в этот код,
а при помощи `Y_DEPRECATION_THROW` - бросать исключение.
С её помощью можно изолированно собрать лог основной массу срабатываний, например, через прогон тестов.

2. После того, как основная масса кода найдена и вычищена при помощи переменных окружения, можно переключить
`deprecation` на уровень `verbose`. Теперь любое его выполнение будет логгировать свои id и сообщение.
В таком режиме можно смотреть на нагрузку в проде и вычищать все редкие кейсы, которые почему-то не попались вам в тестах.

3. Когда вы уверены, что больше нет процессов, которые затрагивают этот код, в нём можно бросать исключение.
Для этого можно переключиться на уровень `throw`. Теперь любое выполнение этого кода будет бросать исключение
с id и тем же сообщением. Если внезапно выяснилось, что такой сценарий что-то всё-таки ломает, а откатывать - неудобно,
можно поменять поведение через переменные окружения `Y_DEPRECATION_SILENT` или `Y_DEPRECATION_VERBOSE`.

4. Если стало ясно, что исключение никому не мешает, т.е. либо оно никогда не бросается,
либо все его ловят и как-то обрабатывают, то и целевой код никогда не выполняется, а значит его можно удалить.


## Caveats

Важно удалять только код "под deprecation", потому что иначе мы поменяем публичный API. 

Если вы хотите удалить метод, вы можете разметить его реализацию. Например так:
```ts
const obj = {
  f() {
    myDeprecation.log();
    console.log("I'm deprecated"); 
  }
};
```

При таком подходе после перехода на режим `throw` можно удалять вызов `console.log`, можно удалять `f` из тайпингов,
можно полностью заменить код метода на бросок исключения, но нельзя удалять само поле `f`,
иначе можно получить внезапный `undefined` в рантайме, по крайней мере без типизации.

Чтобы удалить метод целиком его надо заменить геттером, и вызывать `deprecation` в коде геттера, например так:

```ts
const obj = {
  get f() {
    myDeprecation.log();
    return () => { 
      console.log("I'm deprecated");
    }; 
  }
};
```

Корректно и делать так сразу, и делать последовательно в два этапа, "правильный" выбор зависит от вашего кейса.

Частично замену геттером реализует готовый враппер: `deprecation.wrapProperty(obj, "key")`.
Пока что он применим только к собственным свойствам. PRs are welcome.

## Переменные окружения

### `Y_DEPRECATION_SILENT`, `Y_DEPRECATION_VERBOSE` и `Y_DEPRECATION_THROW`

Эти переменные управляют поведением каждого конкретного `deprecation`.
Каждая из них принимает несколько id через запятую, `Y_DEPRECATION_SILENT="DEPR-1,DEPR-2"`

### `Y_DEPRECATION_DELAY_MS`

Эта переменная позволяет ограничить частоту логгирования сообщений - после записи в лог в течении
указанного времени сообщения логгироваться не будут.
Не влияет на исключения на уровне `throw`.
Применяется к каждому `deprecation` отдельно.
Значение по умолчанию - 60000, т.е. на чаще чем 1 сообщение в минуту.
Если установить 0 будет логгироваться каждое сообщение.