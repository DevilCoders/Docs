Сюда можно положить api.yaml с openapi спецификацией.
Пример:

openapi: 3.0.1
x-servers:
  url: http://localhost:8080
  env:
    testing:
      url: http://localhost:8080
    production:
      url: http://localhost:8080
    functionalTest:
      url: http://localhost:8080
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
            x-testEnabled: true
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
                    example: "Mary Jane"
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
