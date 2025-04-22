**StickyBox**

Компонент с возможностью приклеивания к нижней или верхней части вьюпорта при прокрутке (sticky)
без ограничения на высоту родителя. Умеет в анимацию, тень блока и приклеивание единожды.

Использует IntersectionObserver. Перед использованием в таче необходимо поменять заглушку:
`platform.touch/client/touch.modules/polyfill/_intersection-observer/polyfill_intersection-observer.yate`

на инлайн-скрипт из десктопа (достаточно скопипастить):
`platform.desktop/client/desktop.blocks/polyfill/_intersection-observer/polyfill_intersection-observer.yate`

Растягивается на всю ширину экрана, так что для полноценного экспириенса рекомендуется скрыть панель слева :)

```jsx noeditor
const styles = require('./Readme.styles.styl');
const {$gray600, $purple600} = require('@self/root/src/uikit/palette/colors');

const staticBlocks = new Array(3).fill().map((k, i) =>
   <div key={i} className={styles.static}>
       Static content
   </div>
);

const paddingProp = {
    type: 'enum',
    required: false,
    values: [
        'none',
        'normal',
        'condensed',
        'extended',
        'mini',
        'compact',
    ],
};

<Helper.Playground
    component={StickyBox}
    forceUpdate={true}
    props={{
        paddingTop: paddingProp,
        paddingBottom: paddingProp,
    }}
    example={(props) => (
        <div>
            {staticBlocks}
            <StickyBox {...props}>
                <div className={styles.content}>
                    Sticky Content
                    <div>
                        {new Array(7).fill().map((k, i) => (
                             <div key={i} className={styles.cube} />
                        ))}
                    </div>
                </div>
            </StickyBox>
            {staticBlocks}
        </div>
    )}
/>

```
