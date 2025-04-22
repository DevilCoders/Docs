Стандартный PhoneInput

```jsx
<PhoneInput codePlaceholder="Код страны" numberPlaceholder="номер" />
```

Со значением

```jsx
<PhoneInput value={{code: '8', number: '1234567', additionalCode: '0000'}} />
```

С заданной страной

```jsx
<PhoneInput countryId={225} />
```

Без добавочного

```jsx
<PhoneInput hasAdditionalCode={false} />
```
