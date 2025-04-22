# effector-helpers

## dialog

Позволяет создать API для управления диалоговым окном.

**Создание диалога с ключом:**

При открытии диалога произойдет синхронизация с query-параметрами: `https://acme.domain/?dialog=dialog-key`

```ts
import { createDialogApi } from '@client/shared/libs/effector-helpers/dialog';

const dialog = createDialogApi('dialog-key');

const MyDialog = () => {
  const isVisible = useStore(dialog.$isVisible);
  const onHide = useEvent(dialog.hide);

  return (
    <Dialog visible={isVisible} onClose={onHide} />
  );
};

dialog.show();
```

**Создание диалога без ключа:**

```ts
import { createDialogApi } from '@client/shared/libs/effector-helpers/dialog';

const dialog = createDialogApi();

const MyDialog = () => {
  const isVisible = useStore(dialog.$isVisible);
  const onHide = useEvent(dialog.hide);

  return (
    <Dialog visible={isVisible} onClose={onHide} />
  );
};

dialog.show();
```

**Создание диалога с данными:**

```ts
import { createDialogApi } from '@client/shared/libs/effector-helpers/dialog';

interface DialogState {
  value: string;
}

const dialog = createDialogApi<DialogState>();

const MyDialog = () => {
  const isVisible = useStore(dialog.$isVisible);
  const state = useStore(dialog.$state);
  const onHide = useEvent([dialog.hide, dialog.reset]);

  // state.value -> 'hello'

  return (
    <Dialog visible={isVisible} onClose={onHide} />
  );
};

dialog.show({ value: 'hello' });
```
