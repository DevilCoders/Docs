# i-utils__web-api-errors #

Утилиты, помогающие преобразовывать объекты ошибок из java-api Директа в тексты ошибок для отображения в интерфейсе

## makeErrorMapper ##

makeErrorMapper - функция, принимающая описание возможных ошибок (пути в объекте и коды ошибок) и способ их преобразования и возвращающая функцию-маппер, которая принимает любую опиcанную ошибку и возвращает соответствующее сообщение.  

Например, предположим, мы сохраняем объект и имеем следующую ошибку:
```
    var errors = [
		{
			path: 'description',
	   		code: 'StringDefectIds.LENGTH_CANNOT_BE_MORE_THAN_MAX',
			params: {
				maxLength: 250
			}
		}
	]
```
которая соответствует объекту
```
	var obj ={
		name: 'объект 1',
		description: 'очень-очень-...-очень длинное описание'
	}
```
и хотим, получив ее, где-то в интерфейсе написать `Объект "объект 1": поле "описание" не может иметь длину больше 250 символов.`.  
Для всех остальных ошибок мы хотим в интерфейсе писать "умолчательное" сообщение `Не удалось сохранить объект`  

Без применения `makeErrorMapper` это можно сделать следующим образом:

```
	function mapError(obj, err) {
		if (err.path === 'description' && err.code === 'StringDefectIds.LENGTH_CANNOT_BE_MORE_THAN_MAX') {
			return 'Объект "' + obj.name + '": поле "описание" не может иметь длину больше ' + err.params.maxLength + ' символов'
		} else {
			return 'Не удалось сохранить объект'
		}
	}
	
	var messages = errors.map(function(err) { return mapError(obj, err) })
```

С `makeErrorMapper` реализацию будет следующей:

```
	var mapError = u['web-api-errors'].makeErrorMapper(function() {
		return [
			{
				path: ['description'],
				codes: [
					{
						code: 'StringDefectIds.LENGTH_CANNOT_BE_MORE_THAN_MAX',
						message: function(obj, err) {
							return 'Объект "' + obj.name + '": поле "описание" не может иметь длину больше ' + err.params.maxLength
						}
					}
				]
			}
		]
	}, function() {
		return 'Не удалось сохранить объект'
	})
	
	var messages = errors.map(function(err) { return mapError(obj, err) })
```

Добавим к возможным ошибкам еще одну:

```
	var errors = [
		{
			path: 'description',
	   		code: 'StringDefectIds.LENGTH_CANNOT_BE_MORE_THAN_MAX',
			params: {
				maxLength: 250
			}
		},
		{
			path: 'items[1].name',
			code: 'StringDefectIds.LENGTH_CANNOT_BE_MORE_THAN_MAX',
			params: {
				maxLength: 5
			}
		}
	]
```
Новый объект выглядит так:
```
	var obj ={
		name: 'объект 1',
		description: 'очень-очень-...-очень длинное описание',
		items: [
			{
				name: 'элемент 1'
			}
		]
	}
```
Новое сообщение - `Объект "объект 1", элемент "элемент 1": название не может иметь длину больше 5 символов`

Реализация без makeErrorMapper
```
	function arePathsEqual(path1, path2) {
		// Возвращает равенство 2 путей. Должна правильно обрабатывать индексы: 
		// считать ['items', '0', 'name'] и ['items', '1', 'name'] одинаковыми
	}
	
	function mapError(obj, err) {
		var path = u._.toPath(err.path),
			code = err.code,
			element = u._.get(obj, err.path);
			
		if (err.path === 'description' && err.code === 'StringDefectIds.LENGTH_CANNOT_BE_MORE_THAN_MAX') {
			return 'Объект "' + obj.name + '": поле "описание" не может иметь длину больше ' + err.params.maxLength + ' символов'
		} else if (arePathsEqual(err.path, ['items', '0', 'name']) && err.code === 'StringDefectIds.LENGTH_CANNOT_BE_MORE_THAN_MAX') {
			return `Объект " + obj.name + ", элемент "' + element.name + '": название не может иметь длину больше ' + err.params.maxLength + ' символов';
		} else {
			return 'Не удалось сохранить объект'
		}
	}
	
	var messages = errors.map(function(err) { return mapError(obj, err) })
```

Реализация c makeErrorMapper
```
	var mapError = u['web-api-errors'].makeErrorMapper(function(opts) {
		var idx = opts.idx; // плейсхолдер для индекса
		
		return [
			{
				path: ['description'],
				codes: [
					{
						code: 'StringDefectIds.LENGTH_CANNOT_BE_MORE_THAN_MAX',
						message: function(obj, err) {
							return 'Объект "' + obj.name + '": поле "описание" не может иметь длину больше ' + err.params.maxLength
						}
					}
				]
			},
			{
				path: ['items', idx, 'name'],
				codes: [
					{
						code: 'StringDefectIds.LENGTH_CANNOT_BE_MORE_THAN_MAX',
						message: function(obj, err) {
							var element = element = u._.get(obj, err.path);
							
							return `Объект " + obj.name + ", элемент "' + element.name + '": название не может иметь длину больше ' + err.params.maxLength + ' символов';
						}
					}
				]
			}
		]
	}, function() {
		return 'Не удалось сохранить объект'
	})
	
	var messages = errors.map(function(err) { return mapError(obj, err) })
```

Конец примера.  

Таким образом, makeErrorMapper нужен ради того, чтобы разделить логику сопоставления пути/кода ошибки с функцией возвращающей текст ошибки и упростить первую.

## commonCodes ##

commonCodes - готовые пары код/функция получение сообщения для неуникальных ошибок из api

С помощью commonCodes можно переписать реализацию из последнего примера следующим образом:

```
	var mapError = u['web-api-errors'].makeErrorMapper(function(opts) {
		var idx = opts.idx;
		
		return [
			{
				path: ['description'],
				codes: [
					u['web-api-errors'].commonCodes['StringDefectIds.LENGTH_CANNOT_BE_MORE_THAN_MAX']({
						fieldName: 'описание'
				    })
				]
			},
			{
				path: ['items', idx, 'name'],
				codes: [
					u['web-api-errors'].commonCodes['StringDefectIds.LENGTH_CANNOT_BE_MORE_THAN_MAX']({
						fieldName: 'название'
				    })
				]
			}
		]
	}, function() {
		return 'Не удалось сохранить объект'
	})
	
	var messages = errors.map(function(err) { return mapError(obj, err) })
```
