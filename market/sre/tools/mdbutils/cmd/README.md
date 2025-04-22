Утилиты:
    mdblist - утилита для получения списка всех БД доступных аккаунту. Возвращает cloud_id, cloud_name, folder_id, description, database. Пример:
    ```
          {
		    "cloud_id": "foosc9sa66qavrs21efj",
    		    "folder_id": "food8s5g4f3v7a3mee68",
                    "cloud_name": "marketapi",
                    "description": "{\"abcServiceId\": \"1227\", \"abcServiceSlug\": \"marketapi\"}",
                    "database": "market_content_api_admin_test"
          }
    ```
       Флаги:
         -json - json формат(по умолчанию текстовый список)
         -debug - debug режим
         -key - облачный ключ(YC) для работы с API. Если не передавать ключ, будет использован механизм сполучения OAuth over SSH.
       Пример получения через YC:
    ```
       yc iam key create --user-account --output key.json - для user акаунта
       yc iam key create --service-account-name robot1 --output robot_key.json - для robot/service_user аккаунта
    ```
