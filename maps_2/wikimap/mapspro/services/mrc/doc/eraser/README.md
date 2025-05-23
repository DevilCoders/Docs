### проблемы
- в условиях ограниченной квоты в MDS мы неизбежно столкнемся с исчерпанием свободного места
- стремительно растет размер датасета, в результате на mrc-browser скоро закончится память

### предложение

#### распубликация "ненужных" снимков
снимок сматченный на граф является "нужным", если выполнено хотя бы одно условие:
- входит в текущее покрытие (формируется экспортом)
- входит в историческое покрытие (вычисляем "на лету" в новом сервисе)
  - периоды: неделя, месяц, квартал, полугодие или старше
  - приоритет: дневной снимок с лучшим quality
- принадлежит к проезду, в котором для одного из снимков выполнено что-то из списка выше
- есть связь с гипотезой

#### удаление из MDS
- все распубликованные снимки старше месяца удаляем из MDS
- записи в таблице feature оставляем, чтобы не нарушать ссылочную целостность
- добавляем поле deleted_from_mds

### результаты эксперимента на дорожном графе
- снимков к распубликации 40M из 519M
- из них с гипотезами 800K
- тайминги на дев-машинке (быстрее чем в проде)
  - загрузка снимков из БД - 1 час 4 минуты
  - вычисление исторических покрытий - 3 минуты
  - загрузка ссылок на гипотезы для 40M снимков  - 1 час 10 минут
- [ссылка на код](https://a.yandex-team.ru/review/2653172/details)
