# Единый роутинг

`react-router` не умеет генерировать ссылки, что является большой проблемой.
Поэтому есть форк [react-router-susanin](https://a.yandex-team.ru/arcadia/classifieds/react-router-susanin),
где урл-матчер заменен на susanin.

## Как это работает

Чтобы проекты могли генерировать кросс-ссылки (например, desktop<->mobile),
все роуты лежат в `auto-core/router` в папках с названием домена.

Внутри есть разделение на `server` и `react`, потому что роутинг происходит немного по-разному.

Получается так:
```
router/
  m.auto.ru/
    routes.js // общие роуты для домена
    react/
      link.js
      routes.js // тут описывается связка "роут - компоненты"
      router.js
    server/
      link.js
      router.js
```

В `routes.js` хранится связка "роут - компоненты", которая декларируется следующим образом:
 ```
 const routes = require('../routes');
 const extendRoutes = require('@vertis/react-router-susanin').extendRoutes;

 module.exports = extendRoutes(routes, {
     'catalog-card': [App, CatalogApp, CatalogCardPage],
     'catalog-card-equipment': [App, CatalogApp, CatalogCardEquipmentPage],
 });
 ```

В переводе на синтаксис `react-router` это означает
 ```
 <Router component={App}>
   <Router component={CatalogApp}>
     <Router component={CatalogCardPage}/>
   </Router>
 </Router>
 ```

Для каждого реакт-роута надо поставить специальный флаг.
  ```
  {
      name: 'dealer-marks',
      pattern: '/dealer-marks/',
      data: {
          controller: 'dealer-marks',
          react: true // флаг, что страница рисуется реактом
      }
  }
  ```

## Генерация ссылок в react

Функция `link` пробрасывается через context, поэтому компоненту надо сделать так
```
class MyComponent extends React.PureComponent {
    render() {
       const {link} = this.context;
       return (
          <div>
            {link('my-route')}
          </div>
       );
    }
}

MyComponent.contextTypes = {
  link: PropTypes.func.isRequired
}
```

# Подводные камни сусанина

* Если в условиях для параметра необходимо указать необязательные части, то всегда делаем это через конструкцию `(?:<выражение>)`. Так мы исключаем эту часть из внутреннего цикла обработки параметров сусанином и получаем разобранные get параметры.

Пример: `certification_id: '\\d+(?:-\\w+)?'`

* Никогда не проставляем ^ и $ в условиях для параметра, так как внутри сусанина происходит склейка полной регулярки для всего урла
