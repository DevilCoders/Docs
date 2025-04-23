Onboarding — подсказка, рассказывающая пользователю про новый функционал, с которым он еще не знаком.

Реализация контейнера тултипа [гайдлайну](https://wiki.yandex-team.ru/Market/Design/yandex-market-design-system/ui-elements/tooltip/)
Позционирование по гайдлайну
Бывает 2-х типов: простой тултип с текстом и формат попапа с картинкой и заголовком.

Пример использования

1) Объявить онбординг в market/src/entities/onboarding/constants.js
```
    {
        id: 'filtersPokupkiOnboarding',
        type: 'popup',
        disableCookie: 'fFgLPoDk',
        countCookie: 'gEgLRoDl',
        exceptExperiments: ['some_exp_signature'],
        platform: ['desktop'],
    }
```
2) Вызвать онбординг в компоненте
```
    <Onboarding<Onboarding
        id="filtersPokupkiOnboarding"
        title="Покупки сразу на Маркете"
        text={() => 'Нажмите, чтобы увидеть только те товары,<br/>' +
            'которые можно купить не уходя с сайта —<br/>' +
            'и получить бонусы'}
        image="//yastatic.net/market-export/_/i/onboarding/calc.svg"
        positions={[['top', 'center'], ['left', 'center']]}
    >
        <Button onClick={changeState(id)}>
            Submit
        </Button>
    </Onboarding>
```
