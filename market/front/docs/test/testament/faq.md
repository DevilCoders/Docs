# Часто встречающиеся ошибки

В ходе использования тестамента программист может столкнуться с рядом ошибок.
Здесь будут представлены сами ошибки и способы их решений.

## Виды ошибок

### Self-invoking functions

Ошибка возникает при тестировании виджета, у которого в реакт компоненте присутствует самовызывающаяся функция.

**Пример**

```js
const InfoBonus = ({authRoute, isAuth}: Props) => {
    const InfoItem = ({children, iconName}) => (
    ...
);

    const manBlockContent = (function getContentByAuthStatus() {
        if (isAuth) {
            return (
                <InfoBonusText>
                    Только постоянные покупатели могут копить купоны&nbsp;
                    &mdash; не&nbsp;выходите из&nbsp;своего аккаунта.
                </InfoBonusText>
            );
        }

        return (
            <Zone name="infoBonusLoginLink" withVisibilitySensor>
                <InfoBonusText>
                    Чтобы копить купоны, нужно
                    <Link
                        route={authRoute}
                        dataAuto="register-link"
                    >
                        {' '}зарегистрироваться{' '}
                    </Link> или войти в&nbsp;личный кабинет.
                </InfoBonusText>
            </Zone>
        );
    }());

    return (
        <div className={styles.root}>
            ...
        </div>
    );
};
```

**Решение**

Избавиться от самовызывающейся функции вынесением оной из главного компонента, либо используя тернарный оператор.

### DataCloneError: autotestModifier(options) { ... }

Ошибка возникает при замене в `market/platform.desktop/configs/development/node.js` сервиса report с тестового на продовый.

**Решение**

Вернуть обратно тестовый сервис, либо положить в stash на время тестирования.

### Can't find mock for ...

Ошибка возникает, если в кадавре не реализован мок для пути из ресурса, либо мок есть, но ему не хватило каких-то данных в стейте

**Решение**

1. Проверяем ресурс по [инструкции](https://docs.yandex-team.ru/marketfront/test/testament/layers/kadavr#kak-opredelit-nuzhnyj-resurs).
2. Если нужный ресурс есть, то ищем ошибку в требующихся данных.

### Тест падает с Cannot add property data-tid, object is not extensible

Ошибка возникает при тестировании виджета, у которого присутствуют компоненты, вынесенные в переменные.

**Пример**

```js
const fullFiltersList = (
    <Fragment>
        {shouldRenderTyres && (
            <Fragment>
                <Slot name="tyresPopup" />
                <Slot name="filtersTyresEntry" />
            </Fragment>
        )}

        {filterGroupsOrder.map(groupName => (
            <FilterGroup
                key={groupName}
                filterIds={filterGroups[groupName]}
                filtersIdsWithPreviewMap={filtersIdsWithPreviewMap}
                kind={kind}
                noveltyFilter={noveltyFilter}
                showOnboarding={false}
                withReset={withReset}
            />
        ))}
    </Fragment>
);
```

```js
{(hasConfirmedFilters && !showPlaceholder)
    ? <SectionWrapper title="Остальные" theme="old">{fullFiltersList}</SectionWrapper>
    : fullFiltersList
}
```

**Решение**

Переделываем в функцию:

```js
const fullFiltersList = () => (
    <Fragment>
        {shouldRenderTyres && (
            <Fragment>
                <Slot name="tyresPopup" />
                <Slot name="filtersTyresEntry" />
            </Fragment>
        )}

        {filterGroupsOrder.map(groupName => (
            <FilterGroup
                key={groupName}
                filterIds={filterGroups[groupName]}
                filtersIdsWithPreviewMap={filtersIdsWithPreviewMap}
                kind={kind}
                noveltyFilter={noveltyFilter}
                showOnboarding={false}
                withReset={withReset}
            />
        ))}
    </Fragment>
);
```

```js
{(hasConfirmedFilters && !showPlaceholder)
    ? <SectionWrapper title="Остальные" theme="old"><fullFiltersList /></SectionWrapper>
    : <fullFiltersList />
}
```
