## Snooper

Простая библиотечка для поиска и/или максирования разнообразных секретов.

### Поддерживаемые секреты

  - Сессионные печеньки
  - Два современных формата OAuth-токенов (legacy слишком фолзит)
  - TVM service/user тикеты
  - s3 presign
  - mds/avatars sign (disabled by default)

### Использование

  - C++ библиотека: [cpp](cpp)
  - Python враппер: [py](py)

Если вы хотите использовать для логирования - можно воспользоваться `NSnooper::TMaskedLogBackend`:
```C++
TStreamLogBackend streamBackend(&Cerr);
TLog log(new NSnooper::TMaskedLogBackend(&streamBackend));
log << "log line with secrets" << Endl;
```

В противном случае:
```C++
// Инстанцируем Snooper-а
NSnooper::TSnooper snooper;

// Создаем ищейку
// Внимание! Searcher НЕ thread-safe в угоду производительности, возьмите у Snooper-а по ищейке на каждый тред
auto searcher = snooper.Searcher();

// Поищем секретики
TString content = R"(
GET /test?sessionid=3%3A1566480756.5.0.1564091077870%3AYWgJJQ%3A88.1%7C1120000000038691.0.2002%7C1120000000049208.490331.2002.2%3A490331%7C142241.804415.ySsdPJeQSM1Zoj32qOMvTKSWVxM HTTP/1.1
Host: localhost:9000
User-Agent: HTTPie/1.0.2
Accept-Encoding: gzip, deflate
Connection: keep-alive
X-Ya-Service-Ticket: 3:serv:CBAQ__________9_IgQIehAD:Jp93z7FrOT2IOaPtAD3s7_zFU6DJrL3HvHbYJKu9Cet5ytYSKzseN-SVmIMH5y4UM51XtJcV3mvD1rv6w_dzt36PxpS7R7EAPbQWkP6wJGQRdKWjmAWkkqD-s062kL4q39fG0hJwxe4s-8zDh5hCXTimzZvFrdo09hQcfFAoj-cJp93z7FrOT2IOaPtAD3s7_zFU6DJrL3HvHbYJKu9Cet5ytYSKzseN-SVmIMH5y4UM51XtJcV3mvD1rv6w_dzt36PxpS7R7EAPbQWkP6wJGQRdKWjmAWkkqD-s062kL4q39fG0hJwxe4s-8zDh5hCXTimzZvFrdo09hQcfFAoj-c
Cookie: yandexuid=654321; Session_id=3:1566480756.5.0.1564091077870:YWgJJQ:88.1|1120000000038691.0.2002|1120000000049208.490331.2002.2:490331|142241.804415.ySsdPJeQSM1Zoj32qOMvTKSWVxM; sessionid2=3:1566820123.5.0.1564091077870:YWgJJQ:88.1|1120000000038691.0.2002|1120000000049208.-1.0|142429.844023.OJbvg_ahfMoFX22xPvf-iEoVNsk; something=brown;
Authorization: OAuth AgAAAAAHYVLuAAX_m477zavGV0GMlcItT-kpRm1

)";
auto results = searcher->Search(content);
// где results - NSnooper::NSnooper в котором инфа о всех пяти секретах

// Или in-place замаскируем все что найдем
searcher->Mask(content);
// теперь content будет содержать строку:
/*
GET /test?sessionid=3%3A1566480756.5.0.1564091077870%3AYWgJJQ%3A88.1%7C1120000000038691.0.2002%7C1120000000049208.490331.2002.2%3A490331%7C142241.804415.XXXXXXXXXXXXXXXXXXXXXXXXXXX HTTP/1.1
Host: localhost:9000
User-Agent: HTTPie/1.0.2
Accept-Encoding: gzip, deflate
Connection: keep-alive
X-Ya-Service-Ticket: 3:serv:CBAQ__________9_IgQIehAD:XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
Cookie: yandexuid=654321; Session_id=3:1566480756.5.0.1564091077870:YWgJJQ:88.1|1120000000038691.0.2002|1120000000049208.490331.2002.2:490331|142241.804415.XXXXXXXXXXXXXXXXXXXXXXXXXXX; sessionid2=3:1566820123.5.0.1564091077870:YWgJJQ:88.1|1120000000038691.0.2002|1120000000049208.-1.0|142429.844023.XXXXXXXXXXXXXXXXXXXXXXXXXXX; something=brown;
Authorization: OAuth AgAAAAAHYVLuAAX_m4XXXXXXXXXXXXXXXXXXXXX

*/
```

Больше примеров для C++:
  - тестовая приложенька: [example](example)
  - тестовая приложенька с логгером: [cpp/logger/example](cpp/logger/example)
  - тесты: [cpp/ut](cpp/ut)
  - перф-приложенька: [cpp/perf](cpp/perf)
  
И для Python:
  - тестовая приложенька: [py/example](py/example)
  - тесты: [py/ut](py/ut)
  
### Вопросы/баги/замечания

Можно складывать в buglloc@ или рассылку security@ или тикетом в очередь [ANTSECRET](https://st.yandex-team.ru/ANTSECRET)
