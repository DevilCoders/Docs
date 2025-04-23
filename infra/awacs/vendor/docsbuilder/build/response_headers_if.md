В точности одно из следующих полей должно быть указано: `if_has_header`, `matcher`.  
Хотя бы одно из следующих полей должно быть указано: `create_header`, `delete_header`.
#|
|| Имя | Тип | Обязательность | Дефолт | Описание ||
|| if_has_header | string |  |  |  ||
|| matcher | [ResponseMatcherModule.Matcher](#ResponseMatcherModule.Matcher) |  |  |  ||
|| create_header | map[string, string] |  |  |  ||
|| erase_if_has_header | bool |  |  |  ||
|| delete_header | string |  |  |  ||
|#