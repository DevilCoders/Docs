# Глобальное хранилище Здоровья

 Чтобы иметь возможность в компонентах получичить доступ к параметрам метрики, экспериментам etc.


## HealthStore
В turboJSON должен присутствовать блок 'health-store', в котороый записываем все значения:
```typescript
{
    block: 'health-store',
    props: {
        metrikaParams: {
            platform: '',
            reqid: '',
            experiments: '',
        },
        expFlags: {},
    },
}
```

## HOC withHealthStore
Обернув нужный компонент в HOC withHealthStore, в props компонента появляется ключ `store`, содержащий всё, что мы передали в `props` блока `health-store`.

```javascript
import * as React from 'react';
import { withHealthStore, IWithHealthStoreProps } from '@yandex-turbo/components/HealthStore/hocs/withHealthStore';

function ExampleBase({ store }: IWithHealthStoreProps) {
    const { metrikaParams: { reqid }, expFlags } = store;

    const isDisabledFlag = Boolean(expFlags['is-disabled']) || false;

    if (isDisabledFlag) {
        return null;
    }

    return <div>reqid: {reqid}</div>;
}

export const Example = withHealthStore(ExampleBase);

```


## HOC withHealthMetrika
Обернув компонент в HOC withHealthMetrika, в `props` компонента появляется метод `reachGoal`, позволяющий отправить событие в метрику и передать дополнительные параметры (все основные параметры берутся из блока `health-store`)

```javascript
import * as React from 'react';
import { withHealthMetrika, IWithHealthMetrikaProps } from '@yandex-turbo/components/HealthStore/hocs/withHealthMetrika';

function ExampleBase(props: IWithHealthMetrikaProps) {
    const { reachGoal } = props;

    return (
        <Button
            onClick={() => {
                reachGoal('button_clicked', { param1: 1 });
            }}
        >
            Нажми меня!
        </Button>
    );
}

export const Example = withHealthMetrika(ExampleBase);
```
