# Тесты (unit, e2e)

> Быстрые, простые, читаемые

## Общее

<a name="tests-5-0"></a><a name="5.0"></a>

- [5.0](#tests-5-0) В названии теста нужно описать какой результат ожидается, и, если эти необходимо, описать условия выполнения теста (ответить на вопрос `когда?` или `если?`).

  > Хорошо, когда не нужно анализировать код, когда достаточно прочитать человеческое описание, чтобы быстро понять тестируемый кейс.

  😟 Плохо:

  ```ts
    it('all good', () => { ... })
    it('all bad', () => { ... })
    it('same', () => { ... })
  ```

  😋 Хорошо:

  ```ts
    it('should return 😋 when menu has 🍉', () => { ... })
    it('should update refs when switching between children', () => { ... })
    it('should be able to query currently animating elements via :animating', () => { ... })
    it('should add bootstrapped module into platform modules list', () => { ... })
  ```

<a name="tests-5-1"></a><a name="5.1"></a>

- [5.1](#tests-5-1) Не тестируем внутренние детали реализации функции/модуля/класса

  > Тестирование внутренних деталей реализации делает тесты более хрупкими.
  > Тесты могут упасть при рефакторинге кода.
  > Тем самым создавая лишний "шум"

  😟 Плохо:

  ```ts
    function internalUtility() {
      const result = [];
      for (const value of numbers) {
        result.push({ value });
      }
      return result;
    }

    export function complexFunction() {
      const numbers = [1, 2, 3, ...];
      return internalUtility(numbers)
    }

    it('complexFunction ...', () => {
      const result = complexFunction()
      expect(result).toBe(...)
    })

    it('complexFunction calls internalUtility', () => {
      // somewhow spy on internalUtility
      const result = complexFunction()

      expect(internalUtility).toBeCalledWith([1, 2, 3, ...])
    })

    it('internalUtility ...', () => {
      const result = internalUtility()
      expect(result).toBe(...)
    })
  ```

  😋 Хорошо:

  ```ts
    function internalUtility() {
      const result = [];
      for (const value of numbers) {
        result.push({ value });
      }
      return result;
    }

    export function complexFunction() {
      const numbers = [1, 2, 3, ...];
      return internalUtility(numbers)
    }

     it('complexFunction ...', () => {
      const result = complexFunction()
      expect(result).toBe(...)
    })
  ```

  > Не экспортируем функцию **internalUtility** так как она не является частью публичного API
  >
  > Не тестируем ее так как тестирование основной функции покрывает наш кейс
  >
  > В дальнейшем мы можем по различным причинам избавиться от нее, например просто использовать map итд.
  > Главное что внешнее поведение остается таким же. И нам не нужно исправлять/удалять тесты которые не влияют на внешнее поведение кода

## e2e

<a name="tests-5-2"></a><a name="5.2"></a>

- [5.2](#tests-5-2) В качестве тестовых селекторов нужно использовать только привязку в специальному атрибуту `data-test-anchor`. Содержание должно быть максимально уникальным, чтобы с легкостью находить в коде и не было вложенностей в тестовых селекторах.

  > Почему? Тяжело понять длинный css селектор и его вложенность (в коде он выглядит не так). Когда меняешь название css свойства соверешенно не подозреваешь, что сломаешь при этом e2e тесты.

  😟 Плохо:

  ```ts
    courierNames: '.dashboard-couriers__table-row a.dashboard-couriers__courier-name-link',
  ```

  😋 Хорошо:

  ```ts
    courierNames: 'a[data-test-anchor="dashboard-courier-name-link"]',
  ```
