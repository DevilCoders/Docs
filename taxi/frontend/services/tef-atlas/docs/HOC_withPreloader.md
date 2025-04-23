### withPreloader({statusPath, loader}) 
Это HOC для отображения индикатора загрузки на месте компонента, если данные находятся в статусе **pending**

#### statusPath: string | array
Путь в **ReduxState**, который отображает статус загрузки данных, вызванных в **loader** (для получения значения из **ReduxState** изпользуется **lodash/get**)
#### loader: function
Функция вызываемая в **componentDidMount** с аргументом **dispatch**

### Пример использования
```javascript
class MyPage extends React.Component {}

export default withPreloader({
	statusPath: 'MY_PAGE.items.status', 
	loader: dispacth => dispatch(MyApi.loadItems())
})(MyPage);
```

Ожидается, что запрос **MyApi.loadItems** будет дополнительно обработан **Redux** экшенами, которые вызывают изменения в **ReduxState** с проставлением статусов загрузки (**pending**, **success**, **failed**)
Ожидается, что запрос MyApi.loadItems будет дополнительно обработан Redux экшенами, которые вызывают изменения в ReduxState с проставлением статусов загрузки (pending, success, failed)