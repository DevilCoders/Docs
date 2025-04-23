## 2.0.0

* Проект переписан на TypeScript.
* Изменен формат входных данных. Все опции отзыва были вынесены в `feedbackOptions`.

```diff
 {
     serviceUrl: 'http://zealot.yandex.ru:32500/',
     family: 6,
-    subject: 'Feedback about beta.maps.yandex.ru',
-    recipientEmail: 'support@maps.yandex.ru',
-    comment: 'Some text',
-    fields: {},
-    additionalFields: {},
+    feedbackOptions: {
+        subject: 'Feedback about beta.maps.yandex.ru',
+        recipientEmail: 'support@maps.yandex.ru',
+        comment: 'Some text',
+        fields: {},
+        additionalFields: {}
+    },
     spamCheckOptions: {
         serviceUrl: 'http://so1h-dev.mail.yandex.net:80/',
         ip: '84.201.173.29',
         host: 'beta.maps.yandex.ru',
         realpath: '/',
         formName: 'maps'
     },
     userHeaders: {}
 }
```

## 1.2.0

* Allow full URL in `serviceUrl` parameter ([#5](https://github.yandex-team.ru/maps/ymaps-feedback/pull/5)).

## 1.1.0
* В `sendMail()` добавлена опция `ipFamily`.

## 1.0.0
* Первая версия.
