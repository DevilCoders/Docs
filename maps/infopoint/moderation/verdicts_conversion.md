Ниже описаны правила применения вердиктов от Чистого Веба. Для дорожного события или комментария мы или разрешаем его показ или запрещаем. Кроме того для дорожных событий можем изменить набор тегов (тип).

Полный набор вердиктов от ЧВ привдён ниже.

### Про отношение к дорожной ситуации
| **Характеристика** | **Краткое описание** |
|-|-|
| road_accident | ДТП |
| road_reconstruction | Дорожные работы |
| road_police | Камера/Контроль/Полиция |
| road_jams | Информация о состоянии пробки и скорости движения |
| road_detour | Советы про то как объехать пробку или другое препятствие |
| road_question | Запрос фактической информации о дорожной ситуации |
| road_ask_for_help | Просьба помощи на дороге |
| road_general_talks | Околодорожные темы общего характера |
| road_place | Есть только информация о месте |
| road_time | Есть только информация о времени |
| road_other | Другая фактическая информация о дорожной ситуации |
| road_spam | Реклама и спам |
| nonroad | Сообщения на неоколодорожные темы |

### Про нарушения
| **Наша характеристика** | **Соответствие в common_toloka** | **Краткое описание** |
|-|-|-|
| text_toloka_insult | text_toloka_insult_light или text_toloka_insult_hard | Лёгкое или тяжёлое оскорбление |
| text_toloka_obscene | text_toloka_obscene_light или text_toloka_obscene_hard | Лёгкий или жёсткий мат |
| text_toloka_rude | text_toloka_rude | Грубая лексика |
| text_toloka_threat_hard | text_toloka_threat_hard | Тяжёлая угроза |
| text_toloka_threat_light | text_toloka_threat_light | Лёгкая угроза |
| text_toloka_vulgarity | text_toloka_vulgarity или text_toloka_porno | Пошлость / Мерзость ( не тяжкое)  + Порнографичность / Грубая пошлость (тяжкое) |
| text_toloka_law_violation | text_toloka_law_violation | Законодательно запрещенное содержание |
| text_toloka_policy | text_toloka_policy | Политизированный текст |
| text_toloka_spam | text_toloka_spam или text_toloka_advert | Спам, в том числе мошенничество  + Реклама. **<font color="red">Внимание!</font>** частные объявления не входят в рекламу в common_toloka |
| text_toloka_no_sense | text_toloka_no_sense | Бессмыслица /Бред |
| text_toloka_personal_data | text_toloka_personal_data | Личные данные |

### Правила применения вердиктов

Дорожные события поделим собственно на "полезные дорожные события" и Разговорчики. Помимо вердиктов у нас есть ещё исходный набор тегов, которые поставил пользовать. Пользователь может ставить события с ровно одним из следующих вариантов тегов:
- accident
- reconstruction
- speed_control, police
- other
- chat (Разговорчики)
- local_chat (Локальные разговорчики)

1. Если есть хотя бы одно нарушение то status = disapproved.

2. Если в наборе есть вердикт nonroad или road_general_talks (пока мы не уверены в качестве general_talks, он часто путается с nonroad), то status = disapproved. Во всех остальных случаях status = approved.

3. Смена типа дорожного события происходит по следующим правилам.

3.1. Смапливаем вердикты в набор тегов по следующей схеме:
- road_accident --> accident
- road_reconstruction --> reconstruction
- road_police --> speed_control, police
- road_other, road_jams, road_detour, road_question, road_ask_for_help --> other
- road_place, road_time --> пустое множество

3.2. То, что получилось, пересечь с пользовательскими тегами. Если пересечение непустое, то это и будет новый набор тегов.

_Пример:_
user_tags = {accident}, verdicts = {road_accident, road_other}
verdict_tags = {accident, other}
result_tags = user_tags & verdict_tags = {accident}

user_tags = {speed_control, police}, verdicts = {road_police, road_accident}
verdict_tags = {speed_control, police, accident}
result_tags = user_tags & verdict_tags = {speed_control, police}

3.3. Если получилось пустое множество, то взять {множество из п.3.1} | {пользовательские теги & {chat, local_chat}}. В новое множество специально подмешиваем chat и local_chat, если они были в пользовательских тегах. Если опять получилось пустое множество, то оставить пользовательский набор тегов. Последнее возможно из-за вердиктов, которые преобразуются в пустой набор тегов в п.3.1 (road_place, road_time).

3.4. Из получившегося множества выбрать главный набор тегов из списка - что встретится первым. Выбранный набор и будет новым набором тегов.
Список по приоритету:
- local_chat
- chat
- accident
- reconstruction
- speed_control, police
- other

_Примеры:_
user_tags = {accident}, verdicts = {road_other, road_reconstruction}
verdict_tags = {other, reconstruction}
user_tags & verdict_tags = {} // пересечение пустое, берём вердикты
candidate_tags = verdict_tags | (user_tags & chat) = {other, reconstruction} 
result_tags = {reconstruction} // reconstruction приоритетнее

user_tags = {chat}, verdicts = {road_accident, road_other}
verdict_tags = {accident, other}
user_tags & verdict_tags = {} // пересечение пустое, берём вердикты и чат раз пользователь его поставил
candidate_tags = verdict_tags | (user_tags & chat) = {chat, accident, other}
result_tags = {chat} // chat всех приоритетнее

user_tags = {accident}, verdicts = {road_reconstruction, road_place}
verdict_tags = {reconstruction}
user_tags & verdict_tags = {} // пересечение пустое, road_place мапится в пустое множество
candidate_tags = verdict_tags | (user_tags & chat) = {reconstruction}
result_tags = {reconstruction}

user_tags = {accident}, verdicts = {road_time}
verdict_tags = {}
user_tags & verdict_tags = {} // пересечение пустое, road_place мапится в пустое множество
candidate_tags = verdict_tags | (user_tags & chat) = {} 
result_tags = {accident} // раз теги-кандидаты пустые, то берём пользовательские теги
