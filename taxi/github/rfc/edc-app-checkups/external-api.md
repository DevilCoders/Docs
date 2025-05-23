# Внешнее апи
## Service-points
На одной площадке (адресе) может оказываться несколько услуг от разных компаний. Поэтому рассматриваем отдельно площадку (public-point; может означать общественную точку или филиал) и отдельно "точку оказания услуги" (service-point). 

Партнер не может самостоятельно "вписаться" на произвольные общественные точки/создать общественную точку по своему усмотрению - только через поддержку Яндекса. Поэтому через внешнее апи нельзя создавать service-point'ы или менять параметры public-point'а. Можно получать service-point'ы вместе со связанными public-point'ами (списком или по одному) и редактировать информацию service-point'а (время работы, работает ли он в принципе)

## Medical-reviews
Создание медосмотра выполнено в три этапа
1. Получить данные для медосмотра по токену. Структура токена не закреплена в апи, на первом этапе будет использоваться, что-нибудь вроде номер путевого листа + id водителя; но подход не помешает нам добавить дополнительных факторов/переделать на случайную строку, например, для прохождения медосмотра без путевого листа
2. Загрузить результат медосмотра. В ответ вернется Титул для подписания врачом. Здесь неприятный момент - Титул - это XML-документ. Но технически подписывается бинарник и лучше бы его закодировать в base64. А отвечаем мы json'ом. То есть получается base64-encoded XML в JSON-строке.
3. Загрузить подпись

Можно сделать в два этапа, но тогда партнер должен формировать Титул; это не очень.