# Баобаб

Подробная документация на Баобаб есть на [wiki/баобаб](https://wiki.yandex-team.ru/search-interfaces/baobab/).

Для работы с Баобабом в React-компонентах используются библиотека [@yandex-int/react-baobab-logger](https://a.yandex-team.ru/arc_vcs/frontend/packages/react-baobab-logger).

## Стандартный процесс работы со счетчиками

1. Добавляем для компонента/блока узел в Баобаб-дерево
  - [React-компонент](../components/howto.md#8-Баобаб)
  - [React-фича](../quick-start.md#Шаг-1-Создать-корневой-компонент-фичи)
  - [блок конструктора](https://wiki.yandex-team.ru/search-interfaces/baobab/#razmetkacherezkonstruktor)
2. Пишем клиентский код, отправляющий логируемое Баобаб-событие
  - [React-код](../components/howto.md#8-Баобаб)
  - [i-bem реализация блока конструктора](https://wiki.yandex-team.ru/search-interfaces/baobab/#vyzovschetchikaizkoda)
3. Проверяем счетчики тулзой (росток/листик) с параметром `&exp_flags=validate_counters`
4. [Пишем hermione-тесты на счетчики](https://wiki.yandex-team.ru/search-interfaces/baobab/#testirovanie)
