## Поддержка multipart

### yhttp::multipart
Структура, описывающая мультипарт запрос.
```(c++)
struct multipart
{
  string type; // тип мультипарта
  post_chunks parts; // список партов
};
```
Парт состоит из типа и его значения, а для `multipart/form-data` - имени параметра и его значения.

### Хелперы
Создание POST запроса, с мультипарт-телом.
```c++
auto request = yhttp::request::MPOST(url, multipart);
auto request = yhttp::request::MPOST(url, headers, multipart);
```

Создание мультипарта определенного типа
```(c++)
multipart body_mixed(parts); // multipart/mixed
multipart body_alternative(parts); // multipart/alternative
multipart body_form_data(parts); // multipart/form-data
```
Создание парта
```(c++)
post_chunk part(name, body); // произвольный парт
post_chunk json_part(body); // application/json
post_chunk rfc822_part(body); // message/rfc822
```

### Пример
```(c++)
auto multipart = body_mixed({json_part("{\"a\": 1}"), rfc822_part("Hello")});
auto request = yhttp::request::MPOST(url, std::move(multipart));
```
