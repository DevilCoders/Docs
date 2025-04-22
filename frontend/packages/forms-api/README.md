# Forms API NodeJS Client
__<span style="color: red;">Пакет переезжает, просьба не вносить изменения в данный репозиторий</span>__

Пакет для работы с API сервиса [Forms](https://forms.yandex-team.ru) из NodeJS окружения.

## Установка

```shell
npm install @yandex-int/forms-api --registry=https://npm.yandex-team.ru
```

## Использование

```ts
import { FormsClient } from '.';

const api = new FormsClient({
    baseUrl: 'https://forms.yandex-team.ru/api/v2', // Current default
});

(async () => {
    const newForm = await api.forms.create({
        uuid: '7031ca9c-ddad-424b-b7d9-be7f2cacc04e',
        autopublish: {
            since: new Date('2020-04-01'),
            till: new Date('2020-06-30'),
        },
        title: 'Example form',
        body: [{
            type: 'page',
            body: [{
                type: 'text',
                key: 'name',
                title: 'Enter your name',
            }, {
                type: 'integer',
                key: 'age',
                title: 'Enter your age',
            }],
        }],
    });

    console.log('created', newForm);

    const sleep = (time: number) => new Promise((resolve) => setTimeout(resolve, time));
    await sleep(SOME_TIME);

    const answers = await api.answers.find({ formUuid: newTrig.uuid });

    console.log(
        answers,
    );
})().catch((error) => console.error(error.stack));
```

## Support

По всем вопросам обращайтесь в [forms@](mailto:forms@yandex-team.ru).
