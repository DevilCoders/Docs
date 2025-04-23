sandbox
=======

Создаёт песочницу с плеером. Не имеет модификаторов, принимает только параметр player.

## Пример использования

```javascript
{
    block: 'sandbox',
    player: {
        playerId: 'youtube', // Id плеера
        html: '<iframe src="..."></iframe>', // HTML для вставки плеера
        params: { // Параметры, передаваемые в песочницу
            version: '1.0-162',
            beta: 1
        }
    }
}
```
