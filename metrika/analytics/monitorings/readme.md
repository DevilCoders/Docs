## Solomon Monitorings

Здесь живет код, который считает соломоновские отчеты

### Принцип работы

1. Каждый код отчета должен лежать в структуре из трех папок. Каждая из папок отобржается на объек соломона в таком порядке project / service/ cluster
2. Отчет должен возвращать DataFrame. В индексе DataFrame должно быть поле с датой fielddate и все dimensions. Все остальное будет sensors
3. В fielddate должен быть timestamp
4. Дока по соломону - https://wiki.yandex-team.ru/jandexmetrika/analytics/knowledgebase/solomonmonitorings/
