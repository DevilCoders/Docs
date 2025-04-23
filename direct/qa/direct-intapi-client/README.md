# direct java intapi client

Чтобы сгенерить классов для работы API нужно запустить 
```mvn clean compile``` для `direct-intapi-client-parent` 
под jdk 9+ может не собираться, помогает сборка 8ой jvm, например так:
```JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_121.jdk/Contents/Home mvn -Dswagger.api.url=http://127.0.0.1:8090/docs/api clean install```

URL откуда брать спецификацию API задается в `pom.xml` внутри `direct-intapi-client-swagger` (или через параметр, как в примере выше)
