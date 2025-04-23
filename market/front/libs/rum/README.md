Это какой-то старый не используемый код, скорее всего вам нужен https://a.yandex-team.ru/arc_vcs/frontend/packages/rum-counter


rum
===

Счётчик для Real User Measurement

Пример использования:
```javascript
blocks['timing'] = function(data) {
  return {
    block: 'timing',
      js: {
        vars: {
          '143': '1035.1034.153',
          '287': '213'
        },
        clckHost: data.clckHost // optional
      }
  }
}
```
