# TouchTable
Таблица для мобильных устройств

Предназначена для отображения данных в отчётах. Предоставляет набор компонентов, с помощью которых можно собрать полностью рабочую таблицу.

Пример:
```ts
<Table>
    <THead>
        <HeaderRow>
            <HeaderDimensionCell>Партнёры</HeaderDimensionCell>
            <HeaderCell>
                <Sortable>Установки</Sortable>
            </HeaderCell>
        </HeaderRow>
    </THead>
    <TBody>
        <TotalRow>
            <DimensionCell>
                <ColoredCheckbox
                    checkedBgColor="white"
                    uncheckedBgColor="white"
                    view="default"
                    size="s"
                    label="Итого"
                />
            </DimensionCell>
            <Cell>1600</Cell>
        </TotalRow>
        {rowsData.map(([partner, installs, color], idx) => (
            <Row key={partner}>
                <DimensionCell level={idx}>
                    <ColoredCheckbox
                        checkedBgColor={color}
                        view="default"
                        size="s"
                        checked={Boolean(idx)}
                        label={partner}
                    />
                </DimensionCell>
                <Cell>{installs}</Cell>
            </Row>
        ))}
    </TBody>
</Table>
```

## Доступные компоненты
Фундаментальные компоненты, повторяющие html теги: Table, BaseRow, Cell, THead, TBody

Продвинутые компоненты:
- Row, HeaderRow, TotalRow - tr, которые добавляют границу, и зазоры справа и слева.
- DimensionCell, HeaderDimensionCell - ячейка для первого столбца. Растягивается на всё оставшееся место, позволяет задать отступ