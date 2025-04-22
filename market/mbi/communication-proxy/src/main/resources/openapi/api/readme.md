Сюда можно положить api.yaml с openapi спецификацией.
Пример:

openapi: 3.0.1
servers:
    - url: localhost:8080
info:
    title: API
    description: API
    version: LATEST
tags:
    - name: helloWorld
      description: Hello World Api
paths:
    /helloWorld:
        get:
            tags:
                - helloWorld
            responses:
                200:
                    description: OK
                    content:
                        text/plain:
                            schema:
                                type: string
            parameters:
                - name: name
                  in: query
                  schema:
                    type: string
    /helloWorldInternal:
        get:
            tags:
                - helloWorld
            responses:
                200:
                    description: OK
                    content:
                        text/plain:
                            schema:
                                type: string
            parameters:
                - name: name
                  in: query
                  schema:
                    type: string
