# API подсистемы слежения за исполнителем на маршруте

Подсистема на входе работает с маршрутными листами. Ручки:
/add_route_list
/delete_route_list
/get_route_list

Выходная точка системы - это ручки/каналы с eta/маршрутом. Ручки:
/timeleft

### Ручка /add_route_list
Эта ручка отвечает за задание маршрутного листа для исполнителя. Она возвращает route_list_id, по которому в последствии можно будет верифицировать выходные Eta, какому именно маршрутному листу они соответсвтуют, т.к. в системе может быть задержка на отслеживание маршрутного листа.
Мы всегда хотим принимать только цельный маршрутный лист, потому что не хотим внутри системы слежения за исполнителем на маршруте решать задачу упорядочивания точек. По нашему мнению все эти манипуляции должны происходить снаружи.

```yaml
/add-route-list:
    post:
        parameters:
            - name: body
                in: body
                schema:
                    $ref: '#/defenitions/RouteList'
        responses:
            200:
                description: ОК
                schema:
                    type: object
                    additionalProperties: false
                    required:
                    - route_list_id
                    properties:
                        route_list_id:
                            description: Идентификатор маршрутного листа
                            type: string
            400:
                description: Некорректные параметры запроса
            500:
                description: Внутренняя ошибка
```

### Ручка /delete_route_list
Эта ручка завершает отслеживание исполнителя по contractor, удалив для исполнителя маршрутный лист.

```yaml
/delete-route-list:
    post:
        parameters:
            - name: body
                in: body
                schema:
                    type: object
                    additionalProperties: false
                    requiered:
                        - contractor
                    properties:
                        contractor:
                            description: Идентификатор исполнителя
                            type: object
                            additionalProperties: false
                            required:
                            - uuid
                            properties:
                                uuid:
                                    description: Первый идентификатор исполнителя
                                    type: string
                                dbid:
                                    description: Второй (опциональный) идентификатор исполнителя
                                    type: string
        responses:
            200:
                description: ОК
            400:
                description: Некорректные параметры запроса
            500:
                description: Внутренняя ошибка
```

### Ручка /get_route_list
Эта ручка возвращает актуальный маршрутный лист для исполнителя по contractor.

```yaml  
/get-route-list:
    post:
        parameters:
            - name: body
                in: body
                schema:
                    type: object
                    additionalProperties: false
                    requiered:
                        - contractor
                    properties:
                        contractor:
                            description: Идентификатор исполнителя
                            type: object
                            additionalProperties: false
                            required:
                            - uuid
                            properties:
                                uuid:
                                    description: Первый идентификатор исполнителя
                                    type: string
                                dbid:
                                    description: Второй (опциональный) идентификатор исполнителя
                                    type: string
        responses:
            200:
                description: ОК
                schema:
                    type: object
                    additionalProperties: false
                    required:
                        - route_list_id
                        - route_list
                    properties:
                        route_list_id:
                            description: Идентификатор маршрутного листа
                            type: string
                        route_list:
                            description: Маршрутный лист
                            type: '#/defenitions/RouteListRequest'
            400:
                description: Некорректные параметры запроса
            500:
                description: Внутренняя ошибка
```

### Ручка timeleft
Эта ручка возвразает eta до точек назначения в маршрутном листе для исполнителя. Она позволяет потребителям влиять на рассчитанное по маршруту eta как им захочется с помощью фильтров.
Например:
1. Фильтровать только интересующие eta по flow_id, order_id, point_id.
2. Изменять время и расстояние под свои бизнес нужды при срабатывании определённых условий. (Если значение меньше 60 секунд, округлять до 60 секунд. Занижать/завышать eta на n%. И т.д...)
3. Дискардить eta при соблюденении определённых условий.
4. ...

Это достаточно гибкий инструмент, который позволяет корректировать eta как требуется. Единственное ограничение - это зафиксированный выходной интерфейс, всё что он позволяет - можно реализовать с помощью фильтров, которые потребитель должен задать в запросе.

```yaml
/timeleft:
    post:
        parameters:
            - name: body
                in: body
                schema:
                    type: object
                    additionalProperties: false
                    requiered:
                        - contractor
                    properties:
                        contractor:
                            description: Идентификатор исполнителя
                            type: object
                            additionalProperties: false
                            required:
                            - uuid
                            properties:
                                uuid:
                                    description: Первый идентификатор исполнителя
                                    type: string
                                dbid:
                                    description: Второй (опциональный) идентификатор исполнителя
                                    type: string
                        with_route:
                            description: Требуется ли отдавать маршрут в запросе
                            type: boolean
                        filters:
                            description: Фильтры применяемые к массиву eta, рассчитаному по маршрутному листу
                            type:
                                $ref: '#/defenitions/Filters'
                        meta:
                            description: Опциональная произвольная метаинформация по запросу
                            type: object
                            additionalProperties: true
                            x-taxi-additional-properties-true-reason: Служебная информация, которая пойдет в логи
        responses:
            200:
                description: ОК
                schema:
                    type: object
                    additionalProperties: false
                    required:
                        - route_list_id
                        - timelefts
                    properties:
                        route_list_id:
                            description: Идентификатор маршрутного листа, по которому рассчитано eta
                            type: string
                        timelefts:
                            description: Массив eta с применёнными фильтрами
                            type: '#/defenitions/Timelefts'
            400:
                description: Некорректные параметры запроса
            500:
                description: Внутренняя ошибка
```
