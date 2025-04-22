Сборка: `gradle shippingsorter-app:build`
Тесты:  `gradle shippingsorter-app:test`    

Запуск локально из папки `/shippingsorter`:  
- из идеи:
  Run на классе ServicebusApp, VM Options: ```-Denv.config=../properties/local/local.properties```

Доступно здесь: `http://localhost:8240//shippingsorter` 

Важно! Сервис принимает на вход самнтиметры и граммы и возвращает их же
