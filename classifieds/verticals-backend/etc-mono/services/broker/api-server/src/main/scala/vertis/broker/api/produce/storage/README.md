StorageProducer - попытка абстракции над хранилищем с 'потоковым' входом.

По идее должна позволять простую комбинацию хранилищ. 
Как вертикально - натягивая _StorageProducerBuffer_ над хранилищем. Тем самым обеспечивая backpressure и собственно буферизацию.
Так и горизонтально - используя _StorageProducersChain_ для объединения хранилищ в цепочку для фоллбэка на следующий при проблемах.

Что плохо
1. Фоллбэк на следующее хранилище происходит только, если текущий упадет.
Он может бесконечно долго держать сообщение у себя и фоллбэка для него не произойдет.
