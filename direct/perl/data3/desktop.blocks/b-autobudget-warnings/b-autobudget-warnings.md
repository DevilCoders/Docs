r104847
Предупрежденния по автобюджету для кампании

## Двухуровневый текст причины ошибки

### Первый уровень - причина появления алерта:

1. "Заданный бюджет не может быть израсходован:" -- Если в настройках стратегии задано условие "тратить n у.е. в неделю".
2. "Заданное количество кликов не может быть получено:" -- Если в настройках стратегии задано условие "получать n кликов в неделю".
3. "Заданная средняя цена за клик не может быть достигнута:" -- Если в настройках стратегии задано условие "удерживать цену клика n у.е. в среднем за неделю".
4. Если в настройках стратегии одновременно задано 2 ограничения: количество кликов и средняя цена клика, то отображаем текст "Заданное количество кликов при указанной средней ставке не может быть получено:".
5. Если в настройках стратегии одновременно задано 2 ограничения: средняя цена клика и недельный бюджет, то отображаем текст "Заданная средняя цена за клик при указанном недельном бюджете не может быть достигнута:".

### Второй уровень - причина самой проблемы (приходит от БК): (campaign.autobudget_warning.bsAutobudgetProblem)
- 1 => Достигнута максимальная выставленная ставка/Достигнута максимальная ставка, которую автобюджет считает эффективной
- 2 => Достигнута максимальная позиция выдачи (слишком большой бюджет) **(важно: если от БК приходит такая проблема - не отображаем её (т.е. второй уровень) в тексте. Алерт будет состоять только из первого уровня текста).**
- 3 => Для некоторых доменов заказа максимальная разрешенная ставка автобюджета не позволяет показываться на выдаче **(важно: если от БК приходит такая проблема - не отображаем первый уровень в тексте алерта. Алерт будет состоять только из второго уровня текста).**
- 4 => Достигнуты ограничения дневного бюджета для общего счета

## Список рекомендаций

1. увеличить максимальную ставку в настройках стратегии;
2. подключить показы на тематических площадках/ снять ограничения на расход по показам на тематических площадках
3. подключить показы по дополнительным релевантным фразам/снять ограничения на расход по дополнительным релевантным фразам
4. добавить новые целевые ключевые фразы
5. повысить эффективность рекламной кампании
