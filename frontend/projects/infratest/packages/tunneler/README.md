# tunneler
Плагин для поднятия туннеля

Необходим для работы [Templar](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/templar)
[плагина](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/templar-runner) для запуска gemini и hermione тестов в темпларе

## Установка

`npm install @yandex-int/tunneler`

## Выбор инстанса туннелера

Осуществляется на основе ключа для равномерного распределения нагрузки между между всеми инстансами. Если инстанс не отвечает, выбор инстанса
повторяется без неработающего. Ключ вычисляется следующим образом:
```
process.env.TUNNELER_HOST_ID || process.env.TUNNELER_USERNAME || имя пользователя в системе
```

Указать требуемый хост таннелера, в том числе не прописанный в конфиге, можно переменной окружения TUNNELER_HOST.
**Если указан TUNNELER_HOST, то хосты из конфига использоваться не будут**.

Для фильтрации датацентров инстансов таннелера можно использовать опцию instanceFilter или переменную окружения `tunneler_instance_filter`, в значение
которой нужно передавать строку для конструктора RegExp.

## Тестирование

Проверка синтаксиса с помощью eslint: `npm run lint`.

Запуск тестов: `npm test`.
