Компонент для вывода тостов (нотификашек).
Тосты появляются внизу экрана. В случае десктопа они привязаны к ToastContainer-у. Т.е. имеют такой же отступ от левого края экрана и имеют такую же ширину.

```javascript
import Toast, {ToastContainer, ToastContent, ToastIcon, ToastMessage, ToastCloser} from '@self/root/src/components/PopupToast';

<div style={{marginTop: 80}}>
    <ToastContainer>
        <Toast>
            <ToastContent>
                <ToastIcon icon="bell" />
                <ToastMessage>
                    Содержимое нотификашки
                </ToastMessage>
                <ToastCloser />
            </ToastContent>
        </Toast>
    </ToastContainer>
</div>
```

А этот `Toast` появится с задержкой в 3с и исчезнет через 3с.

```javascript
import Toast, {ToastContainer, ToastContent, ToastIcon, ToastMessage, ToastCloser} from '@self/root/src/components/PopupToast';

<div style={{marginTop: 80}}>
    <ToastContainer>
        <Toast visibleTimeout={3000} timeout={3000}>
            <ToastContent>
                <ToastIcon icon="bb" />
                <ToastMessage>
                    Содержимое нотификашки
                </ToastMessage>
            </ToastContent>
        </Toast>
    </ToastContainer>
</div>
```

Если передать статус `status: 'DISAPPEARS'`, то `Toast` исчезнет.

При исчезновении будет вызван колбек `onDisappear`

Также есть дополнительные компоненты для отображения контента: ToastCloser, ToastContent, ToastIcon, ToastMessage
