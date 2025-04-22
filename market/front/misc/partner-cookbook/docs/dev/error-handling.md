# Обработка ошибок

Есть 2 основных типа ошибок

- [Ошибки на сервере](#ошибки-на-сервере)
- [Ошибки в браузере](#ошибки-в-браузере)
  - [Ошибки при отрисовке на клиенте](#ошибки-при-отрисовке-на-клиенте)
  - [Ошибки в сайдэффектах на клиенте](#ошибки-в-сайдэффектах-на-клиенте)

## Ошибки на сервере

Ошибки на сервере нужно обрабатываться с помощью BaseError для лучшего логгирования вместо `UncaughtExceptionError`

TODO: пример

Больше примеров и описание смотрите в [market/error](https://github.yandex-team.ru/market/error).

## Ошибки в браузере

- Для логгирования клиентских ошибок мы используем [`error-counter`](https://github.yandex-team.ru/RUM/error-counter). Для удобства работы на клиенте сущестует экшен `logError` в `'~/actions/errors'`.
- Для уведомления пользователя об ошибке используется `showError` из `~/actions/errors`, он отобразит тост с заданным контентом, а также залоггирует ошибку в `error-counter`.

Посмотреть залоггированные ошибки можно в [error.yandex-team.ru](https://error.yandex-team.ru/projects/partner_market_front/projectDashboard?filter=level%20==%20error%20AND%20domain%20==%20partner.market.yandex.ru). Так же для него есть [документация](https://wiki.yandex-team.ru/users/alantukh/market/error-booster/) от @alantuh

### Ошибки при отрисовке на клиенте

Для отлавливания ошибок при отрисовке реактом используется пакет `react-error-boundary`. Он предоставляет более удобное API для работы с [`componentDidCatch`](https://ru.reactjs.org/docs/error-boundaries.html). Сейчас доступен из `~/containers/ErrorBoundary`, где ему присваиваются типы для flow.

По умолчанию если при отрисовке реакт дерева(в том чиле mapStateToProps, mergeProps и тд) была выброшена ошибка, ломается приложение целиком. Предохранители позволяют отловить ошибку на наиболее низком шаге и локализовать сломанную часть. Сейчас в партнёрке на каждой странице есть 4 предохранителя, а именно для хедера, сайдбара, футера и главного приложения.

Если на вашей странице есть что то ~~как виджет~~ самостоятельное. А именно, при поломке этой части приложения не затрагивает остальной функционал на этой странице, то eё стоит обернуть в предохранитель.

```tsx
// ~/pages/MyPage/App.js

import {useDispatch, useSelector} from 'react-redux'
import {Column, Button, Text} from '@yandex-levtian/b2b'

import {ErrorBoundary} from '~/containers/ErrorBoundary'
import {logError} from '~/actions/errors';

import {WidgetLike} from './components/WidgetLike'
import {OtherContent} from './components/OtherContent'

function FallbackComponent({error, resetErrorBoundary}) {
    return (
        <Column>
            <Text>Произошла ошибка: {error.toString()}</Text>
            <Button onClick={resetErrorBoundary}>
                Восстановить состояние
            </Button>
        </Column>
    )
}

function App() {
    const dispatch = useDispatch()
    /**
     * Не все ошибки нужно логировать,
     * если вы сомневаетесь, логируйте
     */
    const onError = (error: Error) =>
        dispatch(
            logError({
                type: 'CUSTOM_&_UNIQUE_STRING_TO_BE_LOGGED',
                error,
            }),
        );

    return (
        <>
            <ErrorBoundary FallbackComponent={FallbackComponent} onError={onError}>
                <WidgetLike />
            </ErrorBoundary>
            <OtherContent />
        </>
    )
}

export default App
```

Нужно отметить что предохранители спасут вас от ошибок в рендере ваших компонентов или в селекторах. Ошибки их хендлеров(onClick и тд) ловиться не будут.

### Ошибки в сайдэффектах на клиенте

Сайдэффекты в ПИ обрабатываются в эпиках

```tsx
// ~/pages/MyPage/epics.js

import {from, of, EMPTY} from 'rxjs'
import {catchError, delay, mergeMap, switchMap} from 'rxjs/operators'
import {ofType} from 'redux-observable'

import {logError, showError} from '~/actions/errors'

// только логгируем ошибку
export const actionEpic: Epic<State, Actions> = (actions$, state$) =>
    actions$.pipe(
        ofType(ACTION_TYPE),
        switchMap(() => {
            // logic

            return from(resolver(ctx, payload)).pipe(
                switchMap(response => {
                    // more logic
                }),
                catchError(error =>
                    of(
                        // реагируем на ошибку в приложении
                        resolverErrorAction(),

                        // логгирование
                        logError({
                            type: 'LONG_AND_UNIQUE_STRING_TO_BE_LOGGED',
                            error,
                        }),
                    ),
                ),
            )
        }),
    )

// логгируем и показываем тост для пользователя
export const actionEpic: Epic<State, Actions> = (actions$, state$) =>
    actions$.pipe(
        ofType(ACTION_TYPE),
        switchMap(() => {
            // logic

            return from(resolver(ctx, payload)).pipe(
                switchMap(response => {
                    // more logic
                }),
                catchError(error =>
                    of(
                        // реагируем на ошибку в приложении
                        resolverErrorAction(),

                        // лоиггирование и тост
                        showError({
                            title: <I18n id="текс для пользователя, что произошла ошибка" />,
                            closable: true,
                            details: <I18n id="больше информации, если нужно" />,
                            type: 'LONG_AND_UNIQUE_STRING_TO_BE_LOGGED',
                            // обязательно прокидываем саму ошибку что бы она прорасла в error-booster
                            error,
                        }),
                    ),
                ),
            )
        }),
    )
```
