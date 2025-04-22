# Baobab

Baobab - механизм логирования событий на клиенте. [Документация](https://wiki.yandex-team.ru/baobab/)

## Покрытие блока Баобабом

Для покрытие блока счетчиками используется HOC `withBaobab`.
Он читает данные из общего контекста счетчиков, вычисляет позицию в дереве и создает необходимые data-атрибуты, которые становятся доступны в компоненте через проп `counter`.

Пример:

``` tsx
import { compose } from '@yandex-turbo/core/hoc';
import { withDisplayName } from '@yandex-turbo/components/withDisplayName/withDisplayName';
import { withBaobab } from '@yandex-turbo/components/withBaobab/withBaobab';
import { IBaobabLogableComponent } from '@yandex-turbo/components/withBaobab/typings';

export interface ILinkProps extends IBaobabLogableComponent {
    url?: string;
    text?: string;
}

const LinkPresenter: React.SFC<ILinkProps> = props => (
    <a href={props.url} {...props.counter}>{props.text}</a>
);

export const Link = compose<ILinkProps>(
    withDisplayName('Link'),
    withBaobab({ name: 'link' })
)(LinkPresenter);
```

## Переопределение дефолтного счетчика блока

При вызове одного блока внутри другого, можно изменить дефолтный сечтчик вызываемого блока. Для этого надо вызываемому блоку в `props` надо передать `logNode`. Например:

```
<Link
    className={cls('link')()}
    text={props.localization.supportText}
    url={props.localization.supportUrl}
    logNode={{ name: 'link-support', attrs: { target: 'source', from: 'footer' } }}
/>
```

Параметр из `props.logNode` приоритетнее. Ссылка быдет залогировна с именем `link-support`, а не `link`.

**Важно:** Если встречаются 2 блока с одним именем на одном уровне вложенности, то механизм генерации уникальных идентификаторов поставит им одинаковые `id`, так как он работает опираясь на имя блока. Чтобы имена были разными, надо добавить параметр `pos` в `logNode.attrs`, который будет уникальным у каждого из этих блоков. Например:

```
<Link logNode={{ attrs: { pos: 1 } }} />
<Link logNode={{ attrs: { pos: 2 } }} />
```

## Как посмотреть на баобаб в логах

Для того, чтобы его найти, понадобится информация, которую выводит темплар при запуске:

```
clickdaemon запущен на порту 53059
Репорт-рендерер запущен на порту 53063, pid: 22144
Логи пишутся в директорию /Users/username/.yandex-int/logs/rr
```

### Blockstat-лог (серверные счетчики)

Полученное баобабное дерево (оно же "дерево показов", "счетчики показов", "серверные счетчики") пишется в blockstat-лог. Логи лежат в директории `/Users/username/.yandex-int/logs/rr`

`current-report-renderer_blockstat-53063` - имя blockstat-лога, где 53063 - порт на котором запущен репорт-рендерер

В логе дерево лежит следующим образом:

```
ÿ{"event":"show","tree":{"name":"$page","attrs":{"schema-ver":"0","ui":"touch","service":"turbo"},"id":"uniq15447766434821","children":[{"name":"$main","id":"uniq15447766434821","children":[{"name":"$result","attrs":{"type":"article"},"id":"uniq15447766434822","children":[{"name":"footer","id":"5h4ltaaar","children":[{"name":"link-full","attrs":{"target":"source","from":"footer"},"id":"5h4ltaaas"},{"name":"link-support","attrs":{"target":"source","from":"footer"},"id":"5h4ltaaat"}]}]}]}]}}
```

### Redir-лог (клиентские счетчики)

Клики пишутся в redir-лог. Логи лежат в директории `/Users/username/.yandex-int/logs/clickdaemon`

`redir-58096.log` - имя файла redir-лога, где 58096 - порт на котором запущен clickdaemon

Также срабатывание счетчиков на клик можно смотреть во вкладке network в виде:

```
https://olliva-1-ws1.si.yandex.ru/clck/safeclick/data=AiuY0DBWFJ5fN_r-AEszky6XRh2bw2-PxOhhGtBqVOkrm9QAV-BaBhX99nn7QU2q6FMnrPANkm-XVhn1sIu5dog31G10VwA5SE_RUBNOyBVP8W0cUfShJYfdswx_mqFXcPw6H798Tur2a2n4kCLXJorN4qdo0a8aAzmMcSDU3fV9wuTrqw94iVyZFNuw0cmysmtrV3NnQfK5l0v1Aovaf7AXEnDYn1E_ST0Zawioe1JECr_CCulsSNhR85VZx7KA9LgBtn4Fpbh2ssg-kyFMTf5-1WYLEMQPZBapuV65r5xjHmBWFW8iAGPWf2PN_r-N4eA8sUQ__cWFVH9Bo9txpgdTbK82-ysKb6Es-UOMirjW2bJqfqQQwU1xsy0KbfjfTFh9jO7-5K4pcLYM6tow2oNdIEcZ4xKTOwt0MCjlzAkpHJFqfmkOTOOOqkGiC-6KUtbYAYV287bbip0jYZ_cuZPORz1L-QpBatNxG-E31KjqDMyG2c8arHTC23PZX3DzSQ66whro_A4,/sign=f1c338753d5e34467ed7fd12031caa6e/keyno=0/vars=-baobab-event-json=%5B%7B%22event%22%3A%22click%22%2C%22id%22%3A%221ira35pxqo%22%2C%22cts%22%3A1544777857882%7D%5D/cts=1544777857882/*https://ya.ru/
```

Данные о баобабе лежат в `-baobab-event-json`

## Тестирование Баобаб-счетчиков в hermione

В Hermione-тестах можно проверять и счетчики показов, и клиентские счетчики.

### Серверный баобаб-счетчик

Для проверки наличия счетчика в баобабном дереве используется команда `.yaCheckBaobabServerCounter`. Например:

```
this.browser
    .yaCheckBaobabServerCounter({
        path: '$page.$main.$result.footer.link-full',
        attrs: { attrName: 'attrVal' }
    })
```

где в `path` указывается путь от корня дерева `$page`.

### Клиентский баобаб-счетчик

Для проверки срабатывания счетчиков на клик и другие клиентские взаимодействия используется команда `.yaCheckBaobabCounter`. Например:

```
this.browser
    .yaCheckBaobabCounter(PO.footer.links.fullVersion(), {
        path: '$page.$main.$result.footer.link-full'
    })
```

где в `path` указывается путь от корня дерева `$page`.
