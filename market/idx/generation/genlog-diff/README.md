# genlog-diff

## В первую очередь смотрим в Вики

- Подробная инструкция разработчика
  - https://wiki.yandex-team.ru/market/development/indexer/yt-genlogs/how-to/
- Верхнеуровневое описания проекта Генлоги в YT
  - https://wiki.yandex-team.ru/market/development/indexer/yt-genlogs/project-summary/

## О программе

Сравнивает два множества генлогов (в протобуфном формате), пишет результаты в таблицу и статистику - в файл.
- Идея - один MapReduce-джойн
  - Маппер нормализует и тегирует строки
    - В частности, удаляет из протобуфа поля, которые нам пока не интересны. В теории их можно было бы игнорировать в редьюсере, но зачем тащить лишние данные по сети?
  - Редьюсер считает дифф
    - Использует [гугловую библиотеку](https://developers.google.com/protocol-buffers/docs/reference/cpp/google.protobuf.util.message_differencer) для сравнения полей
      - Она очень мощная, обязательно посмотрите на все ее содержимое перед тем, как писать велосипед :)
    - Прикапывает тег изменения (A|M|D)
    - Прикапывает обе версии протобуфа генлога, если они есть
    - Ведет подсчет статистики числа A, M, D
- Статистику пишем файл, полный дифф пишем в таблицу
 
Подводные камни
- Держим в белом списке только поля, на которые мы сейчас коммитимся
  - В конце работ нужно будет убрать белый список, чтобы ничего не пропустить
  - Поля не в белом списке удаляем еще на этапе маппера, чтобы вся операция была дешевле
  - Когда мы добавляем новые поля в белый список, мы получаем деградацию
    - Это норма, но нужно стремиться к тому, чтобы уменьшать дифф, не оставлять это на потом

## Пример запуска

`./genlog-diff/genlog-diff --yt-proxy arnold --yt-token-path $HOME/.yt/token --yt-client-log-path yt_client.log --yt-old-table=//home/market/testing/indexer/stratocaster/statscalc/$GENERATION/in/{0..7}_all.seq --yt-new-table=//tmp/$LOGNAME/{0000..0015} --yt-diff-table-path //tmp/$LOGNAME/diff --summary-path /dev/stdout`

Если вы хотите создать синтетические различия между записями генлога с помощью поля `chaos`, добавьте параметр `--chaos-level`:
`./genlog-diff/genlog-diff --yt-proxy arnold --yt-token-path $HOME/.yt/token --yt-client-log-path yt_client.log --yt-old-table=//home/market/testing/indexer/stratocaster/statscalc/$GENERATION/in/{0..7}_all.seq --yt-new-table=//tmp/$LOGNAME/{0000..0015} --yt-diff-table-path //tmp/$LOGNAME/diff --summary-path /dev/stdout --chaos-level 0.01`

На данный момент не предусмотренна синтетическая модификация каких-либо полей, кроме `chaos`, но это неплохая идея для стартапа!

## Точки расширения

Используемый алгоритм универсален, предполагается, что вы будете расширять программу в двух точках:
- `FIELDS_WHITE_LIST` - поля протобуфа, котрые должны учитываться в диффе. Поле `chaos` всегда учитывается
- `CreateMessageDifferencer` - здесь вы можете определять, как именно сравниваются поля. Например, вы можете сделать некоторые из `repeated` полей множествами или мапами (чтобы не учитывать порядок)
