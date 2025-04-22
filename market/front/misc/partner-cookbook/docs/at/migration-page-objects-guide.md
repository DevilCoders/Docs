# Переход на новый подход описания Page Objects

Исторически PO в партнерке описываются через функцию makePO из ginny-helpers. Однако с таким подходом не получится сделать нормальную типизацию в typescript. Поэтому мы мигрируем на новый подход к описанию PO, который под капотом не меняется, но позволяет получить типизацию. Здесь описаны фрагменты кода старого и нового подходов.

Вкратце: теперь мы создаем класс-наследник `AbstractPO` и описываем селекторы и вложенные PO как геттеры класса, а селекторы с параметрами и методы как методы класса. И помечаем соответствующими декораторами. Затем экспортим из файла не сам класс, а `new PO().makePO();`.

## Селекторы
```javascript
// Старый подход
export default makePO({
  selectors: {
    // обычные селекторы - строки
    root: select`${AwesomeComponent}`,
    reloadBtn: '[data-e2e="reload-btn"]',
    // селектор - колбек
    tooltipIcon: PO => PO.by`[data-e2e="balance-access-label"] ${Icon}`,
    // глобальный селектор
    tooltipLink: PO => ({
      selector: PO.by`${Popup.root} [data-e2e-i18n-key="common:hint"] ${Link}`,
      global: true,
    })  
  },
  // ...
})
```
```javascript
// Новый подход
class PO extends AbstractPO {
  @Selector()
  get root() {
    return selectorCreate(select`${AwesomeComponent}`);
  }
  @Selector()
  get reloadBtn() {
    return selectorCreate('[data-e2e="reload-btn"]');
  }
  @Selector()
  get tooltipIcon() {
    // Используем this
    return selectorCreate(this.by`[data-e2e="balance-access-label"] ${Icon}`);
  }
  // для глобальных передаем параметр в декоратор
  @Selector({global: true})
  get tooltipLink() {
    return selectorCreate(this.by`${Popup.root} [data-e2e-i18n-key="common:hint"] ${Link}`);
  }
}
export default new PO().makePO();
```

## Селекторы с параметрами

```javascript
// Старый подход
export default makePO({
  selectorsWithParams: {
    // обычный селектор
    loginRowByUserType: PO => (userType: string) => PO.by`[data-e2e="${userType}-login-row"]`,
    // глобальный селектор
    toastTextByKey: PO => (key: string) => ({
      selector: PO.by`[data-e2e-i18n-key="common:success.${key}-text"]`,
      global: true,
    }),
  },
  // ...
})
```
```javascript
// Новый подход
class PO extends AbstractPO {
  @SelectorWithParams()
  loginRowByUserType(userType: string) {
    // Используем this
    return selectorCreate(this.by`[data-e2e="${userType}-login-row"]`);
  }
  // для глобальных передаем параметр в декоратор
  @SelectorWithParams({global: true})
  toastTextByKey(key: string) {
    return selectorCreate(this.by`[data-e2e-i18n-key="common:success.${key}-text"]`);
  }
}
export default new PO().makePO();
```

## Вложенные Page Objects
```javascript
// Старый подход
export default makePO({
  innerPO: {
    // Простой PO
    modal: {PO: ModalWindow},
    // PO - колбек
    operationalRatingWidget: po => ({PO: OperationalRatingWidget, parent: po.root}),
    dsbsRating: po => ({PO: Rating, parent: po.root, root: '[data-e2e="dsbs"]'}),
  },
  // ...
})
```
```javascript
// Новый подход
class PO extends AbstractPO {
  @InnerPO()
  get modal() {
    return innerPOCreate({PO: ModalWindow});
  }
  @InnerPO()
  get operationalRatingWidget() {
    // используем this
    return innerPOCreate({PO: OperationalRatingWidget, parent: this.root});
  }
  @InnerPO()
  get dsbsRating() {
    // используем this
    return innerPOCreate({PO: Rating, parent: this.root, root: '[data-e2e="dsbs"]'});
  }
}
export default new PO().makePO();
```

## Методы
```javascript
// Старый подход
export default makePO({
  methods: {
    // Метод без описания
    clickClose: po => [() => po.modal.clickClose()],
    // Метод с аргуметом
    checked: po => [
      async (weekDay: string) => {
        const pressed = await po.day(weekDay).getAttribute('aria-pressed');
        return pressed === 'true';
      },
    ],
    // Метод с простым описанием
    getProgramId: po => [
      'Получаем ID программы',
      async () => {
        const label = await po.idLabel.getText(); // здесь idLabel - селектор
        return (label.match(/\d+/) || [])[0];
      },
    ],
    // Метод с вычислимым описанием
    selectDate: po => [
      (date: string) => `Устанавливаем дату ${moment(date).format('YYYY-MM-DD')}`,
      async (date: string) => {
        await po.datepickerButton.click();
        await po.popup.waitForOpen();
        await po.datepicker.setDate(date);
        await po.popup.waitForClosed();
      },
    ],
  },
  // ...
})
```
```javascript
// Новый подход
class PO extends AbstractPO {
  @Method()
  clickClose() {
    // Селекторы все уже в this
    return this.modal.clickClose();
  }
  @Method()
  async checked(weekDay: string) {
    const pressed = await this.day(weekDay).getAttribute('aria-pressed');
    return pressed === 'true';
  }
  // Описание вынесено в декоратор
  @Method('Получаем ID программы')
  async getProgramId() {
    const label = await this.idLabel.getText();
    return (label.match(/\d+/) || [])[0];
  }
  // Вычислимое описание тоже в декораторе - сигнатура должна принимать 
  // не больше параметров, чем сам метод
  @Method(date => `Устанавливаем дату ${moment(date).format('YYYY-MM-DD')}`)
  async selectDate(date: string) {
    await this.datepickerButton.click();
    await this.popup.waitForOpen();
    await this.datepicker.setDate(date);
    await this.popup.waitForClosed();
  }
}
export default new PO().makePO();
```
