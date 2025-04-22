# WikiEditor

<a
  href='https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/tools-components/src/components/WikiEditor'
  target='_blank'>
  <img
    src='https://badger.yandex-team.ru/custom/[Исходники]/[Github][green]/badge.svg'
  />
</a>

<!-- description:start -->
Компонент, предназначенный для редактирования текста с поддержкой вики-разметки. Поддерживает хоткеи для вставки форматированных блоков и подключение тулбоксов

## Пропсы
Большая часть пропсов наследуется от [lego-components/textarea](https://lego.yandex-team.ru/lego-components/components/textarea/code), добавляется всего два дополнительных пропса:
- `config?` `{ actions: [Action] }` - Для управления хоткеями предусмотрен не обязательный параметр config, являющийся объектом с единственным полем `actions`. `actions` является массивом объектов типа [Action](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/tools-components/src/hooks/useWikiEditor/types/Action.ts). По умолчанию включено несколько хоткеев (выделение жирным, курсив и тп)
- `toolbox?` `(actionHandler: (actionKey: string) => void) => FC` - Функция, принимающая первым аргументом обработчик действия, описанного в Action. В обраотчки нужно пережать ключ действия, чтобы инициировать обработку. Предполагается разработка типовых реализаций функции

<!-- description:end -->

## Пример подключения

```tsx
import { WikiEditor } from '@yandex-int/tools-components/WikiEditor/desktop';
import { TrackerPreset } from '@yandex-int/tools-components/WikiEditor/toolbox/TrackerPreset';
import { WikiFormatter } from '@yandex-int/tools-components/WikiFormatter/WikiFormatter';

// ***
() => {
    const [text, setText] = useState('');
    const onWikiEditorChange = (event: React.ChangeEvent<HTMLTextAreaElement>) => {
        setText(event.target.value)
    };
    return (
        <div style={{ display: 'flex' }}>
            <div style={{ flex: 1 }}>
                <h2>Сам эдитор</h2>
                <WikiEditor
                    toolbox={TrackerPreset}
                    rows={10}
                    value={text}
                    onChange={onWikiEditorChange}
                />
            </div>
            <div style={{ flex: 1 }}>
                <h2>Предпросмотр</h2>
                <WikiFormatter nonce="42">{ text }</WikiFormatter>
            </div>
        </div>
    );
}
```
