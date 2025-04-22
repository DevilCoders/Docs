# Скрипт для разбора проблем с пушами
Использует логи Xiva и логи мобильных iOS и Android приложений

### Как установить и запустить
- Настраиваем svn для скачивания репозитория https://wiki.yandex-team.ru/arcadia/Arcadia-Starter-Guide/
- Скачиваем svn co svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/mail/mobmail/mobmail-scripts/pyyamail/tools/push
- Устанавливаем python 2 
- Устанавливаем зависимости (можно в вируальное окужение) 
```
pip install requests
pip install -i https://pypi.yandex-team.ru/simple/ yql
```
- Запускаем push.py для интересующего пользователя
```
python push.py --platform ios --uid 1120000000155158 --corp --xiva-token 22576271a1a9c5b0f8451e14d01a9c1422fc40e8 --date-from 2019-10-01 --date-to 2019-10-03 --report-json report.json --report-html report.html
```
Результаты будут в report.json и report.html. Список аргументов можно изучить в скрипте

### Как обновить кубик
- Клонируем блок https://nirvana.yandex-team.ru/flow/b063f27a-d1b4-4874-befd-353eda1b7f62/639a903b-bf5c-45d7-bfdb-fae4b8312077/graph/FlowchartBlockOperation/15d95aec-ba63-4680-b7d3-5b1119fa7930
- Нажимаем на лупу у кубика и идем в настройки кубика
- Открываем вкладку Resources, удаляем ресурс push и добавляем такой же новый - загружаем обновленный push.py
- Сохраняем операцию и депрекейтим предыдущую версию
- Отправляем изменения в push.py в аркадию `svn commit -m 'comment'`