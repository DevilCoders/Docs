## FormGroup
```javascript
FormGroup.propTypes = {
        fields: PropTypes.array, // {name(required), label, type, initialValue, rules, help, ...additionalProps}[] где additionalProps - необходимые поля для различных типов компонент(options для select и т.д.)
        form: PropTypes.object, //  объект приходящий из Ant.Design From.Create
        label: PropTypes.string, // заголовок группы
        columnsCount: PropTypes.number, // количество колонок в группе
        defaultValues: PropTypes.object, // объект с ключами, совпадающими с name из fields
        stringTemplate: PropTypes.string // строка шаблон, `Hello, {user}`, где user, одно из полей в fields
};
```
Если в FormGroup передано свойство **stringTemplate**, то группа рендерится по строке шаблону, иначе как Grid

### FormField - базовый компонент Form, регистрируется в Ant.Form и отображает нужный тип Ant.Form компонента
```javascript
FormField.propTypes = {
        form: PropTypes.object.isRequired,
        item: PropTypes.shape({
            type: PropTypes.string, // 'select' | 'color' | 'checkbox' | 'multi-select' | 'boolean-select', 'text' by default
            name: PropTypes.string, // имя в модели формы
            label: PropTypes.string,
        }),
        initialValue: PropTypes.any,
        inline: PropTypes.bool // рендерится как 'inline-block'
}
```
### StringTemplate
```javascript
StringTemplate.propTypes = {
    stringTemplate: PropTypes.string,
    values: PropTypes.object // объект, где каждому ключу(ключ модели) соответсвует FormField
};
```
StringTemplate поддерживает создание своего паттерна, для этого используется функция makePattern

```javascript
import styled from 'styled-components';

const RedText = styled.span`
    color: #f5222d;
`;

const patterns = {
    red: makePattern(RedText) // red: ({children}) => <RedText
};
```

### Пример
```javascript
const stringTemplate = 
`SELECT <red>ts_agg_key</red>, {selection_rules[0]} AS value
FROM (
    SELECT <red>ts_key</red>, {selection_rules[1]}
    FROM (
        SELECT <red>ts_key</red>, <red>geohash_key</red>, {selection_rules[2]}
        FROM (
            SELECT <red>ts_key</red>, <red>geohash_key</red>, <red>car_class_key</red>, {selection_rules[3]}
            FROM {database}.{table}
            WHERE 1 = 1
                AND $conditions
        )
        GROUP BY <red>ts_key</red>, <red>geohash_key</red>
    )
    GROUP BY <red>ts_key</red>
)
GROUP BY <red>ts_agg_key</red>`;

const groups = [
        {
            label: translate({id: 'METRICS.NAME_PARAMETERS'}),
            fields: [
                {
                    name: '_id',
                    label: translate({id: 'METRICS.ID'}),
                    required: true
                },
                {
                    name: 'metric',
                    label: translate({id: 'METRICS.NAME'}),
                    required: true
                },
                {
                    name: 'en',
                    label: translate({id: 'METRICS.EN'}),
                    required: true
                },
                {
                    name: 'optgroup',
                    label: translate({id: 'METRICS.GROUP'}),
                    help: translate({id: 'METRICS.GROUP_HELP'}),
                    required: true
                },
                {
                    name: 'optgroup_en',
                    label: translate({id: 'METRICS.GROUP_EN'}),
                    required: true
                },
                {
                    name: 'desc',
                    label: translate({id: 'METRICS.DESC'})
                },
                {
                    name: 'desc_en',
                    label: translate({id: 'METRICS.DESC_EN'})
                }
            ]
        },
        {
            label: translate({id: 'METRICS.CLICK_HOUSE_REQUEST_PARAMETERS'}),
            stringTemplate: ClickHouseRequestPattern,
            fields: [
                {
                    name: 'selection_rules[0]',
                    required: true
                },
                {
                    name: 'selection_rules[1]',
                    required: true
                },
                {
                    name: 'selection_rules[2]',
                    required: true
                },
                {
                    name: 'selection_rules[3]',
                    required: true
                },
                {
                    name: 'database',
                    required: true
                },
                {
                    name: 'table',
                    required: true
                }
            ]
        }
];


class MyForm extends React.Component {
    render() {
        return (
             <Form onSubmit={this.handleSubmit}>
                    {groups.map(({label, fields, stringTemplate}) => (
                        <FormGroup
                            key={fields[0].name}
                            form={form}
                            stringTemplate={stringTemplate}
                            fields={fields}
                            label={label}
                            columnsCount={3}
                            defaultValues={data}
                        />
                    ))}
             </Form>
        );
    }
}

export default Form.create()(MyForm);
```
![](https://jing.yandex-team.ru/files/russhakirov/Screen%20Shot%202018-11-09%20at%2016.47.47.png)