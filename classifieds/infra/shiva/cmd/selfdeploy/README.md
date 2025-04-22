# Disclaimer

Самодеплой шивы в случае когда протеряли все полимеры

Шаги:
1. Копируем карту из https://github.com/YandexClassifieds/services/tree/master/maps в files:sMapStr
2. Копируем манифест деплоя из https://github.com/YandexClassifieds/services/tree/master/deploy в files:manifestStr
3. Заменеям секреты в манифесте на реальные значения из секретницы
4. В dev.env в переменную selfdeploy_version вписываем версию (аккуратно, она не бует проверена в docker registry)
5. Запускаем main

Примечания:
* п3 - как только научимся привозить секреты в дев окружение, пункт удалится сам собой
* конфигурация хранится в dev.env
