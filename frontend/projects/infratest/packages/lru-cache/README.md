# Декоратор для пакета LRU

[LRU на npm](https://www.npmjs.com/package/lru-cache)

## Установка

```bash
npm install @yandex-int/si.ci.lru-cache
```

## Пример использования

```js
const { cached } = require('@yandex-int/si.ci.lru-cache');

// Опции для кэширования
const cacheOptions = {
  max: 10,
  maxAge: 3600000, // Один час
  id: 'users'
};

// Генератор ключей для кэша
const generateKey = (group) => `key_${group}`;

// Общее количество запросов совершённых на сервер
let count = 0;

// Функция, выполняющая запрос на поиск пользователя по группе и имени
async function fetchUsersByGroup (group) {
  count += 1;

  return `List of users by group "${group}"`;
}

// Инициализация системы кэширования
const getUsersByGroup = cached(fetchUsersByGroup, generateKey, cacheOptions);

// Выполняем запрос 3 раза и выводим результат
Promise.all([
  getUsersByGroup('group_1'),
  getUsersByGroup('group_1'),
  getUsersByGroup('group_1')
]).then((responses) => {
  responses.map((response) => console.log(response));

  console.log(count);
});

/*
 * Output:
 * User "Username_1" by group "group_1"
 * User "Username_1" by group "group_1"
 * User "Username_1" by group "group_1"
 *
 * 1
 */
```
