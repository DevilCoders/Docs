# Кастомный вариант валидации oneOf, написано на замену стандартному
oneOf при ошибке не сообщает почему объект не прошел валидацию по каждой из предложенных схем, что делает очень сложным отладку
Если проверка не прошла - выводит ошибки валидации для каждого из items, содержащихся в объекте

## Пример
`
{
    "type": "object",
    "format": "one-of-custom",
    "items": [ $schema1, $schema2 ]
}
`
