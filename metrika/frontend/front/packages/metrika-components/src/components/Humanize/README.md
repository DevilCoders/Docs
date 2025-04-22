Компонент для преобразования данных в читаемый / человеческий вид.

Содержит набор базовых типов для форматирования, которые будут доступны при импорте блока в сторонний проект.

Для добавления кастомных типов специфичных для вашего проекта или для ускорения разработки, в компонент можно передать свои обработчики использую TS Generic.

Примеров использования см. в папке \_\_tests\_\_ (в styleguide не работают Generic компоненты)

```jsx
const arr = Array(10).fill(Math.random());

<div>
    <article>
        <h4>Percentage</h4>
        <div style={{ margin: '5px 0' }}>
            0 = 
            <Humanize value={0} type="percentage">
                {(v) => v}
            </Humanize>
        </div>
        {arr.map((base, idx) => {
            const value = base * Math.pow(10, -5 + idx);

            return (
                <div style={{ margin: '5px 0' }} key={idx}>
                    {value} = 
                    <Humanize value={value} type="percentage">
                        {(v) => v}
                    </Humanize>
                </div>
            );
        })}
        <h5>With approximate value</h5>
        <div style={{ margin: '5px 0' }}>
            0 = 
            <Humanize value={0} type="percentage" approximationThreshold={0.02}>
                {(v) => v}
            </Humanize>
        </div>
        {arr.map((base, idx) => {
            const value = base * Math.pow(10, -3 + idx);

            return (
                <div style={{ margin: '5px 0' }} key={idx}>
                    {value} = 
                    <Humanize value={value} type="percentage" approximationThreshold={0.02}>
                        {(v) => v}
                    </Humanize>
                </div>
            );
        })}
    </article>
    <article>
        <h4>Number</h4>
        {arr.map((base, idx) => {
            const value = base * Math.pow(10, -5 + idx);

            return (
                <div style={{ margin: '5px 0' }} key={idx}>
                    {value} = 
                    <Humanize value={value} type="number">
                        {(v) => v}
                    </Humanize>
                </div>
            );
        })}
        <h5>With compress</h5>
        {arr.map((base, idx) => {
            const value = base * Math.pow(10, 3 * idx + 3);

            return (
                <div style={{ margin: '5px 0' }} key={idx}>
                    {value} = 
                    <Humanize value={value} type="number" compress>
                        {(v) => v}
                    </Humanize>
                </div>
            );
        })}
    </article>
    <article>
        <h4>Float</h4>
        {arr.map((base, idx) => {
            const value = base * Math.pow(10, -5 + idx);

            return (
                <div style={{ margin: '5px 0' }} key={idx}>
                    {value} = 
                    <Humanize value={value} type="float" accuracy={3}>
                        {(v) => v}
                    </Humanize>
                </div>
            );
        })}
        <h5>With approximate value</h5>
        {arr.map((base, idx) => {
            const value = base * Math.pow(10, -3 + idx);

            return (
                <div style={{ margin: '5px 0' }} key={idx}>
                    {value} = 
                    <Humanize value={value} type="float" approximationThreshold={0.01}>
                        {(v) => v}
                    </Humanize>
                </div>
            );
        })}
    </article>
    <article>
        <h4>Currency</h4>
        {arr.map((base, idx) => {
            const value = base * Math.pow(10, -3 + idx);

            return (
                <div style={{ margin: '5px 0' }} key={idx}>
                    {value} = 
                    <Humanize value={value} type="currency">
                        {(v) => v}
                    </Humanize>
                </div>
            );
        })}
        <h5>With symbol</h5>
        {arr.map((base, idx) => {
            const value = base * Math.pow(10, -3 + idx);

            return (
                <div style={{ margin: '5px 0' }} key={idx}>
                    {value} = 
                    <Humanize value={value} type="currency" currency="RUB">
                        {(v) => v}
                    </Humanize>
                </div>
            );
        })}
    </article>
    <article>
        <h4>Invalid values</h4>
        <div style={{ margin: '5px 0' }}>
            undefined = 
            <Humanize value={undefined} type="float" accuracy={3}>
                {(v) => v}
            </Humanize>
        </div>
        <div style={{ margin: '5px 0' }}>
            null = 
            <Humanize value={null} type="float" accuracy={3}>
                {(v) => v}
            </Humanize>
        </div>
    </article>
</div>
```