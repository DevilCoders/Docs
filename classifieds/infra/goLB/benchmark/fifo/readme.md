Рассматривал только варианты с максимально отдачей. Так же все варианты concurrency safe

* **simple**            -   простоя реализация на основе массива, в конец пишем с начала читаем
* **list**              -   связанный список, так же классический вариант
* **channel**           -   не расширяемый канал, прост как пробка и по существует не треубует обертки
* **flexibleChannel**   -   расширяемый канал
* **reuse**             -   подход переиспользующий предсозданные чанки фиксированного размера
* **chunk**             -   по сути таже реализация, что и выше, но с фатальным недостатком (https://github.com/foize/go.fifo/blob/master/fifo.go)

````
    MIX - имитация реальной нагрзуки в один поток
    
BenchmarkMixList-8                          3000000             543 ns/op   
BenchmarkMixSimple-8                        5000000             403 ns/op   
BenchmarkMixFlexibleChannel-8               2000000             557 ns/op   
BenchmarkMixChannel-8                       5000000             309 ns/op  
BenchmarkMixChunk-8                         5000000             333 ns/op  
BenchmarkMixReuse-8                         5000000             319 ns/op   

    POP - чтение в один поток      
                             
BenchmarkPopList-8                          30000000            51.7 ns/op  
BenchmarkPopSimple-8                        30000000            53.3 ns/op  
BenchmarkPopFlexibleChannel-8               30000000            35.6 ns/op  
BenchmarkPopChannel-8                       50000000            35.3 ns/op  
BenchmarkPopReuse-8                         30000000            54.4 ns/op  
BenchmarkPopChunk-8                         20000000            69.2 ns/op  

    PUSH - заполнение в один поток   
       
BenchmarkPushList-8                         2000000             787 ns/op
BenchmarkPushSimple-8                       3000000             397 ns/op
BenchmarkPushFlexibleChannel-8              3000000             519 ns/op
BenchmarkPushChannel-8                      5000000             287 ns/op
BenchmarkPushReuse-8                        5000000             303 ns/op
BenchmarkChunk-8                            5000000             345 ns/op

    Concurrency -  имитация реальной нагрзуки в 16 потоков

BenchmarkConcurrencyList-8                  2000000             725 ns/op
BenchmarkConcurrencySimple-8                2000000             621 ns/op
BenchmarkConcurrencyFlexibleChannel-8       3000000             592 ns/op
BenchmarkConcurrencyChannel-8               3000000             451 ns/op
BenchmarkConcurrencyReuse-8                 3000000             596 ns/op
BenchmarkConcurrencyChunk-8                 3000000             568 ns/op
    
````