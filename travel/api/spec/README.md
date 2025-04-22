
Принятый в https://st.yandex-team.ru/TRAVELBACK-2213 layout proto файлов спеки таков:

```
/common/ - совсем общие модели (валюта, цена, язык)
  model1.proto - файл модели
  model2.proto - файл модели

/common_functionalityXXX/ - модели и ручки для кросс-вертикальной функциональности. например, affiliate
  common/
    model1.proto - какие-то модельки
    model2.proto - какие-то модельки
  handle_get_statistics/  - описание ручки get_statistics
    request.proto
    response.proto
  handle_get_user_info.proto/ - описание ручки get_user_info
    request.proto
    response.proto
    

/hotels/ - папка для отелей
  common/ - аналогично верхнеуровневому common-у, но общие отельно-специфичные модельки
    ...
  search_hotels/ - модельки и ручки для функциональности поиска
    common/
      model1.proto
      model2.proto
    handle_search_hotels/
      request.proto
      response.proto
    handle_count_hotels/
      request.proto
      response.proto
   
/avia/
/trains/
```
