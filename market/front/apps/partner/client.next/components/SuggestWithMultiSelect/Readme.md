# Компонент SuggestWithMultiSelect

Компонент предназначен для отображения списка элементов с возможностью выбора нескольких по ключам, с поиском, постраничной ленивой загрузкой, кастомизацией вьюх отдельных элементов, автопрокруткой к выбранным в списке и т.д.

## Пример описания полей

```jsx static
const suggestProps = {
    // Каллбек загрузки данных
    loadAction?: ({part, size, nextPageToken}) => void;
    // Массив элементов
    items: [];
    // Токен след страницы для ленивой загрузки
    nextPageToken?: '';
    // Ключи выбранных элементов
    selectedKeys?: [];
    // Каллбек для выбора элементов по ключам
    onChange: (selectedKeys) => void;
    // Кол-во элементов грузящихся за один раз
    pageSize?: number;
    // Каллбеки с переводами, нужны чтобы избежать проблем с неподтягивающимися ключами переводов на стендах
    i18nBtnSelected: () => '';
    i18nNotFoundMessage?: () => '';
    i18nSearchPlaceholder?: () => '';
    i18nBtnNotSelected?: () => '';
    // Каллбеки для получения значений из эелемента
    getItemKey?: (item) => '';
    getItemName?: (item) => '';
    getItemHint?: (item) => '';
    getItemDisabled?: (item) => false;
    // Ширина попапа с саджестом
    width?: string;
    // Вьюха отдельного элемента
    itemComponent?: <Item />;
    // Каллбек для того чтобы менять логику выбора ключей, например можно при условии сбрасывать выбранные ранее ключи или выбрать дополнительные
    handleNewKeys?: (keys, newKey) => [];
    // Флаг по которому саджест скрывается при выборе элемента
    applyByClick?: false;
    // Класс для попапа с саджестом
    popupClassName?: '';
    // Флаг блокирующий компонент
    disabled?: false;
};
```

## Пример с поиском и ленивой загрузкой

```jsx
type StateToProps = {
    shopSkus: string[];
    items: ShopSkuInfo[];
    nextPageToken?: string;
};

type DispatchToProps = {
    applyParam: (a: Record<string, string[]>) => void;
    loadFiltersGoodsData: (a: {part: string; size?: number; nextPageToken?: string}) => void;
};

type Props = StateToProps & DispatchToProps & I18nProps;

const getItemKey = ({shopSku}: ShopSkuInfo) => shopSku;
const getItemName = ({title}: ShopSkuInfo) => title;
const getItemHint = ({shopSku}: ShopSkuInfo) => `SKU ${shopSku}`;

const GoodsSuggest = ({i18n, shopSkus, items, nextPageToken, loadFiltersGoodsData, applyParam}: Props) => {
    return (
        <SuggestWithMultiSelect<ShopSkuInfo>
            loadAction={loadFiltersGoodsData}
            items={items}
            nextPageToken={nextPageToken}
            selectedKeys={shopSkus}
            onChange={ids => applyParam({shopSkus: ids})}
            getItemKey={getItemKey}
            getItemName={getItemName}
            getItemHint={getItemHint}
            i18nBtnSelected={params => i18n`pages.supplier-sales-statistics:goods-suggest.selected-count`.with(params)}
            i18nBtnNotSelected={() => i18n`pages.supplier-sales-statistics:filter.not-selected`}
            i18nNotFoundMessage={() => i18n`pages.supplier-sales-statistics:goods-suggest.not-found-message`}
            i18nSearchPlaceholder={() => i18n`pages.supplier-sales-statistics:goods-suggest.search-placeholder`}
            width="700px"
            pageSize={50}
        />
    );
};

export {GoodsSuggest as Base};

const mapStateToProps = (state: State): StateToProps => ({
    shopSkus: getArrayParam(state, 'shopSkus'),
    items: selectFiltersGoodsState(state),
    nextPageToken: selectFiltersGoodsNextPage(state),
});

const mapDispatchToProps: DispatchToProps = {
    applyParam,
    loadFiltersGoodsData,
};

export const enhance: HOC<Props, {}> = compose(connect(mapStateToProps, mapDispatchToProps), withI18n);

export default enhance(GoodsSuggest);
```

## Пример с поиском и "древовидным" выбором категорий

Работает через утилиты getAllKeys, getLastKeys, handleCategoriesKeysOnSelect

handleCategoriesKeysOnSelect - отвечает за выбор ключа, если выбираем элемент и у него есть дочерние, то они все выбираются

getAllKeys - возвращает все родительские ключи вместе с поданными на вход ключами листовых узлов

getLastKeys - возвращает ключи листовых узлов по поданным на вход ключам

```jsx
type StateToProps = {
    categories: string[];
    items: Category[];
};

type DispatchToProps = {
    applyParam: (a: Record<string, string[]>) => void;
    loadFiltersCategoriesData: (a: {part: string}) => void;
};

type Props = StateToProps & DispatchToProps & I18nProps;

const getItemKey = ({id}: Category) => String(id);
const getItemName = ({name}: Category) => name;

const CategoriesSuggest = ({i18n, categories, items, loadFiltersCategoriesData, applyParam}: Props) => {
    return (
        <SuggestWithMultiSelect<Category>
            loadAction={loadFiltersCategoriesData}
            items={items}
            selectedKeys={getAllKeys(items)(categories)}
            onChange={ids => applyParam({categories: getLastKeys(items)(ids)})}
            getItemKey={getItemKey}
            getItemName={getItemName}
            handleNewKeys={handleCategoriesKeysOnSelect(items)}
            i18nBtnSelected={params =>
                i18n`pages.supplier-sales-statistics:categories-suggest.selected-count`.with(params)
            }
            i18nBtnNotSelected={() => i18n`pages.supplier-sales-statistics:filter.not-selected`}
            i18nNotFoundMessage={() => i18n`pages.supplier-sales-statistics:categories-suggest.not-found-message`}
            i18nSearchPlaceholder={() => i18n`pages.supplier-sales-statistics:categories-suggest.search-placeholder`}
            width="700px"
        />
    );
};

export {CategoriesSuggest as Base};

const mapStateToProps = (state: State): StateToProps => ({
    categories: getArrayParam(state, 'categories'),
    items: selectFiltersCategoriesState(state),
});

const mapDispatchToProps: DispatchToProps = {
    applyParam,
    loadFiltersCategoriesData,
};

export const enhance: HOC<Props, {}> = compose(connect(mapStateToProps, mapDispatchToProps), withI18n);

export default enhance(CategoriesSuggest);
```
