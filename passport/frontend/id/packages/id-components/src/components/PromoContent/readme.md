# PromoContent

Компонент `PromoContent` реализован на механизме подкомпонентов-слотов, которые прокидывают свое содержимое в нужные места компонента. Ниже представлен список этих компонентов-слотов:

- `PromoContent.Title` - заголовок (не следует путать с суперзаголовком). Прокидывает контент в основной заголовок (крупный жирный текст). Обязательный. Следует класть только текст
- `PromoContent.Button` - основная кнопка. Прокидывает контент в область где должна располагаться кнопка с основным действием. Обязательный. Следует класть только кнопку.
- `PromoContent.Supertitle` - суперзаголовок. Прокидывает контент в текст, располагающийся над основным заголовком. Следует класть только текст.
- `PromoContent.Image` - изображение в шапке компонента. Вроде договорились, что пока там могут быть только картинки, но в теории ничего не взорвется если положить туда любое блочное содержимое.
- `PromoContent.Description` - описательный текст под заголовком.
- `PromoContent.SecondaryButton` - кнопка с дополнительным действием. Стоит прокидывать только кнопку.
- `PromoContent.Control` - дополнительный контент под текстовыми блоками.

![Схема расположения слотов](scheme.png)
