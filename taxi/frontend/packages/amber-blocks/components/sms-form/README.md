SmsForm

```jsx harmony
const Grid = require('../../styleguide/components/grid/Grid').default;
const phoneProps = {
    placeholder: '+7 XXX XXX-XX-XX',
    contentButton: "Отправить",
    mask: "+7 (999) 999 99 99",
};

const getCaptcha = () => new Promise(resolve => {
    c1 = {key: '416377', src: 'components/sms-form/example/captcha.jpg'};
    c2 = {key: '431237', src: 'components/sms-form/example/captcha2.jpg'};
    setTimeout(() => resolve(Math.random() > 0.5 ? c1 : c2), 1000);
});

const sendSms = ({phone, code, key}) => new Promise((resolve, reject) => {
    setTimeout(() => Math.random() > 0.2 ? resolve() : reject(), 1000);
    console.log(phone, code, key);
});

const props = {
    phoneProps,
    showCaptchaByClick: true,
    getCaptcha,
    sendSms,
    captchaWarning: 'Произошла ошибка\nпопробуйте ещё раз',
    updateCaptchaText: 'Обновить картинку'
};

<Grid container spacing={2}>
    {state.success ?  <p>Ссылка успешно отправлена</p> :
        <SmsForm
            onSuccess={() => setState({success: true})}
            {...props}
        />
    }
</Grid>;
```

Uber
```jsx harmony
const Grid = require('../../styleguide/components/grid/Grid').default;
const Cross = require('../icon/Cross').default;
const RightIcon = require('../icon/Right').default;
require('./example/UberSmsForm.styl').default;

const phoneProps = {
    placeholder: '+7 XXX XXX-XX-XX',
    contentButton: <span className="UberSmsForm__button">Атрымаць спасылку 
                        <RightIcon className="UberSmsForm__button-icon"/>
                   </span>,
    mask: "+9 999 999-99-9999",
    maskChar: null,
    clear: <Cross/>
};

const getCaptcha = () => new Promise(resolve => {
    c1 = {key: '416377', src: 'components/sms-form/example/captcha.jpg'};
    c2 = {key: '431237', src: 'components/sms-form/example/captcha2.jpg'};
    setTimeout(() => resolve(Math.random() > 0.5 ? c1 : c2), 1000);
});

const sendSms = ({phone, code, key}) => new Promise((resolve, reject) => {
    setTimeout(() => Math.random() > 0.2 ? resolve() : reject(), 1000);
    console.log(phone, code, key);
});

const props = {
    className: 'UberSmsForm',
    phoneProps,
    getCaptcha,
    sendSms,
    captchaWarning: 'Произошла ошибка\nпопробуйте ещё раз',
    updateCaptchaText: 'Обновить картинку'
};

<Grid container spacing={2}>
    {state.success ? <p>Ссылка успешно отправлена</p> :
        <SmsForm
            onSuccess={() => setState({success: true})}
            {...props}
        />
    }
</Grid>;
```


Yandex
```jsx harmony
const Grid = require('../../styleguide/components/grid/Grid').default;
require('./example/YandexSmsForm.styl').default;

const phoneProps = {
    placeholder: '+7 XXX XXX-XX-XX',
    contentButton: 'ПОЛУЧИТЬ ССЫЛКУ',
    mask: "+9 999 999-99-9999",
    maskChar: null,
};

const getCaptcha = () => new Promise(resolve => {
    c1 = {key: '416377', src: 'components/sms-form/example/captcha.jpg'};
    c2 = {key: '431237', src: 'components/sms-form/example/captcha2.jpg'};
    setTimeout(() => resolve(Math.random() > 0.5 ? c1 : c2), 1000);
});

const sendSms = ({phone, code, key}) => new Promise((resolve, reject) => {
    setTimeout(() => Math.random() > 0.2 ? resolve() : reject(), 1000);
    console.log(phone, code, key);
});

const props = {
    className: 'YandexSmsForm',
    phoneProps,
    getCaptcha,
    sendSms,
    captchaWarning: 'Произошла ошибка\nпопробуйте ещё раз',
    updateCaptchaText: 'Обновить картинку'
};

<Grid container spacing={2}>
    {state.success ? <p>Ссылка успешно отправлена</p> :
        <SmsForm
            onSuccess={() => setState({success: true})}
            onError={() => console.log('error')}
            {...props}
        />
    }
</Grid>;
```
