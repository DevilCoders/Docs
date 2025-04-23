### CartBusinessGroup

Группировка cartItems по бизнес схемам (экспресс, дбс и т.д.)

### Правила группировки

Указываются в splitRules.js как массив SPLIT_RULES.

Каждое правило соответствует отдельной группе cartItems.

Группы формируются на основании соответствий типов офферов, указанных в offerTypesMatchers.

Типы оффера генерируются в selectors.js в selectBusinessTypesByCartItemId как Map для быстрой проверки на нужный тип.
