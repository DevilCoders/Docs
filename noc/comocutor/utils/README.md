### sock_proxy.py
Прокси для отлаживания работы comocutor. Работает как прокси-сервер для tcp-соединений. Пример использования:

```bash
./sock_proxy.py -d iva-b-i6:23 localhost:65123  
```
В другой консоли вызываем

```bash
telnet localhost 65123 
```
Скрипт sock_proxy.py выведет следующие:
```
2017-10-17 13:57:01,492 - l:53 - __init__() - DEBUG - Using selector: EpollSelector
2017-10-17 13:57:01,492 - l:64 - main() - DEBUG - create server on localhost:65123
2017-10-17 13:57:02,196 - l:84 - handle_new_con() - DEBUG - make new connection to iva-b-i6:23
2017-10-17 13:57:02,212 - l:141 - proxy_client() - DEBUG - start client reader
2017-10-17 13:57:02,217 - l:146 - proxy_client() - DEBUG - read from client b'xffxfbx01xffxfbx03xffxfdx18xffxfdx1f'
2017-10-17 13:57:02,218 - l:129 - proxy_server() - DEBUG - read from server b'xffxfdx01xffxfdx03xffxfbx18xffxfbx1fxffxfax1fx00xe2x00Mxffxf0'
2017-10-17 13:57:02,221 - l:146 - proxy_client() - DEBUG - read from client b'rnrnUser Access VerificationrnrnUsername: '
2017-10-17 13:57:02,222 - l:146 - proxy_client() - DEBUG - read from client b'xffxfax18x01xffxf0'
2017-10-17 13:57:02,259 - l:129 - proxy_server() - DEBUG - read from server b'xffxfax18x00xtermxffxf0'
2017-10-17 13:57:32,794 - l:146 - proxy_client() - DEBUG - read from client b'rn% Username:  timeout expired!'
```

```
client(in 0ms): bytearray(b'\xff\xfb\x01\xff\xfb\x03\xff\xfd\x18\xff\xfd\x1f')
server(in 2ms): bytearray(b'\xff\xfd\x01\xff\xfd\x03\xff\xfb\x18\xff\xfb\x1f\xff\xfa\x1f\x00\xe2\x00M\xff\xf0')
client(in 38ms): bytearray(b'\r\n\r\nUser Access Verification\r\n\r\nUsername: \xff\xfa\x18\x01\xff\xf0')
server(in 30534ms): bytearray(b'\xff\xfa\x18\x00xterm\xff\xf0')
client(in 0ms): '\r\n% Username:  timeout expired!'
```
При работе с SSH могут возникнуть проблемы с аутентификацией так как ее будет делать прокси, а не клиент.

У утилиты **telnet** есть возможность отображения работы с опциями телнета. Пример:
```bash
# telnet
telnet> toggle options   
Will show option processing.
telnet> open iva-b-i6
Trying 95.108.197.166...
Connected to iva-b-i6.yndx.net.
Escape character is '^]'.
SENT DO SUPPRESS GO AHEAD
SENT WILL TERMINAL TYPE
SENT WILL NAWS
SENT WILL TSPEED
SENT WILL LFLOW
SENT WILL LINEMODE
...
```
### inventory.py
Сбор инвентаря.
