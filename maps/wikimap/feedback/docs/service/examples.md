## Примеры запросов в Feedback Int

### Изменение статуса заявки
```
curl -d '{"status": "published"}' -X PUT -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks/{id заявки}"
```

### Топонимы
#### Изменение адреса топонима
```
curl -d '{
    "form_id":"toponym",
    "question_id": "wrong_address",
    "answer_id": "report_address",
    "form_point": {
        "lat": 56.129158,
        "lon": 47.309987
    },
    "metadata": {
        "client_id": "mobile_maps_ios",
        "version": "1.0",
        "locale": "ru_RU"
    },
    "question_context": {
        "toponym": {
            "address": [
                {
                    "kind": "street",
                    "name": "Старая улица"
                },
                {
                    "kind": "house",
                    "name": "1"
                }
            ],
            "center_point": {
                "lat": 55.73736,
                "lon": 37.486481
            }
        }
    },
    "answer_context": {
        "toponym": {
            "address": [
                {
                    "kind": "street",
                    "name": "Новая улица"
                },
                {
                    "kind": "house",
                    "name": "1"
                }
            ],
            "center_point": {
                "lat": 55.73736,
                "lon": 37.486481
            }
        }
    },
    "object_id": "773399585",
    "object_url": "https://n.maps.yandex.ru/#!/objects/773399585"
}' -X POST -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks"
```
#### Добавление адреса у топонима без адреса
```
curl -d '{
    "form_id":"toponym",
    "question_id": "add_object",
    "answer_id": "toponym",
    "form_point": {
        "lat": 56.129158,
        "lon": 47.309987
    },
    "form_context": {
        "assignment_id": "fb:assignment1",
        "search_text": "User search request"
    },
    "metadata": {
        "client_id": "mobile_maps_ios",
        "version": "1.0",
        "locale": "ru_RU"
    },
    "answer_context": {
        "toponym": {
            "address": [
                {
                    "kind": "street",
                    "name": "Новая улица"
                },
                {
                    "kind": "house",
                    "name": "1"
                }
            ],
            "center_point": {
                "lat": 55.73736,
                "lon": 37.486481
            }
        }
    },
    "object_id": "773399585",
    "object_url": "https://n.maps.yandex.ru/#!/objects/773399585"
}' -X POST -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks"
```
#### Добавление подъезда у топонима
```
curl -d '{
    "form_id":"toponym",
    "question_id": "add_object",
    "answer_id": "entrance",
    "form_point": {
        "lat": 56.129158,
        "lon": 47.309987
    },
    "metadata": {
        "client_id": "mobile_maps_ios",
        "version": "1.0",
        "locale": "ru_RU"
    },
    "answer_context": {
        "entrance": {
            "name": "2",
            "center_point": {
                "lat": 55.738803742131125,
                "lon": 37.59734473872754
            }
        }
    },
    "object_id": "773399585",
    "object_url": "https://n.maps.yandex.ru/#!/objects/773399585"
}' -X POST -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks"
```
#### Подъезд топонима указан неверно
```
curl -d '{
    "form_id":"toponym",
    "question_id": "wrong_entrance",
    "answer_id": "report_location",
    "form_point": {
        "lat": 56.129158,
        "lon": 47.309987
    },
    "metadata": {
        "client_id": "mobile_maps_ios",
        "version": "1.0",
        "locale": "ru_RU"
    },
    "question_context": {
        "entrance": {
            "name": "Old name",
            "center_point": {
                "lat": 55.738803742131125,
                "lon": 37.59734473872754
            }
        }
    },
    "answer_context": {
        "entrance": {
            "name": "New name",
            "center_point": {
                "lat": 55.738803742131125,
                "lon": 37.59734473872754
            }
        }
    },
    "object_id": "773399585",
    "object_url": "https://n.maps.yandex.ru/#!/objects/773399585"
}' -X POST -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks"
```
#### Местоположение топонима указано неверно
```
curl -d '{
    "form_id":"toponym",
    "question_id": "wrong_location",
    "answer_id": "report_location",
    "form_point": {
        "lat": 56.129158,
        "lon": 47.309987
    },
    "metadata": {
        "client_id": "mobile_maps_ios",
        "version": "1.0",
        "locale": "ru_RU"
    },
    "question_context": {
        "toponym": {
            "center_point": {
                "lat": 55.738803742131125,
                "lon": 37.59734473872754
            }
        }
    },
    "answer_context": {
        "toponym": {
            "center_point": {
                "lat": 55.738803742131125,
                "lon": 37.59734473872754
            }
        }
    },
    "object_id": "773399585",
    "object_url": "https://n.maps.yandex.ru/#!/objects/773399585"
}' -X POST -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks"
```
#### Местоположение остановки указано неверно
```
curl -d '{
    "form_id":"toponym",
    "question_id": "wrong_location",
    "answer_id": "report_location",
    "form_point": {
        "lat": 56.129158,
        "lon": 47.309987
    },
    "metadata": {
        "client_id": "mobile_maps_ios",
        "version": "1.0",
        "locale": "ru_RU"
    },
    "question_context": {
        "stop": {
            "center_point": {
              "lat": 55.73736,
              "lon": 37.486481
            },
            "uri": "ymapsbm1://transit/stop?id=stop__10125314",
            "lines": [
              {
                "uri": "ymapsbm1://transit/line?id=239_60_bus_roadconssochi",
                "threads": [
                  {
                    "threadId": "239B_60_bus_roadconssochi"
                  }
                ]
              },
              {
                "uri": "ymapsbm1://transit/line?id=3332698775",
                "threads": [
                  {
                    "threadId": "3332702615"
                  }
                ]
              }
            ]
        }
    },
    "answer_context": {
        "stop": {
            "center_point": {
              "lat": 65.73736,
              "lon": 67.486481
            },
            "uri": "ymapsbm1://transit/stop?id=stop__10125314",
            "lines": [
              {
                "uri": "ymapsbm1://transit/line?id=239_60_bus_roadconssochi",
                "threads": [
                  {
                    "threadId": "239B_60_bus_roadconssochi"
                  }
                ]
              },
              {
                "uri": "ymapsbm1://transit/line?id=3332698775",
                "threads": [
                  {
                    "threadId": "3332702615"
                  }
                ]
              }
            ]
        }
    },
    "object_id": ""
}' -X POST -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks"
```
#### Подъезд топонима указан неверно (его здесь нет)
```
curl -d '{
    "form_id":"toponym",
    "question_id": "wrong_entrance",
    "answer_id": "not_found",
    "form_point": {
        "lat": 56.129158,
        "lon": 47.309987
    },
    "metadata": {
        "client_id": "mobile_maps_ios",
        "version": "1.0",
        "locale": "ru_RU"
    },
    "question_context": {
        "entrance": {
            "name": "2",
            "center_point": {
                "lat": 55.738803742131125,
                "lon": 37.59734473872754
            }
        }
    },
    "object_id": "773399585",
    "object_url": "https://n.maps.yandex.ru/#!/objects/773399585"
}' -X POST -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks"
```
#### Комментарий к топониму
```
curl -d '{
    "form_id":"toponym",
    "question_id": "other",
    "answer_id": "comment",
    "form_point": {
        "lat": 56.129158,
        "lon": 47.309987
    },
    "metadata": {
        "client_id": "mobile_maps_ios",
        "version": "1.0",
        "locale": "ru_RU"
    },
    "message": "Комментарий",
    "object_id": "773399585",
    "object_url": "https://n.maps.yandex.ru/#!/objects/773399585"
}' -X POST -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks"
```
#### Неправильный набор маршрутов на остановке
```
curl -d '{
    "form_id":"toponym",
    "question_id": "wrong_lines",
    "answer_id": "report_lines",
    "form_point": {
        "lat": 56.129158,
        "lon": 47.309987
    },
    "metadata": {
        "client_id": "mobile_maps_ios",
        "version": "1.0",
        "locale": "ru_RU"
    },
    "question_context": {
        "stop": {
            "center_point": {
              "lat": 55.73736,
              "lon": 37.486481
            },
            "uri": "ymapsbm1://transit/stop?id=stop__10125314",
            "lines": [
              {
                "uri": "ymapsbm1://transit/line?id=1",
                "threads": [
                  {
                    "threadId": "thread1"
                  }
                ]
              },
              {
                "uri": "ymapsbm1://transit/line?id=2",
                "threads": [
                  {
                    "threadId": "thread2"
                  }
                ]
              }
            ]
        }
    },
    "answer_context": {
        "stop": {
            "center_point": {
              "lat": 55.73736,
              "lon": 37.486481
            },
            "uri": "ymapsbm1://transit/stop?id=stop__10125314",
            "lines": [
              {
                "uri": "ymapsbm1://transit/line?id=3",
                "threads": [
                  {
                    "threadId": "thread3"
                  }
                ]
              }
            ]
        }
    },
    "object_id": ""
}' -X POST -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks"
```

### Организации
#### Добавление организации
```
curl -d '{
    "form_id": "organization",
    "question_id": "add_object",
    "answer_id": "organization",
    "answer_context": {
        "company": {
            "name": "Деловой центр Диапазон",
            "urls": [
                "http://business-center-diapazon.ru/",
                "http://www.bc-diapason.ru/"
            ],
            "hours": [
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Monday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Tuesday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Wednesday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Thursday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Friday"
                }
            ],
            "status": "open",
            "emails": [],
            "phones": [
                "+7 (999) 768-71-04"
            ],
            "address": "Россия, Москва, 1-й Волоколамский проезд, 10, стр. 1",
            "entrances": [
                {
                    "name": "main",
                    "center_point": {
                        "lat": 55.803215,
                        "lon": 37.490647
                    }
                }
            ],
            "coordinates": {
                "lat": 55.803317,
                "lon": 37.490735
            },
            "rubric_names": [
                "Бизнес-центр"
            ]
        }
    },
    "metadata": {
        "client_id": "mobile_maps_ios",
        "version": "0",
        "locale": "ru_RU"
    }
}' -X POST -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks"
```
#### Добавление подъезда организации
```
curl -d '{
    "form_id": "organization",
    "question_id": "add_object",
    "answer_id": "entrance",
    "object_id": "1124715036",
    "object_url": "https://yandex.ru/maps/org/1124715036",
    "question_context": {
        "company": {
            "entrances": [
                {
                    "name": "main",
                    "center_point": {
                        "lat": 53.80436280112614,
                        "lon": 37.490062957720085
                    }
                }
            ]
        }
    },
    "answer_context": {
        "company": {
            "entrances": [
                {
                    "name": "main",
                    "center_point": {
                        "lat": 55.80436280112614,
                        "lon": 37.490062957720085
                    }
                }
            ]
        }
    },
    "metadata": {
        "client_id": "mobile_maps_ios",
        "version": "0",
        "locale": "ru_RU"
    }
}' -X POST -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks"
```
#### Неправильный вход организации (вход указан)
```
curl -d '{
    "form_id": "organization",
    "question_id": "wrong_entrance",
    "answer_id": "report_location",
    "object_id": "1124715036",
    "object_url": "https://yandex.ru/maps/org/1124715036",
    "question_context": {
        "company": {
            "entrances": [
                {
                    "name": "main",
                    "center_point": {
                        "lat": 53.80436280112614,
                        "lon": 37.490062957720085
                    }
                }
            ]
        }
    },
    "answer_context": {
        "company": {
            "entrances": [
                {
                    "name": "main",
                    "center_point": {
                        "lat": 55.80436280112614,
                        "lon": 37.490062957720085
                    }
                }
            ]
        }
    },
    "metadata": {
        "client_id": "mobile_maps_ios",
        "version": "0",
        "locale": "ru_RU"
    }
}' -X POST -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks"
```
#### Неправильный вход организации (вход не указан)
```
curl -d '{
    "form_id": "organization",
    "question_id": "wrong_entrance",
    "answer_id": "not_found",
    "object_id": "1124715036",
    "object_url": "https://yandex.ru/maps/org/1124715036",
    "question_context": {
        "company": {
            "entrances": [
                {
                    "name": "main",
                    "center_point": {
                        "lat": 53.80436280112614,
                        "lon": 37.490062957720085
                    }
                }
            ]
        }
    },
    "answer_context": {
        "company": {
            "entrances": [
                {
                    "name": "main",
                    "center_point": {
                        "lat": 55.80436280112614,
                        "lon": 37.490062957720085
                    }
                }
            ]
        }
    },
    "metadata": {
        "client_id": "mobile_maps_ios",
        "version": "0",
        "locale": "ru_RU"
    }
}' -X POST -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks"
```
#### Изменение информации об организации
```
curl -d '{
    "form_id": "organization",
    "question_id": "wrong_information",
    "answer_id": "report_information",
    "object_id": "1124715036",
    "object_url": "https://yandex.ru/maps/org/1124715036",
    "question_context": {
        "company": {
            "name": "Старая организация",
            "urls": [
                "http://business-center-diapazon.ru/",
                "http://www.bc-diapason.ru/"
            ],
            "hours": [
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Monday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Tuesday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Wednesday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Thursday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Friday"
                }
            ],
            "status": "closed_unknown",
            "emails": [],
            "phones": [
                "+7 (999) 768-71-04"
            ],
            "address": "Россия, Москва, 1-й Волоколамский проезд, 10, стр. 1",
            "entrances": [
                {
                    "name": "main",
                    "center_point": {
                        "lat": 55.803215,
                        "lon": 37.490647
                    }
                }
            ],
            "coordinates": {
                "lat": 55.803317,
                "lon": 37.490735
            },
            "rubric_names": [
                "Бизнес-центр"
            ]
        }
    },
    "answer_context": {
        "company": {
            "name": "Новая организация",
            "urls": [
                "http://business-center-diapazon.ru/",
                "http://www.bc-diapason.ru/"
            ],
            "hours": [
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Monday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Tuesday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Wednesday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Thursday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Friday"
                }
            ],
            "status": "closed_unknown",
            "emails": [],
            "phones": [
                "+7 (999) 768-71-04"
            ],
            "address": "Россия, Москва, 1-й Волоколамский проезд, 10, стр. 1",
            "entrances": [
                {
                    "name": "main",
                    "center_point": {
                        "lat": 55.803215,
                        "lon": 37.490647
                    }
                }
            ],
            "coordinates": {
                "lat": 55.803317,
                "lon": 37.490735
            },
            "rubric_names": [
                "Бизнес-центр"
            ]
        }
    },
    "metadata": {
        "client_id": "mobile_maps_ios",
        "version": "0",
        "locale": "ru_RU"
    }
}' -X POST -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks"
```
#### Организация открыта
```
curl -d '{
    "form_id": "organization",
    "question_id": "opened",
    "answer_id": "report_open",
    "object_id": "1124715036",
    "object_url": "https://yandex.ru/maps/org/1124715036",
    "question_context": {
        "company": {
            "name": "Старая организация",
            "urls": [
                "http://business-center-diapazon.ru/",
                "http://www.bc-diapason.ru/"
            ],
            "hours": [
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Monday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Tuesday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Wednesday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Thursday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Friday"
                }
            ],
            "status": "closed_unknown",
            "emails": [],
            "phones": [
                "+7 (999) 768-71-04"
            ],
            "address": "Россия, Москва, 1-й Волоколамский проезд, 10, стр. 1",
            "entrances": [
                {
                    "name": "main",
                    "center_point": {
                        "lat": 55.803215,
                        "lon": 37.490647
                    }
                }
            ],
            "coordinates": {
                "lat": 55.803317,
                "lon": 37.490735
            },
            "rubric_names": [
                "Бизнес-центр"
            ]
        }
    },
    "answer_context": {
        "company": {
            "status": "closed_permanently"
        }
    },
    "metadata": {
        "client_id": "mobile_maps_ios",
        "version": "0",
        "locale": "ru_RU"
    }
}' -X POST -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks"
```
#### Организация закрыта временно
```
curl -d '{
    "form_id": "organization",
    "question_id": "closed",
    "answer_id": "temporary",
    "object_id": "1124715036",
    "object_url": "https://yandex.ru/maps/org/1124715036",
    "question_context": {
        "company": {
            "name": "Старая организация",
            "urls": [
                "http://business-center-diapazon.ru/",
                "http://www.bc-diapason.ru/"
            ],
            "hours": [
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Monday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Tuesday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Wednesday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Thursday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Friday"
                }
            ],
            "status": "closed_unknown",
            "emails": [],
            "phones": [
                "+7 (999) 768-71-04"
            ],
            "address": "Россия, Москва, 1-й Волоколамский проезд, 10, стр. 1",
            "entrances": [
                {
                    "name": "main",
                    "center_point": {
                        "lat": 55.803215,
                        "lon": 37.490647
                    }
                }
            ],
            "coordinates": {
                "lat": 55.803317,
                "lon": 37.490735
            },
            "rubric_names": [
                "Бизнес-центр"
            ]
        }
    },
    "answer_context": {
        "company": {
            "status": "closed_permanently"
        }
    },
    "metadata": {
        "client_id": "mobile_maps_ios",
        "version": "0",
        "locale": "ru_RU"
    }
}' -X POST -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks"
```
#### Организация закрыта навсегда
```
curl -d '{
    "form_id": "organization",
    "question_id": "closed",
    "answer_id": "permanent",
    "object_id": "1124715036",
    "object_url": "https://yandex.ru/maps/org/1124715036",
    "question_context": {
        "company": {
            "name": "Старая организация",
            "urls": [
                "http://business-center-diapazon.ru/",
                "http://www.bc-diapason.ru/"
            ],
            "hours": [
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Monday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Tuesday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Wednesday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Thursday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Friday"
                }
            ],
            "status": "closed_unknown",
            "emails": [],
            "phones": [
                "+7 (999) 768-71-04"
            ],
            "address": "Россия, Москва, 1-й Волоколамский проезд, 10, стр. 1",
            "entrances": [
                {
                    "name": "main",
                    "center_point": {
                        "lat": 55.803215,
                        "lon": 37.490647
                    }
                }
            ],
            "coordinates": {
                "lat": 55.803317,
                "lon": 37.490735
            },
            "rubric_names": [
                "Бизнес-центр"
            ]
        }
    },
    "answer_context": {
        "company": {
            "status": "closed_permanently"
        }
    },
    "metadata": {
        "client_id": "mobile_maps_ios",
        "version": "0",
        "locale": "ru_RU"
    }
}' -X POST -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks"
```
#### Организация, возможно, закрыта
```
curl -d '{
    "form_id": "organization",
    "question_id": "closed",
    "answer_id": "probably",
    "object_id": "1124715036",
    "object_url": "https://yandex.ru/maps/org/1124715036",
    "question_context": {
        "company": {
            "name": "Старая организация",
            "urls": [
                "http://business-center-diapazon.ru/",
                "http://www.bc-diapason.ru/"
            ],
            "hours": [
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Monday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Tuesday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Wednesday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Thursday"
                },
                {
                    "breaks": [
                        {
                            "end_time": 840,
                            "start_time": 780
                        }
                    ],
                    "end_time": 1140,
                    "start_time": 600,
                    "day_of_week": "Friday"
                }
            ],
            "status": "closed_unknown",
            "emails": [],
            "phones": [
                "+7 (999) 768-71-04"
            ],
            "address": "Россия, Москва, 1-й Волоколамский проезд, 10, стр. 1",
            "entrances": [
                {
                    "name": "main",
                    "center_point": {
                        "lat": 55.803215,
                        "lon": 37.490647
                    }
                }
            ],
            "coordinates": {
                "lat": 55.803317,
                "lon": 37.490735
            },
            "rubric_names": [
                "Бизнес-центр"
            ]
        }
    },
    "answer_context": {
        "company": {
            "name": "3"
        }
    },
    "metadata": {
        "client_id": "mobile_maps_ios",
        "version": "0",
        "locale": "ru_RU"
    }
}' -X POST -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks"
```
### Маршруты
#### Неправильный маршрут
```
curl -d '{
    "form_id":"route",
    "question_id": "wrong_route",
    "answer_id": "report_route",
    "form_point": {
        "lat": 56.129158,
        "lon": 47.309987
    },
    "metadata": {
        "client_id": "mobile_maps_ios",
        "version": "1.0",
        "locale": "ru_RU"
    },
    "question_context": {
      "route": {
        "travel_mode": "truck",
        "traffic_jams": false,
        "way_points": [
          {"lon": 37.588461580598135, "lat": 55.73387438556429},
          {"lon": 37.58926969774817, "lat": 55.73381419716051}
        ],
        "uri": "ymapsbm1://route/driving/0LfQtNC10YHRjCDQsdGD0LTQtdGCINC-0L_QuNGB0LDQvdC40LUg0LzQsNGA0YjRgNGD0YLQsA",
        "encoded_points": "4o89AuhwUgMzAAAA3____yQAAADo____PAEAADX___87AAAA2v___3UAAAC0____6QAAAG7___9CAAAA2P___7MAAACR____NQAAAN____8=",
        "segments": [{
          "from": {"lon": 37.588461580598135, "lat": 55.73387438556429},
          "to": {"lon": 37.58926969774817, "lat": 55.73381419716051},
          "travel_mode": "pedestrian"
        }],
        "vehicle_restrictions": {
          "weight": 23.2323,
          "width": 23,
          "eco_class": 5
        }
      }
    },
    "answer_context": {
      "route": {
        "errors": [
          {
            "point": {"lon": 37.588461580598135, "lat": 55.73387438556429},
            "type": "obstruction"
          },
          {
            "point": {"lon": 37.588461580598135, "lat": 55.73387438556429},
            "type": "prohibiting_sign",
            "context": {
              "vehicle_restrictions": {
                "payload": 12,
                "has_trailer": false
              }
            }
          }
        ],
        "segments": [{
          "points": [
            {"lon": 37.588461580598135, "lat": 55.73387438556429},
            {"lon": 37.58926969774817, "lat": 55.73381419716051}
          ],
          "travel_mode": "truck"
        }]
      }
    },
    "object_id": ""
}' -X POST -H "Content-Type: application/json" "http://core-feedback-api.maps.yandex.net/v1/tasks"
```
