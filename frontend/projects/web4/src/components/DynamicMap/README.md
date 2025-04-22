## Компонент DynamicMap
Компонент предназначен для отображения динамической карты с возможностью включить контролы карты.

### Props:
 - <font color="#aaa">**className**: string — класс контейнера карты;</font>
 - <font color="#aaa">**height**: number —высота контейнера карты;</font>
 - <font color="#aaa">**width**: number — ширина контейнера карты;</font>
 - <font color="#aaa">**zoom**: number — начальный масштаб карты;</font>
 - <font color="#aaa">**center**: [number, number] — координаты центра карты;</font>
 - **url**: string — путь к API карт;
 - **enableMapControls** — наличие этого атрибута включает контролы карты.

### Пример:

    import { DynamicMap } from './DynamicMap';

    <DynamicMap
        center={[37.620393, 55.753960]}
        height={320}
        width={640}
        zoom={10}
        url="https://yandex.ru/maps"
        enableMapControls
    />

![Пример динамической карты](https://jing.yandex-team.ru/files/filgaponenko/Storybook_2019-07-01_14-24-43.png)
