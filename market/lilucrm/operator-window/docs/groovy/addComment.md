# Комментарии к тикету

### Внутренний комментарий

```groovy
 api.bcp.edit(ticket, [
        '@comment'  : [
            'metaclass': 'comment$internal',
            'body'     : "нашелся order " + ticket.order.title.toString()
        ]])
```
  Где:
   - ticket - тикет, к которому хотим добавить комментарий
   - metaclass - `comment$internal` -  показывает что комментарий внутренний
   - body - текст комментария
### Внешний комментарий
```groovy
 api.bcp.edit(ticket, ['status'    : 'resolved',
                                  '@comment'  : [
                                      'metaclass': 'comment$public',
                                      'body'     : commentText
                                  ]])


```
отличия от пункта выше только в metaclass = `comment$public`
### Вложения

```groovy
def order =  api.db.get('order@2011T7428235')
if (!order) {
  return 'NO ordeer'
}

def receipts  = api.db.of('orderReceipt')
  .withFilters(
    api.db.filters.eq('parent', order),
  ).list()


def attachments = []
for(def r in receipts) {
  if (r.mdsPdfUrl) {
  attachments << api.bcp.create('attachment$default', ['name': r.mdsPdfUrl.value, "url": r.mdsPdfUrl.href, 'contentType': 'application/pdf'])
  }
}

api.bcp.create('comment$public', ['entity': 'ticket@1318812', 'body': 'чек вот', '@attachments': attachments])
```
