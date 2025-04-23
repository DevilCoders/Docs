# MIFD

## Сервер
<pre>
ya make -r mifd
./mifd/mifd -d tmp
</pre>

## Клиент

### Простой интерфейс
<pre>
user@laptop:~/src/arcadia/market/idx/mif$ ./mifclt/mifclt ping
True
user@laptop:~/src/arcadia/market/idx/mif$ ./mifclt/mifclt test.sleep 1
2018-03-21 18:33:50,730   524 INFO  test.sleep: started test.sleep(1,)
2018-03-21 18:33:51,731   524 INFO  test.sleep: finished test.sleep(1,) time=1.0
null
</pre>

### Запуск задач
<pre>
user@laptop:~/src/arcadia/market/idx/mif$ ./mifclt/mifclt start test.sleep 1000
20161221_172452.1452126710

user@laptop:~/src/arcadia/market/idx/mif$ ./mifclt/mifclt info 20161221_172452.1452126710
{
  "tid": "20161221_172452.1452126710", 
  "state": "running",
  ...

user@laptop:~/src/arcadia/market/idx/mif$ ./mifclt/mifclt kill 20161221_172452.1452126710
{
  "tid": "20161221_172452.1452126710", 
  "state": "finished",
  ...
</pre>
