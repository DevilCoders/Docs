# DifferenceKit + KotlinNative

Для каждого мультиплатформенного экрана из мультиплатформы торчит интеррактор с интерфейсом:

```
	protocol MyScreenInteractor {
		func dispatch(action: MyScreenAction)
		func viewStates() -> Observable<[MyScreenItem]>
	}
```

Чтобы отрендерить очередное изменение интерфейса на платформе нужно высчитать диф между предыдущем значением `viewStates` и текущим.
Для этого используем `DifferenceKit`.

Примеры использования: <br />
[TableView/DiffableTableViewController.swift](./TableView/DiffableTableViewController.swift) <br />
[CollectionView/DiffableCollectionViewController.swift](./CollectionView/DiffableCollectionViewController.swift)

`DiffableDataSource` - обертка над даниными, которая позволяет удобно посчитать дифф.

`UITableView.reload(...)`  - экстеншен, который для анимированного применения дифа.

На каждое изменение viewState мы должны вызвать `.reload(...)` у `UITableView` или `UICollectionView`

-

### Анимированное изменение контента в ячейках

По умолчанию `UITableView.reload(...)` для ячейки, у которой изменился контент вызовет  reloadRows  и тем самым сделает невозможным кастомные анимации.

Для замены  reloadRows  на ручное обновление содержимого ячейки нужно реализовать `UITableViewDiffDataSource`

```
	public enum UITableViewDiffableRenderCellResult {
		case rendered
		case needsToReload
	}

	public protocol UITableViewDiffDataSource: UITableViewDataSource {
		func tableView(_ tableView: UITableView, tryRenderCell cell: UITableViewCell, forRowAt indexPath: IndexPath)
		-> UITableViewDiffableRenderCellResult
	}
```


В этом методе мы можем самостоятельно изменить содержимое ячейки или вернуть `.needsToReload` , тогда будет вызван  reloadRows  для этой ячейки.

-

### Базовые ячейки
`GenericTableViewCell`, `GenericAnimatedTableViewCell`,  `GenericCollectionViewCell` и `GenericAnimatedCollectionViewCell` - базовые ячейки для мультиплатформенных экранов.

Для этих ячеек уже реализованы хелперы экстеншены, чтоб удобней доставать ячейку и наполнять ее данными.

```
	tableView.dequeueCellAndRender(ofType: MyTableTextCell.self, viewState: x, for: indexPath)
```

Примеры таких ячеек: <br />
[TableView/Cells](./TableView/Cells) <br />
[CollectionView/Cells](./CollectionView/Cells)

-

### Реализация DataSource / Delgate

Обычно для описания ячеек используются sealed class-ы.
Поэтому в каждом методе `DataSource` / `Delgate` мы кастим айтем к конкретному типу: <br />
[TableView/DiffableTableViewController.swift](./TableView/DiffableTableViewController.swift) <br />
[CollectionView/DiffableCollectionViewController.swift](./CollectionView/DiffableCollectionViewController.swift)

-

### DiffableTableViewAdapter

Чтобы избавится от буллерплейтного кода с кучей кастов воспользуйся  `DiffableTableViewAdapter`

Адаптер реализует `UITableViewDelegate`, `UITableViewDataSource`, `UITableViewDiffDataSource` и предоставляет декларативный API для работы с типизированной ячейкой и вью моделью.

Пример: <br />
[TableView/DiffableTableViewControllerWithUsingAdapter.swift](./TableView/DiffableTableViewControllerWithUsingAdapter.swift)

Вся работа с ячейкой описывается в одном месте при регистрации ячейки.
Адаптер из коробки умеет работать с `GenericTableViewCell` и  `GenericAnimatedTableViewCell`.

Для `GenericTableViewCell` вытоматически будет вызываться `.render(viewState)`.

В самом простом случае можно зарегистрировать ячейку и она будет корректно отображаться с тем `viewState`, который прилетел из мультиплатформы:

```
	tableViewAdapter.registerCell(ofType: DiffableTableButtonCell.self)
```


Сделать обработку нажатий или другие настройки можно в замыканиях при регистрации ячейки:

```
	tableViewAdapter.registerCell(
		ofType: DiffableTableButtonCell.self,
		prepareCell: { [weak self] cell, viewState in
			cell.onButtonTap = { [weak self] in 
				self?.interactor.dispatch(action: .select(itemId: viewState.itemId)) 
			}
		},
		didSelect: { [weak self] viewState in
			self?.interactor.dispatch(action: .select(itemId: viewState.itemId))
			return .deselect
		},
		shouldHighlight: { _ in false }
	)
```

Для `GenericAnimatedTableViewCell` будет вызваться `.render(viewState, animated: true)` вместо `UITableView.reload(...)`

Пример одинакового экрана с адаптером и без: <br />
[TableView/DiffableTableViewController.swift](./TableView/DiffableTableViewController.swift)<br />
[TableView/DiffableTableViewControllerWithUsingAdapter.swift](./TableView/DiffableTableViewControllerWithUsingAdapter.swift)

Если будет нахватать реализованных методов `DataSource` / `Delgate` то их можно добавить в адаптер.

-

### YandexMapsOverlayScreen.OverlayScreenContent

Чтоб было проще встраивать мультиплатформенный экран в карточку
`DiffableTableViewAdapter` предоставляет `scrollDelegate`, который нужен для реализации `OverlayScreenContent`.