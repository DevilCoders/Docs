# mbi-bpmn
[Документация](http://mbi-bpmn.tst.vs.market.yandex.net/swagger-ui/index.html?url=/openapi/mbi-bpmn.yaml#/mbibpmn).

## startProcess

[Документация](http://mbi-bpmn.tst.vs.market.yandex.net/swagger-ui/index.html?url=/openapi/mbi-bpmn.yaml#/mbibpmn/post_process)

В стейте объект по ключу `startProcessResponse` вида

```
{
    records: [{
        processInstanceId: 'abcd',
        businessKey: '1234',
        status: 'ACTIVE'
    }]
}
```

## getProcessStatus

[Документация](http://mbi-bpmn.tst.vs.market.yandex.net/swagger-ui/index.html?url=/openapi/mbi-bpmn.yaml#/mbibpmn/get_process_status)

В стейте объект по ключу `getProcessStatusResponse` вида

```
{
    records: [{
        processInstanceId: 'abcd',
        businessKey: '1234',
        status: 'COMPLETED'
    }]
}
```

## getProcessInfo

[Документация](http://mbi-bpmn.tst.vs.market.yandex.net/swagger-ui/index.html?url=/openapi/mbi-bpmn.yaml#/mbibpmn/get_process__processId_)

В стейте объект по ключу `getProcessInfoResponse` вида

```
{
    processInstanceId: 'abcd',
    businessKey: '1234',
    status: 'COMPLETED',
    params: {
        parameter1Name: 'parameter1Value',
        parameter2Name: 'parameter2Value',
    }
}
```
