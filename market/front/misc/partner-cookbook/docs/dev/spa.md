# SPA

## Как перевести страницу в SPA

Процесс перевода временно находится на вики: https://wiki.yandex-team.ru/users/tzota/market/tutorials/vedjomstranicupivspa/

Перенесён сюда будет в ближайшее время после реализации одного блокирующего тикета

## Ключевые места

### Продуктовое

Реакт-роуты спа-страниц https://a.yandex-team.ru/arc/trunk/arcadia/market/front/apps/partner/client.next/routes/
Там также находится файл spaApplication.tsx, в котором эти роуты регистрируются

Резолверы инишел стейтов: https://a.yandex-team.ru/arc_vcs/market/front/apps/partner/shared/resolvers/spaInitialStateResolvers
В том числе один-общий-обвязочный - defaultInitialState (то, что раньше находилось в makeHtmlPage)

### Инфраструктура

-   Загрузка данных и чанка новой страницы: https://a.yandex-team.ru/arc/trunk/arcadia/market/front/apps/partner/client.next/routes/utils/lazyPageLoader.tsx
-   Загрузка i18n https://a.yandex-team.ru/arc/trunk/arcadia/market/front/apps/partner/client.next/hooks/useI18nFetch/index.ts
-   Подмена страничных эпиков-редьюсеров после загрузки данных https://a.yandex-team.ru/arc/trunk/arcadia/market/front/apps/partner/client.next/hooks/useSpaWrapper/index.tsx
-   Редьюсер спа-страниц: https://a.yandex-team.ru/arc/trunk/arcadia/market/front/apps/partner/client.next/reducers/spaReducers/initialState.ts
-   Инишел стейт - общий и страничные: https://a.yandex-team.ru/arc_vcs/market/front/apps/partner/shared/resolvers/spaInitialStateResolvers

## FAQ

Q: Вопрос, а у нас нет умного линк-роутер компонента, который можно использовать для всех видов ссылок?  
A: По-простому можно импортировать Link из реакт-роутера и построить ссылку на ней. Но это, наверное, нехорошо, потому что мы должны использовать левитановский линк.  
У нас есть вот такая реализация аналога [~/containers/Link](https://a.yandex-team.ru/arcadia/market/front/apps/partner/client.next/containers/Link/Link.tsx?rev=r9640375#L48) но для СПА.  
Наружу она [проброшена](https://a.yandex-team.ru/arcadia/market/front/apps/partner/client.next/containers/Link/index.tsx?rev=r9640375#L75) только с платформенным енхансом.  
Наверное, если ты точно знаешь, что у тебя переход на СПА-страницу и не хочешь, чтобы enhance ходил в стейт за платформой, то мы должны где-нить в папке ~/components сделать что-то аналогичное SpaLink, чтобы там левитановский линк был проброшен в пропсу component реакт-роутерной линки. Но пока не очень понятно, надо оно нам или нет. В принципе, сейчас в большинстве случаев можно использование левитановского линка поменять на SpaPlatformLink, а дальше разберёмся.  
В результате если в неё передадут обычный роут, то отрисуется обычная линка, а если SPA-шный - то реакт-тоутерная.

Q: У меня два заголовка!  
А: Добавлю это в вики, когда разблокируется страница.  
Надо выпилить заголовок с сервера и перенести на клиента.  
[На сервере](https://a.yandex-team.ru/review/2612056/files/4#file-0-186488610:R27) можно оставить title и LayoutHeader в null.  
А всю логику [украсть с сервера](https://a.yandex-team.ru/review/2612056/files/4#file-0-186488611:L16), адаптировать [на клиента](https://a.yandex-team.ru/review/2612056/files/4#file-0-186488624), заюзав там `import {LayoutHeader} from '~/components/LayoutHeader';`  

Q: На фронте куча ошибок типа "cannot read properties of undefined (reading foobar)  
A: При повторном заходе на SPA-страницу компонент подгружается из кэша и маунтится моментально. Но при этом в стейте ещё пусто, данные не пришли. Хоть компонент при этом ещё не видно, в консоли уже есть ошибки.  
Предлагается временное решение [насувать в стейт](https://a.yandex-team.ru/arcadia/market/front/apps/partner/client.next/routes/OnboardingRouter.tsx?rev=r9574625#L11) значений-заглушек. Раут подложит их перед сменой страницы и она не будет ругаться.   
Будет исправлено в https://st.yandex-team.ru/MARKETPARTNER-41386
Если есть желание, то NullInitialState можно протипизировать с помощью `DeepPartial<InitialPageState>`, где `DeepPartial` - хелперный типизатор, делающий все поля в глубину необязательными (импортится из `@yandex-market/b2b-core/shared/types`), а `InitialPageState` - тип вашего страничного инишел стейта. Не спасёт от всех случаев, но частично может помочь на то время, пока MARKETPARTNER-41386 не доедет.  

Q: Кнопка "назад" иногда срабатывает вхолостую.  
A: Там [все сложно](https://st.yandex-team.ru/MARKETPARTNER-41489), но если не вдаваться в подробности, то алгоритм следующий:
-    Если на странице нет ни `page`, ни `pageSize`, например сводка или страница заказа, то в конфиге страницы надо прописать пустой массив stateList:
```javascript
const config = Config({
    epics,
    reducers,
    stateManagerConfig: {
        stateList: [],
    },
});
```
- Если на странице имеется постраничка и пейджер смотрит в `app.state`, то: 
    - в appStateManager должны попасть значения `['page', 'pageSize']`. Для этого либо `stateList` либо должен вообще отсутствовать в конфиге страницы (и тогда заполнится нужными значениями из умолчаний), либо в вашем `stateList` среди прочих параметров должны присутствовать и эти.
    - в резолвере страничного инишел стейта в `app.params` и в `app.state` (в оба!), должны попасть `page` и `pageSize`
- Если в вашей постраничке вы используете пейджер в режиме `useAppParams`, и вся постраничка идёт через `applyParams`, и в стейте пусто - то менять ничего не надо, у вас и так всё сломано ))
