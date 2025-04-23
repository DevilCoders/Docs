1. Скачай данные из YT, примерно так:
   ![Примерно так](https://jing.yandex-team.ru/files/yuramalinov/Screenshot_2020-10-23%20results%20-%20Navigation%20-%20Arnold.png)
   - в файл вроде `watson.json`

2. Выгрузи список товаров из КИ (внутренний формат)
   - надо оставить две колонки: shop_sku, url
   - и сохранить как csv файл, например, [такой](https://jing.yandex-team.ru/files/yuramalinov/shop_skus.csv)
   
3. Запусти скрипт (нужен python3)
   ```bash
   python3 watson2csv.py watson.json shop_skus.csv output.csv 
   ```

4. Файл `output.csv` можно загружать в МТ.

5. Profit!
