# Новый чарт

### C шаблоном {#with-template}

1. Создайте новый чарт в [ChartEditor](https://charts.yandex-team.ru/editor).
Выберите шаблон, который наиболее отвечает вашим потребностям.

2. Далее, нажмите "предпросмотр" и вы увидите результат работы скрипта.

### Без шаблонов и запросов API {#without-template}

1. Создайте новый чарт в [ChartEditor](https://charts.yandex-team.ru/editor). Укажите опцию
`без шаблона`. Для простой отрисовки чарта (графика) достаточно только заполнить таб `JavaScript'.

2. Редактируем таб `JavaScript'
```(js)
const preparedData = {
    graphs: [
        {
            data: [
                76400445,
                86400445,
                96672938
            ],
        },
    ],
    categories_ms: [
        1417392000000,
        1417478400000,
        1417564800000,
    ]
};

module.exports = preparedData;

```

В результате будет показана одна линия с тремя точками.

---

Изменяя параметры, код в табах вы добьётесь изменения чарта. Не забудьте его сохранить
и опубликовать. Об архитектуре, табах и их работе читайте подробнее в разделе [Архитектура](architecture.md);

## Отладка {#debug}

Для отладки кода включите консоль Javascript вашего браузера и при нажатии кнопки
`Предпросмотр` вся отладочная информация будет выводиться в консоли.

Для вывода дополнительной информации в нужном месте кода напишите:

```js
console.log(value);
```

В случае ошибок в коде вы увидите:

```js
Config:8
    subtitle: `Scale: ${scale}`,
    ^^^^^^^^

SyntaxError: Unexpected identifier
```

Из этого ответа хорошо видно, что ошибка произошла на табе `Config`, на 8 строчке.
