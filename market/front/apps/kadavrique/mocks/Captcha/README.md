# Captcha

Данные в стейте:
```js
{
    "captcha": {
        "value": CaptchaValue
    }
}
```
где `CaptchaValue` - строка, которая якобы изображена на картинке капчи.
## Метод check
Проверяет что переданное значение капчи соответствует значению в стейте. В параметре `rep` запроса должно быть значение, указанное пользователем в поле ввода капчи.
