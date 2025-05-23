# ACYNC

Этот модуль содержит утилиты для асинхронного вызова.
* `async.ts` - функция `runAsync` для отложенного вызова в следующем тике.
* `executor.ts` - функция `executeIterator` для добавления задач в общую очередь.
* `helpers.ts` - функция `iterateTaskWithConstraints`, запускающая `executeIterator`.
* `iterator.ts` - набор итераторов.
* `task.ts` - основной интерфейс задач (функциональный аналог `Promise`).

## Task
Самая интересная часть модуля. Содержит всю логику задач.

**Важно:** отложенное выполнение задач осуществляется с помощью `setDefer`. Это значит, что работа осуществляется наравне с остальными событиями в рамках *MacroTaskQueue* JavaScript движка в отличие от *MicroTaskQueue* в случае `Promise`. Благодаря этому возможно более гармонично вписать таски в основную работу браузера, так как основные события создаваемые пользователем при использовании сайта имеют такой же приоритет, как наш код. (Если использовать `Promise`, их обработка будет вестись в *MicroTaskQueue*, которая имеет более высокий приоритет, чем основная очередь событий. Все микрозадачи завершаются до обработки каких-либо событий или рендеринга, или перехода к другой макрозадаче. Тем самым есть возможность существенно затормозить выполнения событий интерфейса сайта.)

`task` - минимальная единица выполнения. Создает задачу c выполняемой функцией типа `(reject, resolve) => void`.

После создания задачи в полученную функцию можно передавать следующие обработчики:
* `taskFork` - запускает выполнения задач.
* `taskMap` - функция для синхронной обработки полученных данных. Возвращает обработанный результат.
* `taskChain` - функция для асинхронной обработки полученных данных. Возвращает новую задачу.
* `taskRace` - аналог `Promise.race`. Выполняет все переданные задачи и возвращает результат первого удачного выполнения. Иначе возвращает массив ошибок.
* `taskAll` аналог `Promise.all`. Выполняет все переданные задачи и возвращает массив результатов. При возникновении ошибки останавливается и возвращает ошибку.
* `fromPromise` - создание задачи из `Promise`.
* `taskOf` - создает задачу возвращающую заданное значение.
