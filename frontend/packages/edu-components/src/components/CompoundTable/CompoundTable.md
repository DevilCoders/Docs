# CompoundTable

<!-- description:start -->
Используется для создания таблиц со скролящейся правой частью и панелью с контролами.
<!-- description:end -->

## Пример использования

```ts
class App extends Component<{}, IState> {
  // ...

  public render() {
    return (
      <CompoundTable
        headerHeight={44}
        controlsHeight={48}
        fixedColumns={2}
        content={{
          headings: [
            'Дата',
            'Посылка',
            'Задача',
            'Участник',
            'Вердикт',
            'Баллы',
            'Время',
            'Память',
          ],
          rows: [
            [
              '12:08:24 15.05',
              <a href="/">4621134</a>,
              'A',
              'MrSidney',
              'OK(0)',
              '0,12345',
              '63 ms',
              '4.4 MB',
            ],
            [
              '12:08:24 15.05',
              <a href="/">4621134</a>,
              'A',
              'MrSidney',
              'OK(0)',
              '0,12345',
              '63 ms',
              '4.4 MB',
            ],
          ],
        }}
        controls={
          <div>
            <Button theme="normal" size="m">
              Изменить
            </Button>
            <Button theme="normal" size="m">
              Пересудить
            </Button>
          </div>
        }
        areControlsVisible={this.state.areControlsVisible}
      />
    );
  }
}
```

## Свойства

<!-- props:start -->
| Свойство            | Тип                                                                                                                                                                                                                                                               | По умолчанию | Описание                                                                                                     |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ------------------------------------------------------------------------------------------------------------ |
| content             | `ITableContent`                                                                                                                                                                                                                                                   | —            | Содержимое таблицы.                                                                                          |
| fixedColumns?       | `number`                                                                                                                                                                                                                                                          | `0`          | Количество зафиксированных колонок в левой части.                                                            |
| headerHeight?       | `number`                                                                                                                                                                                                                                                          | —            | Высота шапки.                                                                                                |
| controls?           | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | —            | Отрендеренный компонент, который будет располагаться в плашке для контролов.                                 |
| controlsHeight?     | `number`                                                                                                                                                                                                                                                          | —            | Высота плашки, в которой будут располагаться контролы.                                                       |
| areControlsVisible? | `false \| true`                                                                                                                                                                                                                                                   | `false`      | Булево значение, для управления отображением плашки с контролами.                                            |
| innerRef?           | `RefObject<HTMLDivElement>`                                                                                                                                                                                                                                       | —            | Ссылка на корневой DOM-элемент компонента.                                                                   |
| className?          | `string`                                                                                                                                                                                                                                                          | —            | Дополнительный className.                                                                                    |
| spinner?            | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | —            | Спинер для показа во время загрузки вместо тела таблицы.                                                     |
| emptyPlaceholder?   | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | —            | Плейсхолдер для пустой таблицы.                                                                              |
| overlapColor?       | `string`                                                                                                                                                                                                                                                          | `'#fff'`     | Цвет перекрытия тени. Скорее всего, вы хотите, чтобы он был равен цвету фона, на котором расположена таблица |
<!-- props:end -->

## Модификаторы

<!-- modifiers:start -->
### withShadows

Задает отображение теней.

**Допустимые значения:** `false`, `true`.
<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/CompoundTable)
