# Отправка парметров визита

Для отправки параметров визита сущесвуют несколько частых кейсов:
- в ответ на событие
- при изменении значения
- при первой отрисовке

## В ответ на событие

```typescript
const value = useSelector(duck.selector); // например возвращает 'hello' или 'bye'
const sendParams = useCounterSendParams<number>(
    (payload) => ['value', value, 'payload', payload],
    [value],
);

sendParams(3); // dispatch
/**               v
 *     ymSendParams(['value', 'hello', 'payload', 3])
 *     или
 *     ymSendParams(['value', 'bye', 'payload', 3])
 */
```

В `useCounterSendParams` передаем депсы (если они есть, на примере выше это `value`) и получаем функцию, которая принимает динамическое значение для отправки парамеров визита.
Хук принимает callback описывающий тело параметров визита (должен вернуть массив либо объект).

Пример с отрпавкой статических значений:

```typescript
const sendParams = useCounterSendParams<void>(() => ['pv', '1'], []);
sendParams(); // всегда отправляет ['pv', '1']
```

Динамические значения в `useCounterSendParams` предпочительнее передавать как `payload` нежели как `deps` так как в таком случае у React'a будет шанс максимально закешировать
обработчики событий:

```typescript
const const sendParams = useCounterSendParams<number>((payload) => ['id', payload], []); // не меняется
const handleChange = useCallback((value) => {
    sendParams(value);
}, [sendParams]); // не меняется

// где-то дальше по коду...
<Counter onChange={handleChange} />
```

## При изменении значения

Для реагирования на изменения состояния компонента можно использовать `useCounterParamsEffect`, в депсы передаем массив значений на изменения которых нужно отсылать парамеры визита.
В примере ниже мы хотим отсылать параметры визита при инициализации компонента, а также при изменении `counterId`:

```typescript
const inited = useSelector(duck.selector);
const counterId = useSelector(duck.selector);

const sendCounterId = useCounterSendParams<number>((payload) => ['counter', 'id', payload], []);
const sendPageView = useCounterSendParams<void>(() => ['pv', '1'], []);

useCounterParamsEffect(() => {
    if (inited) {
        sendPageView();
    }
}, [inited]);

useCounterParamsEffect(() => {
    sendCounterId(counterId);
}, [counterId]);
```

`useCounterParamsEffect` - это обертка над `useEffect`, она необходима так как `useEffect` требует от нас передачи в депсы _всех_ переменных, которые переданный ей callback использует
у себя в замыкании, даже если изменение одного депса повлечет за собой изменение второго, что в итоге приведет к двойной отправке параметров визита:

```typescript
const counterId = useSelector(duck.selector);
const [sentCounterIds, setSentCounterIds] = useState<number[]>([]);
const sendCounterId = useCounterSendParams<number>((payload) => ['counter', 'id', payload], []);

// 👎 useEffect вызовется дважды: при изменении counterId а также после отправки counterId когда мы изменим sentCounterIds
useEffect(() => {
    if (!sentCounterIds.includes(counterId)) {
        setSentCounterIds((ids) => [...ids, counterId]);
        sendCounterId(counterId);
    }
}, [counterId, sentCounterIds, sendCounterId, setSentCounterIds]);

// 👍 при измеенении counterId в callback попадает актуальный массив sentCounterIds и акуальный counterId
useCounterParamsEffect(() => {
    if (!sentCounterIds.includes(counterId)) {
        setSentCounterIds((ids) => [...ids, counterId]);
        sendCounterId(counterId);
    }
}, [counterId]);
```

## При первой отрисовке

```typescript
const sendPageView = useCounterSendParams<void>(() => ['pv', '1'], []);

useCounterSendParamsOnMount(() => {
    sendPageView();
});
```
