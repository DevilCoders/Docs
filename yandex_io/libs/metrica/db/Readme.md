### api usage example
```
ITelemetryEventsDB *db = initDb();
AppMetricaBatcher batcher;
auto sink = [&batcher](ISinkHandler& sinkHander, auto event, auto env) {
    if (!batcher.addEvent(event, env)) {
        sendBatch(batcher.flushBatch()); // return when sent
        sinkHandler.releaseBeforeLast();
        batcher.addEvent(event, env);
    }
    if (batcher.isFull()) {
        sendBatch(batcher.flushBatch());
        sinkHandler.releaseIncludingLast();
    }
    sinkHandler.readyFornext();
};
auto sinkHandler = db->registerSink(sink);
sinkHandler->readyForNext();
```
