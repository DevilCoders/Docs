# InteractionLayout

Лейаут с упрощенной шапкой для создания интерактивных страниц, например форм или визардов.

## Составные части

* InteractionLayout - основной компонент, Header и Body должны быть его children
* InteractionLayout.Header - компонент шапки, выводит левые/правые контролы и логотип маркета
* InteractionLayout.Controls - обёртка для контролов, выставляет правильные отступы между ними
* InteractionLayout.BackButton - контрол "Вернуться назад"
* InteractionLayout.Body - компонент для основного контента

## Пример использования

```js

const View = () => {
    // Контролы для вывода в левой части шапки
    // Должны быть обёрнуты в InteractionLayout.Controls для правильных отступов
    const leftControls = (
        <InteractionLayout.Controls>
            <InteractionLayout.BackButton>Назад</InteractionLayout.BackButton>
            <div>Обновлено 2 часа назад</div>
        </InteractionLayout.Controls>
    );

    // Контролы для вывода в правой части шапки
    // Должны быть обёрнуты в InteractionLayout.Controls для правильных отступов
    const rightControls = (
        <InteractionLayout.Controls>
            <button type="button">Отмена</button>
            <button type="button">Сохранить</button>
        </InteractionLayout.Controls>
    );

    // Рендерим InteractionLayout
    // Передаём левые/правые контролы в Header через пропсы
    // Основной контент оборачиваем в Body
    return (
        <InteractionLayout>
            <InteractionLayout.Header
                leftControls={leftControls}
                rightControls={rightControls}
            />

            <InteractionLayout.Body>
                Основной контент
            </InteractionLayout.Body>
        </InteractionLayout>
    );
};

<View />
```
