## Quick Start Guide

### Шаг 1. Чекаут репозитория и поднятие инстанса
Для начала необходимо клонировать репозиторий Геохелпера и запустить инстанс.
Для примера я буду использовать инстанс морды **v173d1** и, во избежание путаницы, инстанс геохелпера **d1**.

Замени в коде ниже d1 на свой инстанс (d1/d2/d3 etc.) и выполни его в консоли :)

```
sudo mkdir /opt/www/geohelper-d1
sudo chown $USER. /opt/www/geohelper-d1
git clone git@github.yandex-team.ru:morda/geohelper.git /opt/www/geohelper-d1
cd /opt/www/geohelper-d1
make conf dev start
```

Проверить, что инстанс собрался и запустился, можно, запустив логирование с помощью:
```
make log
```

Если нет ошибок (обычно выделяются красным) и есть следующие отбивки - все хорошо.
```
[nodemon] 2.0.2
[nodemon] to restart at any time, enter `rs`
[nodemon] watching dir(s): *.*
[nodemon] watching extensions: js,mjs,json
[nodemon] starting `/opt/nodejs/12/bin/node debug_server.js`
18:16:40.770 [551998] [INFO] debug server started. Starting debug server. PID: 551998 Nodejs version: v12.14.1 
18:16:41.257 [551998] [INFO] app started on /tmp/geohelper.d1.0.sock 
```

### Шаг 2. Переводы, название и описание
Для заведения блока тебе рано или поздно понадобятся переводы с названием и описанием блока. 
Заведем их сразу. В дальнейшем значение ключей можно будет поменять. Также на данном этапе пора придумать id (если его еще нет).

Допустим id нашего блока - **myblock**.

{% note info %}

По-умолчанию мы считаем, что блок реализован на **Div 2**. Если в конкретном случае это не так - лучше отразить это в id. К примеру **myblock_div** для **Div 1** блока. 

{% endnote %}


[Кликай, чтобы попасть в танкер (Home > geohelper)](https://tanker.yandex-team.ru/?project=home&branch=master&keyset=geohelper)

Переходим по ссылке и заводим два ключа наподобие:
* **myblock.title** - название
* **myblock.description** - краткое описание

После заведения необходимо подтянуть переводы на инстанс морды и геохелпера с помощью
```
cd /opt/www/morda-v173d1
make lang restart
cd /opt/www/geohelper-d1
make lang stop start
```
### Шаг 3. Заводим экспорты


Идем в MADM вашего инстанса (https://madm-v173d1.wdevx.yandex-team.ru) и редактируем следующие экспорты:

#### subs_cards_v3 **(Для ПП)**
 
geos| content| lang| block_id| topic_card | type| title|	default|	order|	app_platform|	app_version_min|	app_version_max|	os_version_min|	description|snackbar|	icon|	exp|	from|	till|	disabled|	delete
:--- | :--- | :--- | :--- | :--- |:--- |:--- |:--- |:--- |:--- |:--- |:--- |:--- |:--- |:--- |:--- |:--- |:--- |:--- |:--- |:---  
`10000`| api_search_2_only| all| `myblock`| `myblock_card`| `card`| `geohelper.myblock.title` | 1| `73` **(последний в экспорте + 1)** | `android` **(для тестирования на android)** | `8010100` **(для тестирования)**| | |`geohelper.myblock.description` | `api_search.menu.undo_snackbar_text` | | | | | | 

#### div_blocks_api

content|	id|	json_data|	description|	exp|	exp_except|	disabled|	delete
:--- | :--- | :--- | :--- | :--- |:--- |:--- |:--- 
api_search_2_only | `myblock` | `{"api_search_redefine_type": "div2", "show": 1, "api_search_heavy": "myblock", "heavy_data": { "type": "div2", "id": "myblock", "ttl": 400, "ttv": 1200 }}`| `div2 Тестовый блок для ПП на android` | | | |

#### inserts_api

domain|	geos|	content|	id|	position|	shuffle|	filter|	exp|	exp_except|	app_platform|	app_version_min|	app_version_max|	os_version_min|	os_version_max|	bk_tag|	disabled|	delete
:--- | :--- | :--- | :--- | :--- |:--- |:--- |:---|:---|:---|:---|:---|:---|:---|:---|:---|:---
all| `10000` | api_search_2_only | `myblock` | `40` | `0` | | | |android| `8010100` | | | | | |  

### Шаг 4. Добавляем блок
Создаем **папку**:
```
server/api/v3/divproxy/blocks/div2/app/myblock
```
И **файлы**:

{% note tip %}

Создавай файлы в указанном ниже порядке - так компилятор не будет ругаться на несуществующие импорты.

{% endnote %}

{% cut "config.ts" %}

```
import {AppDivOptions} from '../../../app-div-options';
import {RequestParams} from '../../../div-data-provider';

export const config = {
    id: 'myblock' // Поменять на id вашего блока
};

export function requestBuilder(opts: AppDivOptions): RequestParams {
    
    return {
        options: {
            timeout: 300,
            retries: 1
        },
        url: {
            protocol: 'http',
            hostname: 'paste.yandex-team.ru/4125785/text'
        }
    };
}
```
{% endcut %}

{% note info %}

В файле `config.ts` не забудь поменять поле id на id своего блока (если отличается от myblock)

{% endnote %}

{% cut "data.ts" %}
```
export interface HandleData {
  text: string,
}

export function validator(data: HandleData): boolean {
  return Boolean(data && data.text);
}
```
{% endcut %}

{% cut "templates.ts" %}
```
import {commonRedesignTemplates, GRAY_COLOR} from '../common/_redesign/templates';
import {
    templateHelper,
} from 'divcard2';

const newTemplates = {
    ...commonRedesignTemplates
    // Сюда вам предстоит добавить собственные шаблоны
};

export function templates() {
    return newTemplates;
}

export const thelperRedesign = templateHelper(newTemplates);
```
{% endcut %}

{% cut "renderer.ts" %}
```
import {
    Block,
} from 'divcard2';
import {thelperRedesign} from './templates';
import {makeHeader} from '../common/_redesign/templates';
import {config} from './config';
import {AppDivOptions} from '../../../app-div-options';
import {I18n} from '@divproxy/i18n';
import { HandleData } from './data';


export function blockRenderer(i18n: I18n, opts: AppDivOptions, data: HandleData): Block {
    return thelperRedesign.ghRedesignBlock({
        items: [
            makeHeader({
                id: config.id,
                i18n,
                title: data.text,
                titleUrl: '/', 
                customIcon: 'https://yastatic.net/s3/home/yandex-app/verticals_v2/staff_new/home.2.png',
                opts
            })
        ]
    });
}

```
{% endcut %}

{% cut "index.ts" %}
```
import {config, requestBuilder} from './config';
import {makeAppDivHandler} from '@divproxy/blocks/app-div-handler';
import {validator} from './data';
import {makeAppDiv2CardRenderer} from '../app-div2-helpers';
import {blockRenderer} from './renderer';
import {templates} from './templates';

const renderer = makeAppDiv2CardRenderer(config.id, blockRenderer);

export default makeAppDivHandler(
    config,
    requestBuilder,
    validator,
    renderer,
    templates
    );
```
{% endcut %}

В **файле** 
```
server/api/v3/divproxy/blocks/div2/app/index.ts
```  
импортируем созданный блок
```
import MyBlock from './MyBlock'
```
и добавляем в массив **cards**
```
export const cards: AppDivHandler<any, any>[] = [
    MyBlock,
    NewsFeed,
    NewsVideo,
    NewsUnitFeed,
    .......
```
### Шаг 5. Настраиваем ПП
Ищем в debug-панели раздел Custom hosts и редактируем следующие поля:
#### HOST_HOME
```
http://www-v173d1.wdevx.yandex.ru/portal/api/search?geohelper_host=http://geohelper-v173d1.wdevx.yandex.ru/
```

{% note alert %}

В зависимости от используемого устройства\эмулятора и сертификатов на нем параметр `geohelper_host` может работать некорректно c `http` - запрос будет приходить в инстанс морды **(v173d1)**, однако не доходить до инстанса геохелпера (в этом случае при выполнении `make log` в инстансе ГХ запрос не отобразится в логах).
В этом случае стоит попробовать `https`

{% endnote %}

#### HOST_HOME_TOPICS
```
http://www-v173d1.wdevx.yandex.ru/portal/subs/config/0
```

{% note info %}

Не забудьте заменить инстансы в ссылках (**v173d1**) на собственные 

{% endnote %}

После чего в настройках приложения (иконка с шестеренкой) идем в раздел **"Очистить данные"**, в появившемся окне выделяем галками **все пункты** и жмем на кнопку **"Очистить данные"**.

**Перезагружаем** приложение и входим в аккаунт (опционально).

После этих действий в настройках ленты появится ваш блок (названный ключами из танкера), а сам блок - в ленте!

![Пример](https://jing.yandex-team.ru/files/obi-wan/2021-03-09T18:34:09Z.dd2f89c.png =290x500)

{% note tip %}

Для того, чтобы было проще найти блок, можно выключить ненужные блоки и ленту Дзена (потребуется перезагрузка) в настройках приложения.

{% endnote %}
