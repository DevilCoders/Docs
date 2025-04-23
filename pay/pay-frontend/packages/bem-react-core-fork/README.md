# Форк функции withBemMod из @bem-react/core

## Что изменилось
Логика работы с `modValue = '*'`
 *   в оригинале — `(modValue === '*' && Boolean(propValue))`
 *   в форке — `(modValue === '*' && typeof propValue !== 'undefined')`
 
Это все

## TODO
* Сделать PR в оригинальную либу
